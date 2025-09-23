---
hide:
  - toc
---

# Capítulo 1: Introdução a Computação em Nuvem

# 1.7 Cloud Native

<a href="https://en.wikipedia.org/wiki/Cloud-native_computing" target="_blank">Cloud Native</a> é um termo que se refere a uma abordagem de desenvolvimento voltada para aplicações projetadas e executadas nativamente na nuvem. Essas aplicações são projetadas para serem distribuídas e desenvolvidas com o objetivo de aproveitar ao máximo as características e benefícios da Computação em Nuvem, como escalabilidade, resiliência e agilidade.

Uma aplicação que se beneficia dos recursos da nuvem possui a capacidade de se antecipar a falhas e manter sua estabilidade, mesmo diante de indisponibilidades na infraestrutura, sejam elas planejadas ou não <a href="https://en.wikipedia.org/wiki/Downtime" target="_blank">(zero downtime)</a>. Nesse contexto, a _"indisponibilidade"_ pode se referir tanto a problemas técnicos quanto também a qualquer alteração que exija a implementação de um novo código.

É importante dizer que aplicações Cloud Native não se limitam a serem executadas apenas em serviços básicos do modelo _IaaS_, como rede, máquinas virtuais ou bare metal. Em vez disso, elas são projetadas para tiraram o máximo de proveito dos diversos serviços e recursos oferecidos pela nuvem. Uma abordagem que se restringe apenas ao _"move to cloud"_, não torna sua aplicação Cloud Native.

Como discutido na seção sobre DevOps, a responsabilidade de manter o <a href="https://en.wikipedia.org/wiki/Uptime" target="_blank">Uptime</a> das aplicações não recai apenas sobre a equipe de operações, mas também sobre os desenvolvedores. Ambas as equipes têm a responsabilidade de projetar sistemas com <a href="https://en.wikipedia.org/wiki/Loose_coupling" target="_blank">baixo acoplamento</a> que sejam resilientes, gerenciáveis e observáveis.

Arquiteturas baseadas em <a href="https://en.wikipedia.org/wiki/Microservices" target="_blank">microserviços</a> são especialmente adequadas nesse contexto, pois promovem a decomposição de uma <a href="https://en.wikipedia.org/wiki/Monolithic_application" target="_blank">aplicação monolítica</a> em serviços menores, autônomos e distribuídos, evitando assim os chamados <a href="https://en.wikipedia.org/wiki/Single_point_of_failure" target="_blank">pontos únicos de falha</a>. Cada serviço possui uma única responsabilidade, e a proposta é que esses serviços colaborem entre si para formar a aplicação como um todo.

Nesse contexto, _Computação em Nuvem_ refere-se ao ambiente onde o software é executado, enquanto _Cloud Native_ diz respeito à forma como esse software é projetado e executado.

Além de tudo o que já foi dito, desenvolver software de acordo com os padrões Cloud Native frequentemente contribui para a redução de custos, pois elimina o <a href="https://en.wikipedia.org/wiki/Overprovisioning" target="_blank">overprovisioning</a> ao permitir que os recursos sejam escalados conforme a demanda de utilização. 

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

A <a href="https://www.cncf.io/" target="_blank">CNCF</a>, ou <a href="https://www.cncf.io/" target="_blank">Cloud Native Computing Foundation</a>, fundada em 2015, é uma organização sem fins lucrativos associada à <a href="https://www.linuxfoundation.org/" target="_blank">Linux Foundation</a>, dedicada a promover e facilitar o desenvolvimento e a adoção de tecnologias nativas da nuvem.

![alt_text](./img/cncf-logo-1.png "Cloud Native Computing Foundation")

<a href="https://www.cncf.io/" target="_blank">CNCF</a> promove, por meio de um ecossistema de projetos de código aberto e independentes de fornecedores, a adoção de paradigmas que possibilitam o desenvolvimento de aplicações _escaláveis, resilientes, gerenciáveis e observáveis_. Isso permite a implementação de mudanças de alto impacto de forma frequente e previsível, com o mínimo de esforço.

Conforme mencionado em seu <a href="https://www.cncf.io/about/faq/#why-is-cncf-needed" target="_blank">FAQ</a>, as tecnologias da <a href="https://www.cncf.io/" target="_blank">CNCF</a> não estão sujeitas ao chamado <a href="https://en.wikipedia.org/wiki/Vendor_lock-in" target="_blank">vendor lock-in</a> e são portáveis entre diferentes provedores de nuvem.

!!! note "NOTA"
    Consulte <a href="https://github.com/cncf/toc/blob/main/DEFINITION.md#portugu%C3%AAs-brasileiro" target="_blank"><i>"Cloud Native da CNCF versão 1.1"</i></a>, que descreve os princípios e características fundamentais desse conceito.

A <a href="https://www.cncf.io/" target="_blank">CNCF</a> hospeda diversos projetos que possibilitam o desenvolvimento de aplicações <a href="https://en.wikipedia.org/wiki/Cloud-native_computing" target="_blank">Cloud Native</a> sem o risco de <a href="https://en.wikipedia.org/wiki/Vendor_lock-in" target="_blank">vendor lock-in</a>, garantindo a portabilidade entre diferentes provedores de nuvem.

![alt_text](./img/cncf-projects-logo-1.png "Projetos desenvolvidos pela CNFC")

!!! note "NOTA"
    Consulte <a href="(https://www.cncf.io/projects/" target="_blank"><i>"Graduated and Incubating Projects"</i></a> para acessar a lista dos projetos mantidos pela CNCF.