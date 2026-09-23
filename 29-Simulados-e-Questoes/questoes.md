# Questões — Módulo 29: Simulados e Questões

> Estratégia de estudo para a prova

---

**Sobre as questões do simulado**

O README deste módulo contém o simulado completo com 65 questões. Este arquivo reúne questões complementares de estratégia de prova e meta-perguntas sobre o formato do exame.

---

**1.** No exame SAA-C03, uma questão pede para escolher a solução "mais custo-efetiva". Qual abordagem de eliminação usar?

- A) Escolher sempre a opção com Lambda (serverless é sempre mais barato)
- B) Eliminar opções com recursos ociosos (EC2 sempre ligado, instâncias sobre-provisionadas), depois comparar custo das restantes
- C) Escolher sempre Reserved Instances (maior desconto)
- D) Escolher a opção com menos serviços AWS (menos serviços = menos custo)

<details><summary>Resposta</summary>

**B** — "Mais custo-efetiva" varia pelo contexto: para cargas intermitentes, Lambda/Fargate/Spot são mais baratos. Para cargas 24/7 estáveis, Reserved Instances. Elimine primeiro: (1) over-provisioning, (2) recursos idle, (3) redundância desnecessária. Então compare os serviços restantes pelo modelo de precificação.

</details>

---

**2.** Uma questão do exame pede para escolher 2 respostas corretas de 5 opções. Qual é a melhor estratégia?

- A) Marcar as 2 primeiras opções que parecem corretas
- B) Identificar as 2 incorretas mais óbvias, eliminar, e das 3 restantes escolher as 2 mais corretas
- C) Marcar como incerto e voltar depois
- D) Procurar por palavras-chave como "sem servidor" ou "gerenciado" nas opções

<details><summary>Resposta</summary>

**B** — Estratégia de eliminação: remova primeiro as opções claramente erradas (serviço errado para o contexto, viola princípio de segurança óbvio). Das restantes, escolha as 2 que melhor atendem TODOS os requisitos da questão. Em questões de múltipla seleção, todas as opções corretas devem ser escolhidas para pontuar.

</details>

---

**3.** O exame pede uma arquitetura "altamente disponível". Qual é o critério mínimo que a resposta deve atender?

- A) Usar o serviço mais novo da AWS
- B) Ter recursos em pelo menos 2 Availability Zones com failover automático
- C) Usar Reserved Instances em 3 regiões
- D) Ter backup diário dos dados

<details><summary>Resposta</summary>

**B** — Alta disponibilidade = tolerância a falha de uma AZ. Mínimo: recursos em 2+ AZs com failover automático (ELB + ASG multi-AZ, RDS Multi-AZ, etc.). Backup é para recovery (não HA). Multi-region é para disaster recovery ou alcance global (diferente de HA simples).

</details>

---

**4.** Uma questão descreve uma aplicação que "às vezes tem picos de tráfego imprevisíveis" e precisa de uma solução de compute. Qual serviço é a resposta mais provável?

- A) EC2 On-Demand fixo
- B) EC2 Reserved Instances
- C) Lambda ou ECS Fargate com Auto Scaling
- D) EC2 Spot Instances

<details><summary>Resposta</summary>

**C** — "Imprevisível" e "picos" = serverless/auto-scaling. Lambda escala para zero quando não há carga e para milhares quando há pico, sem configuração manual. Fargate com ASG baseado em métricas também. Reserved Instances são para carga previsível; Spot pode ser interrompida durante picos.

</details>

---

**5.** No exame, quando a questão menciona "menor mudança na aplicação existente" (lift-and-shift), qual categoria de resposta é mais provável?

- A) Lambda e DynamoDB (serverless nativo)
- B) EC2 + RDS (equivalente de VM + banco relacional)
- C) EKS + S3 (containers + armazenamento)
- D) CloudFormation + CodePipeline (automação)

<details><summary>Resposta</summary>

**B** — "Menor mudança possível" = lift-and-shift = EC2 (VM equivalente), RDS (banco gerenciado, mesma engine), ELB (load balancer). A aplicação não precisa ser reescrita. Lambda/DynamoDB requerem refactoring. EKS requer containerização. A questão está testando reconhecer o padrão "Rehost" dos 7Rs.

</details>

---

**6.** Qual é a dica mais importante ao ler uma questão do exame SAA-C03?

- A) Ler a última frase da questão primeiro para entender o que está sendo perguntado
- B) Identificar todos os requisitos (disponibilidade, custo, segurança, performance) explicitamente mencionados antes de olhar as opções
- C) Eliminar as opções mais longas (geralmente complexidade desnecessária)
- D) Sempre escolher a opção com o serviço mais gerenciado

<details><summary>Resposta</summary>

**B** — Leia o cenário completo e anote os requisitos explícitos (ex: "RTO < 1 hora", "sem código customizado", "menor custo"). Cada requisito pode eliminar opções. Algumas questões têm distractors que atendem parte dos requisitos mas violam outros. Identificar TODOS os requisitos antes de avaliar as respostas é a estratégia mais efetiva.

</details>

---

**7.** No dia do exame, quanto tempo dedicar para a primeira passagem pelas 65 questões?

- A) Resolver todas as questões meticulosamente na primeira passagem (sem pular)
- B) ~1,5 minuto por questão na primeira passagem (~97 min); marcar questões difíceis; usar tempo restante para revisar
- C) Pular as primeiras 20 questões (geralmente mais difíceis)
- D) Responder as mais fáceis primeiro (últimas 30 questões)

<details><summary>Resposta</summary>

**B** — Gestão de tempo: 130 minutos / 65 questões = 2 min/questão. Reserve ~97 min para primeira passagem (~1,5 min/questão). Questões que você está confiante: responder e seguir. Questões difíceis: marcar e pular. Com os 33 min restantes, revise as marcadas. Nunca fique preso em uma única questão por 10 minutos.

</details>

---

**8.** Uma questão do exame tem as seguintes opções e pede a resposta "mais segura":
- A) Usar access keys IAM hardcoded no código da aplicação
- B) Usar IAM Role associada ao EC2 instance profile
- C) Armazenar access keys em variáveis de ambiente do EC2
- D) Usar um arquivo ~/.aws/credentials no servidor

<details><summary>Resposta</summary>

**B** — IAM Role via Instance Profile: credenciais temporárias rotacionadas automaticamente pelo STS; nunca expostas em código, env vars ou arquivos. Access keys hardcoded (A), env vars (C) e arquivo de credenciais (D) são todos riscos de vazamento. A regra geral: nunca use long-lived credentials quando IAM Roles são possíveis.

</details>

---

**9.** Qual domínio do exame SAA-C03 tem o maior peso?

- A) Design de Arquiteturas Resilientes (26%)
- B) Design de Arquiteturas de Alta Performance (24%)
- C) Design de Aplicações Seguras (30%)
- D) Design de Arquiteturas Otimizadas em Custo (20%)

<details><summary>Resposta</summary>

**C** — Design de Aplicações Seguras tem 30% do exame — é o domínio mais pesado. Foque em: IAM (roles, policies, conditions), KMS, VPC security (SG vs NACL), S3 (Block Public Access, OAC, pre-signed), Cognito, SecretsManager, GuardDuty, Shield, WAF. 30% das questões são sobre segurança.

</details>

---

**10.** Qual é a pontuação mínima para aprovação no SAA-C03?

- A) 65% (700/1000)
- B) 72% (720/1000)
- C) 75% (750/1000)
- D) 80% (800/1000)

<details><summary>Resposta</summary>

**B** — Score mínimo: **720/1000** (numa escala de 100-1000). Não é 72% das questões corretas — a pontuação usa modelo psicométrico (questões de pruning não pontuam). Na prática, precisar acertar aproximadamente 43-47 das 65 questões pontuadas (existem questões de teste não pontuadas que aparecem aleatórias).

</details>

---

**11.** Uma questão descreve: "a empresa precisa de uma solução que processe dados **em lote** uma vez por dia". Qual serviço/combinação é candidato a resposta correta?

- A) Kinesis Data Streams + Lambda
- B) EventBridge Scheduler + Lambda (ou ECS/Batch)
- C) SQS FIFO + Lambda
- D) Kinesis Data Firehose

<details><summary>Resposta</summary>

**B** — "Uma vez por dia" = processamento agendado. EventBridge Scheduler (ou Rule do tipo `schedule`) + Lambda/ECS Fargate/AWS Batch é o padrão. Kinesis é para streaming contínuo em tempo real, não batch diário. AWS Batch é excelente para jobs de computação pesada em batch.

</details>

---

**12.** Você está no exame e uma questão pede para escolher entre RDS Multi-AZ e Read Replicas. O requisito diz "alta disponibilidade para escrita". O que escolher?

- A) Read Replicas (podem ser promovidas para primary em caso de falha)
- B) RDS Multi-AZ (failover automático síncrono para standy; sem perda de dados de escrita)
- C) Ambos, com Read Replicas apontando para o standby Multi-AZ
- D) Aurora em vez de RDS padrão

<details><summary>Resposta</summary>

**B** — Multi-AZ: replicação **síncrona** para standby em outra AZ. Failover automático em 1-2 minutos. Sem perda de writes (síncrono). Read Replicas: replicação **assíncrona** — podem ter lag; se o primary falhar, requer promoção manual (não automático para RDS — apenas Aurora promove automaticamente).

</details>

---

**13.** Uma questão menciona "custo de saída de dados" (data transfer out). Qual é o impacto arquitetural disso?

- A) Dados transferidos entre regiões AWS são gratuitos
- B) Upload para S3 é gratuito; transferência S3 → internet tem custo (~$0.09/GB); usar CloudFront reduz o custo de transferência
- C) VPC Peering nunca tem custo de transferência de dados
- D) Lambda não tem custo de transferência de dados

<details><summary>Resposta</summary>

**B** — Data transfer pricing: UPLOAD para AWS = gratuito. Download da AWS para internet = ~$0.09/GB. CloudFront tem custo menor por GB que S3 direto + inclui edge caching. Transferência intra-região (mesma AZ) = geralmente gratuito entre serviços. AZ para AZ na mesma região = com custo ($0.01/GB). Entre regiões = sempre tem custo.

</details>

---

**14.** No exame, quando uma questão menciona uma "startup com orçamento limitado" precisando de alta disponibilidade, qual abordagem o exame geralmente favorece?

- A) Multi-region active-active para máxima HA
- B) Multi-AZ com instâncias menores + Auto Scaling (HA sem super-provisionar)
- C) On-Demand instances em única AZ (mais barato)
- D) Reserved Instances de 3 anos imediatamente

<details><summary>Resposta</summary>

**B** — O exame frequentemente testa: alta disponibilidade custo-efetiva. Multi-AZ é suficiente para a maioria dos casos de HA. Instâncias menores + Auto Scaling evitam on-demand caro e desnecessário. Multi-region é para DR (diferente de HA) e custa muito mais. Reserve só após o crescimento estabilizar.

</details>

---

**15.** Qual é o propósito das questões "unscored" (não pontuadas) no exame SAA-C03?

- A) Não existem questões não pontuadas no SAA-C03
- B) São questões de piloting (testando novas questões para futuras versões do exame), distribuídas aleatoriamente entre as 65
- C) São as 5 questões mais fáceis para garantir pontuação mínima
- D) São questões sobre serviços novos que foram anunciados recentemente

<details><summary>Resposta</summary>

**B** — AWS inclui questões de "field trial" ou "pre-operational" — questões novas que estão sendo testadas para calibração. Você não sabe quais são pontuadas e quais não são. Implicação: não pule nenhuma questão (mesmo as que parecem muito difíceis podem ser não-pontuadas; mesmo as fáceis são pontuadas). Responda todas.

</details>

---

## Simulado Completo 2 — 65 Questões

> Distribuição aproximada: Resiliência 17, Performance 16, Segurança 20, Custo 12. Questões marcadas como "Selecione duas" ou "Selecione três" simulam múltipla resposta.

### Domínio 1 — Arquiteturas Resilientes (1-17)

**1.** Uma aplicação web em duas AZs usa ALB e EC2. O banco RDS está em Single-AZ e é ponto único de falha. Qual ajuste atende alta disponibilidade com menor mudança?
- A) Migrar para RDS Multi-AZ
- B) Criar snapshot manual diário
- C) Trocar ALB por NLB
- D) Colocar a instância EC2 em placement group

<details><summary>Resposta</summary>

**A.** RDS Multi-AZ adiciona standby em outra AZ e failover automático. **B** ajuda recuperação, mas não HA. **C** muda o balanceador, não o banco. **D** melhora posicionamento de EC2, não remove o ponto único no RDS.

</details>

**2.** Uma empresa precisa que objetos novos em um bucket S3 sejam copiados para outra região para recuperação de desastre. O que configurar?
- A) S3 Cross-Region Replication com versioning
- B) S3 Transfer Acceleration
- C) S3 Select
- D) S3 Inventory apenas

<details><summary>Resposta</summary>

**A.** CRR replica objetos entre regiões e exige versioning nos buckets. **B** acelera upload. **C** filtra conteúdo de objeto. **D** inventaria metadados, mas não replica.

</details>

**3.** Um serviço assíncrono falha em algumas mensagens e bloqueia o processamento. Qual padrão isola mensagens problemáticas?
- A) Dead-letter queue
- B) NAT Gateway
- C) CloudFront cache policy
- D) EBS snapshot

<details><summary>Resposta</summary>

**A.** DLQ recebe mensagens que excedem tentativas e permite análise sem travar o fluxo. **B** é saída de rede. **C** é cache HTTP. **D** é backup de volume.

</details>

**4.** Uma API regional precisa failover para outra região com controle DNS quando health check falhar. Qual serviço usar?
- A) Route 53 failover routing
- B) AWS Backup
- C) IAM Access Analyzer
- D) S3 Lifecycle

<details><summary>Resposta</summary>

**A.** Route 53 failover usa health checks para responder endpoint secundário. **B** protege backups. **C** analisa acesso. **D** move objetos entre classes.

</details>

**5. (Selecione duas)** Para tornar um processamento em EC2 mais resiliente a falha de AZ, quais ações ajudam?
- A) Usar Auto Scaling Group distribuído em múltiplas AZs
- B) Colocar instâncias atrás de um Load Balancer
- C) Usar uma instância maior em uma única AZ
- D) Desabilitar health checks
- E) Guardar estado apenas no disco local da instância

<details><summary>Resposta</summary>

**A e B.** ASG multi-AZ repõe capacidade e o load balancer envia tráfego para targets saudáveis. **C** mantém ponto único. **D** prejudica detecção de falha. **E** dificulta substituição de instâncias.

</details>

**6.** Um banco Aurora precisa recuperação regional com RPO baixo. Qual opção é mais alinhada?
- A) Aurora Global Database
- B) Backup manual mensal
- C) EBS sc1
- D) SQS FIFO

<details><summary>Resposta</summary>

**A.** Aurora Global Database replica para região secundária com baixa latência. **B** tem RPO alto. **C** é volume EBS frio. **D** é fila, não replicação de banco.

</details>

**7.** Uma aplicação usa sessões locais em EC2 e sofre perda de login após substituição de instância. O que melhora resiliência?
- A) Externalizar sessão em ElastiCache ou DynamoDB
- B) Aumentar o tamanho da instância
- C) Usar AMI mais recente apenas
- D) Trocar Security Group por NACL

<details><summary>Resposta</summary>

**A.** Estado fora da instância permite substituição transparente. **B** não resolve perda de estado. **C** melhora manutenção, não sessão. **D** muda controle de rede, não persistência.

</details>

**8.** Uma fila precisa preservar ordem estrita de eventos por cliente. Qual opção usar?
- A) SQS FIFO com MessageGroupId por cliente
- B) SQS Standard
- C) SNS Standard sem fila
- D) EventBridge Scheduler

<details><summary>Resposta</summary>

**A.** FIFO mantém ordem dentro do grupo. **B** tem ordem best-effort. **C** publica eventos, mas não garante processamento ordenado por cliente. **D** agenda execuções, não ordena eventos.

</details>

**9.** Uma aplicação crítica tem RTO de horas e orçamento baixo. Qual estratégia de DR tende a ser mais custo-efetiva?
- A) Backup and Restore
- B) Active-active full capacity
- C) Multi-site com capacidade total
- D) Duplicar todos os recursos 24/7

<details><summary>Resposta</summary>

**A.** RTO de horas aceita restauração e reduz custo. **B/C/D** reduzem RTO, mas aumentam muito o custo e excedem o requisito.

</details>

**10.** O ALB envia tráfego para instâncias quebradas. Qual configuração corrigir?
- A) Health checks do target group
- B) KMS key policy
- C) S3 bucket ACL
- D) Route 53 geoproximity

<details><summary>Resposta</summary>

**A.** Health checks controlam quais targets recebem tráfego. **B/C** são segurança. **D** roteia DNS, não saúde de targets no ALB.

</details>

**11.** Um workflow com várias etapas precisa retry, timeout e tratamento de erro por etapa. Qual serviço gerenciado usar?
- A) Step Functions
- B) EC2 userdata
- C) S3 Inventory
- D) CloudFront Functions

<details><summary>Resposta</summary>

**A.** Step Functions orquestra estados, retries e catches. **B** inicializa instância. **C** lista objetos. **D** executa lógica leve na borda.

</details>

**12. (Selecione duas)** Para reduzir risco de perda acidental de objetos S3 críticos, escolha:
- A) Versioning
- B) Object Lock quando houver requisito de retenção
- C) Desabilitar MFA na conta root
- D) Tornar o bucket público
- E) Usar apenas lifecycle expiration curto

<details><summary>Resposta</summary>

**A e B.** Versioning permite recuperar versões; Object Lock aplica retenção WORM. **C** piora segurança. **D** expõe dados. **E** pode apagar dados mais cedo.

</details>

**13.** Um consumidor SQS processa mensagens por 2 minutos, mas elas reaparecem após 30 segundos. O que ajustar?
- A) Visibility timeout
- B) Bucket policy
- C) ALB idle timeout apenas
- D) KMS alias

<details><summary>Resposta</summary>

**A.** Visibility timeout deve cobrir o tempo de processamento. **B/D** são segurança. **C** trata conexão ALB, não SQS.

</details>

**14.** Uma empresa quer fanout de eventos para Lambda, SQS e email. Qual serviço é mais direto?
- A) SNS com múltiplas assinaturas
- B) EBS Multi-Attach
- C) NAT Gateway
- D) CloudTrail

<details><summary>Resposta</summary>

**A.** SNS publica para múltiplos assinantes. **B** é armazenamento de bloco. **C** é rede. **D** audita APIs.

</details>

**15.** A aplicação precisa continuar servindo conteúdo estático mesmo com falha na origem S3 regional por desenho multi-origem. Qual recurso ajuda?
- A) CloudFront origin failover
- B) IAM permission boundary
- C) SSM Parameter Store
- D) Inspector

<details><summary>Resposta</summary>

**A.** CloudFront pode alternar para origem secundária quando a primária falha. **B/C/D** não fazem failover de conteúdo.

</details>

**16.** Uma instância EC2 individual precisa recuperar em novo hardware mantendo IP privado e instance ID, quando suportado. O que usar?
- A) EC2 Auto Recovery
- B) Auto Scaling Group sempre
- C) Spot Instance
- D) S3 Replication

<details><summary>Resposta</summary>

**A.** Auto Recovery preserva identidade da instância em falha de hardware compatível. **B** substitui por nova instância. **C** pode ser interrompida. **D** replica objetos.

</details>

**17.** Uma arquitetura precisa processar pedidos sem perder dados se o backend cair temporariamente. Qual padrão usar?
- A) Colocar SQS entre frontend e workers
- B) Chamar worker por IP fixo
- C) Gravar tudo em memória local
- D) Remover retries

<details><summary>Resposta</summary>

**A.** SQS absorve picos e indisponibilidade temporária. **B/C** aumentam acoplamento e perda. **D** reduz resiliência.

</details>

### Domínio 2 — Alta Performance (18-33)

**18.** Usuários globais acessam imagens estáticas no S3 com alta latência. Qual melhoria é mais adequada?
- A) CloudFront
- B) RDS Proxy
- C) SQS DLQ
- D) AWS Backup

<details><summary>Resposta</summary>

**A.** CloudFront entrega em edge locations. **B** otimiza conexões RDS. **C** isola mensagens com erro. **D** faz backup.

</details>

**19. (Selecione duas)** Consultas Athena em CSV grande estão caras e lentas. O que melhora?
- A) Converter para Parquet
- B) Particionar por colunas de filtro frequente
- C) Usar NAT Gateway maior
- D) Remover compressão
- E) Aumentar ACL do bucket

<details><summary>Resposta</summary>

**A e B.** Parquet reduz leitura de colunas e particionamento reduz scan. **C/E** não otimizam consulta. **D** costuma aumentar dados escaneados.

</details>

**20.** Banco em EC2 exige maior IOPS e baixa latência de bloco. Qual volume é candidato?
- A) EBS io2 Block Express
- B) S3 Glacier
- C) EFS IA
- D) Instance metadata

<details><summary>Resposta</summary>

**A.** io2 Block Express é para I/O crítico. **B/C** são storage de objeto/arquivo com outro perfil. **D** não é armazenamento de dados.

</details>

**21.** Uma aplicação com muitas conexões Lambda para RDS sofre exaustão de conexões. Qual serviço ajuda?
- A) RDS Proxy
- B) DAX
- C) CloudFront OAC
- D) Macie

<details><summary>Resposta</summary>

**A.** RDS Proxy faz pooling e melhora gerenciamento de conexões. **B** é cache DynamoDB. **C** protege S3 por CloudFront. **D** identifica dados sensíveis.

</details>

**22.** Uma aplicação DynamoDB precisa leitura de baixa latência para itens repetidos. Qual recurso usar?
- A) DAX
- B) Read Replica RDS
- C) EFS Max I/O
- D) Global Accelerator

<details><summary>Resposta</summary>

**A.** DAX é cache em memória para DynamoDB. **B** é relacional. **C** é file system. **D** acelera tráfego de rede global, não cacheia item.

</details>

**23.** Um serviço TCP global precisa IP fixo anycast e failover rápido para endpoints regionais. Qual serviço?
- A) AWS Global Accelerator
- B) CloudTrail
- C) Amazon Macie
- D) S3 Lifecycle

<details><summary>Resposta</summary>

**A.** Global Accelerator usa anycast e rede AWS. **B/C/D** não aceleram tráfego TCP global.

</details>

**24.** Um cluster HPC em EC2 precisa baixa latência entre nós na mesma AZ. O que escolher?
- A) Cluster placement group
- B) Spread placement group
- C) S3 Standard-IA
- D) ALB path routing

<details><summary>Resposta</summary>

**A.** Cluster placement group aproxima instâncias para baixa latência. **B** espalha para resiliência. **C/D** não resolvem comunicação HPC.

</details>

**25.** Uploads grandes para S3 falham em conexões instáveis. Qual técnica melhora confiabilidade e performance?
- A) Multipart Upload
- B) Single PUT obrigatório
- C) SQS FIFO
- D) ACM

<details><summary>Resposta</summary>

**A.** Multipart divide, paraleliza e permite retomar partes. **B** é menos resiliente para arquivos grandes. **C/D** não otimizam upload.

</details>

**26.** Uma API Lambda em Java precisa reduzir cold start. Qual opção é mais direta para Java compatível?
- A) Lambda SnapStart
- B) S3 Transfer Acceleration
- C) RDS Multi-AZ
- D) NAT Gateway

<details><summary>Resposta</summary>

**A.** SnapStart reduz inicialização para runtimes Java suportados. **B/C/D** não tratam cold start de Lambda.

</details>

**27. (Selecione duas)** Para escalar leitura em Aurora sem alterar profundamente o banco:
- A) Adicionar Aurora Replicas
- B) Usar reader endpoint
- C) Usar standby Multi-AZ como endpoint de leitura manual
- D) Trocar para S3 Glacier
- E) Desabilitar índices

<details><summary>Resposta</summary>

**A e B.** Réplicas e reader endpoint distribuem leituras. **C** não é padrão de leitura do standby. **D** não é banco relacional. **E** tende a piorar consultas.

</details>

**28.** Relatórios Redshift sofrem com muitos usuários simultâneos. Qual recurso pode ajudar?
- A) Concurrency Scaling
- B) SQS visibility timeout
- C) Object Lock
- D) Security Group egress only

<details><summary>Resposta</summary>

**A.** Concurrency Scaling adiciona capacidade para concorrência. **B/C/D** não aumentam concorrência analítica.

</details>

**29.** Um app precisa cache HTTP global e controle de TTL por tipo de conteúdo. Qual serviço?
- A) CloudFront com cache policies
- B) EFS Lifecycle
- C) AWS Config
- D) KMS multi-Region key

<details><summary>Resposta</summary>

**A.** CloudFront controla cache/TTL na borda. **B** move arquivos. **C** avalia configuração. **D** gerencia chaves.

</details>

**30.** Containers ECS precisam descoberta de serviço gerenciada. Qual opção usar?
- A) ECS Service Connect ou AWS Cloud Map
- B) S3 Select
- C) AWS Artifact
- D) EBS snapshot

<details><summary>Resposta</summary>

**A.** Ambos oferecem descoberta/comunicação entre serviços. **B/C/D** não fazem service discovery.

</details>

**31.** Um filesystem compartilhado para workloads Linux precisa acesso simultâneo de várias instâncias. Qual serviço?
- A) Amazon EFS
- B) Amazon EBS anexado a todas as instâncias sem restrição
- C) S3 Glacier Deep Archive
- D) DynamoDB Stream

<details><summary>Resposta</summary>

**A.** EFS é NFS gerenciado multi-AZ. **B** EBS é bloco e não é compartilhamento geral. **C** é arquivo frio. **D** é stream de alterações.

</details>

**32.** Um workload compatível com ARM busca melhor preço/performance em EC2. Qual família considerar?
- A) Graviton
- B) GPU P5 obrigatória
- C) Dedicated Host sempre
- D) T2 com CPU credit esgotado

<details><summary>Resposta</summary>

**A.** Graviton costuma entregar bom preço/performance para cargas compatíveis. **B/C** são caros e específicos. **D** pode limitar performance.

</details>

**33.** Uma API no API Gateway precisa limitar taxa por cliente. Qual recurso usar?
- A) Throttling/usage plans
- B) S3 CRR
- C) EBS encryption
- D) IAM Access Analyzer

<details><summary>Resposta</summary>

**A.** API Gateway permite quotas e throttling. **B/C/D** não limitam taxa de API por cliente.

</details>

### Domínio 3 — Aplicações Seguras (34-53)

**34. (Selecione duas)** Para proteger credenciais de aplicação em ECS, quais práticas são adequadas?
- A) Usar Secrets Manager integrado à task definition
- B) Dar permissão mínima à task role/execution role
- C) Gravar senha na imagem Docker
- D) Colocar senha em repositório Git
- E) Usar bucket público para distribuir segredo

<details><summary>Resposta</summary>

**A e B.** Secrets Manager e roles com menor privilégio reduzem exposição. **C/D/E** vazam segredo ou ampliam risco.

</details>

**35.** Uma empresa quer descobrir PII em buckets S3. Qual serviço?
- A) Amazon Macie
- B) AWS Shield
- C) Amazon DAX
- D) AWS Batch

<details><summary>Resposta</summary>

**A.** Macie classifica dados sensíveis no S3. **B** protege DDoS. **C** cacheia DynamoDB. **D** executa jobs.

</details>

**36.** EC2 e imagens ECR precisam análise de vulnerabilidades. Qual serviço?
- A) Amazon Inspector
- B) Route 53
- C) SQS
- D) CloudFront

<details><summary>Resposta</summary>

**A.** Inspector avalia vulnerabilidades em workloads suportados. **B/C/D** não fazem varredura de vulnerabilidade.

</details>

**37.** Usuários federados precisam acessar AWS sem usuários IAM locais. Qual serviço ajuda?
- A) IAM Identity Center integrado ao IdP
- B) Access keys compartilhadas
- C) Bucket ACL pública
- D) S3 Select

<details><summary>Resposta</summary>

**A.** IAM Identity Center fornece acesso federado. **B** é inseguro. **C/D** não resolvem identidade corporativa.

</details>

**38.** Qual controle impede que um bucket S3 seja acessado por HTTP simples?
- A) Bucket policy negando `aws:SecureTransport=false`
- B) Habilitar Transfer Acceleration
- C) Usar S3 Inventory
- D) Criar Read Replica

<details><summary>Resposta</summary>

**A.** Deny explícito força HTTPS. **B/C/D** não bloqueiam HTTP.

</details>

**39.** Uma aplicação em conta A precisa acessar recurso na conta B com credenciais temporárias. Qual padrão?
- A) IAM Role com trust policy e STS AssumeRole
- B) Usuário root compartilhado
- C) Access key em planilha
- D) NACL inbound allow

<details><summary>Resposta</summary>

**A.** AssumeRole cross-account entrega credenciais temporárias. **B/C** são inseguros. **D** não autoriza API AWS.

</details>

**40.** API pública precisa proteção contra SQL injection e XSS. Qual serviço?
- A) AWS WAF com managed rules
- B) KMS
- C) EBS
- D) AWS Backup

<details><summary>Resposta</summary>

**A.** WAF filtra tráfego HTTP camada 7. **B** criptografa. **C** armazena bloco. **D** faz backup.

</details>

**41.** A empresa precisa registrar chamadas de API para auditoria. Qual serviço?
- A) AWS CloudTrail
- B) Amazon EFS
- C) DAX
- D) NAT Gateway

<details><summary>Resposta</summary>

**A.** CloudTrail registra eventos de API. **B/C/D** não auditam chamadas de API.

</details>

**42. (Selecione duas)** Para acesso privado de EC2 em subnet privada a serviços AWS sem internet:
- A) Gateway endpoint para S3/DynamoDB quando aplicável
- B) Interface endpoint para serviços suportados
- C) Bucket público
- D) Internet Gateway direto na subnet privada
- E) Access key hardcoded

<details><summary>Resposta</summary>

**A e B.** VPC endpoints mantêm tráfego privado. **C/D/E** aumentam exposição ou não resolvem roteamento privado.

</details>

**43.** Uma chave KMS deve ter controle de política pelo cliente. Qual tipo usar?
- A) Customer managed key
- B) AWS owned key
- C) Chave SSH
- D) Certificado ACM público

<details><summary>Resposta</summary>

**A.** Customer managed key permite policy/administração. **B** é invisível ao cliente. **C/D** não são KMS data keys.

</details>

**44.** Qual serviço detecta ameaças com base em logs como CloudTrail, DNS e VPC Flow Logs?
- A) GuardDuty
- B) Athena
- C) CloudFormation
- D) Snowball

<details><summary>Resposta</summary>

**A.** GuardDuty detecta comportamentos maliciosos. **B** consulta dados. **C** provisiona. **D** transfere dados fisicamente.

</details>

**45.** Um bucket S3 deve ficar privado mesmo quando alguém tentar ACL pública. Qual controle amplo habilitar?
- A) S3 Block Public Access
- B) Transfer Acceleration
- C) Multipart Upload
- D) S3 Select

<details><summary>Resposta</summary>

**A.** Block Public Access bloqueia políticas/ACLs públicas conforme configuração. **B/C/D** são performance/consulta.

</details>

**46.** Para acessar instâncias EC2 sem abrir SSH inbound nem gerenciar key pair, use:
- A) SSM Session Manager
- B) FTP público
- C) Telnet
- D) Bucket ACL

<details><summary>Resposta</summary>

**A.** Session Manager fornece acesso auditável sem porta SSH pública. **B/C** são inseguros. **D** não acessa EC2.

</details>

**47.** Um segredo de banco precisa rotação gerenciada. Qual serviço é mais apropriado?
- A) AWS Secrets Manager
- B) S3 Standard
- C) CloudTrail
- D) EBS gp3

<details><summary>Resposta</summary>

**A.** Secrets Manager suporta rotação. **B/C/D** não gerenciam ciclo de vida de segredos.

</details>

**48.** Em S3, qual recurso atende retenção WORM rígida por exigência regulatória?
- A) S3 Object Lock em Compliance mode
- B) Bucket público com versioning
- C) NAT Gateway
- D) CloudWatch metric alarm

<details><summary>Resposta</summary>

**A.** Compliance mode impede exclusão/alteração durante retenção, inclusive por administradores. **B** não basta. **C/D** não aplicam retenção.

</details>

**49.** Uma aplicação precisa certificados TLS públicos com renovação automática quando validados corretamente. Qual serviço?
- A) AWS Certificate Manager
- B) AWS Batch
- C) SQS
- D) DMS

<details><summary>Resposta</summary>

**A.** ACM emite/renova certificados públicos gerenciados. **B/C/D** não gerenciam TLS público.

</details>

**50. (Selecione duas)** Para limitar permissões efetivas em contas da AWS Organizations:
- A) SCPs em OUs/contas
- B) Permission boundaries em roles/usuários quando aplicável
- C) Bucket público
- D) Aumentar permissões AdministratorAccess em todos
- E) Desativar CloudTrail

<details><summary>Resposta</summary>

**A e B.** SCP limita ações no nível de conta/OU e boundary define teto por identidade. **C/D/E** aumentam risco ou reduzem auditoria.

</details>

**51.** Qual serviço ajuda a encontrar recursos com políticas que permitem acesso externo não pretendido?
- A) IAM Access Analyzer
- B) Global Accelerator
- C) ElastiCache
- D) EFS

<details><summary>Resposta</summary>

**A.** Access Analyzer avalia políticas de recursos. **B/C/D** não analisam permissões externas.

</details>

**52.** Tráfego entre VPCs precisa inspeção de firewall gerenciado em camada de rede. Qual serviço considerar?
- A) AWS Network Firewall
- B) AWS WAF apenas
- C) Macie
- D) RDS Proxy

<details><summary>Resposta</summary>

**A.** Network Firewall atua na VPC em camada de rede. **B** é HTTP camada 7. **C** dados sensíveis. **D** conexões RDS.

</details>

**53.** Para relatórios de conformidade da AWS, como SOC e ISO, qual recurso consultar?
- A) AWS Artifact
- B) DynamoDB TTL
- C) S3 Select
- D) EC2 Auto Recovery

<details><summary>Resposta</summary>

**A.** Artifact fornece relatórios de compliance da AWS. **B/C/D** não fornecem documentos de auditoria.

</details>

### Domínio 4 — Custo (54-65)

**54.** Workload batch pode ser interrompido e reprocessado. Qual compra reduz custo?
- A) Spot Instances
- B) On-Demand full time
- C) Dedicated Hosts obrigatórios
- D) Multi-region active-active

<details><summary>Resposta</summary>

**A.** Spot é ideal para interrupção tolerável. **B/C/D** custam mais e não são necessários.

</details>

**55.** Aplicação EC2 24/7 com uso previsível por 1 ano. Qual opção tende a reduzir custo?
- A) Compute Savings Plans ou Reserved Instances
- B) Spot para banco primário crítico
- C) On-Demand sem compromisso sempre
- D) Mais NAT Gateways

<details><summary>Resposta</summary>

**A.** Compromisso reduz custo em carga estável. **B** é arriscado para crítico. **C** custa mais. **D** aumenta custo de rede.

</details>

**56.** Buckets S3 com acesso desconhecido e variável. Qual classe evita escolher camada manualmente?
- A) S3 Intelligent-Tiering
- B) S3 One Zone-IA para tudo
- C) Glacier Deep Archive para dados quentes
- D) EBS io2

<details><summary>Resposta</summary>

**A.** Intelligent-Tiering ajusta camadas por padrão de acesso. **B** reduz resiliência. **C** tem latência de recuperação. **D** é bloco.

</details>

**57.** NAT Gateway processa muito tráfego para S3. Como reduzir custo sem expor internet?
- A) Gateway VPC Endpoint para S3
- B) Outro NAT Gateway
- C) IP público nas instâncias privadas
- D) Bucket público

<details><summary>Resposta</summary>

**A.** Endpoint para S3 evita NAT e mantém tráfego privado. **B** aumenta custo. **C/D** elevam exposição.

</details>

**58.** Para identificar EC2 superdimensionada, use:
- A) AWS Compute Optimizer
- B) AWS Artifact
- C) Shield Standard
- D) Route 53 Resolver

<details><summary>Resposta</summary>

**A.** Compute Optimizer recomenda rightsizing. **B** é compliance. **C** DDoS. **D** DNS.

</details>

**59. (Selecione duas)** Ambiente de desenvolvimento deve reduzir custo fora do horário. Quais ações ajudam?
- A) Agendar stop/start com EventBridge Scheduler e Lambda/SSM
- B) Usar tags e relatórios de custo por ambiente
- C) Converter tudo para Multi-AZ full time sem requisito
- D) Remover budgets
- E) Manter instâncias ociosas 24/7

<details><summary>Resposta</summary>

**A e B.** Agendamento corta horas ociosas e tags melhoram governança. **C/E** aumentam custo. **D** reduz controle financeiro.

</details>

**60.** Consultas ad-hoc ocasionais sobre arquivos no S3. Qual opção evita cluster permanente?
- A) Athena
- B) Redshift provisionado 24/7 sempre
- C) EC2 com banco manual
- D) RDS Multi-AZ

<details><summary>Resposta</summary>

**A.** Athena paga por consulta e lê S3 diretamente. **B/C/D** criam recursos permanentes desnecessários.

</details>

**61.** Arquivos acessados raramente, recriáveis e com menor exigência de resiliência. Qual classe pode reduzir custo?
- A) S3 One Zone-IA
- B) S3 Standard obrigatoriamente
- C) EBS io2
- D) EFS Standard sempre

<details><summary>Resposta</summary>

**A.** One Zone-IA é mais barata, mas perde resiliência multi-AZ. **B/D** custam mais. **C** é bloco de alto desempenho.

</details>

**62.** Uma função Lambda esporádica substitui servidor EC2 ocioso. Qual vantagem de custo?
- A) Paga por invocação/duração, sem idle de servidor
- B) Sempre custa mais que EC2
- C) Exige Dedicated Host
- D) Cobra por AZ reservada

<details><summary>Resposta</summary>

**A.** Lambda é custo-efetiva em carga intermitente. **B** é absoluto falso. **C/D** não se aplicam.

</details>

**63.** Para controlar orçamento mensal com alerta quando custo previsto exceder limite:
- A) AWS Budgets
- B) GuardDuty
- C) Inspector
- D) ACM

<details><summary>Resposta</summary>

**A.** Budgets cria alertas de custo/uso/previsão. **B/C** segurança. **D** certificados.

</details>

**64.** EFS tem muitos arquivos frios. Qual recurso reduziria custo?
- A) EFS Lifecycle Management para IA
- B) EBS io2 para todos os arquivos
- C) Global Accelerator
- D) WAF

<details><summary>Resposta</summary>

**A.** Lifecycle move arquivos pouco acessados para classe mais barata. **B/C/D** não reduzem custo de arquivos frios no EFS.

</details>

**65.** Uma equipe quer estimar custo antes de implantar nova arquitetura. Qual ferramenta usar?
- A) AWS Pricing Calculator
- B) CloudTrail
- C) Macie
- D) SQS

<details><summary>Resposta</summary>

**A.** Pricing Calculator estima custos. **B** audita. **C** detecta PII. **D** enfileira mensagens.

</details>

---

## Simulado Completo 3 — 65 Questões

> Distribuição aproximada: Resiliência 17, Performance 16, Segurança 20, Custo 12. Use este simulado como validação final depois de corrigir o Simulado 2.

### Domínio 1 — Arquiteturas Resilientes (1-17)

**1.** Uma aplicação stateful em EC2 precisa sobreviver a substituição de instância. Qual mudança arquitetural é melhor?
- A) Remover estado local e usar armazenamento gerenciado compartilhado ou banco
- B) Aumentar CPU da instância
- C) Usar apenas IP elástico
- D) Desativar Auto Scaling

<details><summary>Resposta</summary>

**A.** Estado externo permite recriar instâncias sem perda lógica. **B/C** não resolvem estado. **D** reduz resiliência.

</details>

**2.** Um banco RDS precisa suportar falha de AZ com failover automático. Qual opção?
- A) Multi-AZ deployment
- B) Read Replica em mesma AZ apenas
- C) Snapshot manual
- D) S3 Inventory

<details><summary>Resposta</summary>

**A.** Multi-AZ é desenhado para HA. **B** escala leitura e pode ter lag. **C** é recuperação manual. **D** inventaria S3.

</details>

**3.** Mensagens de pedidos não podem ser perdidas quando o processador fica fora do ar. Qual serviço inserir?
- A) SQS
- B) CloudFront
- C) ACM
- D) EBS snapshot

<details><summary>Resposta</summary>

**A.** SQS desacopla e retém mensagens. **B/C/D** não enfileiram trabalho.

</details>

**4. (Selecione duas)** Um desenho multi-AZ para aplicação web geralmente inclui:
- A) ALB em subnets de múltiplas AZs
- B) ASG distribuído em múltiplas AZs
- C) Uma instância manual em única AZ
- D) Banco Single-AZ para produção crítica
- E) Desabilitar health checks

<details><summary>Resposta</summary>

**A e B.** ALB e ASG multi-AZ são base de HA. **C/D/E** introduzem ponto único ou removem detecção.

</details>

**5.** Para DR com ambiente mínimo ligado e escalado durante desastre, use:
- A) Pilot light
- B) Active-active full capacity
- C) Sem backup
- D) S3 Select

<details><summary>Resposta</summary>

**A.** Pilot light mantém componentes essenciais. **B** custa mais e é outra estratégia. **C** é risco. **D** consulta objetos.

</details>

**6.** Um serviço precisa repetir chamadas com backoff e lidar com falha transitória entre etapas. Qual serviço ajuda?
- A) Step Functions
- B) IAM Access Analyzer
- C) EBS sc1
- D) AWS Artifact

<details><summary>Resposta</summary>

**A.** Step Functions suporta retry/backoff/catch. **B/C/D** não orquestram fluxo.

</details>

**7.** Para proteger contra exclusão acidental de stack crítica no CloudFormation:
- A) Termination protection e DeletionPolicy quando aplicável
- B) Abrir bucket público
- C) Usar NAT Gateway
- D) Remover tags

<details><summary>Resposta</summary>

**A.** Esses controles reduzem exclusão acidental. **B/C/D** não protegem stack.

</details>

**8.** Um endpoint global HTTP deve alternar para origem secundária quando a primária falhar. Qual recurso?
- A) CloudFront origin failover
- B) KMS alias
- C) Inspector scan
- D) SSM Parameter Store

<details><summary>Resposta</summary>

**A.** Origin failover muda origem baseada em erro/saúde. **B/C/D** não roteiam tráfego HTTP.

</details>

**9.** SQS Standard entrega uma mensagem mais de uma vez. Como a aplicação deve lidar?
- A) Processamento idempotente
- B) Assumir exatamente uma vez sempre
- C) Desabilitar delete message
- D) Remover DLQ

<details><summary>Resposta</summary>

**A.** Standard é at-least-once; idempotência é essencial. **B** é falso. **C/D** pioram duplicidade/operabilidade.

</details>

**10.** Dados on-premises devem ser copiados periodicamente para S3 com serviço gerenciado. Qual serviço?
- A) AWS DataSync
- B) AWS WAF
- C) DAX
- D) Cognito

<details><summary>Resposta</summary>

**A.** DataSync transfere dados entre on-premises e AWS. **B/C/D** não são migração de arquivos.

</details>

**11. (Selecione duas)** Para melhorar recuperação de desastre de dados S3:
- A) Versioning
- B) Cross-Region Replication
- C) S3 Select apenas
- D) ACL pública
- E) Desligar logs

<details><summary>Resposta</summary>

**A e B.** Versioning e CRR aumentam recuperabilidade. **C** consulta objeto. **D/E** pioram segurança/auditoria.

</details>

**12.** Health check Route 53 falha para primário. O que failover routing faz?
- A) Responde com registro secundário configurado
- B) Cria instâncias EC2
- C) Criptografa objetos
- D) Reduz preço de NAT

<details><summary>Resposta</summary>

**A.** Failover routing alterna resposta DNS. **B/C/D** são fora do escopo.

</details>

**13.** Um sistema de pedidos requer deduplicação de mensagens em janela curta. Qual fila?
- A) SQS FIFO
- B) SQS Standard sem idempotência
- C) SNS Standard apenas
- D) CloudWatch Logs

<details><summary>Resposta</summary>

**A.** FIFO tem deduplication ID/content-based dedup. **B/C/D** não fornecem essa garantia.

</details>

**14.** Para centralizar políticas de backup de EBS, RDS e DynamoDB suportados:
- A) AWS Backup
- B) CloudFront
- C) Kinesis Data Streams
- D) ACM

<details><summary>Resposta</summary>

**A.** AWS Backup centraliza planos/vaults. **B/C/D** não fazem backup centralizado.

</details>

**15.** Um worker demora mais que o visibility timeout e processa duplicado. Correção?
- A) Aumentar visibility timeout ou estender durante processamento
- B) Trocar para bucket público
- C) Desativar DLQ
- D) Usar ACM

<details><summary>Resposta</summary>

**A.** Timeout deve acompanhar duração real. **B/C/D** não tratam duplicidade.

</details>

**16.** Para tolerância a falha de AZ em storage de arquivo Linux compartilhado:
- A) EFS Regional
- B) EBS single-AZ apenas
- C) Instance store
- D) S3 Glacier Deep Archive montado como NFS

<details><summary>Resposta</summary>

**A.** EFS Regional replica em múltiplas AZs. **B/C** são locais/AZ. **D** não é NFS ativo de baixa latência.

</details>

**17.** Um backend não pode ser sobrecarregado por picos de requisições. Qual padrão suaviza carga?
- A) Fila SQS e workers escaláveis
- B) Chamada síncrona direta sem limite
- C) Desabilitar retry
- D) Remover cache

<details><summary>Resposta</summary>

**A.** Fila absorve picos e workers consomem no ritmo possível. **B/C/D** pioram resiliência/performance.

</details>

### Domínio 2 — Alta Performance (18-33)

**18. (Selecione duas)** Para reduzir latência de entrega global de conteúdo estático:
- A) CloudFront
- B) Cache em edge locations
- C) RDS Multi-AZ
- D) SQS DLQ
- E) IAM boundary

<details><summary>Resposta</summary>

**A e B.** CloudFront usa edge cache. **C** é HA de banco. **D** fila de erro. **E** limite de permissão.

</details>

**19.** Aplicação precisa roteamento HTTP por host e path. Qual load balancer?
- A) ALB
- B) NLB apenas
- C) Gateway Load Balancer para HTTP path
- D) CLB obrigatório

<details><summary>Resposta</summary>

**A.** ALB é camada 7. **B** é L4. **C** é para appliances. **D** é legado e não preferido.

</details>

**20.** Um cache gerenciado Redis precisa failover e baixa latência. Qual serviço?
- A) ElastiCache for Redis/Valkey
- B) Athena
- C) AWS Backup
- D) S3 Inventory

<details><summary>Resposta</summary>

**A.** ElastiCache gerencia Redis/Valkey. **B/C/D** não são cache em memória.

</details>

**21.** Para consultas DynamoDB com padrões repetidos e leitura muito baixa latência:
- A) DAX
- B) RDS Proxy
- C) CloudFront OAC
- D) EFS IA

<details><summary>Resposta</summary>

**A.** DAX cacheia DynamoDB. **B** é para RDS. **C** protege origem S3. **D** reduz custo de arquivos frios.

</details>

**22.** Arquivos em S3 são consultados por Athena. Qual formato normalmente melhora performance?
- A) Parquet
- B) Texto sem compressão
- C) Imagem PNG
- D) ZIP monolítico sem partição

<details><summary>Resposta</summary>

**A.** Parquet é colunar e eficiente. **B/D** aumentam scan. **C** não é formato analítico tabular.

</details>

**23.** Instâncias precisam rede de alta largura de banda e baixa latência para processamento paralelo. Qual escolha?
- A) Tipo de instância adequado + placement group cluster quando aplicável
- B) S3 Glacier
- C) IAM Identity Center
- D) AWS Budgets

<details><summary>Resposta</summary>

**A.** Compute e posicionamento importam para HPC. **B/C/D** não melhoram rede entre instâncias.

</details>

**24.** Uma API precisa proteger backend com limite de requests. Qual recurso?
- A) API Gateway throttling
- B) S3 Object Lock
- C) KMS rotation
- D) EBS snapshot

<details><summary>Resposta</summary>

**A.** Throttling limita taxa. **B/C/D** são retenção/cripto/backup.

</details>

**25.** Leitura relacional aumenta muito, mas escrita está ok. Qual opção costuma ajudar?
- A) Read Replicas
- B) Multi-AZ apenas para leitura
- C) Aumentar NAT Gateway
- D) Macie

<details><summary>Resposta</summary>

**A.** Réplicas escalam leitura. **B** é HA, não escala leitura no RDS tradicional. **C/D** irrelevantes.

</details>

**26. (Selecione duas)** Para otimizar upload global de arquivos grandes ao S3:
- A) Multipart Upload
- B) S3 Transfer Acceleration quando latência global justificar
- C) S3 Glacier Deep Archive para upload ativo
- D) Desabilitar retry
- E) Usar arquivo único sem retomada

<details><summary>Resposta</summary>

**A e B.** Multipart e Transfer Acceleration podem melhorar upload grande/global. **C** é arquivamento. **D/E** reduzem confiabilidade.

</details>

**27.** Para workloads de machine learning que precisam filesystem de alta performance ligado ao S3:
- A) FSx for Lustre
- B) SQS FIFO
- C) CloudTrail
- D) Parameter Store

<details><summary>Resposta</summary>

**A.** FSx for Lustre atende HPC/ML e pode integrar com S3. **B/C/D** não são filesystem HPC.

</details>

**28.** Muitos clientes acessam uma aplicação TCP regional de diferentes países. Quer acelerar sem cache HTTP. Qual serviço?
- A) Global Accelerator
- B) CloudFront apenas
- C) Macie
- D) S3 Select

<details><summary>Resposta</summary>

**A.** Global Accelerator acelera TCP/UDP sem depender de cache. **B** é CDN HTTP. **C/D** não aceleram rede.

</details>

**29.** Uma função Lambda precisa pacote de dependências muito grande. Qual opção suportada pode ajudar?
- A) Lambda container image
- B) Inline code no console
- C) S3 Object Lock
- D) NACL

<details><summary>Resposta</summary>

**A.** Container image suporta pacotes maiores. **B** é limitado. **C/D** não tratam dependências.

</details>

**30.** Um banco PostgreSQL recebe muitas conexões curtas de Lambda. Melhor componente?
- A) RDS Proxy
- B) DAX
- C) CloudFront
- D) AWS Artifact

<details><summary>Resposta</summary>

**A.** RDS Proxy reutiliza conexões. **B** é DynamoDB. **C** é CDN. **D** compliance.

</details>

**31.** Para reduzir latência de DNS escolhendo endpoint saudável mais próximo:
- A) Route 53 latency-based routing com health checks
- B) AWS Backup
- C) KMS key rotation
- D) SQS DLQ

<details><summary>Resposta</summary>

**A.** Roteamento por latência considera região/saúde. **B/C/D** não roteiam DNS por latência.

</details>

**32.** Uma aplicação precisa processamento assíncrono de stream em tempo quase real. Qual serviço é candidato?
- A) Kinesis Data Streams
- B) S3 Glacier Deep Archive
- C) AWS Budgets
- D) ACM

<details><summary>Resposta</summary>

**A.** Kinesis Data Streams atende streaming. **B** é arquivamento. **C/D** não processam stream.

</details>

**33. (Selecione duas)** Para melhorar performance de consultas em RDS sem mudar engine:
- A) Índices adequados
- B) Read replicas para leitura
- C) Remover todos os índices
- D) Usar Glacier para tabelas ativas
- E) Abrir o banco publicamente

<details><summary>Resposta</summary>

**A e B.** Índices e réplicas melhoram consulta/leitura. **C** piora. **D** não é banco ativo. **E** é risco de segurança.

</details>

### Domínio 3 — Aplicações Seguras (34-53)

**34.** Aplicação em Lambda precisa acessar DynamoDB com permissões mínimas. O que configurar?
- A) IAM execution role com ações/tabelas necessárias
- B) Usuário root
- C) Access key no código
- D) Bucket ACL

<details><summary>Resposta</summary>

**A.** Execution role fornece credenciais temporárias e escopo mínimo. **B/C** são inseguros. **D** não autoriza DynamoDB.

</details>

**35.** Uma empresa quer impedir criação de recursos fora de `us-east-1` e `sa-east-1`. Qual controle organizacional?
- A) SCP com condição `aws:RequestedRegion`
- B) CloudWatch dashboard
- C) S3 Lifecycle
- D) EFS IA

<details><summary>Resposta</summary>

**A.** SCP limita ações por região nas contas da OU. **B/C/D** não bloqueiam criação regional.

</details>

**36.** Para proteger API HTTP contra bots e padrões OWASP, use:
- A) AWS WAF
- B) EBS io2
- C) DataSync
- D) RDS Proxy

<details><summary>Resposta</summary>

**A.** WAF atua em camada 7. **B/C/D** não filtram tráfego HTTP malicioso.

</details>

**37.** Bucket S3 deve ser acessado apenas por CloudFront. Qual padrão moderno?
- A) Origin Access Control
- B) Bucket público
- C) IAM user compartilhado
- D) NAT Gateway

<details><summary>Resposta</summary>

**A.** OAC restringe origem ao CloudFront. **B/C** aumentam exposição. **D** não controla acesso ao S3.

</details>

**38.** A empresa quer detectar buckets S3 públicos e recursos não conformes continuamente. Qual serviço?
- A) AWS Config com regras
- B) DAX
- C) CloudFront Functions
- D) Snowball Edge apenas

<details><summary>Resposta</summary>

**A.** Config avalia configurações contra regras. **B/C/D** não fazem compliance contínuo.

</details>

**39.** Qual serviço fornece credenciais temporárias para assumir role?
- A) AWS STS
- B) S3 Select
- C) EFS
- D) Athena

<details><summary>Resposta</summary>

**A.** STS emite credenciais temporárias. **B/C/D** não gerenciam credenciais.

</details>

**40.** Um segredo deve ser criptografado e rotacionado automaticamente. Melhor opção:
- A) Secrets Manager com KMS
- B) Texto claro no Parameter Store Standard
- C) AMI pública
- D) EBS snapshot público

<details><summary>Resposta</summary>

**A.** Secrets Manager integra criptografia e rotação. **B** pode ser insuficiente para rotação. **C/D** expõem dados.

</details>

**41. (Selecione duas)** Para auditoria e detecção de atividade suspeita:
- A) CloudTrail
- B) GuardDuty
- C) Desativar logs para reduzir ruído
- D) Compartilhar root
- E) Usar bucket público para logs

<details><summary>Resposta</summary>

**A e B.** CloudTrail registra atividade e GuardDuty detecta ameaças. **C/D/E** pioram auditoria/segurança.

</details>

**42.** Qual serviço ajuda a validar permissões externas em políticas de recursos?
- A) IAM Access Analyzer
- B) Global Accelerator
- C) EBS
- D) Kinesis Firehose

<details><summary>Resposta</summary>

**A.** Access Analyzer identifica acesso externo. **B/C/D** não analisam políticas IAM.

</details>

**43.** Em EKS, qual padrão evita credenciais fixas nos pods?
- A) IRSA
- B) Access key em Secret Kubernetes sem rotação
- C) Role admin no node para todos
- D) Bucket público

<details><summary>Resposta</summary>

**A.** IRSA associa service account a IAM role. **B/C** ampliam risco. **D** é irrelevante.

</details>

**44.** Para criptografar dados em repouso em S3 com chave gerenciada pelo cliente:
- A) SSE-KMS com customer managed key
- B) HTTP sem TLS
- C) ACL pública
- D) S3 Select

<details><summary>Resposta</summary>

**A.** SSE-KMS usa KMS e CMK do cliente. **B/C** são inseguros. **D** consulta dados.

</details>

**45.** Para conexão privada de aplicações a um serviço exposto por outra VPC sem peering amplo:
- A) AWS PrivateLink
- B) Internet Gateway público
- C) S3 Lifecycle
- D) Macie

<details><summary>Resposta</summary>

**A.** PrivateLink expõe serviço via interface endpoint. **B** usa internet. **C/D** não conectam VPCs.

</details>

**46.** Qual serviço ajuda com relatórios de compliance e acordos da AWS?
- A) AWS Artifact
- B) Lambda SnapStart
- C) DAX
- D) Spot Fleet

<details><summary>Resposta</summary>

**A.** Artifact reúne relatórios e documentos. **B/C/D** são performance/custo.

</details>

**47.** Para bloquear acesso público acidental em todos os buckets de uma conta:
- A) S3 Block Public Access em nível de conta
- B) Criar mais ACLs públicas
- C) Desativar CloudTrail
- D) Usar EIP

<details><summary>Resposta</summary>

**A.** Conta pode bloquear políticas/ACLs públicas. **B/C/D** não protegem.

</details>

**48.** Qual serviço detecta vulnerabilidades em funções Lambda suportadas e imagens de container?
- A) Amazon Inspector
- B) Amazon Cognito
- C) SQS
- D) Route 53

<details><summary>Resposta</summary>

**A.** Inspector cobre vulnerabilidades em recursos suportados. **B/C/D** não escaneiam CVEs.

</details>

**49. (Selecione duas)** Para proteger logs de auditoria no S3:
- A) Criptografia
- B) Bucket policy restritiva e, se requerido, Object Lock
- C) Bucket público para facilitar análise
- D) Desabilitar versioning sempre
- E) Compartilhar access keys

<details><summary>Resposta</summary>

**A e B.** Criptografia e política/imutabilidade protegem logs. **C/D/E** reduzem segurança/recuperabilidade.

</details>

**50.** Qual opção evita SSH público para administração de EC2?
- A) SSM Session Manager
- B) Porta 22 aberta para internet
- C) Key pair compartilhada por email
- D) Telnet

<details><summary>Resposta</summary>

**A.** Session Manager é auditável e dispensa inbound SSH. **B/C/D** são inseguros.

</details>

**51.** Para autenticar usuários finais com MFA e login social:
- A) Amazon Cognito
- B) IAM root
- C) AWS Backup
- D) EBS

<details><summary>Resposta</summary>

**A.** Cognito atende identidade de usuários finais. **B** é conta AWS. **C/D** não autenticam usuários finais.

</details>

**52.** Qual controle de rede é stateful e aplicado no nível da interface/instância?
- A) Security Group
- B) NACL
- C) Route table
- D) Internet Gateway

<details><summary>Resposta</summary>

**A.** SG é stateful. **B** é stateless em subnet. **C/D** roteiam/conectam, não filtram como SG.

</details>

**53.** Para DDoS avançado com suporte DRT e proteção de custo em recursos cobertos:
- A) AWS Shield Advanced
- B) Macie
- C) Athena
- D) RDS Proxy

<details><summary>Resposta</summary>

**A.** Shield Advanced adiciona suporte e proteções além do Standard. **B/C/D** não são proteção DDoS avançada.

</details>

### Domínio 4 — Custo (54-65)

**54.** Um ambiente não produtivo fica ocioso à noite. Qual medida simples reduz custo?
- A) Agendar stop/start
- B) Tornar multi-region
- C) Usar Dedicated Host
- D) Aumentar instâncias

<details><summary>Resposta</summary>

**A.** Desligar recursos ociosos corta horas cobradas. **B/C/D** aumentam custo.

</details>

**55.** Workload com uso estável e compromisso de gasto em compute. Qual opção?
- A) Savings Plans
- B) Spot apenas para tudo
- C) S3 One Zone-IA
- D) WAF

<details><summary>Resposta</summary>

**A.** Savings Plans reduzem custo para uso previsível. **B** pode interromper. **C/D** não compram compute.

</details>

**56.** Logs antigos devem ser arquivados por anos com acesso raro. Qual caminho?
- A) S3 Lifecycle para Glacier/Deep Archive conforme requisito
- B) EBS io2 sempre ligado
- C) RDS Multi-AZ
- D) Global Accelerator

<details><summary>Resposta</summary>

**A.** Lifecycle move para classes frias. **B/C/D** são caros/inadequados para arquivo.

</details>

**57.** Alto custo de transferência S3 para internet em site público. O que pode ajudar?
- A) CloudFront
- B) Mais NAT Gateway
- C) RDS Proxy
- D) Macie

<details><summary>Resposta</summary>

**A.** CloudFront cacheia e pode reduzir custo/latência. **B** aumenta rede. **C/D** não entregam conteúdo.

</details>

**58. (Selecione duas)** Para governança de custos:
- A) AWS Budgets
- B) Tags de alocação de custo
- C) Desativar billing alerts
- D) Remover ownership de recursos
- E) Tornar tudo público

<details><summary>Resposta</summary>

**A e B.** Budgets alertam e tags atribuem custo. **C/D/E** reduzem controle e segurança.

</details>

**59.** Dados com acesso imprevisível no S3 sem querer gerenciar lifecycle manual. Qual classe?
- A) Intelligent-Tiering
- B) Glacier Deep Archive obrigatório
- C) One Zone-IA para dados críticos
- D) EBS st1

<details><summary>Resposta</summary>

**A.** Intelligent-Tiering automatiza camadas. **B/C** podem violar latência/resiliência. **D** é bloco.

</details>

**60.** Tarefas ECS tolerantes a interrupção buscam menor custo. Qual opção?
- A) Fargate Spot
- B) Dedicated Host
- C) RDS Multi-AZ
- D) CloudTrail

<details><summary>Resposta</summary>

**A.** Fargate Spot reduz custo para tarefas tolerantes a interrupção. **B/C/D** não reduzem compute ECS nesse cenário.

</details>

**61.** Para estimar arquitetura antes da implantação:
- A) AWS Pricing Calculator
- B) GuardDuty
- C) Inspector
- D) Cognito

<details><summary>Resposta</summary>

**A.** Pricing Calculator estima custo planejado. **B/C/D** não fazem estimativa financeira.

</details>

**62.** Workload intermitente de API pequena. Qual opção tende a evitar custo idle?
- A) Lambda + API Gateway
- B) EC2 grande 24/7
- C) Dedicated Host
- D) RDS provisionado sem necessidade

<details><summary>Resposta</summary>

**A.** Serverless paga por uso e escala para zero em muitos cenários. **B/C/D** mantêm capacidade ociosa.

</details>

**63.** DynamoDB tem tráfego previsível alto e constante. Qual modo pode ser mais econômico se bem dimensionado?
- A) Provisioned com auto scaling/reservas quando aplicável
- B) On-demand sempre em qualquer cenário
- C) EC2 manual sem motivo
- D) S3 Glacier

<details><summary>Resposta</summary>

**A.** Provisioned pode ser mais barato em carga previsível. **B** é ótimo para imprevisível, mas não sempre mais barato. **C/D** não substituem bem o caso.

</details>

**64.** NAT Gateway caro por acesso a DynamoDB desde subnets privadas. Melhor alternativa:
- A) Gateway VPC Endpoint para DynamoDB
- B) Mais NAT Gateways
- C) IP público nas instâncias
- D) Bucket ACL

<details><summary>Resposta</summary>

**A.** Endpoint evita NAT para DynamoDB. **B/C** aumentam custo/exposição. **D** não se aplica.

</details>

**65.** Para localizar recursos ociosos e oportunidades de economia na conta:
- A) Cost Explorer, Trusted Advisor e Compute Optimizer conforme caso
- B) ACM apenas
- C) SQS FIFO
- D) Route 53 health check apenas

<details><summary>Resposta</summary>

**A.** Essas ferramentas apoiam análise de custo e otimização. **B/C/D** não fazem diagnóstico financeiro geral.

</details>

---
_Credito autoral: Thiago Cardoso - [LinkedIn](https://www.linkedin.com/in/analyticsthiagocardoso)_

