---
hide:
  - toc
---

# Capítulo 5: Inteligência Artificial (IA)

# 5.1 Introdução à Inteligência Artificial

Big techs tem vários modelos prontos cada um para um uso específico desde respostas gerais ou mais focados em códigos e assuntos específicos.
  - OpenAI: GPT4, Codex
  - Microsoft em conjunto com a Nvidia: Megatron-LM
  - Google: BERT, Minerva
  - Meta: OPT, LLaMA

https://github.com/oobabooga/text-generation-webui

- O tamanho do modelo pode afetar a qualidade das respostas. Quanto menor o modelo, mais simples seriam as respostas.

- Treinar um modelo de IA não é programar regras gramaticais com um monte de if, if, if. Aos invés disso, começamos com um corpo de dados gigante como, todos os artigos da Wikipedia.

- Modelo:
  - A grosso modo, é uma lista de combinações de palavras junto com um número que indica a probabilidade da próxima palavra dada uma palavra anterior. Essas probabilidades é o que chamamos de "pesos".
  - A quantidade de palavras e a probabilidade da próxima palavra, é obtida através de um conjunto de textos ou frases no qual o modelo foi treinado. É a partir dos dados de treinamento que é possível obter, a probabilidade, da próxima palavra.
  - Para completar a próxima palavra o modelo vai usando os "pesos" aprendidos durante o treinamento.
  - Para se obter a próxima palavra, a GPU é usada pois é preciso calcular sempre, com base em todas as frases de treinamento, a próxima palavra.

NLP é um campo de estudo que foca em como fazer os computadores processar linguagem natural humana. A biblioteca NLTK prepara os dados ou pré-processa o texto, ajuda o computador a entender o que são palavras, tokens, gramática do texto, para então, ser possível treinar modelos de IA.

NLP envolve compreender expressões humanas completas até um ponto de ser capaz de dar respostas úteis.

Manipulação e processamento de dados linguísticos. 

Processamento de linguagem: Tagging, Classificação e extração de informação.

NLTK é usado para que seja possível construír programas de NLP em Python.

Fluxo: Texto cru → Limpeza com NLTK → Vetorização → Treinamento com Scikit-learn ou rede neural

NLP tem grande valor em aplicações de inteligência artificial. 
NLP começa com textos não estruturados. A partir de textos não estruturados, precisa-se ter uma forma de estruturar os dados para que o computador entenda a informação e seja capaz de processar.

NLP obtém dados não estruturados de entrada e os converte.

Texto não estruturado:
  - Adicione ovos e leite na minha lista de compras.
Texto estruturado:
  - <shopping-list> 
        <item> ovos </item>
        <item> leite </item>
    </shopping-list>

Estruturar a informação para o computador ser capaz de processar ela. Isso pode ser chamado também de NLU - Natural Language Understanding.
O NLP fica no meio de texto não estruturado para texto estruturado. Ele tem o papel de traduzir entre ambas as formas.

Quais tarefas o NLP é importante?
  - Tradução (Machine Translation). Para traduzir algo é preciso entender o contexto e não tentar traduzir palavra por palavra.
  - Assistentes Virtuais como Alexa ou chatbots. Através do entendimento de declarações humanas, é possível derivar/extraír um comando para ser executado. Fazer um de-para das sentenças humanas ou declarações humanas em uma árvore de decisão para tomar uma ação.
  - Análise de sentimentos. Extraír sentimentos de sentenças (review de um produto que foi comprado). ------> A aplicação OCI PIZZA pode ter uma forma do usuário dizer o que achou da pizza e o NLP pode ser usado para analisar o sentimento.
  - SPAM Detection. 

NLP não é somente um algoritmo e sim, é um conjunto de ferramentas que você usa para ajudar a resolver os casos de uso acima.

Estágios do NLP ou Ferramentas que o NLP disponibiliza para converter um texto não estruturado para um texto estruturado que pode ser usado em aplicações de Inteligência Artificial.
1. Tokenização. Obtém-se uma string e quebra ela em pedaços.
    - A partir da Tokenização é possíver usar ou Steaming ou Lemmatization:
        2. Stemmings. Running, Runs, Ran --> a palavra de stem para as três é run. Normalizar a sentença. Stem não funciona para todas as palavras como é o caso da palavra universidade ou universal.
        3. Lemmatization. A partir do token é possível aprender o significado das palavras através de uma definição de dicionário. Deriva-se o raíz ou o lema da palavra que tem haver com extraír o significado. Better ==> GOOD.
4. Part of Speach Tagging. Procura saber onde o token é usado dentro do contexto de uma sentença. Um verbo dentro de um contexto pode ser um pronome.
5. N.E.R -> Reconhecimento de entidade. A partir de um token, este está associado a alguma entidade? 

NLTK é útil para construír bots que deêm respostas padronizadas.









Quando eu comecei a estudar sobre IA vi que existem vários termos em conjuntos. Para chegamos no entendimento de como um chatgpt funciona, necessitamos entender desde a base, onde os algoritimos de aprendizagem de máquina foram desenvolvidos. Tudo começa no Machine Learning, que é composto de algoritmos possibilitam as "máquinas aprenderem" a partir de grandes quantidades de dados.

- Machine Learning
  - É uma subárea da IA no qual estão presentes os algoritmos que permitem os computadores apreder a partir de dados.
  - É a base para outras subárea da IA incluíndo Deep Learning e NLP.
  - Tudo começa no Machine Learning.
  - É a base que sustenta o Deep Learning.

- Deep Learning
  - É uma subárea de Machine Learning que utiliza Redes Neurais Profundas para resolver problemas complexos.
  - Eficaz sobre grandes quantidades de dados que permite reconhecer imagens e processamente de linguagem natural.
  - É uma técnica avançada dentro do Machine Learning.

- NLP
  - Possibilita os computadores interpretar e gerar texto humanos ou, mais técnicamene dito, em linguagem natural.
  - Uma vez que os textos são interpretados e entendidos, tarefas como tradução, análise de sentimentos e geração de texto humano podem ser feitos.
  - Será que o NLP é uma espécie de acessório que ajuda o Machine Learning e o Deep Learning a interpretarem linguagem humana?
  - NLP são algorítimos?
  - Utiliza o Deep Learning para desenvolver modelos como os LLMs que são projetados para entender linguagem natural.
  - 

- LLMs
  - São especificamente Modelos.
  - São modelos de Deep Learning (treinados por meio de Deep Learning?)
  - treinados em grandes quantidades de dados ttextuais para entender e gerar linguagem natural.
  - Através do treinamento em grandes quantidades de dados, modelos LLMs podem realizar tarefas NLP com precisão.

- Transformer
  - Arquitetura de Deep Learning (Attention is ALL You Need)
  - Mecanismo de atenção usado para entender contextos de uma frase.
  - A paralelização ajuda a entender o contexto de uma frase. Pode-se dizer que entender o contexto através da paralelização significa observar a correlação entre todas as palavras de uma frase para enfim, entender o contexto da frase.

- BERT (Bidirectional Encoder Representations from Transformers) 
  - BERT é um modelo de linguagem (talvez ele represente o formato dos dados salvos em um arquivo) que foi treinado em grandes conjuntos de dados para realizar processamento de linguagem natural.
  - Arquitetura do BERT é transformer.
  - BERT é um algoritmo ou um modo para se treinar usando arquitura transformer?
    - BERT (Bidirectional Encoder Representations from Transformers) é um modelo de linguagem que utiliza a arquitetura Transformer, mas não é um algoritmo em si
  - Modelo de linguagem que utiliza uma arquitetura de rede neural chamada Transformer.
  - Modelo de Linguagem desenvolvido pelo Google.
  - BERT se baseia em princípios de Machine Learning.
  - Usa técnicas de aprendizagem supervisionada e não supervisionada para treinar.
  - Exemplo de Deep Learning.

- Treinamento de Modelo
  - Aprendizagem Supervisionada
  - Aprendizagem Não Supervisionada