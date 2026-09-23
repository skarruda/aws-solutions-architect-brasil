# Reta Final SAA-C03

> Plano objetivo para os últimos 14 ou 7 dias antes da prova. Use junto com os simulados completos, mini-simulados por domínio e caderno de erros do Módulo 29.

---

## Critérios de prontidão para agendar o exame

| Critério | Pronto quando |
|---|---|
| Simulados completos | 2 resultados seguidos com 78% ou mais, sem consulta |
| Domínios fracos | Nenhum domínio abaixo de 70% nos mini-simulados |
| Caderno de erros | Erros recorrentes convertidos em regra de decisão |
| Gestão de tempo | Primeira passagem em até 100 minutos e revisão final em 30 minutos |
| Ansiedade técnica | Você sabe explicar por que a alternativa correta vence as distrações |

Se estiver entre 70% e 77%, ainda é possível passar, mas a margem é menor. Priorize revisão dos erros, não leitura passiva.

---

## Plano de 14 dias

| Dia | Rotina objetiva | Simulado/revisão | Resultado esperado |
|---:|---|---|---|
| D-14 | Revisar pesos do exame, estratégia de tempo e armadilhas gerais | Ler README do Módulo 29 e fazer 20 questões leves | Diagnóstico inicial sem pressão |
| D-13 | Segurança: IAM, policies, KMS, Secrets Manager, S3 privado | Mini-simulado de segurança | Lista dos 5 erros mais importantes |
| D-12 | Resiliência: Multi-AZ, DR, SQS, Route 53, backup | Mini-simulado de resiliência | Regras para HA vs DR |
| D-11 | Performance: cache, banco, rede, compute e storage | Mini-simulado de performance | Mapa de gargalos por serviço |
| D-10 | Custo: modelos de compra, S3 classes, NAT, rightsizing | Mini-simulado de custo | Decisões de custo por cenário |
| D-9 | Revisar caderno de erros D+1 dos dias anteriores | 30 questões misturadas | Reduzir erros repetidos |
| D-8 | Simulado completo cronometrado | Simulado Completo 1 | Baseline de tempo e acerto |
| D-7 | Correção profunda do simulado | Caderno de erros + revisão por domínio | Entender cada alternativa errada |
| D-6 | Reforço dos dois piores domínios | Mini-simulados ou questões segmentadas | Subir domínios fracos para 70%+ |
| D-5 | Simulado completo cronometrado | Simulado Completo 2 | Validar melhora e tempo |
| D-4 | Correção profunda e flashcards | Caderno de erros D+1/D+7 | Fixar regras de decisão |
| D-3 | Revisão final técnica | Cheatsheets dos módulos 05, 06, 08, 10, 13, 14, 17, 22, 25, 26 | Cobrir serviços mais cobrados |
| D-2 | Simulado completo leve ou revisão de erros | Simulado Completo 3 se estiver descansado; senão, revisar erros | Evitar fadiga |
| D-1 | Revisão curta e descanso | Apenas caderno de erros e checklist | Entrar descansado |

---

## Plano de 7 dias

| Dia | Rotina objetiva | Prioridade |
|---:|---|---|
| D-7 | Fazer um simulado completo cronometrado | Medir tempo e lacunas reais |
| D-6 | Corrigir o simulado e preencher caderno de erros | Aprender com alternativas incorretas |
| D-5 | Mini-simulado do pior domínio + revisão direcionada | Atacar lacuna de maior impacto |
| D-4 | Mini-simulado do segundo pior domínio + flashcards | Consolidar decisão arquitetural |
| D-3 | Fazer outro simulado completo | Confirmar consistência |
| D-2 | Revisar erros recorrentes e cheatsheets críticos | Eliminar confusões clássicas |
| D-1 | Revisão leve, logística e descanso | Chegar com energia |

---

## Distribuição recomendada de simulados e revisão

| Situação | Ação |
|---|---|
| Primeiro simulado abaixo de 65% | Voltar aos módulos base antes de repetir simulado completo |
| 65% a 74% | Fazer mini-simulados por domínio e revisar erros por serviço |
| 75% a 84% | Alternar simulado completo e correção profunda |
| 85% ou mais | Focar tempo de prova, pegadinhas e consistência |

Não faça três simulados completos no mesmo dia. O ganho vem da correção ativa, não do volume bruto.

---

## Estratégia de tempo de prova

| Marco | Tempo acumulado | Ação |
|---|---:|---|
| Questão 15 | 30 min | Se passou muito disso, acelere eliminação |
| Questão 32 | 65 min | Metade da prova deve estar praticamente resolvida |
| Questão 50 | 100 min | Entrar na reta final com folga |
| Questão 65 | 115 min | Terminar primeira passagem |
| Revisão | 15 min finais | Revisar marcadas e múltipla resposta |

Regras práticas:

- Leia a última frase primeiro quando o enunciado for longo.
- Marque questões com conflito entre duas alternativas boas.
- Não gaste mais de 3 minutos em uma questão na primeira passagem.
- Em múltipla resposta, conte exatamente quantas alternativas foram pedidas.
- Troque uma resposta apenas se encontrar um requisito explícito que você ignorou.

---

## Checklist de revisão final

| Tema | Pronto? |
|---|---|
| IAM: roles, trust policy, permission boundary, SCP e least privilege | [ ] |
| S3: Block Public Access, OAC, replication, lifecycle, Object Lock e classes | [ ] |
| VPC: route tables, NAT, endpoints, SG vs NACL, peering, TGW e PrivateLink | [ ] |
| Bancos: RDS Multi-AZ, Read Replicas, Aurora, DynamoDB, DAX e ElastiCache | [ ] |
| Resiliência: ELB, ASG, Route 53 failover, backup, pilot light e warm standby | [ ] |
| Serverless: Lambda, API Gateway, SQS, SNS, EventBridge e Step Functions | [ ] |
| Segurança: KMS, Secrets Manager, WAF, Shield, GuardDuty, Macie, Inspector | [ ] |
| Custo: Spot, Savings Plans, S3 Intelligent-Tiering, Compute Optimizer, NAT vs endpoint | [ ] |
| Performance: CloudFront, Global Accelerator, cache, EBS io2, FSx, Athena/Parquet | [ ] |
| Well-Architected: trade-offs entre segurança, confiabilidade, performance e custo | [ ] |

---

## Sinais de alerta antes de agendar

| Sinal | O que fazer |
|---|---|
| Você acerta por intuição, mas não explica por que as outras estão erradas | Corrigir menos questões, porém com mais profundidade |
| Erra repetidamente o mesmo par de serviços | Criar regra de decisão no caderno de erros |
| Estoura tempo em enunciados longos | Treinar leitura da pergunta final + requisitos explícitos |
| Confunde "mais seguro", "menor custo" e "menos operação" | Grifar o objetivo principal antes de olhar alternativas |
| Vai bem em teoria, mas mal em cenário | Revisar casos de uso e labs dos módulos 26 a 28 |

---
_Credito autoral: Thiago Cardoso - [LinkedIn](https://www.linkedin.com/in/analyticsthiagocardoso)_
