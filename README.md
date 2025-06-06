# ☁️ Projeto AWS – Coleta, Processamento e Visualização de Dados Ambientais

## 🎯 Objetivo

Criar uma arquitetura robusta, escalável e integrada, focada em:
- Receber dados externos via API,
- Armazenar dados brutos no S3,
- Processar e armazenar no RDS,
- Visualizar os dados no Grafana via EC2,
- Monitorar com CloudWatch,
- Proteger com IAM e VPC.


## 🗺️ Arquitetura da Solução

![Diagrama do Projeto](./diagrama.jpg)


## 🔧 Serviços Utilizados

### 1. **Amazon API Gateway**
- Recebe dados via HTTP.
- Interface pública e segura para ingestão de dados.

### 2. **AWS Lambda**
- Função serverless que processa os dados e envia para S3 e RDS.
- Converte a temperatura recebida em Fahrenheit para Celsius.
- Envia os dados brutos ao S3 e os dados processados ao RDS.
- Escalável e sem servidor.

### 3. **Amazon S3**
- Armazena os dados brutos recebidos da API (sem alterações).
- Serve como backup e histórico da ingestão.

### 4. **Amazon RDS**
- Banco de dados relacional (MySQL/PostgreSQL).
- Armazena os dados tratados, com a temperatura já convertida para Celsius.

### 5. **Amazon EC2**
- Instância com **Grafana** instalado.
- Realiza a visualização dos dados do RDS em dashboards interativos.

### 6. **Amazon CloudWatch**
- Coleta logs da Lambda e métricas do EC2.
- Permite auditoria, análise de desempenho e alertas.

### 7. **AWS IAM**
- Garante que cada serviço só acesse o que precisa.

### 8. **VPC**
- Isola os recursos críticos (RDS, EC2).
- Aumenta a segurança e performance da comunicação entre serviços.


## 🔁 Processamento de Dados
- A API recebe dados com temperatura em Fahrenheit.

- A função Lambda converte a temperatura para Celsius antes de salvar no banco:

Fórmula usada:

```python
temperatura_c = round((temperatura_f - 32) * 5 / 9, 1)
```
- Essa abordagem permite que os dashboards exibam os dados em °C diretamente, sem necessidade de conversão no Grafana.

## 📊 Exemplo de Payload Enviado para API

```json
{
  "timestamp": "2025-06-06T15:35:27",
  "temperatura": 86.0,
  "umidade": 42
}
```
Nesse exemplo, a temperatura será convertida para 30.0°C e armazenada no RDS dessa forma.

<br>

* [Apresentação Lucas](https://youtu.be/ERcMiJXmX2Y)
