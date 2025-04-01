# Capítulo 2: OCI Foundations

# 2.5 Gerenciando o OCI através do OCI CLI

## 2.5.1 Oracle Cloud Identifier (OCID)

Antes de explorarmos os detalhes do _[OCI CLI](https://docs.oracle.com/pt-br/iaas/Content/API/Concepts/cliconcepts.htm)_, é importante compreender um elemento essencial ao gerenciar recursos no OCI por meio de código.

O **_[Oracle Cloud Identifier](https://docs.oracle.com/en-us/iaas/Content/General/Concepts/identifiers.htm#Oracle)_**, comumente abreviado como **_[OCID](https://docs.oracle.com/en-us/iaas/Content/General/Concepts/identifiers.htm#Oracle)_**, é um identificador exclusivo atribuído a cada recurso dentro do OCI. Ele é utilizado para identificar de forma única recursos como instâncias de computação, redes virtuais, bancos de dados, volumes de armazenamento, entre outros.

!!! note "NOTA"
    Vale lembrar que os valores de _[OCID](https://docs.oracle.com/en-us/iaas/Content/General/Concepts/identifiers.htm#Oracle)_ são utilizados em qualquer meio de acesso ao OCI, seja por meio do _[OCI CLI](https://docs.oracle.com/pt-br/iaas/Content/API/Concepts/cliconcepts.htm)_, _[Terraform](https://www.terraform.io/)_ ou _[Web Console](https://docs.oracle.com/pt-br/iaas/Content/GSG/Concepts/console.htm)_. O _[OCID](https://docs.oracle.com/en-us/iaas/Content/General/Concepts/identifiers.htm#Oracle)_ também é importante ao abrir uma solicitação de suporte à Oracle, pois é fundamental incluir os OCIDs dos recursos afetados por um problema.

Um _[OCID](https://docs.oracle.com/en-us/iaas/Content/General/Concepts/identifiers.htm#Oracle)_ utiliza a seguinte sintaxe:

![alt_text](./img/ocid-1.png "OCID #1")

- **ocid1**
    - Indica a versão do _[OCID](https://docs.oracle.com/en-us/iaas/Content/General/Concepts/identifiers.htm#Oracle)_.

- **RESOURCE TYPE**
    - Identifica o tipo de recurso (como _instance_, _volume_, _vcn_, _user_, entre outros).

- **REALM**
    - O termo _realm_ é usado para designar um conjunto de regiões que compartilham entidades.
        - **oc1**: _realm_ que identifica recursos de uso comercial (usuários individuais, startups ou empresas).
        - **oc2**: _realm_ que identifica recursos utilizados pelo _[setor público](https://docs.oracle.com/pt-br/iaas/Content/gov-cloud/govfedramp.htm#Regions)_.
        - **oc3**: _realm_ que identifica recursos utilizados pelo _[setor público federal](https://docs.oracle.com/pt-br/iaas/Content/gov-cloud/govfeddod.htm#US_Federal_Cloud_with_DISA_Impact_Level_5_Authorization_Console_Signin_URLs)_. 

- **REGION**
    - Indica a região do OCI onde o recurso está localizado.

- **FUTURE USE**
    - Atualmente não utilizado e reservado para uso futuro.

- **UNIQUE ID**
    - String alfanumérica gerada de forma exclusiva para criar a identificação única do recurso.

Por exemplo, o _[OCID](https://docs.oracle.com/en-us/iaas/Content/General/Concepts/identifiers.htm#Oracle)_ que identifica de forma única um _[Compute Instance](https://docs.oracle.com/pt-br/iaas/Content/Compute/Concepts/computeoverview.htm)_ tem o seguinte formato:

![alt_text](./img/ocid-2.png "OCID #2")

Alguns _[OCIDs](https://docs.oracle.com/en-us/iaas/Content/General/Concepts/identifiers.htm#Oracle)_ que identificam recursos globais omitem a parte que indica a região. Por exemplo, os _[OCIDs](https://docs.oracle.com/en-us/iaas/Content/General/Concepts/identifiers.htm#Oracle)_ utilizados para identificar usuários, grupos, políticas, compartimentos e tenancy, não incluem a região:

![alt_text](./img/ocid-3.png "OCID #3")

Além de sua função de identificação, os _[OCIDs](https://docs.oracle.com/en-us/iaas/Content/General/Concepts/identifiers.htm#Oracle)_ são utilizados para atender a dependências ao criar um recurso. Por exemplo, para criar um _[Internet Gateway](https://docs.oracle.com/en-us/iaas/tools/oci-cli/3.53.0/oci_cli_docs/cmdref/network/internet-gateway.html)_ por meio do _[OCI CLI](https://docs.oracle.com/pt-br/iaas/Content/API/Concepts/cliconcepts.htm)_, é necessário fornecer tanto o _[OCID](https://docs.oracle.com/en-us/iaas/Content/General/Concepts/identifiers.htm#Oracle)_ do compartimento [_(--compartment-id)_](https://docs.oracle.com/en-us/iaas/tools/oci-cli/3.53.0/oci_cli_docs/cmdref/network/internet-gateway/create.html#cmdoption-compartment-id) quanto o OCID da VCN [_(--vcn-id)_](https://docs.oracle.com/en-us/iaas/tools/oci-cli/3.53.0/oci_cli_docs/cmdref/network/internet-gateway/create.html#cmdoption-vcn-id):

![alt_text](./img/ocid-4.png "OCID #4")

!!! note "NOTA"
    Lembre-se de que todos os valores de _[OCID](https://docs.oracle.com/en-us/iaas/Content/General/Concepts/identifiers.htm#Oracle)_ utilizados nos exemplos do livro são fictícios e não funcionarão para você. Utilize os valores reais do seu Tenancy.

## 2.5.2 Instalação do OCI CLI

Para começar a utilizar o _[OCI CLI](https://docs.oracle.com/pt-br/iaas/Content/API/Concepts/cliconcepts.htm)_, é necessário primeiro instalá-lo de acordo com o seu sistema operacional. No meu caso, o _[OCI CLI](https://docs.oracle.com/pt-br/iaas/Content/API/Concepts/cliconcepts.htm)_ será instalado em um **_[Oracle Linux versão 8](https://www.oracle.com/linux/technologies/oracle-linux-downloads.html)_**.

```bash linenums="1"
$ cat /etc/oracle-release
Oracle Linux Server release 8.10
```

!!! note "NOTA"
    O _Oracle Linux_ é gratuito e pode ser baixado no site _[Oracle Linux Downloads](https://www.oracle.com/linux/technologies/oracle-linux-downloads.html)_.

**1.** Baixar o instalador do _[OCI CLI](https://docs.oracle.com/pt-br/iaas/Content/API/Concepts/cliconcepts.htm)_ através do seguinte comando:

```bash linenums="1"
$ wget https://raw.githubusercontent.com/oracle/oci-cli/master/scripts/install/install.sh
```

**2.** Execute o script que foi baixado com a opção **_"--accept-all-defaults"_** para realizar uma instalação em que todas as perguntas serão respondidas com os valores padrão:

```bash linenums="1"
$ sh ./install.sh --accept-all-defaults
```

**3.** Por fim, para verificar se o _[OCI CLI](https://docs.oracle.com/pt-br/iaas/Content/API/Concepts/cliconcepts.htm)_ foi instalado com sucesso, basta executar o comando abaixo para exibir a sua versão:

```bash linenums="1"
$ oci -v
3.52.1
```

!!! note "NOTA"
    A documentação disponível no link _[Instalando a CLI](https://docs.oracle.com/pt-br/iaas/Content/API/SDKDocs/cliinstall.htm#Quickstart)_ oferece mais informações sobre como instalar o _[OCI CLI](https://docs.oracle.com/pt-br/iaas/Content/API/Concepts/cliconcepts.htm)_ em diferentes sistemas operacionais.

### Atualizando o OCI CLI

É sempre recomendável verificar se estamos utilizando a versão mais recente do _[OCI CLI](https://docs.oracle.com/pt-br/iaas/Content/API/Concepts/cliconcepts.htm)_ disponível.

```bash linenums="1"
$ oci --latest-version
3.53.0
You are using OCI CLI version 3.52.1, however version 3.53.0 is available. You should consider upgrading using https://docs.oracle.com/iaas/Content/API/SDKDocs/cliupgrading.htm
```

Neste caso, o comando nos alertou sobre a necessidade de atualização. Além de corrigir bugs e implementar melhorias, a atualização também permite a interação com novos serviços do OCI.

Para realizar a atualização, basta executar o comando abaixo:

```bash linenums="1"
$ pip3 install oci-cli --upgrade
```

Pronto! Agora podemos confirmar que a atualização do _[OCI CLI](https://docs.oracle.com/pt-br/iaas/Content/API/Concepts/cliconcepts.htm)_ foi bem-sucedida, pois não há mais avisos relacionados à atualização de versão:

```bash linenums="1"
$ oci --latest-version
3.53.0
```

## 2.5.3 APIs do OCI

O OCI como todo provedor de computação em Nuvem, disponibilizam seus serviços através de um conjunto de diferentes APIs. 

!!! note "NOTA"
    Todas as APIs disponibilizadas pelo OCI estão documentadas no link _[API Reference and Endpoints](https://docs.oracle.com/en-us/iaas/api/#/)_.

As APIs do OCI são públicas, acessíveis pela Internet por meio do protocolo _HTTPS_. Por exemplo, o conjunto de APIs denominado _[Core Services API](https://docs.oracle.com/en-us/iaas/api/#/en/iaas/latest/)_, permite gerenciar recursos como _[VCN](https://docs.oracle.com/pt-br/iaas/Content/Network/Tasks/Overview_of_VCNs_and_Subnets.htm)_, _[Compute Instances](https://docs.oracle.com/pt-br/iaas/Content/Compute/Concepts/computeoverview.htm)_ e _[Block Storage](https://docs.oracle.com/pt-br/iaas/Content/Block/Concepts/overview.htm)_.

![alt_text](./img/core-services-api-1.png "Core Services API #1")
<br>

Todo serviço no OCI, disponível por meio de uma API, possui um **_endpoint_** exclusivo, que varia conforme a região. Para o _[Core Services API](https://docs.oracle.com/en-us/iaas/api/#/en/iaas/latest/)_, o _endpoint_ correspondente é:

![alt_text](./img/core-services-api-2.png "Core Services API #2")
<br>

O fato de as APIs serem públicas, ou seja, possuírem um _endpoint_ acessível pela Internet, não significa que qualquer pessoa possa criar ou excluir recursos. Por exemplo, ao tentar criar uma _[VCN](https://docs.oracle.com/pt-br/iaas/Content/Network/Tasks/Overview_of_VCNs_and_Subnets.htm)_ sem uma credencial válida, a resposta obtida será **_"NotAuthenticated"_**, conforme abaixo:

```bash linenums="1"
$ curl -X POST https://iaas.sa-saopaulo-1.oraclecloud.com/20160918/vcns \
> -H "Content-Type: application/json" \
> -d '{
>   "compartmentId": "ocid1.compartment.oc1..aaaaaaaaaaaaaaaabbbbbbbbccc",
>   "displayName": "vcn-saopaulo",
>   "cidrBlock": "172.16.0.0/16"
> }'
{
  "code" : "NotAuthenticated",
  "message" : "The required information to complete authentication was not provided or was incorrect."
}
```

!!! note "NOTA"
    Existem alguns serviços que permitem a criação de endpoints privados que utilizam um endereço IP da sua sub-rede, como é o caso do _[Object Storage](https://docs.oracle.com/pt-br/iaas/Content/Object/Tasks/private-endpoints.htm)_. Além disso, o recurso de rede _[Service Gateway](https://docs.oracle.com/pt-br/iaas/Content/Network/Tasks/servicegateway.htm)_ possibilita o acesso às APIs diretamente a partir de uma sub-rede no OCI, eliminando a necessidade de utilizar a Internet.

Para interagir com o OCI e criar recursos, é necessário ter um usuário que possa ser _autenticado_ e _autorizado_ com sucesso. Como inicialmente utilizaremos o _[OCI CLI](https://docs.oracle.com/pt-br/iaas/Content/API/Concepts/cliconcepts.htm)_ e o _[Terraform](https://www.terraform.io/)_ para criar recursos de infraestrutura, ambos requerem uma _[API Key](https://docs.oracle.com/pt-br/iaas/Content/Identity/access/working-with-console-passwords-and-API-keys.htm#one)_ válida, que deve ser criada previamente.

Iniciaremos pelo processo de **_autenticação_**, que envolve o uso de _[API Key](https://docs.oracle.com/pt-br/iaas/Content/Identity/access/working-with-console-passwords-and-API-keys.htm#one)_.

### API Keys

Uma _[API Key](https://docs.oracle.com/pt-br/iaas/Content/Identity/access/working-with-console-passwords-and-API-keys.htm#one)_ é um conjunto de _chaves criptográficas_ que servem tanto para o processo de **_autenticação_** quanto para **_assinar as requisições_** enviadas as APIs do OCI.

Sem uma _[API Key](https://docs.oracle.com/pt-br/iaas/Content/Identity/access/working-with-console-passwords-and-API-keys.htm#one)_, que deve ser associada a um usuário válido, não é possível estabelecer comunicação com as APIs do OCI, seja por meio do _[OCI CLI](https://docs.oracle.com/pt-br/iaas/Content/API/Concepts/cliconcepts.htm)_, _[Terraform](https://www.terraform.io/)_ ou _[SDK](https://docs.oracle.com/pt-br/iaas/Content/API/Concepts/developerquickstarts.htm)_.

!!! note "NOTA"
    Inicialmente, para prosseguir com os comandos abordados no livro, a _[API Key](https://docs.oracle.com/pt-br/iaas/Content/Identity/access/working-with-console-passwords-and-API-keys.htm#one)_ que será criada deve pertencer ao usuário **_Administrador do Tenancy_**, criado após a ativação da conta no OCI, conforme descrito na seção _["2.2 Criando e Ativando a sua Conta no OCI"](./criando-e-ativando-a-sua-conta-no-oci.md)_. Posteriormente, serão criados e configurados outros usuários com privilégios mais restritos.
    
É possível criar uma _[API Key](https://docs.oracle.com/pt-br/iaas/Content/Identity/access/working-with-console-passwords-and-API-keys.htm#one)_ manualmente utilizando o utilitário _[OpenSSL](https://www.openssl.org/)_, mas a criação é mais simples e prática por meio da _[Web Console](https://docs.oracle.com/pt-br/iaas/Content/GSG/Concepts/console.htm)_.

Para criar uma _[API Key](https://docs.oracle.com/pt-br/iaas/Content/Identity/access/working-with-console-passwords-and-API-keys.htm#one)_ para um usuário específico por meio da _[Web Console](https://docs.oracle.com/pt-br/iaas/Content/GSG/Concepts/console.htm)_, siga o passo a passo abaixo:

**1.** Acessar o perfil do usuário no canto superior direito da _Web Console_:

![alt_text](./img/api-key-1.png "API Key #1")
<br>

**2.** Dentro do perfil do usuário, no canto inferior esquerdo, selecione **_API keys_** e, em seguida, clique no botão **_Add API key_**:

![alt_text](./img/api-key-2.png "API Key #1")
<br>

**3.** Na tela **_Add API key_**, selecione **_Generate API key pair_** e, em seguida, faça o _download_ e salve em um local seguro tanto a _Private Key_ quanto a _Public Key_:

![alt_text](./img/api-key-3.png "API Key #3")
<br>

**4.** Clique no botão **_Add_** para concluir a adição da _[API Key](https://docs.oracle.com/pt-br/iaas/Content/Identity/access/working-with-console-passwords-and-API-keys.htm#one)_:

![alt_text](./img/api-key-4.png "API Key #4")
<br>

!!! note "NOTA"
    Um usuário pode ter no máximo três _[API Keys](https://docs.oracle.com/pt-br/iaas/Content/Identity/access/working-with-console-passwords-and-API-keys.htm#one)_.

**5.** Por fim, o OCI exibe um conjunto de informações que devem ser inseridas no arquivo **_"~/.oci/config"_** para serem utilizadas pelo _[OCI CLI](https://docs.oracle.com/pt-br/iaas/Content/API/Concepts/cliconcepts.htm)_:

![alt_text](./img/api-key-5.png "API Key #5")

!!! note "NOTA"
    A partir deste ponto, a sequência de comandos via _[OCI CLI](https://docs.oracle.com/pt-br/iaas/Content/API/Concepts/cliconcepts.htm)_ que utilizaremos ao longo do livro, requer que o usuário seja membro do grupo **_Administrators_**. No caso, o usuário **_darmbrust@gmail.com_**, especificado durante o processo de registro da conta, foi adicionado automaticamente pelo OCI no grupo **_Administrators_**. Mais detalhes serão apresentados no capítulo _["2.6 IAM, Limites e Quotas"](./iam-limites-e-quotas.md)_.
    
![alt_text](./img/oci-admin-group-1.png "Administrators Group")

### Utilizando a API Key com o OCI CLI

**1.** Crie o diretório **_"~/.oci"_** e depois o arquivo **_config"_** dentro dele:

```bash linenums="1"
$ mkdir .oci
$ touch .oci/config
$ chmod 0400 .oci/config
```

**2.** Insira o conjunto de informações fornecidas anteriormente **_(API Keys - item 5)_** no arquivo **_"~/.oci/config"_**. O conteúdo deste arquivo deve ser semelhante a isto:

```bash linenums="1"
$ cat ~/.oci/config
[DEFAULT]
key_file=/home/darmbrust/.oci/api.key
user=ocid1.user.oc1..aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa
fingerprint=4f:f7:42:44:f6:c1:bc:2b:da:dd:fd:d5:43:28:e1:9a
tenancy=ocid1.tenancy.oc1..aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa
region=sa-saopaulo-1
```

**3.** Dentro do diretório **_"~/.oci"_**, crie o arquivo **_"api.key"_**:

```bash linenums="1"
$ touch .oci/api.key
$ chmod 0400 .oci/api.key
```

**4.** Transfira o conteúdo da **_chave privada_** que foi baixada anteriormente **_(API Keys - item 3)_** para o arquivo **_"~/.oci/api.key"_**. O conteúdo deste arquivo deve ser semelhante a isto:

```bash linenums="1"
$ cat ~/.oci/api.key
-----BEGIN PRIVATE KEY-----
MIIMIIMRGDkRGDkRGDkRGDkRGDkRGDkMIIMIIMIIMIRGDkMIIMIIMIIMIRGDk
RGDkRGDkRGDkRGDkRGDkMIIMIIMIIMIRGDkMIIMIIMIIMIRGDk
-----END PRIVATE KEY-----
OCI_API_KEY
```

**5.** Teste a comunicação do _[OCI CLI](https://docs.oracle.com/pt-br/iaas/Content/API/Concepts/cliconcepts.htm)_ ao OCI através de um simples comando:

```bash linenums="1"
$ oci os ns get
{
  "data": "grxmw2a9myyj"
}
```

!!! note "NOTA"
    Lembre-se de que todos os valores retornados pelo OCI nos exemplos apresentados aqui para a configuração do _[OCI CLI](https://docs.oracle.com/pt-br/iaas/Content/API/Concepts/cliconcepts.htm)_ são fictícios e não funcionarão para você. Para configurar o _[OCI CLI](https://docs.oracle.com/pt-br/iaas/Content/API/Concepts/cliconcepts.htm)_ corretamente, utilize os valores reais fornecidos pelo seu _Tenancy_.

!!! note "NOTA"
    Nos exemplos apresentados no livro, o _[OCI CLI](https://docs.oracle.com/pt-br/iaas/Content/API/Concepts/cliconcepts.htm)_ sempre utilizará o conjunto de configurações **_DEFAULT_**, conforme indicado por **_[DEFAULT]_** no arquivo **_"~/.oci/config"_**. No entanto, você pode usar o parâmetro global **_[--profile](https://docs.oracle.com/en-us/iaas/tools/oci-cli/3.53.0/oci_cli_docs/oci.html#cmdoption-profile)_** para especificar um conjunto diferente de configurações.
    
## 2.5.4 Trabalhando com o OCI CLI

Após o _[OCI CLI](https://docs.oracle.com/pt-br/iaas/Content/API/Concepts/cliconcepts.htm)_ estar devidamente instalado e funcionando com as configurações do seu _Tenancy_, é hora de entender em como trabalhar diretamente com o OCI através do OCI CLI.

Criar e gerenciar sua infraestrutura no OCI utilizando _[OCI CLI](https://docs.oracle.com/pt-br/iaas/Content/API/Concepts/cliconcepts.htm)_ ou _[Terraform](https://www.terraform.io/)_ é mais rápido do que realizar operações manualmente através de cliques na _Web Console_. Além disso, ao trabalhar com código, você pode automatizar tarefas repetitivas, versionar suas configurações para acompanhar alterações, reverter para versões anteriores quando necessário e facilitar a colaboração com outros membros da equipe.

Para demonstrar a utilização do _[OCI CLI](https://docs.oracle.com/pt-br/iaas/Content/API/Concepts/cliconcepts.htm)_, apresentarei a criação de uma _[VCN (Virtual Cloud Network)](https://docs.oracle.com/pt-br/iaas/Content/Network/Tasks/Overview_of_VCNs_and_Subnets.htm)_ por meio de uma sequência de etapas.

!!! note "NOTA"
    Os recursos de rede do OCI, incluindo a _[VCN (Virtual Cloud Network)](https://docs.oracle.com/pt-br/iaas/Content/Network/Tasks/Overview_of_VCNs_and_Subnets.htm)_, serão abordados no _[Capítulo 4: Conectividade e Redes](../capitulo-4/index.md)_.

**1.** O primeiro passo é localizar o recurso desejado no link _[Oracle Cloud Infrastructure CLI Command Reference](https://docs.oracle.com/en-us/iaas/tools/oci-cli/3.53.0/oci_cli_docs/index.html#)_. Os recursos disponíveis de redes no OCI, incluindo a VCN, estes estão contidos em _[Networking Service (network)](https://docs.oracle.com/en-us/iaas/tools/oci-cli/3.53.0/oci_cli_docs/cmdref/network.html)_:

![alt_text](./img/oci-cli-network-1.png "OCI CLI Network VCN #1")
<br>

**2.** Dentro de _[Networking Service (network)](https://docs.oracle.com/en-us/iaas/tools/oci-cli/3.53.0/oci_cli_docs/cmdref/network.html)_, você encontrará diversos comandos relacionados aos diferentes recursos de rede disponíveis no OCI. Para o nosso exemplo, iremos utilizar a _[vcn](https://docs.oracle.com/en-us/iaas/tools/oci-cli/3.53.0/oci_cli_docs/cmdref/network/vcn.html)_:

![alt_text](./img/oci-cli-network-2.png  "OCI CLI Network VCN #2")
<br>

**3.** Cada recurso no OCI que pode ser gerenciado pelo _[OCI CLI](https://docs.oracle.com/pt-br/iaas/Content/API/Concepts/cliconcepts.htm)_ possui um conjunto específico de **_comandos ou ações_** que podem ser invocadas, permitindo a criação, modificação ou alteração desse recurso. Para a _[vcn](https://docs.oracle.com/en-us/iaas/tools/oci-cli/3.53.0/oci_cli_docs/cmdref/network/vcn.html)_, utilizaremos a ação _[create](https://docs.oracle.com/en-us/iaas/tools/oci-cli/3.53.0/oci_cli_docs/cmdref/network/vcn/create.html)_:

![alt_text](./img/oci-cli-network-3.png  "OCI CLI Network VCN #3")
<br>

**4.** Dentro do comando ou ação, além da descrição e do exemplo de uso, você encontrará os _[Parâmetros Obrigatórios (Required Parameters)](https://docs.oracle.com/en-us/iaas/tools/oci-cli/3.53.0/oci_cli_docs/cmdref/network/vcn/create.html#required-parameters)_, os _[Parâmetros Opcionais (Optional Parameters)](https://docs.oracle.com/en-us/iaas/tools/oci-cli/3.53.0/oci_cli_docs/cmdref/network/vcn/create.html#required-parameters)_ e os _[Parâmetros Globais (Global Parameters)](https://docs.oracle.com/en-us/iaas/tools/oci-cli/3.53.0/oci_cli_docs/cmdref/network/vcn/create.html#required-parameters)_, que determinam as propriedades do recurso a ser criado ou modificado:

![alt_text](./img/oci-cli-network-4.png  "OCI CLI Network VCN #4")
<br>

### Parâmetros Globais

Os **_parâmetros globais_** como o própio nome diz, são globais pois podem ser usados juntos com qualquer outro comando do OCI CLI. 

![alt_text](./img/oci-cli-params-3.png "OCI CLI Parâmetros #3")
<br>

Para os exemplos apresentados no livro, os **_parâmetros globais_** mais utilizados são:

#### [--region](https://docs.oracle.com/en-us/iaas/tools/oci-cli/3.53.0/oci_cli_docs/oci.html#cmdoption-region)

Permite especificar a região do OCI onde ocorrerá a interação com um determinado recurso.

#### [--query](https://docs.oracle.com/en-us/iaas/tools/oci-cli/3.53.0/oci_cli_docs/oci.html#cmdoption-query)

Parâmetro utilizado para filtrar a resposta _JSON_ recebida do _[OCI CLI](https://docs.oracle.com/pt-br/iaas/Content/API/Concepts/cliconcepts.htm)_. A filtragem é especialmente útil ao lidar com grandes volumes de informações vindas através do _[OCI CLI](https://docs.oracle.com/pt-br/iaas/Content/API/Concepts/cliconcepts.htm)_. 

Esta opção utiliza a linguagem de consulta **_[JMESPath](https://jmespath.org/)_** para manipulação de _JSON_. 

Por exemplo, o comando abaixo utiliza a opção **_[--query](https://docs.oracle.com/en-us/iaas/tools/oci-cli/3.53.0/oci_cli_docs/oci.html#cmdoption-query)_** para listar as _[VCNs](https://docs.oracle.com/pt-br/iaas/Content/Network/Tasks/Overview_of_VCNs_and_Subnets.htm)_ cujo nome contém _"vcn-saopaulo"_:

```bash linenums="1"
$ oci network vcn list \
> --compartment-id "ocid1.compartment.oc1..aaaaaaaaaaaaaaaabbbbbbbbccc" \
> --all \
> --query "data [?contains(\"display-name\",'vcn-saopaulo')]"
```

!!! note "NOTA"
    Consulte a página do **_[JMESPath](https://jmespath.org/)_** para explorar opções mais avançadas relacionadas aos filtros _JSON_.

### Parâmetros Simples e Complexos

Tanto um parâmetro sendo obrigatório ou opcional, pode aceitar um **_valor simples_** ou **_complexo_**. O _valor simples_ é um único valor, que pode ser um texto, um número ou um valor booleano. Por outro lado, o _valor complexo_ deve ser fornecido no formato _JSON_, que pode combinar diferentes tipos de valores, como texto, número e booleano.

![alt_text](./img/oci-cli-params-1.png "OCI CLI Parâmetros #1")
<br>

É possível utilizar o parâmetro global **_[--generate-param-json-input](https://docs.oracle.com/en-us/iaas/tools/oci-cli/3.53.0/oci_cli_docs/oci.html#cmdoption-generate-param-json-input)_** para gerar a estrutura do valor _JSON_ que um determinado parâmetro complexo espera receber. Por exemplo, o parâmetro **_[--cidr-blocks](https://docs.oracle.com/en-us/iaas/tools/oci-cli/3.53.0/oci_cli_docs/cmdref/network/vcn/create.html#cmdoption-cidr-blocks)_** espera receber uma lista de valores do tipo string (array de strings) quando especificado:

```bash linenums="1"
$ oci network vcn create --generate-param-json-input cidr-blocks
[
  "string",
  "string"
]
```

!!! note "NOTA"    
    Todo parâmetro utilizado como valor do **_[--generate-param-json-input](https://docs.oracle.com/en-us/iaas/tools/oci-cli/3.53.0/oci_cli_docs/oci.html#cmdoption-generate-param-json-input)_** não deve ser precedido pelos dois traços (--). Por exemplo, o parâmetro complexo **_--cidr-blocks_** deve ser referenciado apenas como **_cidr-blocks_** ao ser usado como valor do **_[--generate-param-json-input](https://docs.oracle.com/en-us/iaas/tools/oci-cli/3.53.0/oci_cli_docs/oci.html#cmdoption-generate-param-json-input)_**.

### Ciclo de Vida (Lifecycle)

Muitos recursos do OCI possuem o chamado **_"Ciclo de Vida" (Lifecycle)_**, que indica o **_estado atual_** de um determinado recurso. É por meio desse _"ciclo de vida"_ que é possível determinar se um recurso já está disponível para uso ou se ainda está em processo de criação, atualização ou exclusão.

Por exemplo, quando um recurso é solicitado para criação, ele não é criado imediatamente. Após o OCI receber a instrução de criação, essa solicitação é colocada em uma _fila de processamento_. Se tudo ocorrer conforme o esperado, o recurso é então criado e disponibilizado para uso. Esse processo não se aplica apenas à ação de _"criar"_, ações de _"exclusão"_ ou _"atualização"_ também são submetidas a uma fila de processamento.

É importante destacar que, durante as etapas do _"ciclo de vida"_, diversas outras atividades são realizadas, como a verificação das permissões do usuário que está solicitando a criação e a confirmação da disponibilidade de recursos computacionais. 

Você verá que é importante saber lidar com essas operações assíncronas que ocorrem durante o _"ciclo de vida"_ de um recurso, em scripts que utilizam o OCI CLI para criar outros recursos. Por exemplo, não é possível criar um _[Compute Instances](https://docs.oracle.com/pt-br/iaas/Content/Compute/Concepts/computeoverview.htm)_ sem que uma _[sub-rede](https://docs.oracle.com/pt-br/iaas/Content/Network/Tasks/Overview_of_VCNs_and_Subnets.htm)_ e uma _[VCN](https://docs.oracle.com/pt-br/iaas/Content/Network/Tasks/Overview_of_VCNs_and_Subnets.htm)_ estejam no estado _AVAILABLE_.

O parâmetro **_[--wait-for-state](https://docs.oracle.com/en-us/iaas/tools/oci-cli/3.53.0/oci_cli_docs/cmdref/network/vcn/create.html#cmdoption-wait-for-state)_**, disponível na maioria dos recursos, pode ser usado para **_aguardar a conclusão_** de uma determinada etapada do _"ciclo de vida"_ antes de _liberar o shell_ para execução de um próximo comando. 

![alt_text](./img/oci-cli-params-2.png "OCI CLI Parâmetros #2")
<br>

O significado de cada etapa do _"ciclo de vida"_ da _[vcn](https://docs.oracle.com/en-us/iaas/tools/oci-cli/3.53.0/oci_cli_docs/cmdref/network/vcn.html)_ é descrito a seguir:

- **AVAILABLE**
    - A _[VCN](https://docs.oracle.com/en-us/iaas/tools/oci-cli/3.53.0/oci_cli_docs/cmdref/network/vcn.html)_ está pronta e disponível para ser utilizada.

- **PROVISIONING**
    - Esse estado indica que o comando para criar a _[VCN](https://docs.oracle.com/en-us/iaas/tools/oci-cli/3.53.0/oci_cli_docs/cmdref/network/vcn.html)_ foi aceito pelo OCI, e o recurso agora está na fila de criação ou provisionamento.

- **UPDATING**
    - A _[VCN](https://docs.oracle.com/en-us/iaas/tools/oci-cli/3.53.0/oci_cli_docs/cmdref/network/vcn.html)_ encontra-se em em processo de atualização.

- **TERMINATING**
    - Esse estado indica que a _[VCN](https://docs.oracle.com/en-us/iaas/tools/oci-cli/3.53.0/oci_cli_docs/cmdref/network/vcn.html)_ entrou em processo de exclusão ou terminate.
    
- **TERMINATED**
    - A _[VCN](https://docs.oracle.com/en-us/iaas/tools/oci-cli/3.53.0/oci_cli_docs/cmdref/network/vcn.html)_ foi excluída com sucesso e não existe mais.

!!! note "NOTA"
    Sempre consulte a documentação do recurso que você deseja gerenciar para entender os estados do seu _"ciclo de vida"_. Por exemplo, os estados disponíveis de uma _[VCN](https://docs.oracle.com/en-us/iaas/tools/oci-cli/3.53.0/oci_cli_docs/cmdref/network/vcn.html)_ são completamente diferentes dos estados de um _[Container Instance](https://docs.oracle.com/en-us/iaas/tools/oci-cli/3.53.0/oci_cli_docs/cmdref/container-instances/container-instance/create.html)_, que incluem _ACCEPTED_, _CANCELED_, _CANCELING_, _FAILED_, _IN\_PROGRESS_ e _SUCCEEDED_.    

### Exemplo: Criando e Consultando Informações sobre uma VCN

O comando a seguir pode ser utilizado para criar uma _[VCN](https://docs.oracle.com/en-us/iaas/tools/oci-cli/3.53.0/oci_cli_docs/cmdref/network/vcn.html)_:

```bash linenums="1"
$ oci network vcn create \
> --region "sa-saopaulo-1" \
> --compartment-id "ocid1.compartment.oc1..aaaaaaaaaaaaaaaabbbbbbbbccc" \
> --cidr-blocks "['10.100.0.0/16', '192.168.0.0/24']" \
> --display-name "vcn-saopaulo" \
> --wait-for-state "AVAILABLE"
```

!!! note "NOTA"
    A interação com a maioria dos recursos por meio do _[OCI CLI](https://docs.oracle.com/pt-br/iaas/Content/API/Concepts/cliconcepts.htm)_ requer o parâmetro _[--compartment-id](https://docs.oracle.com/en-us/iaas/tools/oci-cli/3.53.0/oci_cli_docs/cmdref/network/vcn/create.html#cmdoption-compartment-id)_. Na seção _[2.6 IAM, Limites e Quotas](./iam-limites-e-quotas.md)_, abordaremos o que são _compartments_ e como utilizá-los.

Observe que, após a execução do comando, é exibida a seguinte mensagem:

<div align="center" style="font-weight: bold; font-style: italic;">
Action completed. Waiting until the resource has entered state: ('AVAILABLE',)
</div>

Isso significa que o comando aguardará até que a _[VCN](https://docs.oracle.com/en-us/iaas/tools/oci-cli/3.53.0/oci_cli_docs/cmdref/network/vcn.html)_ atinja o estado _AVAILABLE_ antes de liberar o shell novamente.

Após a conclusão bem-sucedida da execução, uma resposta do OCI em formato _JSON_ será retornada que incluem algumas informações referente a _[VCN](https://docs.oracle.com/en-us/iaas/tools/oci-cli/3.53.0/oci_cli_docs/cmdref/network/vcn.html)_ que acaba de ser criada:

```json linenums="1"
{
  "data": {
    "byoipv6-cidr-blocks": null,
    "cidr-block": "10.100.0.0/16",
    "cidr-blocks": [
      "10.100.0.0/16",
      "192.168.0.0/24"
    ],
    "compartment-id": "ocid1.compartment.oc1..aaaaaaaaaaaaaaaabbbbbbbbccc",
    "default-dhcp-options-id": "ocid1.dhcpoptions.oc1.sa-saopaulo-1.aaaaaaaaaaaaaaaabbbbbbbbccc",
    "default-route-table-id": "ocid1.routetable.oc1.sa-saopaulo-1.aaaaaaaaaaaaaaaabbbbbbbbccc",
    "default-security-list-id": "ocid1.securitylist.oc1.sa-saopaulo-1.aaaaaaaaaaaaaaaabbbbbbbbccc",
    "defined-tags": {
      "Oracle-Tags": {
        "CreatedBy": "default/darmbrust@gmail.com",
        "CreatedOn": "2025-03-24T18:34:10.160Z"
      }
    },
    "display-name": "vcn-saopaulo",
    "dns-label": null,
    "freeform-tags": {},
    "id": "ocid1.vcn.oc1.sa-saopaulo-1.aaaaaaaaaaaaaaaabbbbbbbbccc",
    "ipv6-cidr-blocks": null,
    "ipv6-private-cidr-blocks": null,
    "lifecycle-state": "AVAILABLE",
    "security-attributes": {},
    "time-created": "2025-03-24T18:34:10.244000+00:00",
    "vcn-domain-name": null
  },
  "etag": "4aba8b9d"
}
```

O _[OCID](https://docs.oracle.com/en-us/iaas/Content/General/Concepts/identifiers.htm#Oracle)_ da _[VCN](https://docs.oracle.com/en-us/iaas/tools/oci-cli/3.53.0/oci_cli_docs/cmdref/network/vcn.html)_ recém-criada está disponível na chave **_id_**. Com esse identificador, você pode consultar os detalhes relacionados à _[VCN](https://docs.oracle.com/en-us/iaas/tools/oci-cli/3.53.0/oci_cli_docs/cmdref/network/vcn.html)_:

```bash linenums="1"
$ oci network vcn get \
> --vcn-id "ocid1.vcn.oc1.sa-saopaulo-1.aaaaaaaaaaaaaaaabbbbbbbbccc"
```

Outra maneira de obter o _[OCID](https://docs.oracle.com/en-us/iaas/Content/General/Concepts/identifiers.htm#Oracle)_ dos recursos é através do comando **_["list"](https://docs.oracle.com/en-us/iaas/tools/oci-cli/3.53.0/oci_cli_docs/cmdref/network/vcn/list.html)_**. No exemplo abaixo, serão retornados todos os _[OCIDs](https://docs.oracle.com/en-us/iaas/Content/General/Concepts/identifiers.htm#Oracle)_ das  _[VCNs](https://docs.oracle.com/en-us/iaas/tools/oci-cli/3.53.0/oci_cli_docs/cmdref/network/vcn.html)_ que estão criadas no compartimento especificado:

```bash linenums="1"
$ oci network vcn list \
> --compartment-id "ocid1.compartment.oc1..aaaaaaaaaaaaaaaabbbbbbbbccc" \
> --all
```

## 2.5.5 Work Request

Vimos que a maioria dos recursos possuem um _"ciclo de vida"_, que indica diferentes etapas pelas quais o recurso passa antes de concluir uma ação solicitada pelo usuário.

As ações que não produzem resultados imediatos geram o que é conhecido como **_Work Request_**, que é um _[OCID](https://docs.oracle.com/en-us/iaas/Content/General/Concepts/identifiers.htm#Oracle)_ utilizado para consultar informações relacionadas a uma etapa específica do _"ciclo de vida"_. Isso ocorre porque solicitações que não têm resultados imediatos são **_assíncronas_** e podem levar um tempo indeterminado para serem concluídas com sucesso.

Por exemplo, ao criar o componente de rede _[DRG](https://docs.oracle.com/pt-br/iaas/Content/Network/Tasks/managingDRGs.htm#overview)_, o resultado da operação inclui o campo **_opc-work-request-id_**, que indica o _[OCID](https://docs.oracle.com/en-us/iaas/Content/General/Concepts/identifiers.htm#Oracle)_ do **_Work Request_**:

```bash linenums="1"
$ oci network drg create \
> --region "sa-saopaulo-1" \
> --compartment-id "ocid1.compartment.oc1..aaaaaaaaaaaaaaaabbbbbbbbccc" \
> --display-name "drg"
{
  "data": {
    "compartment-id": "ocid1.compartment.oc1..aaaaaaaaaaaaaaaabbbbbbbbccc",
    "default-drg-route-tables": {
      "ipsec-tunnel": null,
      "remote-peering-connection": null,
      "vcn": null,
      "virtual-circuit": null
    },
    "default-export-drg-route-distribution-id": null,
    "defined-tags": {
      "Oracle-Tags": {
        "CreatedBy": "default/darmbrust@gmail.com",
        "CreatedOn": "2025-03-24T19:27:04.790Z"
      }
    },
    "display-name": "drg",
    "freeform-tags": {},
    "id": "ocid1.drg.oc1.sa-saopaulo-1.aaaaaaaaaaaaaaaabbbbbbbbccc",
    "lifecycle-state": "PROVISIONING",
    "time-created": "2025-03-24T19:27:04.818000+00:00"
  },
  "etag": "282241271",
  "opc-work-request-id": "ocid1.coreservicesworkrequest.oc1.sa-saopaulo-1.aaaaaaaaaaaaaaaabbbbbbbbccc"
}
```

Para consultar informações sobre o **_Work Request_**, utilize o valor do **_opc-work-request-id_** com o comando abaixo:

```bash linenums="1"
$ oci work-requests work-request get \
> --region "sa-saopaulo-1" \
> --work-request-id "ocid1.coreservicesworkrequest.oc1.sa-sa
opaulo-1.aaaaaaaaaaaaaaaabbbbbbbbccc"
{
  "data": {
    "compartment-id": "ocid1.compartment.oc1..aaaaaaaaaaaaaaaabbbbbbbbccc",
    "id": "ocid1.coreservicesworkrequest.oc1.sa-saopaulo-1.aaaaaaaaaaaaaaaabbbbbbbbccc",
    "operation-type": "create",
    "percent-complete": 0.0,
    "resources": [
      {
        "action-type": "CREATED",
        "entity-type": "drg",
        "entity-uri": "/20160918/drgs/ocid1.drg.oc1.sa-saopaulo-1.aaaaaaaaaaaaaaaabbbbbbbbccc",
        "identifier": "ocid1.drg.oc1.sa-saopaulo-1.aaaaaaaaaaaaaaaabbbbbbbbccc"
      }
    ],
    "status": "SUCCEEDED",
    "time-accepted": "2025-03-24T19:27:04.899000+00:00",
    "time-finished": "2025-03-24T19:27:09.988000+00:00",
    "time-started": null
  }
}
```

Trabalhar com **_Work Request_** pode ser extremamente útil em diversos cenários. Por exemplo, considere a situação em que você precisa disponibilizar uma aplicação web por meio de um _[Load Balancer](https://docs.oracle.com/pt-br/iaas/Content/NetworkLoadBalancer/home.htm)_. No entanto, antes, é necessário que o processo de provisionamento de um _[Compute Instance](https://docs.oracle.com/pt-br/iaas/Content/Compute/Concepts/computeoverview.htm)_, que irá hospedar a aplicação, seja concluído.

## 2.5.6 Cloud Shell

Uma instalação _"pronta para uso"_ do _[OCI CLI](https://docs.oracle.com/pt-br/iaas/Content/API/Concepts/cliconcepts.htm)_, está disponível por meio do _[Cloud Shell](https://docs.oracle.com/pt-br/iaas/Content/API/Concepts/cloudshellintro.htm)_, que pode ser acessado pela _Web Console_:

![alt_text](./img/cloud-shell-1.png "Cloud Shell #1")
<br>

O _[Cloud Shell](https://docs.oracle.com/pt-br/iaas/Content/API/Concepts/cloudshellintro.htm)_ é um terminal Linux acessível por meio da _Web Console_ que oferece um _shell_ pré-autenticado com diversas ferramentas já instaladas, incluindo o _[OCI CLI](https://docs.oracle.com/pt-br/iaas/Content/API/Concepts/cliconcepts.htm)_. Isso significa que não é necessário realizar a instalação e configuração de uma _[API Key](https://docs.oracle.com/pt-br/iaas/Content/Identity/access/working-with-console-passwords-and-API-keys.htm#one)_.

![alt_text](./img/cloud-shell-2.png "Cloud Shell #2")

!!! note "NOTA"
    Consulte _["O que está Incluído no Cloud Shel"](https://docs.oracle.com/pt-br/iaas/Content/API/Concepts/cloudshellintro.htm)_ para acessar uma lista completa das ferramentas e utilitários disponíveis no _[Cloud Shell](https://docs.oracle.com/pt-br/iaas/Content/API/Concepts/cloudshellintro.htm)_.