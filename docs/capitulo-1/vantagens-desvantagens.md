# Capítulo 1: Introdução a Computação em Nuvem

# 1.5 Vantagens e Desvantagens da Computação em Nuvem

A seguir, apresento algumas vantagens e desvantagens da utilização da Computação em Nuvem.

## 1.5.1 Vantagens

A computação em nuvem oferece uma variedade de benefícios para as organizações. Na verdade, são tantos os benefícios que se torna quase impossível não considerar a mudança das operações comerciais para uma plataforma baseada na nuvem.

### Acessível de qualquer lugar e dispositivo

Uma das maiores vantagens da Computação em Nuvem é a possibilidade de acessar dados, aplicações e serviços de qualquer lugar e dispositivo, desde que haja uma conexão com a Internet.

Além disso, a Computação em Nuvem é compatível com uma variedade de dispositivos, como laptops, tablets e smartphones. Isso garante que os usuários possam acessar suas informações de maneira conveniente, seja por meio de um computador no escritório ou de um celular durante um deslocamento.

### Habilitadora de Startups (Agilidade)

Uma _Startup_ é uma empresa em fase inicial, geralmente dedicada ao desenvolvimento de um produto, serviço ou modelo de negócio inovador e escalável. Essas empresas se destacam por sua capacidade de crescer rapidamente, aproveitando tecnologias emergentes e explorando mercados não atendidos ou ambientes de incerteza.

As startups se beneficiam amplamente da Computação em Nuvem, pois geralmente dispõem de recursos financeiros limitados para transformar suas ideias em software. A nuvem oferece suporte a inovações através de solução mais econômica, permitindo que uma startup, sem capital suficiente, evite a necessidade de construir seu próprio data center para desenvolver, testar e lançar seu software ao público.

Além disso, as startups necessitam de agilidade para criar, remover ou expandir recursos computacionais, a fim de atender a novas demandas de negócios ou para modificar completamente sua stack de tecnologia.

É importante destacar que as vantagens mencionadas aqui beneficiam não apenas as startups, mas também empresas maiores e já consolidadas no mercado.

### Resiliência

É fácil e economicamente viável configurar sua aplicação para utilizar múltiplos data centers geograficamente distribuídos em diversas regiões do mundo, com o objetivo de aumentar a resiliência e a disponibilidade das aplicações.

Utilizar diversos data centers para projetar uma arquitetura distribuída significa que os serviços são executados em máquinas localizadas em diferentes regiões geográficas, o que reduz o risco de falhas em um único ponto.

### Escalabilidade

Escalabilidade é a capacidade de um sistema, rede ou processo de aumentar sua capacidade e desempenho de maneira eficiente à medida que a demanda cresce. Um sistema escalável pode acomodar um aumento no volume de dados ou no número de usuários sem comprometer o desempenho.

A Computação em Nuvem proporciona uma infraestrutura flexível que pode ser facilmente dimensionada, permitindo que as organizações ajustem rapidamente seus recursos conforme as necessidades do negócio.

### Custo-benefício

Seja qual for o modelo de serviço de nuvem escolhido _(IaaS, PaaS ou SaaS)_, você paga apenas pelos recursos que realmente usa. Isso ajuda a evitar o disperdício de dinheiro ao superdimensionar recursos computacionais.

A Computação em Nuvem permite que empresas e indivíduos testem, monitorem e ajustem seus recursos computacionais de forma mais precisa antes de realizar investimentos. Com a nuvem, existe o conceito de _"custo variável"_, pois os gastos são baseados no consumo dos recursos utilizados. Além disso, não há custo inicial para a aquisição de hardware.

A economia gerada pelo uso da nuvem tem permitido que as empresas transformem sua tecnologia e abordagem de gerenciamento, tornando-as mais colaborativas, orientadas por resultados e em tempo real.

### Computação Ecológica

A Computação em Nuvem é uma solução mais sustentável em comparação com as abordagens tradicionais de TI. Ao migrar para a nuvem, as empresas podem reduzir seu consumo de energia e a pegada de carbono em até 90%, um conceito frequentemente referido como _"TI verde"_.

"TI verde" refere-se à forma como a tecnologia evolui, se desenvolve e se expande em ambientes empresariais e industriais, minimizando impactos negativos no meio ambiente.

## 1.5.2 Desvantagens

Como em qualquer tecnologia, a Computação em Nuvem apresenta tanto vantagens quanto desvantagens. No entanto, as vantagens geralmente superam as desvantagens. Vale destacar que algumas desvantagens são apenas _"pontos de atenção"_ e não constituem limitações irreversíveis.

### Dependência da Internet

Uma das desvantagens mais comuns da Computação em Nuvem é a dependência de uma conexão à Internet. Uma conexão instável pode dificultar o acesso às informações ou aplicativos necessários.

### Custos Imprevisíveis

É simples criar recursos computacionais ou serviços na nuvem. No entanto, essa facilidade exige atenção para evitar despesas inesperadas que podem comprometer o orçamento. Manter CPUs ligadas e sem uso, por exemplo, pode resultar em custos desnecessários. 

A ideia ao se utiliar a Computação em Nuvem é sempre dimensionar para baixo, criar um recurso com o mínimo aceitável de CPU e memória e, ir expandindo, aumentando, gradativamente. 

!!! note "NOTA"
    Utilizo CPU e memória como exemplos para facilitar a compreensão, mas essa lógica se aplica igualmente a todos os outros serviços disponíveis na nuvem.

No OCI, há ferramentas como o _[Cost Analysis](https://docs.oracle.com/en-us/iaas/Content/Billing/Concepts/costanalysisoverview.htm)_ que tornam a gestão e o monitoramento dos seus custos mais simples e eficazes.

!!! note "NOTA"
    Uma excelente ferramenta é [OCI360 - Oracle Cloud Infrastructure 360º View](https://github.com/dbarj/oci360), que permite visualizar os recursos ativos do seu ambiente no OCI de forma abrangente e intuitiva.

### Complexidade

A Computação em Nuvem não é um conceito novo, mas está em constante evolução, com novos serviços sendo lançados continuamente. Essa complexidade exige atenção, pois os administradores da nuvem precisam se manter atualizados sobre as inovações, a fim de conhecer novos serviços e otimizar os já existentes. Muitos dos problemas que surgem durante a migração para a nuvem são resultado de uma falta de compreensão clara sobre o que os provedores oferecem.

Outra complexidade está relacionada à forma como os recursos são provisionados e modificados. É simples provisionar diferentes tipos de recursos computacionais com apenas alguns _cliques do mouse_. No entanto, à medida que o número de ativos na nuvem aumenta ou que esses ativos são modificados ao longo do tempo, torna-se desafiador manter um controle eficaz sobre eles.

A boa notícia é que a nuvem oferece diversas maneiras de criar e atualizar sua infraestrutura. Uma dessas opções é por meio de ferramentas de _Infraestrutura como Código (IaC - Infrastructure as Code)_. Ao representar sua infraestrutura em código, o gerenciamento se torna mais eficiente e organizado, além de o código servir como uma forma de documentação. No entanto, isso requer que os administradores tenham conhecimentos em programação.

!!! note "NOTA"
    Consulte [Why Infrastructure as Code Matters](https://blogs.oracle.com/ateam/post/why-infrastructure-as-code-matters) para uma visão dos benefícios de utilizar ferramentas de IaC.

### Interação com o Suporte

Um aspecto que considero importante e que merece atenção é a interação com o _[Suporte](https://www.oracle.com/br/support/)_.

Quando há suspeitas de problemas na infraestrutura na nuvem, os administradores geralmente recorrem ao suporte em busca de assistência para resolvê-los. No entanto, é importante destacar que o suporte pode não tem conhecimento sobre o seu ambiente e não sabe sobre problema que você está enfrentando ao utilizar o OCI.

É essencial manter uma comunicação clara e precisa ao explicar em detalhes o problema. Essa comunicação deve ser elaborada de forma detalhada e, se necessário, incluir um diagrama de arquitetura para facilitar a compreensão.

Lembre-se de que um problema relacionado ao design e à criação de uma arquitetura na nuvem, resultante da falta de conhecimento técnico, não deve ser considerado uma questão que exija a intervenção do suporte. Essa abordagem é um problema comum que observo e que frequentemente gera insatisfação entre os usuários da nuvem. A Oracle conta com diversas equipes especializadas que podem ajudar com essas questões arquiteturais, as quais abordaremos mais adiante.