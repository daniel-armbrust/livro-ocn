# Capítulo 2: OCI Foundations

# 2.4 Acessando o OCI

## 2.4.1 Formas de Acesso ao OCI

Todo provedor de Computação em Nuvem, incluindo o OCI, disponibiliza seus serviços por meio de **_APIs REST_**. Isso significa que, para criar um recurso - seja uma máquina virtual, um banco de dados ou uma rede - você deve utilizar uma ou mais dessas APIs.

Embora seja possível interagir diretamente com as APIs do OCI, essa abordagem pode ser complexa. Por exemplo, para criar uma _[VCN](https://docs.oracle.com/pt-br/iaas/Content/Network/Tasks/Overview_of_VCNs_and_Subnets.htm)_ diretamente por meio de sua API, é necessário enviar uma solicitação _HTTPS_ utilizando o método _POST_ para um endpoint na região de _São Paulo, Brasil_, semelhante ao exemplo abaixo:

```bash linenums="1"
$ curl -X POST https://iaas.sa-saopaulo-1.oraclecloud.com/20160918/vcns \
> -H "Content-Type: application/json" \
> -d '{
>   "compartmentId": "ocid1.compartment.oc1..aaaaaaaaaaaaaaaabbbbbbbbccc",
>   "displayName": "vcn-saopaulo",
>   "cidrBlock": "172.16.0.0/16"
> }'
```

!!! note "NOTA"    
    Toda interação com as APIs do OCI exige um usuário válido com sua devida credencial de autenticação. Além de ter as credenciais corretas, o usuário deve estar autorizado por meio de _[Policies](https://docs.oracle.com/pt-br/iaas/Content/Identity/policieshow/Policy_Basics.htm)_. Na seção XYZ, abordaremos a criação de novos usuários e a concessão de permissões para utilizar as APIs do OCI.

!!! note "NOTA"
    Para consultar a lista completa de APIs disponíveis para todos os recursos e serviços oferecidos pelo OCI, acesse o link _[API Reference and Endpoints](https://docs.oracle.com/en-us/iaas/api/#/)_.

Diante disso, existem basicamente **_quatro maneiras_** de acessar e interagir com as APIs do OCI sem a necessidade de montar requisições HTTP manualmente. São elas:

### **[Web Console](https://docs.oracle.com/pt-br/iaas/Content/GSG/Concepts/console.htm)**

A _[Web Console](https://docs.oracle.com/pt-br/iaas/Content/GSG/Concepts/console.htm)_, acessível por meio de um navegador de internet _(Mozilla Firefox, Google Chrome ou Opera)_, oferece uma interface gráfica intuitiva para gerenciar todos os serviços de nuvem do OCI. Essa é a forma mais comum e a mais utilizada para acessar e administrar seu ambiente no OCI.

Para acessar a _[Web Console](https://docs.oracle.com/pt-br/iaas/Content/GSG/Concepts/console.htm)_, insira o seguinte endereço no seu navegador:

![alt_text](./img/web-console-1.png "Web Console #1")

Você será direcionado para a página onde deverá inserir o **_Nome da Conta_** ou **_Nome do Tenancy_** que foi criado. No exemplo do livro, o nome da conta é: **_ocipizza_**
<br><br>

![alt_text](./img/web-console-2.png "Web Console #2")
<br>

Será solicitado a escolha de um _[Domínio de Identidade (Identity Domain)](https://docs.oracle.com/pt-br/iaas/Content/Identity/domains/overview.htm#overview-identity-domains)_ para a autenticação do usuário. Neste caso, iremos utilizar o **_Default_** pois nenhum outro domínio de identidade foi criado.
<br><br>

![alt_text](./img/web-console-3.png "Web Console #3")

!!! note "NOTA"
    Consulte a documentação _["Gerenciando Domínios de Identidade"](https://docs.oracle.com/pt-br/iaas/Content/Identity/domains/overview.htm#overview-identity-domains)_ para obter mais informações sobre como criar, administrar e federar outros domínios de identidade.

Após selecionar o _Domínio de Identidade_ a ser utilizado, é hora de inserir o nome de usuário e a senha. Neste caso, o usuário a ser utilizado é o usuário administrador que foi configurado durante a criação da conta no OCI.

![alt_text](./img/web-console-4.png "Web Console #4")
<br><br>

Após a autenticação bem-sucedida, você será redirecionado para a página principal da _[Web Console](https://docs.oracle.com/pt-br/iaas/Content/GSG/Concepts/console.htm)_.

![alt_text](./img/web-console-5.png "Web Console #5")
<br>

!!! note "NOTA"
    Este é um livro _"Orientado a Código"_. Consoles gráficas, como a _[Web Console](https://docs.oracle.com/pt-br/iaas/Content/GSG/Concepts/console.htm)_, sofrem mudanças com maior frequência e por isso, este meio será pouco utilizado nos exemplos apresentados. Para obter mais informações sobre a _[Web Console](https://docs.oracle.com/pt-br/iaas/Content/GSG/Concepts/console.htm)_, consulte a documentação disponível no link _[Home Page da Console](https://docs.oracle.com/pt-br/iaas/Content/GSG/Concepts/console-home.htm)_.

### **[OCI CLI (OCI Command Line Interface)](https://docs.oracle.com/pt-br/iaas/Content/API/Concepts/cliconcepts.htm)**

O _[OCI CLI](https://docs.oracle.com/pt-br/iaas/Content/API/Concepts/cliconcepts.htm)_ é uma ferramenta de _linha de comando_ que permite criar e gerenciar seus recursos no OCI, sendo este o método que será mais utilizado nos exemplos deste livro.

É importante lembrar que tudo o que pode ser realizado por meio do _Web Console_ também pode ser feito através do _[OCI CLI](https://docs.oracle.com/pt-br/iaas/Content/API/Concepts/cliconcepts.htm)_, uma vez que ambos interagem com as mesmas _APIs REST_ disponibilizadas pelo OCI. Vale ressaltar que algumas funcionalidades estão disponíveis exclusivamente no _[OCI CLI](https://docs.oracle.com/pt-br/iaas/Content/API/Concepts/cliconcepts.htm)_ e não na _Web Console_.

Por exemplo, para criar uma _[VCN](https://docs.oracle.com/pt-br/iaas/Content/Network/Tasks/Overview_of_VCNs_and_Subnets.htm)_ utilizando o _[OCI CLI](https://docs.oracle.com/pt-br/iaas/Content/API/Concepts/cliconcepts.htm)_, você pode executar o seguinte comando:

```bash linenums="1"
$ oci --region "sa-saopaulo-1" network vcn create \
> --compartment-id "ocid1.compartment.oc1..aaaaaaaaaaaaaaaabbbbbbbbccc" \
> --cidr-blocks '["172.16.0.0/16"]' \
> --display-name "vcn-saopaulo" \
> --dns-label "vcnsaopaulo" \
> --wait-for-state AVAILABLE
```

### **[OCI SDK (OCI Software Development Kits)](https://docs.oracle.com/pt-br/iaas/Content/API/Concepts/developerquickstarts.htm)**

Um _[SDK](https://docs.oracle.com/pt-br/iaas/Content/API/Concepts/developerquickstarts.htm)_, ou _[Software Development Kit (Kit de Desenvolvimento de Software)](https://docs.oracle.com/pt-br/iaas/Content/API/Concepts/developerquickstarts.htm)_, é projetado para auxiliar os desenvolvedores na integração de funcionalidades e recursos de uma tecnologia específica em seus aplicativos.

No caso do _[OCI SDK](https://docs.oracle.com/pt-br/iaas/Content/API/Concepts/developerquickstarts.htm)_, disponível em várias linguagens de programação, ele proporciona uma maneira simplificada de integrar e acessar as APIs do OCI diretamente no código do seu aplicativo. 

Neste livro, utilizaremos o _[OCI Python SDK](https://docs.oracle.com/en-us/iaas/tools/python/latest/)_, que é um _módulo Python_ que disponibiliza diversas classes e métodos para interagir com as APIs do OCI. Em resumo, a aplicação **_OCI Pizza_**, também desenvolvida em _Python_, faz uso desse _SDK_ para se comunicar com as APIs do OCI.

A instalação do _[OCI Python SDK](https://docs.oracle.com/en-us/iaas/tools/python/latest/)_ é fácil e pode ser feita com um único comando:

```bash linenums="1"
$ python3 -m pip install oci
```

A seguir, um exemplo de como utilizar o _[OCI Python SDK](https://docs.oracle.com/en-us/iaas/tools/python/latest/)_ para criar uma _[VCN](https://docs.oracle.com/pt-br/iaas/Content/Network/Tasks/Overview_of_VCNs_and_Subnets.htm)_:

```python linenums="1"
import oci

config = oci.config.from_file("~/.oci/config", "DEFAULT") 

vcn_client = oci.core.VirtualNetworkClient(config)

create_vcn_details = oci.core.models.CreateVcnDetails(
    compartment_id="ocid1.compartment.oc1..aaaaaaaaaaaaaaaabbbbbbbbccc",
    display_name="vcn-saopaulo",
    cidr_blocks=["172.16.0.0/16"]
)

vcn_client.create_vcn(create_vcn_details)
```

!!! note "NOTA"
    A documentação do _[OCI Python SDK](https://docs.oracle.com/en-us/iaas/tools/python/latest/)_ pode ser acessada através do link _[Oracle Cloud Infrastructure Python SDK](https://docs.oracle.com/en-us/iaas/tools/python/latest/)_.

!!! note "NOTA"
    Consulte _["Interface de Linha de Comando e Kits de Desenvolvimento de Software"](https://docs.oracle.com/pt-br/iaas/Content/API/Concepts/sdks.htm)_ para acessar uma lista dos SDKs disponíveis em outras linguagens de programação.

### **[Terraform](https://docs.oracle.com/pt-br/iaas/Content/dev/terraform/getting-started.htm)**

_[Terraform](https://www.terraform.io/)_ é uma ferramenta de _Infraestrutura como Código (IaC)_ desenvolvida pela _HashiCorp_ que permite definir, criar e gerenciar recursos no OCI por meio de código. Assim como o _OCI CLI_, o _OCI SDK_ e a _Web Console_, o _[Terraform](https://www.terraform.io/)_ utiliza as mesmas APIs para interagir com os serviços e recursos disponíveis no OCI.

Por exemplo, para criar uma _[VCN](https://docs.oracle.com/pt-br/iaas/Content/Network/Tasks/Overview_of_VCNs_and_Subnets.htm)_ utilizando o _[Terraform](https://www.terraform.io/)_, o código seria este:

```terraform linenums="1"
resource "oci_core_vcn" "vcn-saopaulo" {
   compartment_id = "ocid1.compartment.oc1..aaaaaaaaaaaaaaaabbbbbbbbccc"
   display_name = "vcn-saopaulo"
   cidr_blocks = ["172.16.0.0/16"]
}
```

!!! note "NOTA"
    A utilização do _[Terraform](https://www.terraform.io/)_ para criar e gerenciar infraestrutura no OCI será discutida de forma mais detalhada no "Capítulo XYZ - Terraform". Nesse capítulo, também será apresentado o _[Resource Manager](https://docs.oracle.com/pt-br/iaas/Content/ResourceManager/Concepts/resource-manager-and-terraform.htm)_, que é essencialmente uma implementação do Terraform como serviço no OCI.

## 2.4.2 Instalação do OCI CLI

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

## 2.4.3 OCI APIs

O OCI como todo provedor de computação em Nuvem, disponibilizam seus serviços através de um conjunto de diferentes APIs. 

!!! note "NOTA"
    Todas as APIs que o OCI disponibiliza, estão documentadas no link _[API Reference and Endpoints](https://docs.oracle.com/en-us/iaas/api/#/)_.

As APIs do OCI são públicas, acessíveis pela Internet por meio do protocolo _HTTPS_. Por exemplo, o conjunto de APIs denominado _[Core Services API](https://docs.oracle.com/en-us/iaas/api/#/en/iaas/latest/)_, permite gerenciar recursos como _[VCN](https://docs.oracle.com/pt-br/iaas/Content/Network/Tasks/Overview_of_VCNs_and_Subnets.htm)_, _[Compute Instances](https://docs.oracle.com/pt-br/iaas/Content/Compute/Concepts/computeoverview.htm)_ e _[Block Storage](https://docs.oracle.com/pt-br/iaas/Content/Block/Concepts/overview.htm)_.

![alt_text](./img/core-services-api-1.png "Core Services API #1")

Todo serviço no OCI, disponível por meio de uma API, possui um **_endpoint_** exclusivo, que varia conforme a região. Para o _[Core Services API](https://docs.oracle.com/en-us/iaas/api/#/en/iaas/latest/)_, o _endpoint_ correspondente é:

![alt_text](./img/core-services-api-2.png "Core Services API #2")

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
    Lembre-se de que todos os valores retornados pelo OCI nos exemplos apresentados aqui para a configuração do _[OCI CLI](https://docs.oracle.com/pt-br/iaas/Content/API/Concepts/cliconcepts.htm)_ são fictícios e não funcionarão para você. Para concluír com sucesso as configurações, utilize os valores reais fornecidos pelo seu _Tenancy_.

## 2.4.5 Trabalhando com o OCI CLI

Após o OCI CLI estar devidamente configurado e funcionado, é hora de lidar com algums comandos na prática

## 2.4.6 Cloud Shell

Uma instalação _"pronta para uso"_ do _[OCI CLI](https://docs.oracle.com/pt-br/iaas/Content/API/Concepts/cliconcepts.htm)_, está disponível por meio do _[Cloud Shell](https://docs.oracle.com/pt-br/iaas/Content/API/Concepts/cloudshellintro.htm)_, que pode ser acessado pela _Web Console_:

![alt_text](./img/cloud-shell-1.png "Cloud Shell #1")
<br>

O _[Cloud Shell](https://docs.oracle.com/pt-br/iaas/Content/API/Concepts/cloudshellintro.htm)_ é um terminal Linux acessível por meio da _Web Console_ que oferece um _shell_ pré-autenticado com diversas ferramentas já instaladas, incluindo o _[OCI CLI](https://docs.oracle.com/pt-br/iaas/Content/API/Concepts/cliconcepts.htm)_. Isso significa que não é necessário realizar a instalação e configuração de uma _[API Key](https://docs.oracle.com/pt-br/iaas/Content/Identity/access/working-with-console-passwords-and-API-keys.htm#one)_.

![alt_text](./img/cloud-shell-2.png "Cloud Shell #2")

!!! note "NOTA"
    Consulte _["O que está Incluído no Cloud Shel"](https://docs.oracle.com/pt-br/iaas/Content/API/Concepts/cloudshellintro.htm)_ para acessar uma lista completa das ferramentas e utilitários disponíveis no _[Cloud Shell](https://docs.oracle.com/pt-br/iaas/Content/API/Concepts/cloudshellintro.htm)_.