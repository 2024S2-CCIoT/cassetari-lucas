# **Monitoramento de Temperatura de Máquinas Industriais - POC**

## **Descrição do Projeto**
Este projeto de prova de conceito (POC) tem como objetivo implementar uma arquitetura serverless para o monitoramento de temperatura de máquinas industriais em tempo real, utilizando dispositivos IoT para coletar e enviar dados de temperatura para a nuvem. O sistema processa e armazena os dados recebidos e dispara alertas automaticamente caso a temperatura exceda um limite predefinido, garantindo uma resposta rápida em caso de anomalias.

O projeto é simples e eficiente, utilizando tecnologias da AWS para garantir escalabilidade e baixo custo, permitindo o processamento de grandes volumes de dados IoT sem a necessidade de manter infraestrutura física.

---

## **Tecnologias Utilizadas**

### **1. AWS IoT Core**
O **AWS IoT Core** é utilizado para conectar e gerenciar dispositivos IoT. Ele permite que os dispositivos enviem dados para a nuvem de forma segura, usando o protocolo **MQTT** para comunicação eficiente e em tempo real. No projeto, o AWS IoT Core recebe os dados de temperatura dos sensores e os encaminha para processamento.

### **2. AWS Lambda**
O **AWS Lambda** é um serviço de computação serverless que executa código em resposta a eventos. Na POC, uma função Lambda é acionada automaticamente pelo AWS IoT Core sempre que uma nova leitura de temperatura é enviada. A função Lambda processa os dados, armazena-os no banco de dados e verifica se a temperatura ultrapassa o limite configurado.

### **3. Amazon DynamoDB**
O **Amazon DynamoDB** é um banco de dados NoSQL gerenciado, altamente escalável e de baixa latência, utilizado para armazenar as leituras de temperatura enviadas pelos dispositivos IoT. Cada leitura é registrada com o ID da máquina, o timestamp da leitura, e a temperatura medida, criando um histórico para monitoramento.

### **4. Amazon SNS (Simple Notification Service)**
O **Amazon SNS** é um serviço de notificação que facilita o envio de alertas via diferentes canais, como e-mail, SMS ou notificações push. Na POC, o SNS é acionado pela função Lambda para enviar alertas sempre que a temperatura de uma máquina ultrapassar o limite definido, garantindo que os responsáveis sejam notificados imediatamente.

---

## **Objetivo Conceitual do Projeto**

O conceito central desta POC é demonstrar como uma arquitetura **serverless** pode ser aplicada em cenários industriais para monitoramento de dados IoT em tempo real, sem a necessidade de gerenciar servidores ou infraestrutura física. O projeto visa ilustrar como os dados de sensores de máquinas podem ser facilmente processados, armazenados e analisados usando serviços da AWS, além de como gerar alertas automatizados para garantir a segurança e o controle em ambientes industriais.

Esse tipo de solução é altamente escalável, fácil de implementar e pode ser adaptado para diversos outros cenários de IoT, onde o monitoramento em tempo real e a resposta rápida a eventos são críticos para o sucesso da operação.

---

Este projeto serve como um exemplo prático da utilização de tecnologias modernas de nuvem para resolver problemas reais em ambientes industriais, demonstrando o poder e a flexibilidade da **Arquitetura Serverless**.
