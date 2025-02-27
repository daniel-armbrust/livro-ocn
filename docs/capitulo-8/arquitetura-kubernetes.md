# Capítulo 8: Oracle Kubernetes Engine (OKE)

# 8.3 Arquitetura do Kubernetes

O Kubernetes é formado por diversos componentes distribuídos e independentes, cada um com sua própria responsabilidade, todos desenvolvidos na _[linguagem de programação Go](https://go.dev/)_. Para que um cluster Kubernetes funcione, é necessário instalar e configurar esses diferentes componentes.

Para facilitar a identificação, a equipe de desenvolvimento do Kubernetes utiliza o prefixo **_kube_** na maioria dos componentes e utilitários que fazem parte do projeto Kubernetes. A exceção a essa convenção são duas dependências externas: o **_Container Engine_** e o **_etcd_**.

Aqui, será apresentado de forma resumida a aquitetura do Kubernetes e como, esses diferentes componentes trabalham em conjunto.

## 8.3.1 Master Nodes e Worker Nodes

Um cluster Kubernetes típico é composto por várias máquinas, que podem ser físicas, virtuais ou uma combinação de ambas, conhecidas como _Nodes_. Esses nodes são organizados em dois grupos principais:

!!! note "NOTA"
    As máquinas do Master Nodes deve ser Linux. Já as máquinas dos Worker Nodes podem ser Linux ou Windows.

### Control Plane ou Master Nodes

Esse grupo de máquinas supervisiona e envia tarefas para os Worker Nodes. Ou seja, elas são responsáveis por manter o _"estado desejado do cluster"_.

Toda a inteligência do Kubernetes está concentrada nos Master Nodes, e cada cluster deve ter pelo menos uma máquina designada para desempenhar essa função.

Há uma coleção de serviços que operam continuamente em cada Master Node, responsáveis por manter o estado do cluster, incluindo:

!!! note "NOTA"
    A documentação de todos os componentes do Kubernetes está disponível no link _["Core Components"](https://kubernetes.io/docs/concepts/overview/components/#core-components)_

#### [kube-apiserver](https://kubernetes.io/docs/concepts/architecture/#kube-apiserver)

É o _frontend_ do Kubernetes, utilizado para enviar comandos e consultar o estado do cluster.

Esse componente, que expõe uma _API RESTful via HTTPS_, permite comandar, monitorar e obter informações sobre todo o cluster. Todas as interações com essa API podem ser realizadas por meio do utilitário de linha de comando **_[kubectl](https://kubernetes.io/docs/reference/kubectl/)_**.

!!! note "NOTA"
    Devido ao fato de o _[kube-apiserver](https://kubernetes.io/docs/reference/command-line-tools-reference/kube-apiserver/)_ ser uma _API RESTful_, é possível interagir com ele utilizando até mesmo o utilitário de linha de comando _[curl](https://curl.se/)_. No entanto, é mais prático e fácil realizar essas interações através do _[kubectl](https://kubernetes.io/docs/reference/kubectl/)_.

Uma outra função desse componente, é realizar cosultas periódicas ao banco de dados _[etcd](https://etcd.io/)_.

#### [etcd](https://etcd.io/)

Todos os comandos enviados pelo _kube-apiserver_, especialmente aqueles que alteram o _"estado"_, são persistidos ou atualizados em um banco de dados chave/valor distribuído nos Master Nodes, conhecido como _[etcd](https://etcd.io/)_.

A principal função do _etcd_ é armazenar de maneira persistente todas as alterações que foram enviadas ao _kube-apiserver_. O Kubernetes consulta periodicamente o _etcd_ para verificar se o _"estado do cluster"_ está em conformidade com os dados ali armazenados.

Outro ponto importante é que nenhum componente pode ler ou escrever no _etcd_ sem passar pelo _kube-apiserver_. 

O _etcd_ não é um componente do projeto Kubernetes, mas é um projeto independente que também faz parte da _[Cloud Native Computing Foundation (CNCF)](../capitulo-1/cloud-native.md)_.

!!! note "NOTA"
    Existe um playground online acessível pelo link _[http://play.etcd.io/play]_, que permite aprender e gerenciar clusters com o etcd.

#### [kube-scheduler](https://kubernetes.io/docs/concepts/architecture/#kube-scheduler)

A função principal do kube-scheduler é monitorar, por meio de consultas regulares ao kube-apiserver, a presença de novos Pods a serem criados e selecionar um ou mais Worker Nodes para sua execução.

!!! note "NOTA"    
    Uma explicação mais detalhada sobre objetos do Kubernetes, incluindo Pods, será apresentada no capítulo _[8.4 Objetos Kubernetes](./objetos-kubernetes.md)_. Por enquanto, é importante compreender que um Pod é um objeto do Kubernetes utilizado para definir uma unidade de execução que pode conter um ou mais contêineres.
    
Assim que um Pod é criado, ainda não há um Worker Node designado para sua execução. Chamamos de _"Unschedule Pod"_ o Pod que não possui um Worker Node elegível para execução, e seu status permanece como _"Pending"_. Já o termo "Schedule" refere-se ao processo de atribuição do Pod a um Worker Node capaz de realizar a sua execução. Em outras palavras, quando um Pod é _"scheduled"_, isso significa que ele foi atribuído a um Worker Node específico e está pronto para ser executado. 

Além disso, o kube-scheduler desempenha outras funções importantes, como a verificação de regras de afinidade e antiafinidade, a checagem da disponibilidade de portas de rede e a validação dos recursos de CPU e memória.

#### [kube-controller-manager](https://kubernetes.io/docs/concepts/architecture/#kube-controller-manager)

O _[kube-controller-manager](https://kubernetes.io/docs/concepts/architecture/#kube-controller-manager)_, também conhecido como controller, é responsável por executar o _"loop de reconciliação" (reconciliation loop)_, que tem como objetivo manter o estado do cluster em sincronia com as informações armazenadas no _etcd_.

Por exemplo, quando solicitado, o Kubernetes é capaz de manter um número específico de Pods distribuídos entre os diferentes _Worker Nodes_. Se, por qualquer motivo, o número total de Pods ativos divergir do número de Pods registrado no _etcd_, o _"loop de reconciliação"_ garantirá que os Pods ausentes sejam iniciados. Vale ressaltar que essa verificação é um processo contínuo, o que justifica o uso da palavra _"loop"_ para descrever sua funcionalidade.

Há diferentes _controllers_ que fazem parte do _"loop de reconciliação"_ e cada um deles é responsável por gerenciar e cuidar de um tipo específico de objeto Kubernetes. Alguns deles são:

- Replication Controller
- Deployment Controller
- Job Controller
- Namespace Controller

### [OCI Cloud Controller Manager (CCM)](https://github.com/oracle/oci-cloud-controller-manager)

O _[OCI Cloud Controller Manager](https://github.com/oracle/oci-cloud-controller-manager)_, ou _[oci-cloud-controller-manager](https://github.com/oracle/oci-cloud-controller-manager)_, é a implementação do _[cloud-controller-manager](https://kubernetes.io/docs/concepts/architecture/#cloud-controller-manager)_ responsável por conectar o Kubernetes às APIs do OCI.

!!! note "NOTA"
    O _[oci-cloud-controller-manager](https://github.com/oracle/oci-cloud-controller-manager)_ é um projeto de código aberto mantido pela Oracle. O código-fonte da implementação pode ser acessado por meio do link _[https://github.com/oracle/oci-cloud-controller-manager](https://github.com/oracle/oci-cloud-controller-manager)_

Uma das funcionalidades do _[oci-cloud-controller-manager](https://github.com/oracle/oci-cloud-controller-manager)_ é a criação de _[Load Balance](../capitulo-4/load-balancer.md)_ no OCI por meio do do objeto _Service_.

### Compute Nodes ou Worker Nodes

Em resumo, os Worker Nodes têm a função de executar as aplicações.

!!! note "NOTA"
    É importante ressaltar que, embora seja possível executar todos os componentes do Kubernetes em uma única máquina, essa configuração não oferece tolerância a falhas. A abordagem recomendada é ter pelo menos duas máquinas configuradas como Master Nodes e outras duas como Worker Nodes. Essa configuração proporciona maior resiliência e disponibilidade.