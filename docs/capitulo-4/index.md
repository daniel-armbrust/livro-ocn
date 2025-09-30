---
hide:
  - toc
---

# Capítulo 4: Serviços Auxiliares e Persistência de Dados

<h3 style="text-align: center; font-style: italic;">
"O modo como você se organiza acaba direcionando a arquitetura de seus sistemas, para o bem ou para o mal." - Autor: <a href="https://www.linkedin.com/in/samnewman/" target="_blank">Sam Newman</a>
</h3>

Após a ativação da conta no <a href="https://ocn.dev.br/capitulo-3/">OCI</a>, é o momento de iniciar a criação dos serviços que a aplicação **OCI PIZZA** utilizará. Eu me refiro a esses serviços como **Serviços Auxiliares**, que são todos os recursos externos necessários para o funcionamento da aplicação.

Lembre-se de que a aplicação web desenvolvida é composta por um conjunto de regras de negócios expressas através da linguagem de programação <a href="https://ocn.dev.br/capitulo-2/">Python</a>. Todos os recursos necessários para sua execução são considerados como sendo **Serviços Auxiliares**.

Neste capítulo, iniciaremos a criação de alguns desses serviços dos quais a aplicação **OCI PIZZA** depende. Outros serviços, como o <a href="https://ocn.dev.br/capitulo-6/">OCI Functions</a>, serão discutidos e implementados em capítulos posteriores, pois necessitam de uma estrutura de rede pronta para funcionar, tema este que será abordado no <a href="https://ocn.dev.br/capitulo-5/">Capítulo 5</a>.

Logo após a criação dos **Serviços Auxiliares**, será possível acessá-los por meio de suas APIs pela Internet, permitindo a execução da aplicação **OCI PIZZA** localmente, ainda que de forma parcial. O objetivo é desenvolver e testar a aplicação de maneira já integrada à nuvem, uma vez que a maioria dos serviços oferecidos pelo <a href="https://ocn.dev.br/capitulo-3/">OCI</a> não pode ser emulada localmente.

- [4.1 Object Storage](./object-storage.md)
- [4.2 Persistência de dados com o Oracle NoSQL](./persistencia-de-dados-com-o-oracle-nosql.md)
- [4.3 Registro de Logs com OCI Logging](./registro-de-logs-com-oci-logging.md)   
- [4.4 Chatbot com OCI Language](./chatbot-com-oci-language.md)
- [4.5 Email Delivery](./email-delivery.md)