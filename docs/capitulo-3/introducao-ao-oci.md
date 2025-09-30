---
hide:  
  - toc
---

# Capítulo 3: OCI Foundations

# 3.1 Introdução ao OCI

A <a href="https://www.oracle.com/cloud/" target="blank">Oracle Cloud Infrastructure (OCI)</a> é a plataforma de computação em nuvem da <a href="https://www.oracle.com/" target="blank">Oracle</a>, projetada para atender a diversas necessidades pessoais e empresariais. Ela oferece uma ampla gama de serviços, incluindo computação, armazenamento, rede, banco de dados, inteligência artificial e muito mais. Isso permite que você ou sua empresa implementem soluções em nuvem flexíveis e escaláveis em um ambiente seguro e de alto desempenho.

Antes de começar a utilizar o <a href="https://www.oracle.com/cloud/" target="blank">OCI</a>, é fundamental compreender alguns conceitos básicos que ajudarão no planejamento da sua arquitetura computacional na nuvem.

## 3.1.1 Região

Uma <a href="https://docs.oracle.com/pt-br/iaas/Content/General/Concepts/regions.htm" target="blank">região</a> é uma área geográfica que abriga **_um ou mais data centers_**, os quais podem ser utilizados para construir sua infraestrutura de TI. As <a href="https://docs.oracle.com/pt-br/iaas/Content/General/Concepts/regions.htm" target="blank">regiões</a> podem ser separadas por grandes distâncias, abrangendo países ou até mesmo continentes.

A ideia de ter múltiplas <a href="https://docs.oracle.com/pt-br/iaas/Content/General/Concepts/regions.htm" target="blank">regiões</a> disponíveis em todo o mundo é permitir que você expanda seu negócio globalmente, além de possibilitar a construção de arquiteturas altamente disponíveis. Ter a possibilidade de criar e disponibilizar seus recursos computacionais em diversas localidades do mundo, não apenas melhora a resiliência e a redundância dos seus serviços, mas também assegura que seus usuários tenham acesso às suas aplicações com baixa latência, independentemente da sua localização geográfica.

![alt_text](./img/oci-regions-1.png "Regiões do OCI")

Toda <a href="https://docs.oracle.com/pt-br/iaas/Content/General/Concepts/regions.htm" target="blank">região</a> possui **_três tipos de identificações_**, cada uma utilizada em contextos diferentes. As colunas da tabela abaixo, _"Nome da Região"_, _"Identificador"_ e _"Chave da Região"_, são usadas para identificar uma <a href="https://docs.oracle.com/pt-br/iaas/Content/General/Concepts/regions.htm" target="blank">região</a> específica:

| Nome da Região              | Localidade        | Identificador | Chave da Região |
|-----------------------------|-------------------|---------------|-----------------|
| Brazil East (Sao Paulo)     | São Paulo, Brasil | sa-saopaulo-1 | GRU             |
| Brazil Southeast (Vinhedo)  | Vinhedo, Brasil   | sa-vinhedo-1  | VCP             |
| Chile Central (Santiago)    | Santiago, Chile   | sa-santiago-1 | SCL             |
| US East (Ashburn)           | Ashburn, VA       | us-ashburn-1  | IAD             |
| Japan East (Tokyo)          | Tokyo, Japão      | ap-tokyo-1    | NRT             |

!!! note "NOTA"
    Aqui foram listados apenas alguns nomes de <a href="https://docs.oracle.com/pt-br/iaas/Content/General/Concepts/regions.htm" target="blank">regiões</a>. A <a href="https://www.oracle.com/" target="blank">Oracle</a> cria e disponibiliza novas <a href="https://docs.oracle.com/pt-br/iaas/Content/General/Concepts/regions.htm" target="blank">regiões</a> ao redor do mundo periodicamente. Para uma lista completa e atualizada das <a href="https://docs.oracle.com/pt-br/iaas/Content/General/Concepts/regions.htm" target="blank">regiões</a> disponíveis, consulte <a href="https://docs.oracle.com/pt-br/iaas/Content/General/Concepts/regions.htm" target="blank"><i>"Regiões e Domínios de Disponibilidade"</i></a>.

Através da <a href="https://docs.public.oneportal.content.oci.oraclecloud.com/pt-br/iaas/Content/GSG/Tasks/signingin.htm" target="blank">Console Web do OCI</a>, o _"Nome da Região"_ é o utilizado:

![alt_text](./img/oci-region-console-saopaulo-1.png "Console Web - Região São Paulo")
<br><br>

Já para alguns <a href="https://docs.oracle.com/pt-br/iaas/Content/General/Concepts/identifiers.htm" target="blank">Identificadores de Recursos (OCID)</a>, o _"Identificador"_ da <a href="https://docs.oracle.com/pt-br/iaas/Content/General/Concepts/regions.htm" target="blank">região</a> é usado:

![alt_text](./img/region-ocid-1.png "OCID - Região São Paulo")

!!! note "NOTA"
    Por enquanto, é importante entender que todo recurso criado dentro do <a href="https://www.oracle.com/cloud/" target="blank">OCI</a> possui um identificador único chamado <a href="https://docs.oracle.com/pt-br/iaas/Content/General/Concepts/identifiers.htm#Oracle" target="blank"><i>"Oracle Cloud ID (OCID)"</i></a>. Na seção <a href="https://ocn.dev.br/capitulo-3/gerenciando-o-oci-atraves-do-oci-cli/"><i>"3.5 Gerenciando o OCI através do OCI CLI"</i></a>, abordaremos mais detalhes sobre <a href="https://ocn.dev.br/capitulo-3/gerenciando-o-oci-atraves-do-oci-cli/" >OCID</a>.

Já o nome do domínio utilizado pelo serviço do <a href="https://docs.oracle.com/pt-br/iaas/Content/Registry/Concepts/registryoverview.htm" target="blank">Container Registry</a>, pode utilizar tanto o _"Identificador"_ quanto a _"Chave da Região"_:

![alt_text](./img/oci-region-key-1.png "Chave da Região")

Por fim, algumas <a href="https://docs.oracle.com/pt-br/iaas/Content/General/Concepts/regions.htm" target="blank">regiões</a> oferecem conectividade direta com outros provedores de nuvem, como <a href="https://docs.oracle.com/pt-br/iaas/Content/Network/Concepts/azure.htm" target="blank">Microsoft Azure</a> e <a href="https://docs.oracle.com/en-us/iaas/Content/Network/Concepts/access-to-google-cloud-platform.htm" target="blank">Google Cloud</a>, o que possibilita a criação de arquiteturas do tipo <a href="https://docs.oracle.com/pt-br/iaas/Content/multicloud/Oraclemulticloud.htm" target="blank">Multicloud</a>.

![alt_text](./img/oci-regions-3.png "Microsoft Azure e Google Cloud")

## 3.1.2 Availability Domains (AD)

Um <a href="https://docs.oracle.com/pt-br/iaas/Content/General/Concepts/regions.htm" target="blank">Availability Domains (AD)</a> ou <a href="https://docs.oracle.com/pt-br/iaas/Content/General/Concepts/regions.htm" target="blank">Domínio de Disponibilidade</a>, é basicamente um **_data center_** que reside dentro de uma <a href="https://docs.oracle.com/pt-br/iaas/Content/General/Concepts/regions.htm" target="blank">região</a>. 

Dentro de uma <a href="https://docs.oracle.com/pt-br/iaas/Content/General/Concepts/regions.htm" target="blank">região</a>, podem existir um ou, no máximo, três <a href="https://docs.oracle.com/pt-br/iaas/Content/General/Concepts/regions.htm" target="blank">Availability Domains</a> interconectados por links de baixa latência. A principal razão de existir múltiplos <a href="https://docs.oracle.com/pt-br/iaas/Content/General/Concepts/regions.htm" target="blank">Availability Domains</a> em uma <a href="https://docs.oracle.com/pt-br/iaas/Content/General/Concepts/regions.htm" target="blank">região</a> é permitir a criação de recursos de TI de forma distribuída, evitando assim o que é conhecido como **_"ponto único de falha"_**.

Os <a href="https://docs.oracle.com/pt-br/iaas/Content/General/Concepts/regions.htm" target="blank">Availability Domains</a> são isolados uns dos outros, não compartilham infraestrutura e são projetados para serem **_tolerantes a falhas_**. Caso um deles venha a falhar, isso não impacta os outros <a href="https://docs.oracle.com/pt-br/iaas/Content/General/Concepts/regions.htm" target="blank">Availability Domains</a> em operação na mesma <a href="https://docs.oracle.com/pt-br/iaas/Content/General/Concepts/regions.htm" target="blank">região</a>.

![alt_text](./img/availability-domain-1.png "Availability Domains (AD)")

Para algumas <a href="https://docs.oracle.com/pt-br/iaas/Content/General/Concepts/regions.htm" target="blank">regiões</a> onde há somente um <a href="https://docs.oracle.com/pt-br/iaas/Content/General/Concepts/regions.htm" target="blank">Availability Domain</a>, o <a href="https://www.oracle.com/cloud/" target="blank">OCI</a>, oferece a opção de utilizar uma outra <a href="https://docs.oracle.com/pt-br/iaas/Content/General/Concepts/regions.htm" target="blank">região</a> geograficamente mais próxima. Esse é o caso do Brasil, onde existem duas <a href="https://docs.oracle.com/pt-br/iaas/Content/General/Concepts/regions.htm" target="blank">regiões</a> relativamente próximas: São Paulo e Vinhedo.

![alt_text](./img/oci-regions-2.png "GRU e VCP")

Os recursos que você cria no <a href="https://www.oracle.com/cloud/" target="blank">OCI</a> podem ser do tipo **_global (Cross-Region)_**, o que significa que são criados uma vez e disponibilizados em todas as <a href="https://docs.oracle.com/pt-br/iaas/Content/General/Concepts/regions.htm" target="blank">regiões</a> nas quais você está inscrito. Também podem ser **_recursos regionais (Regional Resources)_**, que são criados em uma <a href="https://docs.oracle.com/pt-br/iaas/Content/General/Concepts/regions.htm" target="blank">região</a> e se tornam acessíveis por todos os <a href="https://docs.oracle.com/pt-br/iaas/Content/General/Concepts/regions.htm" target="blank">Availability Domains</a> dessa <a href="https://docs.oracle.com/pt-br/iaas/Content/General/Concepts/regions.htm" target="blank">região</a>, ou **_recursos específicos do Availability Domains (Availability Domain-Specific)_**, que estão disponíveis apenas dentro de um determinado <a href="https://docs.oracle.com/pt-br/iaas/Content/General/Concepts/regions.htm" target="blank">Availability Domain</a>.

Compreender essa característica ao criar seus recursos no <a href="https://www.oracle.com/cloud/" target="blank">OCI</a> permite que você desenvolva uma infraestrutura redundante e resiliente, assegurando que sua arquitetura continue operante mesmo diante de falhas. E lembre-se: é importante ter em mente que **_tudo falha, até o OCI falha_**.

Alguns exemplos referentes à localidade dos recursos incluem:

- **Global (Cross-Region)**
    - <a href="https://docs.oracle.com/pt-br/iaas/Content/Identity/users/about-managing-users.htm" target="blank">Usuários</a>
    - <a href="https://docs.oracle.com/pt-br/iaas/Content/Identity/groups/managinggroups.htm" target="blank">Grupos de Usuários</a>
    - <a href="https://docs.oracle.com/pt-br/iaas/Content/Identity/policieshow/Policy_Basics.htm" target="blank">Políticas do IAM</a>

- **Recursos Regionais (Regional Resources)**
    - <a href="https://docs.oracle.com/pt-br/iaas/Content/Network/Tasks/Overview_of_VCNs_and_Subnets.htm" target="blank">Virtual Cloud Networks (VCNs)</a>
    - <a href="https://docs.oracle.com/pt-br/iaas/Content/Network/Tasks/Overview_of_VCNs_and_Subnets.htm" target="blank">Sub-redes</a>
    - <a href="https://docs.oracle.com/pt-br/iaas/Content/Registry/Concepts/registryoverview.htm" target="blank">Container Registry</a>

- **Recursos Específicos do Availability Domains (Availability Domain-Specific)**
    - <a href="https://docs.oracle.com/pt-br/iaas/Content/Compute/Concepts/computeoverview.htm" target="blank">Compute Instances (Máquinas Virtuais ou Físicas)</a>
    - <a href="https://docs.oracle.com/pt-br/iaas/Content/container-instances/overview-of-container-instances.htm" target="blank">Container Instances</a>
    - <a href="https://docs.oracle.com/pt-br/iaas/Content/Block/Concepts/overview.htm" target="blank">Block Volume</a>

!!! note "NOTA"
    Para uma lista completa sobre os tipos de recursos com base em sua disponibilidade, consulte <a href="https://docs.oracle.com/en-us/iaas/Content/General/Concepts/regions.htm#Resource" target="blank"><i>"Resource Availability"</i></a>.

## 3.1.3 Fault Domains (FD)

Um <a href="https://docs.oracle.com/pt-br/iaas/Content/General/Concepts/regions.htm#fault" target="blank">Fault Domain</a> é um agrupamento de hardware e infraestrutura dentro de um <a href="https://docs.oracle.com/pt-br/iaas/Content/General/Concepts/regions.htm" target="blank">Availability Domain</a>. Cada <a href="https://docs.oracle.com/pt-br/iaas/Content/General/Concepts/regions.htm" target="blank">Availability Domain</a> possui **_três Fault Domains_**, que também podem ser utilizados para distribuir os recursos computacionais que você cria no <a href="https://www.oracle.com/cloud/" target="blank">OCI</a> em diferentes conjuntos isolados de hardware.

Ao criar um recurso de computação <a href="https://docs.oracle.com/pt-br/iaas/Content/Compute/Concepts/computeoverview.htm" target="blank">(Compute Instance)</a>, é possível selecionar em qual dos três <a href="https://docs.oracle.com/pt-br/iaas/Content/General/Concepts/regions.htm#fault" target="blank">Fault Domains</a> disponíveis sua <a href="https://docs.oracle.com/pt-br/iaas/Content/Compute/Concepts/computeoverview.htm" target="blank">máquina virtual</a> será criada. Falhas ou eventos de manutenção que afetam um determinado <a href="https://docs.oracle.com/pt-br/iaas/Content/General/Concepts/regions.htm#fault" target="blank">Fault Domain</a> não causam indisponibilidade em outros <a href="https://docs.oracle.com/pt-br/iaas/Content/General/Concepts/regions.htm#fault" target="blank">Fault Domains</a>. Caso um <a href="https://docs.oracle.com/pt-br/iaas/Content/General/Concepts/regions.htm#fault" target="blank">Fault Domain</a> não seja selecionado, o <a href="https://www.oracle.com/cloud/" target="blank">OCI</a> escolherá automaticamente um para você.

![alt_text](./img/fault-domain-1.png "Fault Domains (FD)")

!!! note "NOTA"
    Consulte <a href="https://docs.oracle.com/pt-br/iaas/Content/Compute/References/infrastructure-maintenance.htm#infrastructure-maintenance" target="blank"><i>"Manutenção da Infraestrutura"</i></a> para obter mais informações sobre as manutenções realizadas pelo <a href="https://www.oracle.com/cloud/" target="blank">OCI</a> que podem afetar suas <a href="https://docs.oracle.com/pt-br/iaas/Content/Compute/Concepts/computeoverview.htm" target="blank">instâncias computacionais</a> em diferentes <a href="https://docs.oracle.com/pt-br/iaas/Content/General/Concepts/regions.htm#fault" target="blank">Fault Domains</a>.

!!! note "NOTA"
    Um <a href="https://docs.oracle.com/pt-br/iaas/Content/General/Concepts/regions.htm#fault" target="blank">Fault Domain</a> pode ser entendido como um **_data center lógico (ou rack)_** dentro de um data center físico ou, mais especificamente, dentro de um <a href="https://docs.oracle.com/pt-br/iaas/Content/General/Concepts/regions.htm" target="blank">Availability Domain</a>.

## 3.1.4 Níveis de Proteção

Em resumo, os níveis de proteção contra falhas que o <a href="https://www.oracle.com/cloud/" target="blank">OCI</a> disponibiliza são:

- **Regiões**
    - Em muitos países, há duas <a href="https://docs.oracle.com/pt-br/iaas/Content/General/Concepts/regions.htm" target="blank">regiões</a> relativamente próximas que podem ser utilizadas caso uma <a href="https://docs.oracle.com/pt-br/iaas/Content/General/Concepts/regions.htm" target="blank">região</a> venha a falhar.

- **Availability Domains**
    - Proporciona proteção e disponibilidade contra falhas gerais que podem ocorrer em um <a href="https://docs.oracle.com/pt-br/iaas/Content/General/Concepts/regions.htm" target="blank">Availability Domain</a> específico.

- **Fault Domains**
    - Proporciona proteção e disponibilidade dentro de um <a href="https://docs.oracle.com/pt-br/iaas/Content/General/Concepts/regions.htm" target="blank">Availability Domain</a>, isolando os recursos em diferentes conjuntos de hardware.

## 3.1.5 OCI Status

<a href="https://ocistatus.oraclecloud.com" target="blank">OCI Status</a> ou <a href="https://ocistatus.oraclecloud.com" target="blank">OCI Service Health Dashboard</a> é um painel de acesso público que fornece o _"status atual"_ de todos os serviços do <a href="https://www.oracle.com/cloud/" target="blank">OCI</a> por <a href="https://docs.oracle.com/pt-br/iaas/Content/General/Concepts/regions.htm" target="blank">região</a>. Além da monitoração em tempo real, é possível consultar o histórico de incidentes que já ocorreram na infraestrutura do <a href="https://www.oracle.com/cloud/" target="blank">OCI</a>.

Para acessar a página do <a href="https://ocistatus.oraclecloud.com" target="blank">OCI Status</a>, insira o seguinte endereço no seu navegador:

![alt_text](./img/oci-status-1.png "OCI Status #1")

Assim que a página for carregada, você poderá selecionar a localidade geográfica para verificar o _"status atual"_ dos serviços nas regiões da localidade selecionada:

![alt_text](./img/oci-status-2.png "OCI Status #2")
<br><br>

Por meio do link **_History_**, é possível consultar os problemas anteriores de uma <a href="https://docs.oracle.com/pt-br/iaas/Content/General/Concepts/regions.htm" target="blank">região</a> específica:

![alt_text](./img/oci-status-3.png "OCI Status #3")

!!! note "NOTA"
    Para mais informações, consulte a documentação do <a href="https://ocistatus.oraclecloud.com" target="blank">OCI Status</a> em <a href="https://docs.oracle.com/pt-br/iaas/Content/General/Concepts/status-service.htm" target="blank"><i>"Status do Sistema"</i></a>.