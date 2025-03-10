# Capítulo 2: OCI Foundations

# 2.3 Modelos de Cobraça

Um dos principais benefícios que a computação em nuvem trouxe é a redução de custos. Gerenciar esses custos envolve realizar estimativas, orçamentos e controle. Devido à vasta gama de recursos que o OCI disponibiliza e que podem ser facilmente criados, muitas vezes a análise prévia das necessidades de custos acaba ficando em segundo plano.

Dito isso, é fundamental entender como o OCI cobra pelos seus diferentes serviços e qual é a real necessidade do seu negócio. Começar a responder algumas questões, como: 

_"Esse servidor de desenvolvimento ou homologação precisa ficar ligado 24 horas por dia ou podemos mantê-lo ativo apenas 8 horas por dia, durante 5 dias da semana?"_

Começar a responder e refletir sobre questões como essa ajudará a otimizar os custos e a utilizar os recursos de forma mais eficiente, garantindo que você pague apenas pelo que realmente precisa. Esse é o segredo da economia que a Computação em Nuvem proporciona. Ao adotar uma abordagem consciente e estratégica em relação ao uso de recursos, você pode maximizar os benefícios da nuvem e minimizar despesas.

Começaremos pelo entendimento de como alguns dos serviços são cobrados e forma como você paga por eles pode reduzir o custo final de utilização.

## 2.3.1 Pay-As-You-Go ou Upfront Subscription

Devemos entender que um recurso, seja um Banco de Dados, uma Compute Instance, etc., quando solicitado para sua criação, tem um custo mais alto do que um recurso que você previu utilizar ao longo de todo o ano, por exemplo.

É aqui que entram os _Modelos de Cobrança_ que o OCI disponibiliza. Basicamente, existem dois modelos:

### Pay-As-You-Go

### Upfront Subscription

## 2.3.2 Free Tier e o Always Free

Há dois modos de utilização gratuita que se tornam disponíveis após a criação e ativação da sua conta no OCI. São eles:

### Free Tier

Após criar e ativar sua conta no OCI, a Oracle oferece **_US$300_** em créditos válidos por até **_30 dias_**, que podem ser utilizados em qualquer serviço disponível no OCI. Esse benefício é conhecido como _[Modo Gratuito](https://www.oracle.com/br/cloud/free/)_ ou _[Free Tier](https://www.oracle.com/br/cloud/free/)_ e é disponibilizado como um período de avaliação logo após a conclusão da ativação da sua nova conta no OCI.

!!! note "NOTA"
    Consulte _["Perguntas frequentes do Modo Gratuito da OCI Cloud"](https://www.oracle.com/br/cloud/free/faq/)_ para maiores detalhes sobre o _[Modo Gratuito](https://www.oracle.com/br/cloud/free/)_.

!!! note "NOTA"
    Lembrando que o _[Modo Gratuito](https://www.oracle.com/br/cloud/free/)_ não inclui SLAs. Isso quer dizer que, usuários que usam apenas recursos de uso livre não podem utilizar o _[Oracle Support](https://www.oracle.com/br/support/)_.

### Always Free

Todas as contas criadas no OCI, sejam gratuitas ou pagas, possuem um _[conjunto de recursos](https://docs.oracle.com/pt-br/iaas/Content/FreeTier/freetier_topic-Always_Free_Resources.htm)_ disponíveis para uso na _[Home Region](https://docs.oracle.com/pt-br/iaas/Content/Identity/regions/managingregions.htm#Home)_, conhecidos como _[Always Free](https://docs.oracle.com/pt-br/iaas/Content/FreeTier/freetier_topic-Always_Free_Resources.htm)_. Os recursos _[Always Free](https://docs.oracle.com/pt-br/iaas/Content/FreeTier/freetier_topic-Always_Free_Resources.htm)_ são vitalícios, ou seja, não há cobrança e estarão sempre disponíveis para uso gratuito enquanto sua conta estiver ativa.

Os recursos elegíveis ao _[Always Free](https://docs.oracle.com/pt-br/iaas/Content/FreeTier/freetier_topic-Always_Free_Resources.htm)_ podem ser consultados através do link _"[Recursos Always Free](https://docs.oracle.com/pt-br/iaas/Content/FreeTier/freetier_topic-Always_Free_Resources.htm)"_. 

Alguns dos serviços elegíveis incluem:

- Até duas instâncias de computação do tipo AMD shape VM.Standard.E2.1.Micro.
- 4 OCPUs e 24 GB de memória, que podem ser utilizados para até quatro instâncias de computação do tipo ARM shape VM.Standard.A1.
- 200 GB de Block Volume.
- 20 GB de Object Storage.
- Três tabelas Oracle NoSQL Database com até 25 GB de armazenamento, além de 133 milhões de leituras e 133 milhões de gravações por mês.
- Dois Oracle Autonomous Database com 1 OCPU e 20 GB de armazenamento.
- Um Load Balancer com largura de banda mínima e máxima de 10 Mbps.

Esses serviços permitem que você explore e utilize o OCI sem custos, enquanto sua conta estiver ativa.

!!! note "NOTA"
    Sempre consulte o link _"[Recursos Always Free](https://docs.oracle.com/pt-br/iaas/Content/FreeTier/freetier_topic-Always_Free_Resources.htm)"_ para obter uma lista completa e atualizada dos recursos elegíveis ao  _[Always Free](https://docs.oracle.com/pt-br/iaas/Content/FreeTier/freetier_topic-Always_Free_Resources.htm)_.