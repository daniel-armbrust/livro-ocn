---
hide:
  - toc
---

# Capítulo 8: CaaS e FaaS

# 8.5 Conclusão

Neste capítulo, abordamos a importância dos contêineres, o processo de construção de uma imagem de contêiner e como enviá-la para o serviço _OCIR_. 

Também exploramos as funcionalidades e características do _OCI Functions_, uma plataforma _serverless_ no qual é possibilida a execução de código em contêineres. Além das funcionalidades e características, foi exporado algumas particularidades que devem ser consideradas ao projetar funções, como o tempo de _"cold start"_, o tempo máximo de vida do contêiner e a alocação de memória. Todos esses detalhes devem ser levados conta ao se projetar funções, visto que uma função é destinada para execução de uma única tarefa.