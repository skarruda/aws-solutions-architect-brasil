# Caderno de Erros — SAA-C03

> Use este arquivo depois de cada simulado. O objetivo não é registrar culpa; é transformar cada erro em uma regra de decisão reutilizável na prova.

---

## Como usar

1. Resolva o simulado sem consultar material.
2. Corrija apenas depois de terminar o bloco.
3. Para cada erro ou chute, preencha o template.
4. Revise em D+1, D+7 e D+21.
5. Antes da prova, leia apenas as regras de decisão.

---

## Template reutilizável

| Campo | Preenchimento |
|---|---|
| Questão | Simulado, número e enunciado curto |
| Tema/serviço | Ex.: RDS Multi-AZ, S3 Lifecycle, IAM Role |
| Motivo do erro | Confundi serviço, ignorei requisito, forcei solução mais complexa, errei custo, errei segurança |
| Conceito correto | Explicação objetiva do comportamento do serviço |
| Regra de decisão para prova | Frase curta que ajuda a eliminar alternativas |
| Revisão agendada | D+1: [ ] / D+7: [ ] / D+21: [ ] |

### Entrada em branco

| Campo | Preenchimento |
|---|---|
| Questão |  |
| Tema/serviço |  |
| Motivo do erro |  |
| Conceito correto |  |
| Regra de decisão para prova |  |
| Revisão agendada | D+1: [ ] / D+7: [ ] / D+21: [ ] |

---

## Exemplos preenchidos

### 1. RDS Multi-AZ vs Read Replica

| Campo | Preenchimento |
|---|---|
| Questão | Alta disponibilidade para banco relacional com escrita crítica |
| Tema/serviço | Amazon RDS Multi-AZ |
| Motivo do erro | Escolhi Read Replica porque vi "replicação" e "banco" no enunciado |
| Conceito correto | Multi-AZ usa standby em outra AZ para failover automático e alta disponibilidade. Read Replica escala leitura e usa replicação assíncrona. |
| Regra de decisão para prova | Se o requisito é HA/failover de escrita, pense Multi-AZ; se é leitura, pense Read Replica. |
| Revisão agendada | D+1: [ ] / D+7: [ ] / D+21: [ ] |

### 2. NAT Gateway vs VPC Endpoint

| Campo | Preenchimento |
|---|---|
| Questão | EC2 privada acessando S3 sem sair pela internet |
| Tema/serviço | Gateway VPC Endpoint para S3 |
| Motivo do erro | Escolhi NAT Gateway por associar subnet privada a saída externa |
| Conceito correto | NAT Gateway permite saída para internet. Gateway VPC Endpoint permite acesso privado a S3/DynamoDB sem internet e costuma reduzir custo de tráfego. |
| Regra de decisão para prova | Se o destino é S3 ou DynamoDB a partir de subnet privada, endpoint costuma ser melhor que NAT. |
| Revisão agendada | D+1: [ ] / D+7: [ ] / D+21: [ ] |

### 3. S3 Intelligent-Tiering vs Glacier

| Campo | Preenchimento |
|---|---|
| Questão | Dados com padrão de acesso imprevisível |
| Tema/serviço | S3 Intelligent-Tiering |
| Motivo do erro | Escolhi Glacier por focar só em menor custo por GB |
| Conceito correto | Intelligent-Tiering move objetos entre camadas conforme acesso. Glacier é arquivamento e pode ter latência de recuperação e cobrança mínima de retenção. |
| Regra de decisão para prova | Acesso imprevisível pede Intelligent-Tiering; arquivamento com baixa frequência e tolerância a recuperação pede Glacier. |
| Revisão agendada | D+1: [ ] / D+7: [ ] / D+21: [ ] |

### 4. IAM Role vs Access Key

| Campo | Preenchimento |
|---|---|
| Questão | Aplicação em EC2 acessando S3 com segurança |
| Tema/serviço | IAM Role e Instance Profile |
| Motivo do erro | Considerei guardar access key em variável de ambiente |
| Conceito correto | IAM Roles fornecem credenciais temporárias rotacionadas automaticamente. Access keys de longa duração aumentam risco operacional. |
| Regra de decisão para prova | Recurso AWS chamando outro serviço AWS deve usar role sempre que possível. |
| Revisão agendada | D+1: [ ] / D+7: [ ] / D+21: [ ] |

### 5. SQS Standard vs FIFO

| Campo | Preenchimento |
|---|---|
| Questão | Processamento de pedidos que exige ordem estrita |
| Tema/serviço | Amazon SQS FIFO |
| Motivo do erro | Escolhi Standard por lembrar de maior throughput |
| Conceito correto | SQS FIFO preserva ordem por message group e oferece deduplicação. Standard entrega ao menos uma vez, com ordem best-effort e possíveis duplicatas. |
| Regra de decisão para prova | Ordem estrita ou deduplicação explícita aponta para FIFO; escala máxima e tolerância a duplicatas aponta para Standard. |
| Revisão agendada | D+1: [ ] / D+7: [ ] / D+21: [ ] |

### 6. CloudFront OAC vs bucket público

| Campo | Preenchimento |
|---|---|
| Questão | Site estático no S3 servido globalmente sem acesso direto ao bucket |
| Tema/serviço | CloudFront Origin Access Control |
| Motivo do erro | Escolhi bucket público por ser mais simples |
| Conceito correto | OAC permite que apenas CloudFront acesse o bucket privado. O bucket não precisa ficar público para entregar conteúdo global. |
| Regra de decisão para prova | S3 privado atrás de CloudFront moderno pede OAC, não bucket público. |
| Revisão agendada | D+1: [ ] / D+7: [ ] / D+21: [ ] |

### 7. Aurora Global Database vs backup/restore

| Campo | Preenchimento |
|---|---|
| Questão | Banco global com RPO baixo entre regiões |
| Tema/serviço | Aurora Global Database |
| Motivo do erro | Escolhi backup/restore porque parecia mais barato |
| Conceito correto | Backup/restore é econômico, mas tem RTO/RPO maiores. Aurora Global Database replica para outra região com baixa latência e permite recuperação regional mais rápida. |
| Regra de decisão para prova | RPO/RTO baixos entre regiões normalmente exigem replicação contínua, não apenas backup. |
| Revisão agendada | D+1: [ ] / D+7: [ ] / D+21: [ ] |

### 8. Savings Plans vs Spot

| Campo | Preenchimento |
|---|---|
| Questão | Workload 24/7 previsível por 1 ano |
| Tema/serviço | Savings Plans |
| Motivo do erro | Escolhi Spot por ser mais barato em preço unitário |
| Conceito correto | Spot é excelente para workloads tolerantes a interrupção. Para carga contínua e previsível, Savings Plans ou Reserved Instances reduzem custo sem risco de interrupção. |
| Regra de decisão para prova | Tolerante a interrupção: Spot. Estável e previsível: Savings Plans/Reserved Instances. |
| Revisão agendada | D+1: [ ] / D+7: [ ] / D+21: [ ] |

---

## Revisão rápida antes da prova

| Sinal no enunciado | Decisão provável |
|---|---|
| "Menor esforço operacional" | Serviço gerenciado ou serverless |
| "Alta disponibilidade para escrita" | Multi-AZ, cluster gerenciado ou failover automático |
| "Escalar leitura" | Read Replicas, cache ou endpoint reader |
| "Acesso privado a serviço AWS" | VPC Endpoint |
| "Dados sensíveis no S3" | Block Public Access, encryption, bucket policy, Macie quando for detecção |
| "Processamento assíncrono" | SQS, SNS, EventBridge ou Step Functions conforme padrão |
| "Custo para acesso imprevisível em S3" | Intelligent-Tiering |
| "Carga batch tolerante a interrupção" | Spot, AWS Batch ou Compute Savings conforme estabilidade |

---
_Credito autoral: Thiago Cardoso - [LinkedIn](https://www.linkedin.com/in/analyticsthiagocardoso)_
