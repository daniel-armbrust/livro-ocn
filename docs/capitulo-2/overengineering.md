---
hide:
  - toc
---

# Capítulo 2: Aplicação OCI PIZZA

# 2.1 Overengineering

Decidi abordar o tema sobre <a href="https://en.wikipedia.org/wiki/Overengineering" target="_blank">Overengineering</a> logo no início do capítulo, pois é importante esclarecer que parte do que será apresentado ao longo do livro é, de fato, um exemplo de <a href="https://en.wikipedia.org/wiki/Overengineering" target="_blank">Overengineering</a>.

<a href="https://en.wikipedia.org/wiki/Overengineering" target="_blank">Overengineering</a> é um termo utilizado para descrever a prática de criar um produto ou sistema com mais complexidade ou recursos do que o necessário, muitas vezes resultando em desperdício de tempo e dinheiro. 

Ao longo dos capítulos deste livro, o <a href="https://en.wikipedia.org/wiki/Overengineering" target="_blank">Overengineering</a> se tornará mais evidente, especialmente ao abordarmos a transição da <a href="https://pt.wikipedia.org/wiki/Aplica%C3%A7%C3%A3o_monol%C3%ADtica" target="_blank">Arquitetura Monolítica</a> para uma <a href="https://pt.wikipedia.org/wiki/Microsservi%C3%A7o" target="_blank">Arquitetura de Microsserviços</a>. Em uma aplicação real e simples como a **OCI PIZZA**, uma <a href="https://pt.wikipedia.org/wiki/Aplica%C3%A7%C3%A3o_monol%C3%ADtica" target="_blank">Arquitetura Monolítica</a> é, de fato, a melhor escolha.

Por fim, é importante lembrar que o objetivo deste livro é explorar as práticas e os conceitos relacionados ao termo <a href="https://ocn.dev.br/capitulo-1/cloud-native/">Cloud Native</a>, utilizando uma aplicação real como exemplo, além de demonstrar como utilizar os serviços em nuvem oferecidos pelo <a href="https://ocn.dev.br/capitulo-3/">OCI</a>. Assim, em determinados momentos, abordaremos soluções mais complexas e que não são necessárias para o problema que a aplicação **OCI PIZZA** busca resolver, mas que ajudam a ilustrar algumas práticas na implementação de aplicações <a href="https://ocn.dev.br/capitulo-1/cloud-native/">Cloud Native</a> no <a href="https://ocn.dev.br/capitulo-3/">OCI</a>.

A dica que fica é: para uma aplicação do mundo real, é importante mantê-la o mais simples possível.

<h3 style="text-align: center; font-style: italic;">
Keep It Simple, Stupid (KISS)
</h3>