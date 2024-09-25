### **Projeto: Monitoramento de Temperatura de Máquinas Industriais com Alerta Automático**

#### **Visão Geral**
Esta POC implementa uma arquitetura serverless para o monitoramento da temperatura de máquinas industriais. O sistema envia leituras de temperatura de sensores IoT para um serviço de nuvem, onde os dados são processados e armazenados. Quando a temperatura excede um limite predefinido, um alerta é disparado para notificar os responsáveis.

---

### **1. Simulação de Sensor IoT**

#### **Descrição:**
- Um script simula o envio periódico de leituras de temperatura para a nuvem via MQTT.

#### **Tecnologia:**
- **Python** (para simulação de dados) ou um **ESP32** real.

#### **Exemplo de Código:**
```python
import time
import random
import paho.mqtt.client as mqtt

broker = "your-endpoint.iot.region.amazonaws.com"
port = 8883
topic = "iot/temperature"

def simulate_temperature():
    while True:
        temperature = random.uniform(20, 100)
        client.publish(topic, str(temperature))
        time.sleep(5)

def on_connect(client, userdata, flags, rc):
    print("Conectado com código:", rc)

client = mqtt.Client()
client.on_connect = on_connect
client.connect(broker, port, 60)

client.loop_start()
simulate_temperature()
```

---

### **2. Configuração do AWS IoT Core**

#### **Descrição:**
- O **AWS IoT Core** recebe as leituras do sensor IoT e envia para uma função **AWS Lambda** para processamento.

#### **Passos:**
1. **Criar Thing no AWS IoT Core:**
   - Acesse **AWS IoT Core** e crie uma nova "Thing".
   - Gere certificados para a autenticação MQTT do dispositivo.

2. **Definir Tópico MQTT:**
   - Crie um tópico chamado `iot/temperature`.
   - Configure uma regra para enviar mensagens recebidas para a função **Lambda**.

---

### **3. Criação da Função AWS Lambda**

#### **Descrição:**
- A função Lambda processa os dados de temperatura, armazena no DynamoDB, e dispara um alerta via SNS se a temperatura exceder o limite.

#### **Tecnologia:**
- **AWS Lambda** (Python).

#### **Código Lambda:**
```python
import json
import boto3
from decimal import Decimal

dynamodb = boto3.resource('dynamodb')
sns = boto3.client('sns')

TABLE_NAME = 'TemperatureReadings'
SNS_TOPIC_ARN = 'arn:aws:sns:region:account-id:temperature-alerts'
TEMPERATURE_THRESHOLD = 80.0

def lambda_handler(event, context):
    temperature = float(event['temperature'])
    timestamp = event['timestamp']
    machine_id = event['machine_id']

    table = dynamodb.Table(TABLE_NAME)
    table.put_item(
        Item={
            'machine_id': machine_id,
            'timestamp': timestamp,
            'temperature': Decimal(str(temperature))
        }
    )

    if temperature > TEMPERATURE_THRESHOLD:
        message = f"Alerta! Temperatura alta detectada: {temperature}°C na máquina {machine_id}"
        sns.publish(
            TopicArn=SNS_TOPIC_ARN,
            Message=message,
            Subject='Alerta de Temperatura'
        )

    return {
        'statusCode': 200,
        'body': json.dumps('Processamento concluído.')
    }
```

#### **Permissões Lambda:**
- A função Lambda precisa de permissões para acessar o **DynamoDB** e o **SNS**.

---

### **4. Armazenamento no DynamoDB**

#### **Descrição:**
- O DynamoDB armazena as leituras de temperatura para criar um histórico de monitoramento.

#### **Passos:**
1. Criar uma tabela chamada `TemperatureReadings`:
   - **Partition Key**: `machine_id` (String)
   - **Sort Key**: `timestamp` (String)

---

### **5. Configuração do Amazon SNS para Alertas**

#### **Descrição:**
- O **Amazon SNS** envia notificações por e-mail ou SMS quando o limite de temperatura é excedido.

#### **Passos:**
1. Criar um tópico SNS chamado `temperature-alerts`.
2. Assinar o tópico SNS com um e-mail ou SMS para receber as notificações.

---

### **6. Conectar AWS IoT Core com Lambda**

#### **Passos:**
1. No **AWS IoT Core**, configure uma regra que acione a função Lambda quando uma mensagem for publicada no tópico `iot/temperature`.

---

### **7. Teste Final**

1. **Simulação do Envio de Dados:**
   - Execute o script de simulação para enviar dados de temperatura.

2. **Monitorar Armazenamento:**
   - Verifique se as leituras estão sendo armazenadas no **DynamoDB**.

3. **Verificar Alertas:**
   - Simule uma temperatura acima do limite para acionar a notificação via **SNS**.

---

### **Fluxo Geral da Solução:**
1. O dispositivo IoT envia dados para o **AWS IoT Core** via MQTT.
2. O **AWS IoT Core** invoca uma **função Lambda** para processar os dados.
3. A função **Lambda** armazena as leituras no **DynamoDB**.
4. Se a temperatura exceder o limite, a **Lambda** dispara uma notificação via **Amazon SNS**.

---

Esse documento técnico descreve de forma simplificada o funcionamento da POC, cobrindo os principais serviços utilizados e seus papéis no fluxo de monitoramento e alerta.
