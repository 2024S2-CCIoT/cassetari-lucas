## **Semana 1: 25 de Setembro a 2 de Outubro**
### **Entrega: 2 de Outubro (Quarta-feira)**

#### **Tarefas:**
1. **Configuração do Ambiente AWS IoT Core**
   - Criar a "Thing" no **AWS IoT Core** para representar o dispositivo IoT.
   - Configurar o endpoint MQTT e os certificados de autenticação.
   - Definir a regra no IoT Core para enviar os dados recebidos para o **AWS Lambda**.

2. **Simulação do Sensor IoT**
   - Implementar o script em Python (ou configurar o dispositivo real) para simular o envio de leituras de temperatura.
   - Testar o envio de dados para o tópico MQTT criado no **AWS IoT Core**.

#### **Objetivo:**
Estabelecer a comunicação entre o dispositivo IoT e o **AWS IoT Core** via MQTT, com os dados sendo enviados corretamente.

---

## **Semana 2: 3 de Outubro a 9 de Outubro**
### **Entrega: 9 de Outubro (Quarta-feira)**

#### **Tarefas:**
1. **Criação e Configuração da Função AWS Lambda**
   - Criar a função **AWS Lambda** em Python para processar as leituras de temperatura recebidas.
   - Definir as permissões necessárias (acesso ao DynamoDB e SNS).
   - Implementar a lógica de processamento dos dados e a verificação do limite de temperatura.

2. **Configuração do Amazon DynamoDB**
   - Criar a tabela no **DynamoDB** para armazenar os dados de temperatura (com `machine_id` e `timestamp`).
   - Testar o armazenamento de leituras reais no DynamoDB através da função Lambda.

#### **Objetivo:**
Garantir que a função **Lambda** processe os dados e os armazene no **DynamoDB** com sucesso.

---

## **Semana 3: 10 de Outubro a 16 de Outubro**
### **Entrega: 16 de Outubro (Quarta-feira)**

#### **Tarefas:**
1. **Implementação do Amazon SNS**
   - Criar o tópico no **Amazon SNS** para os alertas de temperatura.
   - Configurar assinaturas (e-mail ou SMS) para receber as notificações.

2. **Integração do SNS com a Função Lambda**
   - Modificar a função **Lambda** para disparar alertas via SNS caso a temperatura exceda o limite.
   - Realizar testes de disparo de alertas com dados simulados acima do limite.

#### **Objetivo:**
Testar o envio de alertas automáticos quando as temperaturas ultrapassarem o valor configurado.

---

## **Semana 4: 17 de Outubro a 23 de Outubro**
### **Entrega: 23 de Outubro (Quarta-feira)**

#### **Tarefas:**
1. **Testes de Carga e Performance**
   - Simular um volume maior de dados para verificar a escalabilidade do sistema.
   - Validar se o **AWS Lambda**, **DynamoDB** e **SNS** conseguem processar grandes volumes de dados em tempo hábil.

2. **Ajustes de Configuração e Monitoramento**
   - Analisar logs do **AWS CloudWatch** para identificar possíveis otimizações no código da função Lambda.
   - Ajustar limites de performance e possíveis gargalos nos serviços AWS.

#### **Objetivo:**
Validar a capacidade do sistema de lidar com alta carga de dados de sensores e ajustes finais no processamento.

---

## **Semana 5: 24 de Outubro a 30 de Outubro**
### **Entrega: 30 de Outubro (Quarta-feira)**

#### **Tarefas:**
1. **Documentação Técnica**
   - Criar a documentação final com detalhes do setup, funcionamento do sistema, e guias de instalação e operação.
   - Elaborar o README final com explicações sobre cada tecnologia utilizada.

2. **Revisão e Preparação para a Entrega**
   - Fazer uma revisão final da POC.
   - Testar o projeto completo e garantir que todos os componentes estejam funcionando conforme o esperado.
   - Preparar o projeto para a apresentação ou envio.

#### **Objetivo:**
Finalizar a documentação técnica e garantir que a POC esteja pronta para entrega e apresentação.

---

## **Semana 6: 31 de Outubro a 6 de Novembro**
### **Entrega: 6 de Novembro (Quarta-feira)**

#### **Tarefas:**
1. **Apresentação Final ou Entrega**
   - Preparar slides ou uma explicação resumida para a apresentação do projeto.
   - Fazer uma apresentação demonstrando o funcionamento da POC e destacando os pontos principais da arquitetura serverless.

#### **Objetivo:**
Apresentar e entregar o projeto final com todos os requisitos atendidos.
