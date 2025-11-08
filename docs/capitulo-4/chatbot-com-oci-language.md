---
hide:
  - toc
---

# Capítulo 4: Serviços Auxiliares e Persistência de Dados

# 4.3 Chatbot com OCI Language

## 4.3.1 O que é um Chatbot?

Um **Chatbot**, também conhecido como **Assistente Virtual Inteligente (AVI)**, é um programa de computador projetado para interagir e auxiliar os clientes de uma empresa. Ele é desenvolvido para interpretar a linguagem natural, possibilitando simular uma conversa humana com os usuários por meio de interfaces de chat. Essas interfaces podem ser integradas de diversas maneiras, como em páginas da web, assistentes de voz como a Amazon Alexa, ou em aplicativos de mensagens, incluindo WhatsApp, Telegram, Facebook ou Instagram Messenger.

Uma vez que o chatbot pode interpretar e _"entender"_ linguagem natural, ou seja, a linguagem que os humanos utilizam no dia a dia, ele pode ser programado, por exemplo, para realizar ações como fornecer informações sobre produtos e serviços e manter diálogos complexos com os usuários.

No caso da aplicação **OCI PIZZA**, o chatbot tem a função de auxiliar os clientes da pizzaria em diversas questões, como:

- Fazer pedidos de pizza
- Verificar o andamento de um pedido já realizado
- Cancelar um pedido
- Consultar o cardápio e preços
- Verificar a viabilidade de entrega no endereço solicitado

Para compreender melhor o funcionamento de um chatbot, seus conceitos e como ele pode ser desenvolvido, é necessário entender como as máquinas interpretam palavras, frases e expressões por meio do **Processamento de Linguagem Natural**, tema que será abordado a seguir.

## 4.3.2 Processamento de Linguagem Natural (PLN)

Um computador é uma máquina projetada para processar números, o que significa que ele não consegue interpretar ou processar letras, palavras ou textos nativamente. Em outras palavras, o computador não consegue, por conta própria, compreender a linguagem humana.

Por exemplo, como fazer com que o computador compreenda a ação presente em uma frase que solicita a entrega de uma pizza para um determinado endereço?

![alt_text](./img/nlp-frase-1.png "NLP Frase #1")

No contexto de uma pizzaria, é possível desenvolver um código que verifique que qualquer texto que siga as palavras "Rua" ou "Avenida", tem alta probabilidade de indicar uma solicitação para entrega de pizza em um endereço específico. 

Dessa forma, conseguimos reduzir a ambiguidade e os limites de interpretação, considerando que a palavra "Aparecida" faz referência exclusiva a uma "Rua" ou "Avenida", e não a uma cidade ou a um verbo.

```python linenums="1"
#!/usr/bin/env python3

import re

def verifica_entrega(localidade: str):
    print('Localidade Encontrada!')

frase = 'É possível entregar uma pizza grande na Rua Aparecida n123?'

# Retorna a string rua ou avenida, se presentes na frase.
palavra_chave = ', '.join(re.findall(r'\b(rua|avenida)\b', frase, re.IGNORECASE)).lower()

if palavra_chave:
    # Encontra a posição numérica da palavra chave na frase (rua ou avenida).
    posicao = frase.lower().index(palavra_chave)

    # Extrai o texto após a palavra chave. O resultado será "Rua Aparecida n123?".
    texto_apos_palvra_chave = frase[posicao + len(palavra_chave):].strip()

    # Remove todos os caracteres especiais. O resultado será "Rua Aparecida n123".
    localidade = re.sub(r'[^\w\s]', '', texto_apos_palvra_chave)

    # Chama uma função para verificar se é possível entregar uma pizza
    # no endereço solicitado.
    verifica_entrega(localidade)

else:
    print('Desculpe, não consegui entender ou não é possível entregar no endereço solicitado.')
```

Os primeiros chatbots eram capazes de fornecer respostas para prompts específicos. Foram programados de maneira semelhante, baseando-se na extração de palavras-chave dos textos para verificar se havia uma resposta ou ação pré-programada.

!!! note "NOTA"
    <a href="https://github.com/wadetb/eliza" target="_blank">ELIZA</a> foi um dos primeiros chatbots, desenvolvido na década de 1960, projetado para simular uma conversa entre uma pessoa e seu terapeuta. Seu funcionamento baseava-se em uma simples árvore de decisão `if...else`, onde o programa extraía palavras-chave do texto de entrada do usuário e consultava um arquivo de respostas pré-definidas para determinar a resposta a ser retornada. Você pode conferir a implementação em Python do chatbot <a href="https://github.com/wadetb/eliza" target="_blank">ELIZA</a> no seguinte link: <a href="https://github.com/wadetb/eliza" target="_blank">https://github.com/wadetb/eliza</a>

No entanto, com o tempo, novas possibilidades de diálogo surgem, exigindo mais código e estruturas `if...else` para executar ações de correspondência. Com mais código, aumentam as chances de bugs e, ao interpretar a linguagem humana, a probabilidade de erros de interpretação também cresce. 

Determinar o número de palavras utilizadas na linguagem natural é uma tarefa quase impossível. O vocabulário da linguagem natural cresce constantemente a cada ano e, por exemplo, difere de uma linguagem de programação, onde existe um conjunto fixo de palavras reservadas que são usadas para especificar ações exatas (`if`, `then`, `else`, `elif`, `except`, `while`, `continue`, `def`, `class`, entre outras).

Na linguagem humana, por outro lado, as palavras podem ter múltiplos significados (duplo sentido), especialmente quando escritas em frases diferentes. Para compreender o significado de uma frase, é necessário analisar o contexto como um todo, e não apenas palavra por palavra. Tentar processar cada palavra individualmente pode não fazer sentido e pode levar a erros de interpretação.

Nesse cenário, imagine desenvolver um chatbot que possa interpretar contextos mais amplos, além do ambiente de uma pizzaria. Nesse caso, a palavra "Aparecida", do exemplo anterior, pode ter diversos significados, como:

1. Nome próprio feminino comum no Brasil.
2. Pode se referir a uma localidade, como a cidade de Aparecida do Norte.
3. Nossa Senhora Aparecida padroeira do Brasil.
4. Verbo "aparecer", significando que algo ou alguém tornou-se visível. 

Não se programam regras gramaticais. Em vez disso, são desenvolvidos modelos estatísticos que permitem identificar as probabilidades entre as palavras de um texto. Isso torna o processo muito mais assertivo ao programar algo capaz de "entender" e "responder" em linguagem humana, sem recorrer a um monte de `if...else`.

!!! note "NOTA"
    Outro exemplo é o funcionamento de programas de tradução, como o Google Translate. Estes sistemas não traduzem palavra por palavra e se fosse o caso, muitas vezes o resultado das frases traduzidas não faria sentido. A análise contextual é essencial para realizar traduções precisas entre diferentes línguas.

Para superar as limitações que levam a erros de interpretação ao processar a linguagem humana, é necessário converter esses textos em representações numéricas por meio de um conjunto de técnicas conhecidas como **Processamento de Linguagem Natural**.

**Processamento de Linguagem Natural (PLN)**, ou em inglês, **Natural Language Processing (NLP)**, é uma subárea da **Inteligência Artificial (IA)** voltada para o processamento e análise de dados em linguagem natural.

Aplicações que utilizam técnicas de **Processamento de Linguagem Natural** podem "entender" sentenças faladas e escritas por humanos, ou seja, em linguagem natural. Elas são capazes de gerar respostas úteis e manter diálogos complexos.

A seguir, examinaremos como o serviço **OCI Language** pode ajudar nas questões que envolvem o **Processamento de Linguagem Natural**.

## 4.3.3 Introdução ao OCI Language

Language é um serviço de **Processamento de Linguagem Natural (NLP)** oferecido pelo OCI no qual permite os desenvolvedores processar, analisar e extrair informações importantes a patir de textos não estruturados.

O OCI Language disponibiliza, através de sua API REST, as seguintes funcionalidades para o processamento de textos:

- <a href="https://docs.oracle.com/pt-br/iaas/Content/language/using/lang-detect.htm" target="_blank"><b>Detecção de Idioma</b></a>
    - Identifica o idioma do texto fornecido, apresentando uma pontuação de confiança associada.

- <a href="https://docs.oracle.com/pt-br/iaas/Content/language/using/text-class.htm" target="_blank"><b>Classificação de Texto</b></a>
    - Determina a categoria e subcategoria à qual o texto pertence.

- <a href="https://docs.oracle.com/pt-br/iaas/Content/language/using/ner.htm" target="_blank"><b>Reconhecimento de Entidade Nomeada</b></a>
    - Identifica nomes de pessoas, lugares, organizações e outras entidades relevantes.

- <a href="https://docs.oracle.com/pt-br/iaas/Content/language/using/key_ref.htm" target="_blank"><b>Extração de Palavras-Chave</b></a>
    - Extrai um conjunto significativo de frases de um bloco de texto.

- <a href="https://docs.oracle.com/pt-br/iaas/Content/language/using/sentment.htm" target="_blank"><b>Análise de Sentimentos</b></a>
    - Classifica o texto como positivo, negativo ou neutro.

- <a href="https://docs.oracle.com/pt-br/iaas/Content/language/using/translate-text.htm" target="_blank"><b>Tradução de Texto</b></a>
    - Traduz o texto para o idioma desejado.

- <a href="https://docs.oracle.com/pt-br/iaas/Content/language/using/pii.htm" target="_blank"><b>Informações de Identificação Pessoal</b></a>
    - Identifica, classifica e anonimiza informações sensíveis em textos.

O chatbot da aplicação **OCI PIZZA** utiliza as funcionalidades de **Classificação de Texto** para identificar a intenção do usuário e **Reconhecimento de Entidade Nomeada** para extrair nomes de pessoas, lugares e endereços.

No entanto, para que o chatbot possa processar o diálogo dos usuários, é necessário antes preparar o serviço. Isso significa que, para reconhecer as intenções específicas dos usuários do chatbot que estão relacionadas ao domínio de negócios da pizzaria, o OCI Language precisa de treinamento.

!!! note "NOTA"
    Na realidade, são os modelos estatísticos do OCI Language que precisam de treinamento, e não o OCI Language em si. O OCI Language é o serviço que oferece funcionalidades para processar e extrair informações úteis dos textos a partir de modelos pré-treinados ou treinados por você.

### <a href="https://docs.oracle.com/pt-br/iaas/Content/language/using/projects.htm" target="_blank"><b>Projeto</b></a>

Qualquer processamento de texto que será realizado pelo OCI Language depende da criação de um projeto, que serve essencialmente como um meio para organizar as tarefas relacionadas ao **Processamento de Linguagem Natural**.

Para a aplicação **OCI PIZZA**, será criado um projeto com o nome `chatbot-project` nas regiões `sa-saopaulo-1` e `sa-vinhedo-1`, no [compartimento](../capitulo-3/iam-limites-cotas-e-audit.md#compartimentos) `cmp-appl` do ambiente de produção `cmp-prd`. 

Para criar o projeto, utilize o seguinte comando:

```bash linenums="1"
$ oci ai language project create \
> --region "sa-saopaulo-1" \
> --compartment-id "ocid1.compartment.oc1..aaaaaaaaaaaaaaaabbbbbbbbccc" \
> --display-name "chatbot-project" \
> --description "Projeto OCI Language para Chatbot da região \"sa-saopaulo-1\"." \
> --wait-for-state "SUCCEEDED"
```

### **Dados de Treinamento**

Algo que o OCI Language não faz sozinho é identificar qual é a intenção do usuário. No contexto do chatbot, essa é uma das tarefas mais primordiais que ele deve desempenhar.

O termo "intenção" é frequentemente utilizado no contexto de chatbots para descrever o processo de identificar, a partir de uma sentença ou frase, o que um usuário deseja. Uma vez que a intenção foi corretamente identificada, o chatbot pode executar determinadas ações, como, por exemplo, invocar uma função que consulta um banco de dados para fornecer uma resposta.

Para que o OCI Language possa identificar a intenção do usuário, é necessário treiná-lo com um conjunto de dados (dataset) denominado **Dados de Treinamento**.

No diretório <a href="https://github.com/daniel-armbrust/ocn-ocipizza/tree/main/scripts/capitulo-4/data" target="_blank">"scripts/capitulo-4/data"</a> do <a href="https://github.com/daniel-armbrust/ocn-ocipizza" target="_blank">repositório de códigos</a> da aplicação **OCI PIZZA**, existem alguns arquivos que contêm dados que serão utilizados no processo de treinamento para as funções de **Classificação de Texto** e **Reconhecimento de Entidade Nomeada**.

Esses arquivos são:

- <a href="https://github.com/daniel-armbrust/ocn-ocipizza/tree/main/scripts/capitulo-4/data/chatbot-train-intents.csv" target="_blank"><b>chatbot-train-intents.csv</b></a>
    - Arquivo que contém exemplos de declarações utilizados para a função de **Classificação de Texto**.

- <a href="https://github.com/daniel-armbrust/ocn-ocipizza/tree/main/scripts/capitulo-4/data/chatbot-test-intents.csv" target="_blank"><b>chatbot-test-intents.csv</b></a>
    - Arquivo que contém exemplos de declarações utilizados para testar a função de **Classificação de Texto**.

- <a href="https://github.com/daniel-armbrust/ocn-ocipizza/tree/main/scripts/capitulo-4/data/chatbot-ner.json" target="_blank"><b>chatbot-ner.json</b></a>
    - Arquivo que contém informações utilizadas para a função de **Reconhecimento de Entidade Nomeada**.

### **Classificação de Texto**

Os dados de treinamento para as tarefas de **Classificação de Texto** consistem em declarações de exemplo que representam interações típicas de usuários da pizzaria (`text`), acompanhadas de uma string ou mais strings que o OCI Language utiliza para identificar a intenção correspondente a cada declaração (`labels`).

Com isso, você deve agrupar um conjunto de declarações em um arquivo que deve seguir o seguinte formato:

![alt_text](./img/text-classification-1.png "Classificação de Texto #1")

No caso da aplicação **OCI PIZZA**, o arquivo que contém as declarações para **Classificação de Texto** apresenta o seguinte conteúdo:

```bash linenums="1"
$ head -5 capitulo-4/data/chatbot-train-intents.csv
text,labels
"Errei o pedido, cancela por favor",cancelar_pedido
Gostaria de pedir uma pizza grande muçarela por favor,fazer_pedido
"Boa noite, obrigado",despedida
"Olá, gostaria de fazer um pedido",ver_cardapio
```

Alguns detalhes que devem ser levados em consideração ao criar um arquivo para **Classificação de Texto** que são:

- `text,labels`
    - É obrigatório que a primeira linha do arquivo contenha as palavras `text` e `labels`, separadas por vírgula. Caso contrário, o processo de treinamento falhará.

- `text`
    - O texto das declarações é de livre escolha e pode incluir letras maiúsculas, minúsculas, acentos e caracteres especiais. Como regra geral, se a declaração contiver uma vírgula, ela deve ser colocada entre aspas duplas (`"texto com vírgula"`), caso contrário, o processo de treinamento falhará.

- `labels`
    - String que identifica a intenção com base na declaração contida na coluna `text`. O identificador de intenção pode ser multilabel e deve seguir o formato `label_1|label_2|...`.

