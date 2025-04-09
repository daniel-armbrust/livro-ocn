---
hide:
  - toc
---

# Capítulo 1: Introdução a Computação em Nuvem

# 1.7 Cloud Native

_[Cloud Native](https://en.wikipedia.org/wiki/Cloud-native_computing)_ é um termo que se refere a uma abordagem de desenvolvimento voltada para aplicações projetadas e executadas nativamente na nuvem. Essas aplicações são projetadas para serem distribuídas e desenvolvidas com o objetivo de aproveitar ao máximo as características e benefícios da Computação em Nuvem, como escalabilidade, resiliência e agilidade.

Uma aplicação que se beneficia dos recursos da nuvem possui a capacidade de se antecipar a falhas e manter sua estabilidade, mesmo diante de indisponibilidades na infraestrutura, sejam elas planejadas ou não _[(zero downtime)](https://en.wikipedia.org/wiki/Downtime)_. Nesse contexto, a _"indisponibilidade"_ pode se referir tanto a problemas técnicos quanto também a qualquer alteração que exija a implementação de um novo código.

É importante dizer que aplicações Cloud Native não se limitam a serem executadas apenas em serviços básicos do modelo _IaaS_, como rede, máquinas virtuais ou bare metal. Em vez disso, elas são projetadas para tiraram o máximo de proveito dos diversos serviços e recursos oferecidos pela nuvem. Uma abordagem que se restringe apenas ao _"move to cloud"_, não torna sua aplicação Cloud Native.

Como discutido na seção sobre DevOps, a responsabilidade de manter o _[Uptime](https://en.wikipedia.org/wiki/Uptime)_ das aplicações não recai apenas sobre a equipe de operações, mas também sobre os desenvolvedores. Ambas as equipes têm a responsabilidade de projetar sistemas com _[baixo acoplamento](https://en.wikipedia.org/wiki/Loose_coupling)_ que sejam resilientes, gerenciáveis e observáveis.

Arquiteturas de _[microserviços](https://en.wikipedia.org/wiki/Microservices)_ são especialmente adequadas nesse contexto, pois promovem a decomposição de uma _[aplicação monolítica](https://en.wikipedia.org/wiki/Monolithic_application)_ em serviços menores, autônomos e distribuídos, evitando assim os chamados _[pontos únicos de falha](https://en.wikipedia.org/wiki/Single_point_of_failure)_. Cada serviço possui uma única responsabilidade, e a proposta é que esses serviços colaborem entre si para formar a aplicação como um todo.

Nesse contexto, _Computação em Nuvem_ refere-se ao ambiente onde o software é executado, enquanto _Cloud Native_ diz respeito à forma como esse software é projetado e executado.

Além de tudo o que já foi dito, desenvolver software de acordo com os padrões Cloud Native frequentemente contribui para a redução de custos, pois elimina o _[overprovisioning](https://en.wikipedia.org/wiki/Overprovisioning)_ ao permitir que os recursos sejam escalados conforme a demanda de utilização. 

!!! note "NOTA"
    Overprovisioning é um termo utilizado em ambientes de computação e infraestrutura de TI que se refere à prática de alocar mais recursos do que o necessário para atender à demanda de uma aplicação ou serviço.

Aqui estão os principais componentes e características que compõem uma aplicação cloud native:

### **Contêineres**

Os contêineres, como os fornecidos pelo _Docker_, são usados para empacotar microserviços e suas dependências em um ambiente isolado. Isso garante que os serviços sejam executados de maneira consistente em diferentes ambientes, desde o desenvolvimento até a produção.

### **Microserviços**

As aplicações _Cloud Native_ são frequentemente construídas usando uma arquitetura de microserviços, onde a aplicação é dividida em serviços pequenos e independentes. Cada microserviço é responsável por uma funcionalidade específica e pode ser desenvolvido, implantado e escalado de forma independente.

### **Orquestração de Contêineres**

Ferramentas de orquestração, como Kubernetes, são usadas para gerenciar a implantação, escalabilidade e operação de contêineres. Elas ajudam a automatizar tarefas como balanceamento de carga, recuperação de falhas e gerenciamento de configuração.

### **Escalabilidade**

As aplicações _Cloud Native_ são projetadas para escalar horizontalmente, o que significa que novos instâncias de serviços podem ser adicionadas ou removidas conforme a demanda. Isso permite que a aplicação se adapte rapidamente a mudanças no tráfego.

### **Resiliência**

Uma aplicação _Cloud Native_ deve ser resiliente, ou seja, capaz de se recuperar rapidamente de falhas. Isso é alcançado por meio de práticas como redundância, replicação de dados e monitoramento contínuo.

### **DevOps e Automação**

As práticas de DevOps são fundamentais para aplicações _Cloud Native_. Através de técnicas CI/CD, elas permitem que as equipes integrem e implantem código de forma rápida e eficiente, garantindo que novas funcionalidades e correções sejam entregues aos usuários rapidamente.

### **Serviços Gerenciados**

As aplicações _Cloud Native_ frequentemente utilizam serviços gerenciados oferecidos pelos provedores de nuvem, como bancos de dados, serviços de armazenamento, serviços de autenticação e muito mais. Isso permite que as equipes se concentrem no desenvolvimento de funcionalidades em vez de gerenciar a infraestrutura.

### **API-First**

As aplicações _Cloud Native_ são frequentemente construídas com uma abordagem API-first, onde as interfaces de programação de aplicativos (APIs) são projetadas e documentadas antes do desenvolvimento. Isso facilita a integração entre diferentes serviços e sistemas.

### **Observabilidade**

A observabilidade é crucial para entender o comportamento da aplicação em produção. Isso inclui monitoramento, logging e tracing distribuído, permitindo que as equipes identifiquem e resolvam problemas rapidamente.

### **Segurança**

A segurança deve ser incorporada em todas as etapas do ciclo de vida da aplicação, desde o desenvolvimento até a produção. Isso inclui práticas como autenticação e autorização, criptografia de dados e gerenciamento de vulnerabilidades.

## 1.7.1 Cloud Native Computing Foundation (CNCF)

A _[CNCF](https://www.cncf.io/)_, ou _[Cloud Native Computing Foundation](https://www.cncf.io/)_, fundada em 2015, é uma organização sem fins lucrativos associada à _[Linux Foundation](https://www.linuxfoundation.org/)_, dedicada a promover e facilitar o desenvolvimento e a adoção de tecnologias nativas da nuvem.

![alt_text](./img/cncf-logo-1.png "Cloud Native Computing Foundation")

_[CNCF](https://www.cncf.io/)_ promove, por meio de um ecossistema de projetos de código aberto e independentes de fornecedores, a adoção de paradigmas que possibilitam o desenvolvimento de aplicações _escaláveis, resilientes, gerenciáveis e observáveis_. Isso permite a implementação de mudanças de alto impacto de forma frequente e previsível, com o mínimo de esforço.

Conforme mencionado em seu _[FAQ](https://www.cncf.io/about/faq/#why-is-cncf-needed)_, as tecnologias da CNCF não estão sujeitas ao chamado _[vendor lock-in](https://en.wikipedia.org/wiki/Vendor_lock-in)_ e são portáveis entre diferentes provedores de nuvem.

!!! note "NOTA"
    Consulte a definição de [Cloud Native da CNCF na versão 1.1](https://github.com/cncf/toc/blob/main/DEFINITION.md#portugu%C3%AAs-brasileiro), que descreve os princípios e características fundamentais desse conceito.

A CNCF hospeda diversos projetos que possibilitam o desenvolvimento de aplicações Cloud Native sem o risco de _[vendor lock-in](https://en.wikipedia.org/wiki/Vendor_lock-in)_, garantindo a portabilidade entre diferentes provedores de nuvem.

![alt_text](./img/cncf-projects-logo-1.png "Projetos desenvolvidos pela CNFC")

!!! note "NOTA"
    Consulte ["Graduated and Incubating Projects"](https://www.cncf.io/projects/) para acessar a lista dos projetos mantidos pela CNCF.