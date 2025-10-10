---
hide:
  - toc
---

# Capítulo 4: Serviços Auxiliares e Persistência de Dados

# 4.2 Persistência de dados com o Oracle NoSQL

## 4.2.1 SQL vs. NoSQL

O principal propósito de um banco de dados é armazenar, gerenciar e recuperar grandes volumes de dados de forma eficiente e segura.

No <a href="https://pt.wikipedia.org/wiki/Modelo_relacional" target="_blank">modelo relacional</a>, os dados são organizados em tabelas, onde cada tabela é composta por linhas e colunas. Essas tabelas podem se relacionar umas com as outras, **formando relações** que constituem a base do <a href="https://pt.wikipedia.org/wiki/Modelo_relacional" target="_blank">modelo relacional</a>. É por essa razão que os bancos de dados que implementam esse modelo são conhecidos como **Sistemas de Gerenciamento de Banco de Dados Relacional (SGBD)** ou, em inglês, **Relational Database Management System (RDBMS)**.

![alt_text](./img/sql-table-relationship-1.png "Modelo Relacional #1")

Bancos de dados relacionais, como <a href="https://docs.oracle.com/en/database/oracle/oracle-database/23/index.html" target="_blank">Oracle Database</a>, <a href="https://docs.oracle.com/pt-br/iaas/mysql-database/home.htm" target="_blank">MySQL</a> e <a href="https://docs.oracle.com/pt-br/iaas/Content/postgresql/home.htm" target="_blank">PostgreSQL</a>, desempenham um papel vital na persistência segura das informações, além de gerenciar múltiplos acessos de escrita concorrente por meio de <a href="https://pt.wikipedia.org/wiki/Transa%C3%A7%C3%A3o_(banco_de_dados)" target="_blank"><i><b>transações</b></i></a>.

O termo <a href="https://pt.wikipedia.org/wiki/Transa%C3%A7%C3%A3o_(banco_de_dados)" target="_blank"><i>"transação"</i></a> refere-se a <a href="https://pt.wikipedia.org/wiki/Transa%C3%A7%C3%A3o_(banco_de_dados)" target="_blank">transações</a> <a href="https://pt.wikipedia.org/wiki/ACID" target="_blank">ACID (Atômicas, Consistentes, Isoladas e Duráveis)</a>, que asseguram a consistência dos dados, permitindo a adição, exclusão ou modificação de múltiplos registros em diferentes tabelas por meio de uma única operação. As <a href="https://pt.wikipedia.org/wiki/Transa%C3%A7%C3%A3o_(banco_de_dados)" target="_blank">transações</a> incorporam o conceito de unidade de trabalho, garantindo sucesso total ou falha total (tudo ou nada), sem espaço para um meio termo. Além disso, as <a href="https://pt.wikipedia.org/wiki/Transa%C3%A7%C3%A3o_(banco_de_dados)" target="_blank">transações</a> permitem decidir se as alterações devem ser _persistidas (commit)_ ou _descartadas (rollback)_. 

Já os bancos de dados do tipo <a href="https://docs.oracle.com/en/cloud/paas/nosql-cloud/dtddt/" target="_blank">NoSQL</a>, representam uma nova abordagem para o armazenamento e gerenciamento de dados, diferente do <a href="https://pt.wikipedia.org/wiki/Modelo_relacional" target="_blank">modelo relacional</a>. Eles foram desenvolvidos para operar em grandes <a href="https://pt.wikipedia.org/wiki/Cluster" target="_blank">clusters de computadores</a>, que favorecem a [escalabilidade horizontal](../capitulo-1/terminologias-da-computacao-em-nuvem.md#escalabilidade-scalability), e para atender à necessidade de aplicações que exigem um modelo de dados mais flexível ou **schemaless**.

**NoSQL ("Not SQL" ou "Not Only SQL")** não possui uma definição precisa. Ele é utilizado para descrever vários bancos de dados **não relacionais**, como <a href="https://redis.io/" target="_blank">Redis</a>, <a href="https://www.mongodb.com/" target="_blank">MongoDB</a>, <a href="https://docs.oracle.com/en/cloud/paas/nosql-cloud/dtddt/" target="_blank">Oracle NoSQL Database</a>, <a href="https://neo4j.com/" target="_blank">Neo4J</a>, entre outros.

Diferente dos bancos de dados do tipo <a href="https://docs.oracle.com/en/cloud/paas/nosql-cloud/dtddt/" target="_blank">NoSQL</a>, bancos de dados relacionais não conseguem [escalar horizontalmente](../capitulo-1/terminologias-da-computacao-em-nuvem.md#escalabilidade-scalability) devido ao funcionamento das <a href="https://pt.wikipedia.org/wiki/ACID" target="_blank">transações ACID</a>, que são incompatíveis com a execução em <a href="https://pt.wikipedia.org/wiki/Cluster" target="_blank">clusters de computadores</a>. Isso ocorre porque não é possível garantir a consistência dos dados nem realizar um <a href="https://pt.wikipedia.org/wiki/Join_(SQL)" target="_blank">JOIN</a> sobre dados distribuídos entre várias máquinas do cluster.

Para exemplificar, imagine uma instrução SQL que realiza um <a href="https://pt.wikipedia.org/wiki/Join_(SQL)" target="_blank">JOIN</a> entre diferentes tabelas armazenadas em várias máquinas conectadas à rede (<a href="https://pt.wikipedia.org/wiki/Cluster" target="_blank">clusters de computadores</a>). Esse <a href="https://pt.wikipedia.org/wiki/Join_(SQL)" target="_blank">JOIN</a>, que precisa recuperar dados de diferentes tabelas pela rede, pode enfrentar problemas como alta latência ou até mesmo erros de conexão, resultando na impossibilidade de retornar dados ou em um retorno parcial das informações.

![alt_text](./img/sql-cluster-join-1.png "SQL Cluster JOIN #1")

Por outro lado, os bancos de dados relacionais foram projetados para operar em uma única máquina. Isso permite que as <a href="https://pt.wikipedia.org/wiki/ACID" target="_blank">transações ACID</a> sejam viáveis, uma vez que as tabelas estão contidas em uma única camada de storage, que pode ser dividida entre múltiplos discos conectados por barramentos de alta velocidade.

![alt_text](./img/sql-join-storage-1.png "SQL JOIN #1")

É importante mencionar que os bancos de dados <a href="https://docs.oracle.com/en/cloud/paas/nosql-cloud/dtddt/" target="_blank">NoSQL</a> não substituem os bancos de dados relacionais, e vice-versa. Os bancos de dados <a href="https://docs.oracle.com/en/cloud/paas/nosql-cloud/dtddt/" target="_blank">NoSQL</a>, que lidam com dados não estruturados, complementam os bancos de dados SQL em soluções empresariais. Na prática, é fundamental entender as necessidades do negócio e identificar onde cada tecnologia se _"encaixa melhor"_.

### **Resumo das principais diferenças**

![alt_text](./img/sql-vs-nosql-1.png "SQL vs. NoSQL #1")

## 4.2.2 Tipos de Banco de Dados NoSQL

A maioria dos bancos de dados <a href="https://docs.oracle.com/en/cloud/paas/nosql-cloud/dtddt/" target="_blank">NoSQL</a> é baseada em alguma forma de estrutura chave/valor, sendo as quatro principais categorias as seguintes:

![alt_text](./img/nosql-tipos-1.png "Tipos de NoSQL #1")

- **Chave/Valor**
    - Os dados são armazenados por meio de chaves únicas.
    - Aqui, o banco de dados não conhece nem se preocupa com o valor ao qual a chave se refere. Assim, a recuperação de dados só é possível por meio de consultas que envolvam as chaves.
    
- **Documentos**
    - É bastante similar à implementação chave/valor e neste caso, o banco de dados conhece o valor (documento) ao qual a chave se refere.

- **Grafos**
    - Semelhante ao modelo relacional.
    - É especialmente útil para dados altamente interconectados, uma vez que a estrutura de um grafo revela de forma natural os relacionamentos entre os objetos.

- **Colunar**
    - O armazenamento colunar é semelhante a uma tabela.

O <a href="https://docs.oracle.com/en/cloud/paas/nosql-cloud/dtddt/" target="_blank">Oracle NoSQL</a> suporta tanto os tipos chave/valor, quanto documento e colunar na mesma tabela.

![alt_text](./img/nosql-tipos-2.png "Tipos de NoSQL #1")

## 4.2.3 Introdução ao Oracle NoSQL Database Cloud Service

O <a href="https://docs.oracle.com/en/cloud/paas/nosql-cloud/dtddt/" target="_blank">Oracle NoSQL Database Cloud Service</a> é um serviço de banco de dados <a href="https://docs.oracle.com/en/cloud/paas/nosql-cloud/dtddt/" target="_blank">NoSQL</a> disponível no [OCI](../capitulo-3/introducao-ao-oci.md), totalmente gerenciado e que oferece suporte ao armazenamento de documentos <a href="https://pt.wikipedia.org/wiki/JSON" target="_blank">JSON</a>, dados do tipo chave/valor e dados em colunas (tabelas).

O serviço já inclui, por padrão, monitoramento, alta disponibilidade (com dados distribuídos automaticamente entre [Fault Domains](../capitulo-3/introducao-ao-oci.md#313-fault-domains-fd) e [Availability Domains](../capitulo-3/introducao-ao-oci.md#312-availability-domains-ad)), fácil escalabilidade com um tempo de resposta baixo. 

O serviço também oferece outros recursos adicionais, incluindo:

- Suporte a transações ACID.
- Atualizações parciais em documentos JSON.
- Criação de índices adicionais.
- Manipulação e acesso aos dados via linguagem SQL padrão.
- TTL (Tempo de Vida), permitindo a definição de um tempo de expiração para as linhas da tabela.
- Replicação de dados entre diferentes regiões por meio do _Global Active Tables_.

!!! note "NOTA"
    Para mais informações sobre o serviço, consulte o link <a href="https://docs.oracle.com/en/cloud/paas/nosql-cloud/dtddt/" target="_blank"><i>"Oracle NoSQL Database Cloud Service"</i></a>.

### **Armazenamento, Unidades de Escrita e Leitura** 

Para utilizar o serviço, você precisa criar tabelas que representam o seu modelo de dados (esquema) e especificar a quantidade total de armazenamento, além de duas propriedades que controlam as capacidades de leitura e escrita da tabela (throughput). São elas:

- **Unidades de Escrita ou Gravação (WU - Write Unit)**
    - Uma unidade de escrita corresponde a um throughput de até 1 kilobyte (KB) de dados por segundo para operações como inserção, atualização ou exclusão de um registro. Atualizações de índices também consomem unidades de escrita.
    - Por exemplo: um registro com menos de 1 KB requer 1 unidade de escrita. Para operações em registros de 1,5 KB, são necessárias 2 unidades de escrita.

- **Unidades de Leitura (RU - Read Unit)**
    - Uma unidade de leitura corresponde a um throughput de até 1 kilobyte (KB) de dados por segundo em operações de leitura eventualmente consistentes.
    - Por exemplo, um registro com menos de 1 KB de dados exige apenas 1 unidade de leitura eventualmente consistente. Para um registro que contém 1,5 KB de dados, serão necessárias 2 unidades de leitura eventualmente consistentes.

- **Capacidade de Armazenamento (Storage)**
    - A capacidade de armazenamento refere-se ao total disponível em gigabytes (GB) para a tabela de dados NoSQL, representando a quantidade máxima de informações que podem ser armazenadas.

Ao lidar com dados distribuídos, como nos bancos de dados <a href="https://docs.oracle.com/en/cloud/paas/nosql-cloud/dtddt/" target="_blank">NoSQL</a>, outros dois conceitos se tornam fundamentais durante o processo de leitura dos dados que são:

- **Consistência de Leitura Eventual**
    - Isso indica que os dados retornados de uma operação de leitura podem não ser os mais recentemente gravados.
    - Para uma melhor compreensão, imagine que uma operação de escrita (inserção, atualização ou exclusão) foi recentemente executada. Os dados dessa operação precisam ser replicados em todos os nós do cluster para garantir a consistência das informações. O tempo necessário para essa replicação pode impactar a consistência das leituras. Dependendo das exigências do seu negócio, essa latência pode ser aceitável e é denominada **consistência eventual** ou **eventualmente consistente**.

- **Consistência de Leitura Absoluta**
    - Os dados retornados a partir de uma operação de leitura, são os mais recentes gravados.
    - Neste caso, uma operação de leitura é executada em vários nós do cluster para comparar a consistência dos dados entre eles.

Por meio das APIs do <a href="https://docs.oracle.com/en/cloud/paas/nosql-cloud/dtddt/" target="_blank">NoSQL</a>, é possível especificar o tipo de leitura desejada, seja ela Eventual ou Absoluta.

## 4.2.4 Tabelas da Aplicação OCI PIZZA

A aplicação **OCI PIZZA** utiliza quatro tabelas do serviço <a href="https://docs.oracle.com/en/cloud/paas/nosql-cloud/dtddt/" target="_blank">NoSQL</a>, cujos dados são replicados entre as regiões **sa-saopaulo-1** e **sa-vinhedo-1** através da funcionalidade <a href="https://docs.oracle.com/en/cloud/paas/nosql-cloud/gasnd/index.html" target="_blank">Global Active Tables</a>. 

Abaixo, segue uma descrição de cada uma delas:

- **pizza**
    - Tabela que armazena informações sobre o cardápio de pizzas, incluindo o nome da pizza, uma descrição e o nome do arquivo correspondente à imagem da pizza.
    - O nome do arquivo da imagem corresponde ao arquivo que foi transferido para o [Object Storage](./object-storage.md).

- **user**
    - Tabela que armazena os usuários da aplicação, incluindo nome, e-mail, senha, telefone e o status de confirmação do cadastro, indicando se o usuário validou seu registro.
    - Cada novo usuário recebe um e-mail com um link para confirmar seu cadastro após a inscrição.

- **user.order**
    - A tabela **user.order** é do tipo **Child** e estabelece um relacionamento com a tabela **user**. Ela é utilizada para registrar os pedidos de pizzas realizados pelos usuários (ordens de compra).
    - O <a href="https://docs.oracle.com/en/cloud/paas/nosql-cloud/dtddt/" target="_blank">Oracle NoSQL</a> utiliza a notação de ponto entre os nomes das tabelas para representar relacionamentos entre elas.

- **email_verification**
    - Tabela de dados temporários utilizada para confirmar o cadastro de novos usuários e para o processo de redefinição de senha.
    - Cada novo usuário recebe um e-mail com um link que contém um token temporário, utilizado para ativar o cadastro. O processo de redefinição de senha segue a mesma lógica.
    - Essa tabela também utiliza a funcionalidade que remove automaticamente registros com mais de um dia de idade (`TTL 1 DAYS`). Assim, qualquer registro que ultrapassar um dia, será automaticamente excluído pelo serviço.

Para criar a tabela `pizza` na região **sa-saopaulo-1**, no [compartimento](../capitulo-3/iam-limites-cotas-e-audit.md#compartimentos) `cmp-appl` do ambiente de produção, utilize o seguinte comando:

```bash linenums="1"
$ oci nosql table create \
> --region "sa-saopaulo-1" \
> --compartment-id "ocid1.compartment.oc1..aaaaaaaaaaaaaaaabbbbbbbbccc" \
> --name "pizza" \
> --table-limits "{\"capacityMode\": \"PROVISIONED\", \"maxReadUnits\": 5, \"maxWriteUnits\": 5, \"maxStorageInGBs\": 2}" \
> --wait-for-state "SUCCEEDED" \
> --ddl-statement "
     CREATE TABLE IF NOT EXISTS pizza (
        id INTEGER,
        name STRING,
        description STRING,
        image STRING,
        price NUMBER,
        json_replica JSON,
     PRIMARY KEY(id))"
```

!!! note "NOTA"
    Os scripts para a criação das tabelas de ambas as [regiões](../capitulo-3/introducao-ao-oci.md#311-região) do [OCI](../capitulo-3/introducao-ao-oci.md) estão localizados no diretório <a href="https://github.com/daniel-armbrust/ocn-ocipizza/tree/main/scripts/capitulo-4" target="_blank">"scripts/capitulo-4"</a> do <a href="https://github.com/daniel-armbrust/ocn-ocipizza" target="_blank">repositório de códigos</a> da aplicação **OCI PIZZA**. Os arquivos estão nomeados como <a href="https://github.com/daniel-armbrust/ocn-ocipizza/blob/main/scripts/capitulo-4/nosql-tables-saopaulo.sh" target="_blank">"nosql-tables-saopaulo.sh"</a> e <a href="https://github.com/daniel-armbrust/ocn-ocipizza/blob/main/scripts/capitulo-4/nosql-tables-vinhedo.sh" target="_blank">"nosql-tables-vinhedo.sh"</a>.

O parâmetro `--table-limits` especifica o throughput máximo de escrita  (`maxReadUnits`), o throughput máximo de leitura (`maxWriteUnits`), a capacidade de armazenamento máxima em gigabytes (`maxStorageInGBs`) e o modo de capacidade da tabela (`capacityMode`).

A capacidade da tabela (`capacityMode`) pode ser definida como `ON_DEMAND` ou `PROVISIONED`. Se o valor `ON_DEMAND` for especificado, o <a href="https://docs.oracle.com/en/cloud/paas/nosql-cloud/dtddt/" target="_blank">Oracle NoSQL</a> irá escalar automaticamente o armazenamento (`maxStorageInGBs`) e o throughput (unidades de escrita e leitura) conforme a demanda de utilização aumenta. 

Por outro lado, o valor `PROVISIONED`, utilizado pela aplicação **OCI PIZZA**, exige especificar os valores para `maxReadUnits`, `maxWriteUnits` e `maxStorageInGBs`. Quando a capacidade máxima é atingida para qualquer um desses parâmetros, o serviço retorna um erro que requer a intervenção do administrador para ajuste da nova capacidade.

Permitir que o serviço <a href="https://docs.oracle.com/en/cloud/paas/nosql-cloud/dtddt/" target="_blank">Oracle NoSQL</a> escale automaticamente a tabela quando necessário (`ON_DEMAND`) é financeiramente mais caro do que realizar ajustes manuais conforme necessário (`PROVISIONED`).

Por exemplo, para ajustar o parâmetro `maxReadUnits` para o valor `15`, utilize o seguinte comando:

```bash linenums="1"
$ oci nosql table update \
> --region "sa-saopaulo-1" \
> --compartment-id "ocid1.compartment.oc1..aaaaaaaaaaaaaaaabbbbbbbbccc" \
> --table-name-or-id "pizza" \
> --table-limits "{\"capacityMode\": \"PROVISIONED\", \"maxRea
dUnits\": 15,\"maxWriteUnits\": 5, \"maxStorageInGBs\": 2}" \
> --wait-for-state "SUCCEEDED" \
> --force
```

!!! note "NOTA"
    Independentemente de o ajuste de limites ser feito apenas em um dos parâmetros, todos eles devem estar incluídos no comando de atualização da tabela (`maxReadUnits`, `maxWriteUnits` e `maxStorageInGBs`).

### **Child Tables**

### **<a href="https://docs.oracle.com/en/cloud/paas/nosql-cloud/gasnd/index.html" target="_blank">Global Active Tables</a>**

<a href="https://docs.oracle.com/en/cloud/paas/nosql-cloud/gasnd/index.html" target="_blank">Global Active Tables</a> permite a criação de tabelas que podem ser replicadas em diversas [regiões](../capitulo-3/introducao-ao-oci.md#311-região) do [OCI](../capitulo-3/introducao-ao-oci.md), garantindo que qualquer atualização realizada em uma tabela em uma [região](../capitulo-3/introducao-ao-oci.md#311-região) seja automaticamente propagada para as tabelas réplicas nas outras [regiões](../capitulo-3/introducao-ao-oci.md#311-região) participantes.

