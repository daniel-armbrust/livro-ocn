# Apêndice A: OCI HOWTOs

# A.7 Perguntas e Respostas sobre OCI

## A.7.1 OCI Core Architecture & Networking

### 1. Como você projetaria uma arquitetura altamente disponível e tolerante a falhas em OCI em todas as regiões?

### 2. Quais são os principais componentes da Virtual Cloud Network (VCN) do OCI e como você protege o tráfego entre sub-redes?

### 3. Explique as diferenças entre Local Peering e Remote Peering. Quando você usaria cada um?

### 4. Como você implementa uma configuração de nuvem híbrida com OCI e data centers locais?

### 5. Quais são as diferenças entre o OCI Load Balancer e o API Gateway?

### 6. Qual é a função do Dynamic Routing Gateway (DRG) em uma configuração de nuvem híbrida?

## A.7.2 Security & Identity

### 1. Como você projeta uma arquitetura OCI segura usando políticas do IAM, compartimentos e grupos dinâmicos?

### 2. Qual é sua abordagem para criptografar dados em repouso (data at rest) e em trânsito no OCI (in transit)?

### 3. Como você usa o Cloud Guard e as Zonas de Segurança para aplicar as melhores práticas?

### 4. Explique como compartimentos e políticas funcionam juntos no OCI.

### 5. Como você gerencia segredos e credenciais com segurança no OCI?

## A.7.3 Compute, Storage & Database

### 1. Como você escolhe entre instâncias Bare Metal, VM e Container Instances no OCI?

### 2. Explique o ciclo de vida (lifecycle) de um Block Volume e como você lida com cenários de backup e restauração.

### 3. Como você arquitetaria o Oracle RAC ou o Data Guard no OCI para alta disponibilidade?

### 4. Qual é a diferença entre Autonomous Transaction Processing (ATP) e Autonomous Data Warehouse (ADW)? Quando escolher um em vez do outro?

### 5. Como o OCI Autonomous Database lida com escalabilidade e aplicação de patches?

### 6. Como você configura clusters WebLogic no OCI usando imagens do Marketplace?

### 7. Quais são os parâmetros de ajuste que você ajustaria no Oracle DB para um desempenho lento de OLTP?

### 8. Qual é a diferença entre PGA e SGA? Como você os ajustaria?

### 9. Quais são as melhores práticas para monitorar o desempenho do Oracle Golden Gate?

### 10. Explique o impacto do processamento de consultas paralelas e quando não usá-lo (parallel query processing). 

### 11. Qual é a diferença entre o Data Guard e o Active Data Guard no OCI?

### 12. Qual é a função do Resource Manager no gerenciamento de CPU e I/O no Oracle DB?

### 13. Como você ajustaria as configurações da JVM no WebLogic para melhorar o desempenho?

### 14. Quais ferramentas você usaria para analisar relatórios AWR e ASH?

### 15. Como funciona o autoscaling em instâncias de computação OCI?

### 16. Quais são as causas comuns de contenção em ambientes RAC?

### 17. Como você solucionaria um cenário de alto uso de CPU em um servidor WebLogic hospedado no OCI?

## A.7.4 Automation, DevOps & Monitoring

### 1. Como automatizar o provisionamento de infraestrutura no OCI? Quais ferramentas você utiliza (Terraform, Resource Manager, etc.)?

### 2. Como você monitora a integridade e o desempenho dos recursos no OCI? Qual é a sua abordagem para alertas proativos?

### 3. Como configurar alertas e monitoramento para recursos OCI usando o OCI Monitoring?

## A.7.5 Scenario-Based Questions

### 1. Você precisa migrar um grande banco de dados local para o OCI com o mínimo de tempo de inatividade. Como você planejaria e executaria isso?

### 2. Seu aplicativo está apresentando latência intermitente no OCI. Que medidas você tomaria para solucionar o problema?

### 3. Você precisa reduzir custos em uma configuração OCI atual sem afetar o desempenho. Quais áreas você exploraria?

### 4. Descreva um cenário em tempo real em que o Oracle Integration Cloud foi usado para integração B2B.

## A.7.6 Containers & Modern Workloads

### 1. Como você implanta e gerencia clusters do Kubernetes usando o OCI OKE?

### 2. Compare OKE e Compute Instances para cargas de trabalho baseadas em contêineres. Quais são as vantagens e desvantagens?

### 3. Como você garantiria o registro, o monitoramento e a escalabilidade do seu cluster OKE no OCI?

## A.7.6 Perguntas comportamentais, colaboração em equipe, stakeholder

### 1. Conte-me sobre uma ocasião em que você lidou com um stakeholder difícil. Como você lidou com isso?

### 2. Como você garante a satisfação do cliente durante uma jornada de transformação na nuvem?

### 3. Dê um exemplo de uma situação em que você assumiu a responsabilidade por uma tarefa que não lhe foi atribuída inicialmente.

### 4. Descreva uma situação em que sua equipe enfrentou um conflito. Qual foi seu papel na resolução?

### 5. Como você equilibra as prioridades técnicas com os objetivos de negócios em um projeto de migração para a nuvem?

### 6. Conte-nos sobre uma ocasião em que você fracassou e como se recuperou.

### 7. Como você comunica soluções complexas para stakeholders que não são técnicos?

### 8. Se você fosse designado para liderar o design de uma solução de nuvem para um cliente global, como você abordaria isso?
