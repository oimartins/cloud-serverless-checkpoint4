# Checkpoint 4 - Observabilidade e Otimização

Este projeto amplia a arquitetura serverless construída nos checkpoints anteriores adicionando observabilidade, monitoramento e análise de desempenho.

## Tecnologias Utilizadas

- Google Cloud Functions
- Google Cloud Pub/Sub
- Google Cloud Workflows
- Google Cloud Logging
- Google Cloud Monitoring

---

# Objetivo

Monitorar todo o pipeline de execução, coletando logs estruturados e métricas operacionais que permitam analisar desempenho, disponibilidade e custo da solução.

---

# Arquitetura

```text
Workflow
   |
   v
validateOrder
   |
   v
Pub/Sub
   |
   v
notifyOrder
   |
   v
Cloud Logging

Cloud Monitoring
```

---

# Como Testar

Executar Workflow:

```bash
gcloud workflows execute order-workflow \
  --location=us-central1 \
  --data='{"orderId":"123"}'
```

---

# Consultar Logs

Logs da validação:

```bash
gcloud logging read \
'resource.type="cloud_run_revision"' \
--limit=20
```

---

# Consultar Workflow

```bash
gcloud workflows executions list order-workflow \
  --location=us-central1
```

---

# Métricas Monitoradas

- Número de execuções
- Tempo de resposta
- Taxa de erro
- Mensagens processadas
- Utilização de recursos

---

# Análise Crítica

## Otimização 1 - Redução de Custos

As Cloud Functions podem utilizar menos memória quando realizam apenas validações simples.

Benefício:

- Menor custo por execução.
- Menor consumo de recursos.

---

## Otimização 2 - Retry Inteligente

Aplicar retry apenas em falhas temporárias.

Benefício:

- Evita reprocessamentos desnecessários.
- Reduz custo operacional.

---

## Otimização 3 - Ampliação da DLQ

Aumentar o monitoramento do tópico orders-dlq.

Benefício:

- Identificação rápida de erros.
- Recuperação mais eficiente.

---

# Conclusão

A solução demonstra uma arquitetura serverless totalmente observável com monitoramento centralizado, logs estruturados e métricas operacionais capazes de apoiar decisões de otimização e redução de custos.
