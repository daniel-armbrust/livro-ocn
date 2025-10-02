---
hide:
  - toc
---

# Capítulo 4: Serviços Auxiliares e Persistência de Dados

# 4.1 Object Storage

## 4.1.1 O que é o Object Storage?

O <a href="https://docs.oracle.com/pt-br/iaas/Content/Object/home.htm" target="_blank">Object Storage</a> é um serviço que oferece uma plataforma de armazenamento de dados não estruturados, ilimitado de alto desempenho, seguro, escalável, durável, além de estar disponível em múltiplas [regiões](../capitulo-3/introducao-ao-oci.md#311-região).

**_Multi-região_** refere-se ao fato de que o serviço de <a href="https://docs.oracle.com/pt-br/iaas/Content/Object/home.htm" target="_blank">Object Storage</a> é disponibilizado nas várias [regiões](../capitulo-3/introducao-ao-oci.md#311-região) do [OCI](../capitulo-3/introducao-ao-oci.md) por meio de uma **_URL Base_** específica. Alguns exemplos incluem:

- **São Paulo, Brasil (sa-saopaulo-1)**
    - <a href="https://objectstorage.sa-saopaulo-1.oraclecloud.com" target="_blank">https://objectstorage.sa-saopaulo-1.oraclecloud.com</a>

- **Vinhedo, Brasil (sa-vinhedo-1)**
    - <a href="https://objectstorage.sa-vinhedo-1.oraclecloud.com" target="_blank">https://objectstorage.sa-vinhedo-1.oraclecloud.com</a>

- **Montreal, Canadá (ca-toronto-1)**
    - <a href="https://objectstorage.ca-montreal-1.oraclecloud.com" target="_blank">https://objectstorage.ca-montreal-1.oraclecloud.com</a>

Isso significa que é possível distribuir e recuperar conteúdo através da Internet e que estejam fisicamente mais próximos dos usuários da aplicação, o que resulta em uma melhoria principalmente na latência de acesso aos dados.

!!! note "NOTA"
    É possível acessar os objetos armazenados no <a href="https://docs.oracle.com/pt-br/iaas/Content/Object/home.htm" target="_blank">Object Storage</a> de forma privada a partir de uma a <a href="https://docs.oracle.com/pt-br/iaas/Content/Network/Tasks/Overview_of_VCNs_and_Subnets.htm" target="_blank">VCN</a> por meio de um recurso chamado <a href="https://docs.oracle.com/pt-br/iaas/Content/Network/Tasks/servicegateway.htm#overview" target="_blank">Service Gateway</a>, eliminando a necessidade de utilizar a Internet. O <a href="https://docs.oracle.com/pt-br/iaas/Content/Network/Tasks/servicegateway.htm#overview" target="_blank">Service Gateway</a> será abordado no [Capítulo 5](../capitulo-5/index.md).

Algumas das principais características do <a href="https://docs.oracle.com/pt-br/iaas/Content/Object/home.htm" target="_blank">Object Storage</a> incluem:

- **Seguro**
    - Todos os objetos armazenados no <a href="https://docs.oracle.com/pt-br/iaas/Content/Object/home.htm" target="_blank">Object Storage</a> são automaticamente criptografados antes de serem salvos. Além disso, o serviço oferece a opção de criptografia dos objetos utilizando uma chave fornecida pelo cliente.
    - O acesso aos objetos também é controlado pelo [Serviço IAM](../capitulo-3/iam-limites-cotas-e-audit.md).

- **Escalável**
    - Escalável significa que o serviço oferece espaço praticamente ilimitado, ajustando-se automaticamente de acordo com a demanda de uso.

- **Durável**
    - Os objetos são armazenados em vários servidores de forma redundante sem qualquer intervenção. Isso significa que o <a href="https://docs.oracle.com/pt-br/iaas/Content/Object/home.htm" target="_blank">Object Storage</a> mantém cópias dos objetos entre vários servidores dentro da [região](../capitulo-3/introducao-ao-oci.md#311-região).
    - Em [regiões](../capitulo-3/introducao-ao-oci.md#311-região) com mais de um [Availability Domain (AD)](../capitulo-3/introducao-ao-oci.md#312-availability-domains-ad), os dados são replicados automaticamente entre os [ADs](../capitulo-3/introducao-ao-oci.md#312-availability-domains-ad) da [região](../capitulo-3/introducao-ao-oci.md#311-região).

- **Compatível com Amazon S3**
    - O <a href="https://docs.oracle.com/pt-br/iaas/Content/Object/home.htm" target="_blank">Object Storage</a> é totalmente compatível com o <a href="https://docs.oracle.com/pt-br/iaas/Content/Object/Tasks/s3compatibleapi.htm" target="_blank">Amazon S3</a>, permitindo que você migre sua aplicação do <a href="https://docs.oracle.com/pt-br/iaas/Content/Object/Tasks/s3compatibleapi.htm" target="_blank">Amazon S3</a> para o <a href="https://docs.oracle.com/pt-br/iaas/Content/Object/home.htm" target="_blank">Object Storage</a> sem a necessidade de modificar o código.
    
## 4.1.2 Bucket

Um <a href="https://docs.oracle.com/pt-br/iaas/Content/Object/Tasks/managingbuckets.htm" target="_blank">bucket</a> é um contêiner lógico que funciona basicamente como um _"diretório raiz"_ dentro do <a href="https://docs.oracle.com/pt-br/iaas/Content/Object/home.htm" target="_blank">Object Storage</a>, a partir do qual é possível armazenar e recuperar objetos (download).

Um <a href="https://docs.oracle.com/pt-br/iaas/Content/Object/Tasks/managingbuckets.htm" target="_blank">bucket</a> possui **_dois modos de acesso_** que são definidos durante sua criação:

- **Privado (`NoPublicAccess`)**
    - Um <a href="https://docs.oracle.com/pt-br/iaas/Content/Object/Tasks/managingbuckets.htm" target="_blank">bucket</a> privado requer um usuário autenticado e com a devida autorização para acessar os objetos armazenados.

- **Público (`ObjectRead` ou `ObjectReadWithoutList`)**
    - Um <a href="https://docs.oracle.com/pt-br/iaas/Content/Object/Tasks/managingbuckets.htm" target="_blank">bucket</a> público pode ser acessado de forma anônima, sem a necessidade de autenticação ou autorização. Isso significa que os objetos armazenados nele estão disponíveis para qualquer pessoa na Internet.

Independentemente de o <a href="https://docs.oracle.com/pt-br/iaas/Content/Object/Tasks/managingbuckets.htm" target="_blank">bucket</a> ser público ou privado, existem duas opções que determinam como o acesso aos objetos pode ser realizado:

- **Listar e Download (`ObjectRead`)**
    - Permite que os usuários façam download e visualizem todos os objetos armazenados no <a href="https://docs.oracle.com/pt-br/iaas/Content/Object/Tasks/managingbuckets.htm" target="_blank">bucket</a> em formato de lista.

- **Somente Download (`ObjectReadWithoutList`)**
    - Permite que os usuários façam o download apenas sem ser possível visualizar a lista de objetos armazenados no <a href="https://docs.oracle.com/pt-br/iaas/Content/Object/Tasks/managingbuckets.htm" target="_blank">bucket</a>. Nesse caso, o usuário deve ter a URL completa do arquivo para poder realizar o download.

### **Buckets da Aplicação OCI PIZZA**

A aplicação **OCI PIZZA** utiliza dois <a href="https://docs.oracle.com/pt-br/iaas/Content/Object/Tasks/managingbuckets.htm" target="_blank">buckets</a> públicos, um em cada [região](../capitulo-3/introducao-ao-oci.md#311-região), chamado **"pizza"**. Esses <a href="https://docs.oracle.com/pt-br/iaas/Content/Object/Tasks/managingbuckets.htm" target="_blank">buckets</a> não permitirão a listagem de objetos, oferecendo apenas a opção de download (`ObjectReadWithoutList`) e, serão utilizados exclusivamente para armazenar as imagens das pizzas.

Para criar o <a href="https://docs.oracle.com/pt-br/iaas/Content/Object/Tasks/managingbuckets.htm" target="_blank">bucket</a> na região **"sa-saopaulo-1"**, no [compartimento](../capitulo-3/iam-limites-cotas-e-audit.md#compartimentos) `cmp-appl` do ambiente de produção, utilize o seguinte comando:

```bash linenums="1"
$ oci os bucket create \
> --region "sa-saopaulo-1" \
> --compartment-id "ocid1.compartment.oc1..aaaaaaaaaaaaaaaabbbbbbbbccc" \
> --name "pizza" \
> --public-access-type "ObjectReadWithoutList"
```

!!! note "NOTA"
    Os scripts para a criação dos <a href="https://docs.oracle.com/pt-br/iaas/Content/Object/Tasks/managingbuckets.htm" target="_blank">bucket</a> de ambas as regiões estão localizados no diretório <a href="https://github.com/daniel-armbrust/ocn-ocipizza/tree/main/scripts/capitulo-4" target="_blank">"scripts/capitulo-4"</a> do <a href="https://github.com/daniel-armbrust/ocn-ocipizza" target="_blank">repositório de códigos</a> da aplicação **OCI PIZZA**. Os arquivos estão nomeados como <a href="https://github.com/daniel-armbrust/ocn-ocipizza/blob/main/scripts/capitulo-4/bucket-saopaulo.sh" target="_blank">"bucket-saopaulo.sh"</a> e <a href="https://github.com/daniel-armbrust/ocn-ocipizza/blob/main/scripts/capitulo-4/bucket-vinhedo.sh" target="_blank">"bucket-vinhedo.sh"</a>.

### **Ativando a Replicação de Objetos**

<a href="https://docs.oracle.com/pt-br/iaas/Content/Object/Tasks/managingbuckets.htm" target="_blank">Buckets</a> podem ter seus objetos <a href="https://docs.oracle.com/pt-br/iaas/Content/Object/Tasks/usingreplication.htm" target="_blank">replicados</a> para outra [região](../capitulo-3/introducao-ao-oci.md#311-região) por meio de <a href="https://docs.oracle.com/pt-br/iaas/Content/Object/Tasks/usingreplication.htm" target="_blank">politicas de replicação</a>.

No caso da aplicação **OCI PIZZA**, cada objeto criado no <a href="https://docs.oracle.com/pt-br/iaas/Content/Object/Tasks/managingbuckets.htm" target="_blank">bucket</a> **"pizza"** na [região](../capitulo-3/introducao-ao-oci.md#311-região) **"sa-saopaulo-1"** será automaticamente replicado para a [região](../capitulo-3/introducao-ao-oci.md#311-região) **"sa-vinhedo-1"**. Essa <a href="https://docs.oracle.com/pt-br/iaas/Content/Object/Tasks/usingreplication.htm" target="_blank">replicação</a> de dados é ativada para garantir que a aplicação esteja acessível aos usuários em ambas as [regiões](../capitulo-3/introducao-ao-oci.md#311-região) (deploy multi-região).

![alt_text](./img/objectstorage-repl-1.png "Object Storage Replica #1")

Para ativar a <a href="https://docs.oracle.com/pt-br/iaas/Content/Object/Tasks/usingreplication.htm" target="_blank">replicação</a> dos objetos do <a href="https://docs.oracle.com/pt-br/iaas/Content/Object/Tasks/managingbuckets.htm" target="_blank">bucket</a> **"pizza"**, utilize o comando abaixo:

```bash linenums="1"
$ oci os replication create-replication-policy \
> --region "sa-saopaulo-1" \
> --bucket-name "pizza" \
> --destination-bucket "pizza" \
> --destination-region "sa-vinhedo-1" \
> --name "pizza-repl-policy"
```

!!! note "NOTA"
    A <a href="https://docs.oracle.com/pt-br/iaas/Content/Object/Tasks/usingreplication.htm" target="_blank">replicação</a> de objetos requer uma [Política IAM](../capitulo-3/iam-limites-cotas-e-audit.md#políticas-de-acesso) para funcionar. Consulte o capítulo _["3.7 Cotas, Políticas IAM e Compartimentos da Aplicação OCI PIZZA"](../capitulo-3/cotas-politicas-iam-e-compartimentos-da-aplicacao-oci-pizza.md)_ para obter informações sobre como criar essas políticas.

!!! note "NOTA"
    O script para ativar a <a href="https://docs.oracle.com/pt-br/iaas/Content/Object/Tasks/usingreplication.htm" target="_blank">replicação</a> pode ser encontrado no diretório <a href="https://github.com/daniel-armbrust/ocn-ocipizza/tree/main/scripts/capitulo-4" target="_blank">"scripts/capitulo-4"</a> do <a href="https://github.com/daniel-armbrust/ocn-ocipizza" target="_blank">repositório de códigos</a> da aplicação **OCI PIZZA**, sob o nome <a href="https://github.com/daniel-armbrust/ocn-ocipizza/blob/main/scripts/capitulo-4/bucket-replication.sh" target="_blank">"bucket-replication.sh"</a>.

Após a ativação da <a href="https://docs.oracle.com/pt-br/iaas/Content/Object/Tasks/usingreplication.htm" target="_blank">réplica</a>, o <a href="https://docs.oracle.com/pt-br/iaas/Content/Object/Tasks/managingbuckets.htm" target="_blank">bucket</a> de destino, localizado na [região](../capitulo-3/introducao-ao-oci.md#311-região) **"sa-vinhedo-1"**, é configurado em **modo somente-leitura**. Desso modo, não é possível excluír, renomear ou criar novos objetos.

![alt_text](./img/objectstorage-repl-2.png "Object Storage Replica #2")

Após a exclusão da <a href="https://docs.oracle.com/pt-br/iaas/Content/Object/Tasks/usingreplication.htm" target="_blank">réplica</a>, o modo **leitura-escrita** no <a href="https://docs.oracle.com/pt-br/iaas/Content/Object/Tasks/managingbuckets.htm" target="_blank">bucket</a> **"sa-vinhedo-1"** pode ser ativado. Para isso, é necessário primeiro obter o identificador da réplica ativa no <a href="https://docs.oracle.com/pt-br/iaas/Content/Object/Tasks/managingbuckets.htm" target="_blank">bucket</a> de origem, localizado na [região](../capitulo-3/introducao-ao-oci.md#311-região) **"sa-saopaulo-1"**, utilizando o seguinte comando:

```bash linenums="1"
$ oci os replication list-replication-policies \
> --region "sa-saopaulo-1" \
> --bucket-name "pizza" \
> --all \
> --query data[].id
[
  "aBcDEEdf33-X12c-3434-111-iuiuzocip"
]
```

A partir do identificador da réplica, você pode excluí-la utilizando o seguinte comando:

```bash linenums="1"
$ oci os replication delete-replication-policy \
> --region "sa-saopaulo-1" \
> --bucket-name "pizza" \
> --replication-id "aBcDEEdf33-X12c-3434-111-iuiuzocip" \
> --force
```

## 4.1.3 Arquivo ou Objeto?

Vimos que o <a href="https://docs.oracle.com/pt-br/iaas/Content/Object/home.htm" target="_blank">Object Storage</a> é um serviço regional, no qual cada [região](../capitulo-3/introducao-ao-oci.md#311-região) possui uma **_URL Base_** específica no qual concede acesso aos objetos. Dessa forma, os objetos são acessados por meio de [APIs REST](../capitulo-2/apis-restful.md) que operam sobre o protocolo <a href="https://pt.wikipedia.org/wiki/HTTP" target="_blank">HTTP</a>.

Como o serviço opera sobre o protocolo <a href="https://pt.wikipedia.org/wiki/HTTP" target="_blank">HTTP</a>, os dados armazenados são chamados de objetos, pois um objeto é composto por dados e metadados. 

Por exemplo, é possível consultar os metadados do objeto `marguerita.jpg`, que contém o conteúdo de uma imagem, utilizando o seguinte comando:

```bash linenums="1"
$ oci os object head --region "sa-saopaulo-1" --bucket-name "pizza" --name "marguerita.jpg"
{
  "accept-ranges": "bytes",
  "access-control-allow-credentials": "true",
  "access-control-allow-methods": "POST,PUT,GET,HEAD,DELETE,OPTIONS",
  "access-control-allow-origin": "*",
  "access-control-expose-headers": "accept-ranges,access-control-allow-credentials,access-control-allow-methods,access-control-allow-origin,content-length,content-md5,content-type,date,etag,last-modified,opc-client-info,opc-client-request-id,opc-request-id,storage-tier,strict-transport-security,version-id,x-api-id,x-content-type-options",
  "content-length": "18002",
  "content-md5": "0mIM561nf0J7gGLW/f5aeA==",
  "content-type": "image/jpeg",
  "date": "Wed, 01 Oct 2025 12:36:15 GMT",
  "etag": "7a98c9cf-58f2-4137-ab38-2af8e5288b84",
  "last-modified": "Wed, 01 Oct 2025 12:30:28 GMT",
  "opc-client-request-id": "ED8CC93602EE4A36B4E83561A57FA62D",
  "opc-request-id": "gru-1:24yOkt3xjpxo72oi2YZ5K5T7l6GLd9vfvw6yxJepR3kK6-uSNRezaCdKA_FD7_X_",
  "storage-tier": "Standard",
  "strict-transport-security": "max-age=31536000; includeSubDomains",
  "version-id": "be0ded23-00e6-4cec-8f3e-7a73b8d69bbe",
  "x-api-id": "native",
  "x-content-type-options": "nosniff"
}
```

Metadados são úteis porque descrevem os dados por meio de propriedades. No exemplo acima, é possível verificar a data de criação do objeto através da propriedade `date`, o tamanho do objeto pela propriedade `content-length`, o tipo de conteúdo do arquivo pela propriedade `content-type`, etc.

Com isso, é possível concluir que um arquivo local, após ser enviado ao <a href="https://docs.oracle.com/pt-br/iaas/Content/Object/home.htm" target="_blank">Object Storage</a> (upload), se torna um objeto. Isso ocorre porque, além do seu conteúdo, são criados metadados que descrevem várias propriedades do arquivo.