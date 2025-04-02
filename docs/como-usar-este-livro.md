# Como usar este Livro

A motivação para escrever um livro sobre _[Cloud Native](./capitulo-1/cloud-native.md)_ na _[Oracle Cloud (OCI)](./capitulo-2/index.md)_ surgiu principalmente da minha falta de entendimento sobre o tema. Posso afirmar que o processo de escrita, combinado com minha experiência cotidiana, me ajudaram a compreender um pouco mais sobre o assunto.

O livro foi escrito em português, pois o objetivo é contribuir, primeiro, com os brasileiros. Optei por não traduzir alguns termos pois eles são usados sem tradução pelos profissionais de TI do Brasil no seu dia a dia.

A _[Oracle Cloud](./capitulo-2/index.md)_ e o conceito de _[Cloud Native](./capitulo-1/cloud-native.md)_ estão em constante evolução, e foi por essa razão que decidi manter o livro aberto e disponível publicamente na Internet, pois isso facilita a atualização do conteúdo.

A versão aberta, em HTML, está disponível em: **[https://ocn.dev.br/](https://ocn.dev.br/)**

É recomendável que a leitura do livro seja feita de forma sequencial, começando pelo Capítulo 1 e seguindo até o final. Isso se deve ao fato de que não faz sentido tentar provisionar um recurso computacional sem uma rede devidamente configurada, assim como não é eficaz criar um _[Container Instance](./capitulo-7/container-instances.md)_ sem entender o que é um contêiner e como ele funciona.

Vale lembrar que a ordem sugerida para a leitura dos capítulos não é uma exigência, mas sim uma recomendação para que você possa aproveitar melhor o conteúdo apresentado neste livro.

Além de apresentar alguns dos serviços disponíveis na Oracle Cloud, o livro inclui uma aplicação web simples, desenvolvida em _[Python/Flask](https://flask.palletsprojects.com/en/stable/)_ pelo próprio autor. O objetivo de incluir essa aplicação é fornecer uma demonstração prática de como implantar uma aplicação utilizando os serviços do OCI.

Boas práticas para a escrita de aplicações web, assim como orientações sobre desenvolvimento, não estão incluídas no escopo deste livro. Da mesma forma, detalhes avançados sobre arquitetura de sistemas, separação de responsabilidades entre serviços, também não são abordados.

Por fim, o livro conta com três repositórios no _[GitHub](https://github.com/)_:

- [https://github.com/daniel-armbrust/ocipizza-iac](https://github.com/daniel-armbrust/ocipizza-iac)
    - Este repositório contém os códigos de exemplo para a criação da infraestrutura no OCI, utilizados ao longo dos capítulos.

- [https://github.com/daniel-armbrust/ocipizza-monolito](https://github.com/daniel-armbrust/ocipizza-monolito)
    - Este repositório contém o monolito da aplicação OCI PIZZA, desenvolvida em Python/Flask. O repositório é utilizando tanto no deployment da aplicação em _[Compute Instance](./capitulo-6/index.md)_ e _[Container Instance](./capitulo-7/container-instances.md)_.

- [https://github.com/daniel-armbrust/ocipizza-microsservicos](https://github.com/daniel-armbrust/ocipizza-microsservicos)
    - Este repositório contém os códigos referentes aos microsserviços da aplicação OCI PIZZA. Os serviços que compõem a aplicação, disponíveis neste repositório, serão implantados utilizando o _[OKE (Oracle Kubernetes Engine)](./capitulo-8/index.md)_.

A descrição sucinta do que cada capítulo abrange pode ser consultada a seguir:

- [Capítulo 1: Introdução a Computação em Nuvem](./capitulo-1/index.md)
    - O capítulo aborda os aspectos históricos que levaram à criação da Computação em Nuvem, além de discutir suas vantagens e desvantagens. Também são apresentados conceitos como DevOps e Cloud Native.

- [Capítulo 2: OCI Foundations](./capitulo-2/index.md)
    - O capítulo oferece uma explicação sobre os fundamentos do OCI, abordando tópicos que vão desde a ativação de uma nova conta na Oracle Cloud até questões relacionadas à cobrança dos serviços, controle de acesso e a utilização do OCI CLI, que é o principal meio utilizado no livro para gerenciar os recursos do OCI.

- [Capítulo 3: Aplicação OCI Pizza](./capitulo-3/index.md)
    - Aqui, é apresentada a aplicação de exemplo OCI PIZZA, desenvolvida em Python/Flask. Serão abordados conceitos relacionados a requisitos funcionais e não funcionais, histórias de usuário, além das arquiteturas monolítica e de microsserviços.

- [Capítulo 4: Conectividade e Redes](./capitulo-4/index.md)
    - Este capítulo apresenta o serviço de redes do OCI, juntamente com a criação da arquitetura de redes utilizada pela aplicação OCI PIZZA.

- [Capítulo 5: Oracle NoSQL Database Cloud Service](./capitulo-5/index.md)
    - Neste capítulo, são abordados os conceitos relacionados a bancos de dados do tipo NoSQL e a utilização do OCI NoSQL, que é o banco de dados utilizado pela aplicação OCI PIZZA.

- [Capítulo 6: Serviço de Computação](./capitulo-6/index.md)
    - Aqui, é apresentado o Serviço de Computação, onde o monolito da aplicação será implantado.

- [Capítulo 7: Desenvolvimento Moderno](./capitulo-7/index.md)
    - Este capítulo aborda o que são contêineres e o processo de conteinerização da aplicação OCI PIZZA. Além disso, são apresentados e utilizados o Serviço Functions e o Serviço Container Instances do OCI.

- [Capítulo 8: Oracle Kubernetes Engine (OKE)](./capitulo-8/index.md)
    - Este capítulo aborda a história e os motivos que levaram à criação do Kubernetes. Além disso, será apresentado e utilizado o OKE (Oracle Kubernetes Engine) para o deployment da aplicação OCI PIZZA, que é o serviço Kubernetes gerenciado do OCI.

- [Capítulo 9: Serviço DevOps](./capitulo-9/index.md)
    - Este capítulo aborda o Serviço DevOps do OCI, focando nas ações de CI/CD (Integração Contínua e Entrega Contínua) da aplicação OCI PIZZA.

- [Capítulo 10: Monitoração e Observabilidade](./capitulo-10/index.md)
    - Aqui, são tratadas questões relacionadas à monitoração da aplicação.

- [Capítulo 11: Ferramental de IA](./capitulo-11/index.md)
    - Este capítulo demonstra as ferramentas de IA disponíveis no OCI e como a funcionalidade de "chat" da aplicação utiliza esses serviços.

- [Apêndice A: OCI HOWTOs](./apendice-a/index.md)
    - Este apêndice contém HOWTOs (guias práticos) sobre temas variados e úteis que não se encaixaram na abordagem linear proposta pelo livro, todos relacionados ao OCI.

Para críticas, sugestões ou reportar qualquer erro, seja um link "quebrado" ou mesmo um simples erro ortográfico, entre em contato comigo pelo e-mail: <a href="darmbrust@gmail.com">darmbrust@gmail.com</a>

Direitos autorais reservados. Versão para uso pessoal. 