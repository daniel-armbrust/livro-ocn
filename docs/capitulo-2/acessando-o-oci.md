# Capítulo 2: OCI Foundations

# 2.4 Acessando o OCI

## 2.4.1 Formas de Acesso ao OCI

Todo provedor de Computação em Nuvem, incluindo o OCI, disponibiliza seus serviços por meio de **_APIs REST_**. Isso significa que, para criar um recurso - seja uma máquina virtual, um banco de dados ou uma rede - você deve utilizar uma ou mais dessas APIs.

Embora seja possível interagir diretamente com as APIs do OCI, essa abordagem pode ser complexa. Por exemplo, para criar uma _[VCN](https://docs.oracle.com/pt-br/iaas/Content/Network/Tasks/Overview_of_VCNs_and_Subnets.htm)_ diretamente por meio de sua API, é necessário enviar uma solicitação _HTTPS_ utilizando o método _POST_ para um _endpoint_ na região de _São Paulo, Brasil_, semelhante ao exemplo abaixo:

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

_[Terraform](https://www.terraform.io/)_ é uma ferramenta de _Infraestrutura como Código (Infrastructure as Code - IaC)_ desenvolvida pela _HashiCorp_ que permite definir, criar e gerenciar recursos no OCI por meio de código. Assim como o _OCI CLI_, o _OCI SDK_ e a _Web Console_, o _[Terraform](https://www.terraform.io/)_ utiliza as mesmas APIs para interagir com os serviços e recursos disponíveis no OCI.

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