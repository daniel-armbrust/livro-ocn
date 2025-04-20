---
hide:
  - toc
---

# Capítulo 3: Aplicação OCI PIZZA

Após a análise dos requisitos, é hora de converter essas informações em código, ou seja, em instruções que o computador possa executar. Essa fase é conhecida como codificação e, no contexto de aplicações web, é geralmente dividida em duas partes:  a _codificação do frontend_ e a _codificação do backend_.

O frontend, frequentemente chamado de _"client side"_, refere-se à interface gráfica que atua como o principal ponto de interação do usuário. Em outras palavras, é a parte da aplicação que o usuário visualiza e com a qual interage, sendo desenvolvida com as tecnologias _HTML_, _CSS_ e _JavaScript_. É importante destacar que os navegadores _(web browsers)_ são responsáveis pela renderização das páginas da web, que são compostas por marcações HTML, estilizadas com CSS e se tornam interativas por meio do JavaScript.

Iniciarei com uma descrição básica do desenvolvimento do frontend, seguida pela explicação do desenvolvimento do backend da aplicação **OCI PIZZA**.

# 3.1 Frontend com Bootstrap e React

Frameworks e bibliotecas podem ser usadas para facilitar e auxiliar no desenvolvimento do frontend e no caso do frontend da aplicação **OCI PIZZA**, será utilizado o framework _[Bootstrap](https://getbootstrap.com/)_ e a biblioteca JavaScript _[React](https://react.dev/)_ para desenvolver a interface do usuário.

- **[Bootstrap](https://getbootstrap.com/)**
    - Bootstrap é um framework de código aberto criado inicialmente por desenvolvedores do Twitter que facilita o desenvolvimento de sites e aplicações web responsivas e móveis.

- **[React](https://react.dev/)**
    - React é uma biblioteca JavaScript de código aberto desenvolvida e mantida pelo Facebook para a construção de interfaces de usuário especialmente para aplicações web de página única conhecidas pela sigla _SPA (Single Page Application)_.

O _[Bootstrap](https://getbootstrap.com/)_ fornece uma série de componentes HTML responsivos e estilos predefinidos prontos para uso que serão usados para a construção do _layout_ das páginas da aplicação. Já o _[React](https://react.dev/)_, será usado para construir toda a estrutura de navegação do site, gerenciar a interação com as APIs do backend e atualizar o frontend com os dados recebidos do servidor.

## 3.1.2 Layout da Aplicação

O _layout_ básico da aplicação **OCI PIZZA** é organizado tendo um _menu de navegação no topo (navbar)_, o _logotipo_, uma _seção central_ que muda o seu conteúdo de acordo com a página da aplicação que está sendo acessada, um _rodapé (footer)_ e um botão para acessar um _assistente digital_ que tem como finalidade ajudar o usuário a realizar consultas e obter informações sobre pizzas e pedidos.

![alt_text](./img/ocipizza-page-layout-1.png "OCI PIZZA - Layout #1")
<br>

Dessa forma, a seção central da _página principal (index.html)_ exibe o cardápio da pizzaria, que inclui todos os sabores de pizzas disponíveis:

![alt_text](./img/ocipizza-page-layout-2.png "OCI PIZZA - Layout #2")
<br>

A página de _Novo Usuário (newuser.html)_, exibe um formulário destinado ao cadastro de novos usuários:

![alt_text](./img/ocipizza-page-layout-3.png "OCI PIZZA - Layout #3")
<br>

A página de _Login (login.html)_ exibe um formulário onde usuários já cadastrados podem inserir suas credenciais de acesso para realizar um pedido:

![alt_text](./img/ocipizza-page-layout-4.png "OCI PIZZA - Layout #4")
<br>

Assim, pode-se afirmar que as páginas da aplicação compartilham a mesma estrutura, sendo que somente a _seção central_ muda conforme a página muda.

### **Bootstrap**

## 3.1.3 Pensando como um desenvolvedor React

Uma aplicação web é composta por diversas páginas HTML, cada uma contendo elementos visuais que colaboram para oferecer uma experiência interativa e funcional ao usuário. Estruturar a aplicação em múltiplas páginas facilita a organização do conteúdo, permitindo que cada página tenha um propósito específico, como a página de login, a página do cardápio de pizzas, a página para adicionar um novo usuário, entre outras.

Com base na estrutura da aplicação **OCI PIZZA** apresentada, é possível identificar alguns **_elementos visuais_** que se repetem em todas as páginas. Entre esses elementos, destacam-se o _menu de navegação no topo (navbar)_, o _logotipo_, o _rodapé (footer)_ e o botão para acessar o _assistente digital_.

No mundo _[React](https://react.dev)_, esses elementos visuais independentes são conhecidos como **_componentes_** e são a essência de qualquer aplicação _[React](https://react.dev)_. 

Por enquanto, sem entrar em detalhes, um componente _[React](https://react.dev)_ é uma função JavaScript que pode receber dados, encapsula sua própria lógica e aparência, e, por fim, retorna um elemento HTML. Ele pode representar desde uma página inteira até um simples botão e, o mais importante, deve ser projetado para ser **_reutilizável_**. Quanto maior a abstração do seu componente, maior será sua capacidade de reutilização.

!!! note "NOTA"
    A abordagem de desenvolvimento que consiste em dividir a interface gráfica em partes menores, projetadas para serem reutilizáveis em diferentes páginas da aplicação, é conhecida pela sigla _[DRY (Don't repeat yourself - Não repita a si mesmo)](https://pt.wikipedia.org/wiki/Don%27t_repeat_yourself)_.

Por exemplo, o elemento visual que representa o _menu de navegação no topo (navbar)_ é exibido em todas as páginas da aplicação. Com isso, é possível criar um componente _[React](https://react.dev)_ que pode ser reutilizado em todas as páginas, eliminando a necessidade de repetir o mesmo HTML em cada uma delas. Isso não significa que o elemento HTML do menu não esteja presente em todas as páginas; na verdade, em _[React](https://react.dev)_, você escreve o componente uma única vez e o referencia nas páginas que quiser, promovendo assim a reutilização.

A proposta é criar componentes sempre que você identificar um _"padrão de repetição"_, ou seja, elementos visuais iguais que aparecem em diferentes páginas. Com isso em mente, podemos inicialmente identificar e nomear os seguintes componentes da aplicação **OCI PIZZA**, destacados em azul no desenho abaixo:

![alt_text](./img/ocipizza-react-component-1.png "OCI PIZZA - Componentes React #1")
<br>

Outra forma de identificar componentes em uma aplicação web é consultar a página de documentação do _[Bootstrap](https://getbootstrap.com/docs/5.3/getting-started/introduction/)_, disponível neste _[link aqui](https://getbootstrap.com/docs/5.3/getting-started/introduction/)_.

![alt_text](./img/componentes-bootstrap-1.png "Bootstrap - Componentes #1")
<br>

### **E por que toda essa explicação sobre o React?**

Lembre-se de que o objetivo do livro é conhecer os serviços do OCI para possibilitar você a implantar (deploy) e gerenciar aplicações _[Cloud Native](../capitulo-1/cloud-native.md)_. Uma das características desse tipo de aplicação é que elas fazem uso de _APIs REST (são API-First)_ para a troca de informações.

Isso nos leva a um outro conceito importante no desenvolvimento de aplicações _[Cloud Native](../capitulo-1/cloud-native.md)_: o frontend é _desacoplado_ do backend. 

!!! note "NOTA"
    Para fins de informação, a definição da palavra _"desacoplado"_ refere-se à condição que dois ou mais elementos, sistemas ou componentes funcionem de maneira independente, de modo que uma alteração ou falha em um deles não afete diretamente o outro.

Isso significa que, como uma boa prática, o frontend web deve operar de maneira independente do backend. Uma das vantagens dessa abordagem é a possibilidade de separar o desenvolvimento frontend, criando páginas web com _[React](https://react.dev)_ e uma aplicação móvel nativa para _[Android](https://pt.wikipedia.org/wiki/Android)_ desenvolvida em _[Java](https://www.java.com/en/)_ ou _[Kotlin](https://kotlinlang.org/)_, por exemplo, ambas utilizando o mesmo backend.

!!! note "NOTA"
    Para o desenvolvimento de aplicativos móveis, também é possível utilizar o framework _[React Native](https://reactnative.dev/)_.

## 3.1.4 Desenvolvimento React

### **Node.js**

Para desenvolver uma aplicação _[React](https://react.dev)_, é necessário primeiro instalar o _[Node.js](https://nodejs.org/en)_, que é um ambiente de execução JavaScript (runtime) que possibilita a execução de código JavaScript fora do navegador.

!!! note "NOTA"
    O processo de instalação do _[Node.js](https://nodejs.org/en)_ é bastante simples e não será detalhado aqui. Instruções específicas para cada sistema operacional podem ser encontradas diretamente na página do _[Node.js](https://nodejs.org/en/download)_ através deste _[link](https://nodejs.org/en/download)_.

A versão do _[Node.js](https://nodejs.org/en)_ utilizada no livro pode ser conferida abaixo:

```bash linenums="1"
$ node -v
v22.14.0
```

### **Create React App (create-react-app)**

O _[Create React App](https://create-react-app.dev/)_ é uma ferramenta que simplifica o processo de configuração e inicialização de projetos React. Ideal para iniciantes, ela permite que os desenvolvedores se concentrem na construção de seus componentes, sem se preocupar com a configuração do ambiente. Com o _[Create React App](https://create-react-app.dev/)_, é possível iniciar rapidamente novos projetos, fornecendo uma estrutura de arquivos e diretórios que organiza a aplicação e simplifica o processo de desenvolvimento.

Para o frontend da aplicação **OCI PIZZA**, utilizaremos o _[Create React App](https://create-react-app.dev/)_ para inicializar e criar toda a estrutura de arquivos e diretórios da aplicação _[React](https://react.dev)_ no diretório _"frontend/"_, conforme exibido abaixo:

```bash linenums="1"
$ npx create-react-app frontend
```

Após alguns minutos temos a seguinte estrutura de diretórios que foram criadas pelo _[Create React App](https://create-react-app.dev/)_:

```bash linenums="1"
$ tree -d -L 1 frontend/
frontend/
├── node_modules
├── public
└── src

3 directories
```

- **node_modules/**
    - O diretório _"node\_modules/"_ armazena todas as dependências e pacotes instalados para um projeto _[Node.js](https://nodejs.org/en)_, incluindo suas dependências.

- **public/**
    - Contém arquivos estáticos que são servidos diretamente pelo servidor, incluindo o arquivo _index.html_, que é o ponto de entrada da aplicação.

- **src/**
    - O diretório _"src/"_ em um projeto _[React](https://react.dev)_ contém o código-fonte da aplicação, incluindo componentes, estilos CSS e outros arquivos JavaScript que compõem a lógica e a interface do usuário. 

O diretório _"node\_modules/"_ possui uma extensa estrutura de arquivos e subdiretórios, pois contém todas as dependências do projeto. Abaixo, utilizaremos a opção _-I_ do comando _tree_ para ocultar a exibição do diretório _"node\_modules/"_ e assim obter uma visão mais enxuta de como o _[Create React App](https://create-react-app.dev/)_ organizou a aplicação:

```bash linenums="1"
$ tree -I "node_modules" frontend/
frontend/
├── README.md
├── package-lock.json
├── package.json
├── public
│   ├── favicon.ico
│   ├── index.html
│   ├── logo192.png
│   ├── logo512.png
│   ├── manifest.json
│   └── robots.txt
└── src
    ├── App.css
    ├── App.js
    ├── App.test.js
    ├── index.css
    ├── index.js
    ├── logo.svg
    ├── reportWebVitals.js
    └── setupTests.js

2 directories, 17 files
```

### **Dependências Complementares**

O frontend da aplicação **OCI PIZZA** requer a instalação de outros pacotes, que podem ser instalados com o comando abaixo:

```bash linenums="1"
$ npm install react-router-dom@latest
```

- **react-router-dom**

### **npm start**

Utiliza-se o comando _"npm start"_ dentro do diretório _"frontend/"_ para iniciar o ambiente de desenvolvimento da aplicação _[React](https://react.dev)_:

```bash linenums="1"
$ npm start
```

Após a conclusão da inicialização, você pode acessar a aplicação pelo endereço: _http://localhost:3000/_

De forma simplificada, as etapas de inicialização de uma aplicação _[React](https://react.dev)_ seguem o seguinte fluxo:


### **Criando um Componente**

Antes de criar um componente, vamos criar dois diretórios dentro do diretório _"src/"_ para organizar melhor os componentes e as páginas que farão parte da aplicação.

```bash linenums="1"
$ mkdir src/componentes
$ mkdir src/pages
```