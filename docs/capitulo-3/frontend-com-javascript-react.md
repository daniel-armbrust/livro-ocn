---
hide:
  - toc
---

# Capítulo 3: Aplicação **OCI PIZZA**

Após a análise dos requisitos, é hora de converter essas informações em código, ou seja, em instruções que o computador possa executar. Essa fase é conhecida como codificação e, no contexto de aplicações web, é geralmente dividida em duas partes:  a _codificação do frontend_ e a _codificação do backend_.

O frontend, também conhecido como _"client side"_, é a interface gráfica que serve como o principal ponto de interação do usuário. Ou seja, é a parte da aplicação que o usuário vê e interage, sendo desenvolvido com as tecnologias _HTML_, _CSS_ e _JavaScript_.

Por outro lado, o backend, também conhecido como _"server side"_, é responsável pelo processamento dos dados da aplicação através das suas regras de negócios (ou lógica de negócios). É no backend que são tratadas questões relacionadas à autenticação de usuários e à comunicação com o banco de dados.

Iniciarei com uma descrição básica do desenvolvimento do frontend, seguida pela explicação do desenvolvimento do backend da aplicação **OCI PIZZA**.

# 3.1 Desenvolvimento Frontend e Backend

## 3.1.1 Desenvolvimento Frontend com Bootstrap e React

Frameworks e bibliotecas podem ser usadas para facilitar e auxiliar no desenvolvimento do frontend e no caso do frontend da aplicação **OCI PIZZA**, será utilizado o framework _[Bootstrap](https://getbootstrap.com/)_ e a biblioteca JavaScript _[React](https://react.dev/)_ para desenvolver a interface do usuário.

- **[Bootstrap](https://getbootstrap.com/)**
    - Bootstrap é um framework de código aberto criado inicialmente por desenvolvedores do Twitter que facilita o desenvolvimento de sites e aplicações web responsivas e móveis.

- **[React](https://react.dev/)**
    - React é uma biblioteca JavaScript de código aberto desenvolvida e mantida pelo Facebook para a construção de interfaces de usuário especialmente para aplicações web de página única conhecidas pela sigla _SPA (Single Page Application)_.

O _[Bootstrap](https://getbootstrap.com/)_ fornece uma série de componentes HTML responsivos e estilos predefinidos prontos para uso que serão usados para a construção do _layout_ das páginas da aplicação. Já o _[React](https://react.dev/)_, será usado para construir toda a estrutura de navegação do site, gerenciar a interação com as APIs do backend e atualizar o frontend com os dados recebidos do servidor.

### **Layout da Aplicação**

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

### **Pensando como um Desenvolvedor React**

Uma aplicação web é composta por diversas páginas HTML, cada uma contendo elementos visuais que colaboram para oferecer uma experiência interativa e funcional ao usuário. Estruturar a aplicação em múltiplas páginas facilita a organização do conteúdo, permitindo que cada página tenha um propósito específico, como a página de login, a página do cardápio de pizzas, a página para adicionar um novo usuário, entre outras.

Com base na estrutura da aplicação **OCI PIZZA** apresentada, é possível identificar alguns **_elementos visuais_** que se repetem em todas as páginas. Entre esses elementos, destacam-se o _menu de navegação no topo (navbar)_, o _logotipo_, o _rodapé (footer)_ e o botão para acessar o _assistente digital_.

No mundo _[React](https://react.dev)_, esses elementos visuais são conhecidos como **_componentes_** e são a essência de qualquer aplicação _[React](https://react.dev)_. Cada componente possui sua própria lógica e aparência, e, o mais importante, são projetados para serem **_reutilizáveis_**.

Por exemplo, o elemento visual que representa o _menu de navegação no topo (navbar)_ é exibido em todas as páginas da aplicação. Com isso, é possível criar um componente _[React](https://react.dev)_ que pode ser reutilizado em todas as páginas, eliminando a necessidade de repetir o mesmo HTML em cada uma delas. Isso não significa que o elemento HTML do menu não esteja presente em todas as páginas; na verdade, em  _[React](https://react.dev)_, você escreve o componente uma única vez e o referencia nas páginas desejadas, promovendo assim a reutilização do componente.

A proposta é criar componentes sempre que você identificar um "padrão de repetição", ou seja, elementos que aparecem em diferentes páginas. Com isso em mente, podemos inicialmente identificar e nomear os seguintes componentes da aplicação, destacados em azul no desenho abaixo:

![alt_text](./img/ocipizza-react-component-1.png "OCI PIZZA - Componentes React #1")
<br>