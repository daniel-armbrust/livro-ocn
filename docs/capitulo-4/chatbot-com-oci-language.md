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

A seguir, examinaremos como o serviço <a href="https://docs.oracle.com/pt-br/iaas/Content/language/using/home.htm" target="_blank"><b>OCI Language</b></a> pode ajudar nas questões que envolvem o **Processamento de Linguagem Natural**.

## 4.3.3 Introdução ao OCI Language

<a href="https://docs.oracle.com/pt-br/iaas/Content/language/using/home.htm" target="_blank">Language</a> é um serviço de **Processamento de Linguagem Natural (NLP)** oferecido pelo OCI no qual permite os desenvolvedores processar, analisar e extrair informações importantes a partir de textos não estruturados.

!!! note "NOTA"
    O nome oficial do serviço é <a href="https://docs.oracle.com/pt-br/iaas/Content/language/using/home.htm" target="_blank">"Language"</a>, mas neste livro, ele será chamado de <a href="https://docs.oracle.com/pt-br/iaas/Content/language/using/home.htm" target="_blank">"OCI Language"</a>. Essa escolha se deve ao fato de que o termo "Language" pode ter diferentes significados dependendo do contexto em que é utilizado.

O <a href="https://docs.oracle.com/pt-br/iaas/Content/language/using/home.htm" target="_blank">Language</a> disponibiliza, através de sua API REST, as seguintes funcionalidades para o processamento de textos:

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

Algumas das funcionalidades já estão disponíveis para uso imediato, utilizando modelos pré-treinados pela Oracle. Esses modelos são treinados com um conjunto abrangente de dados genéricos, que, em muitos casos, podem não atender a contextos específicos de certas aplicações.

Para superar essa limitação, é possível desenvolver e treinar modelos utilizando dados específicos do seu negócio. O primeiro passo nesse processo é a criação de um projeto, seguido pela preparação dos dados de treinamento. Após essa etapa, os dados devem ser enviados para um bucket no OCI. Em seguida, pode-se realizar o treinamento do modelo e, por fim, executar testes para validar a eficácia do modelo após o treinamento.

### <a href="https://docs.oracle.com/pt-br/iaas/Content/language/using/projects.htm" target="_blank"><b>Projeto</b></a>

Um projeto serve basicamente como um meio ou contêiner para organizar tarefas relacionadas ao **Processamento de Linguagem Natural** para processar dados específicos do seu contexto de negócio.

A aplicação chatbot do **OCI PIZZA** utiliza um projeto localizado nas regiões `sa-saopaulo-1` e `sa-vinhedo-1`, dentro da estrutura de [compartimento](../capitulo-3/iam-limites-cotas-e-audit.md#compartimentos) `cmp-prd:cmp-appl`, denominado `chatbot-project`.

Para criar o projeto na região `sa-saopaulo-1` dentro da estrutura de [compartimento](../capitulo-3/iam-limites-cotas-e-audit.md#compartimentos) `cmp-prd:cmp-appl`, utilize o seguinte comando:

```bash linenums="1"
$ oci ai language project create \
> --region "sa-saopaulo-1" \
> --compartment-id "ocid1.compartment.oc1..aaaaaaaaaaaaaaaabbbbbbbbccc" \
> --display-name "chatbot-project" \
> --description "Projeto OCI Language para Chatbot da região \"sa-saopaulo-1\"." \
> --wait-for-state "SUCCEEDED"
```

### **Dados de Treinamento**

Algo que o <a href="https://docs.oracle.com/pt-br/iaas/Content/language/using/home.htm" target="_blank">OCI Language</a> não faz sozinho é identificar qual é a intenção do usuário. No contexto do chatbot, essa é uma das tarefas mais primordiais que ele deve desempenhar.

O termo "intenção" é frequentemente utilizado no contexto de chatbots para descrever o processo de identificar, a partir de uma sentença ou texto, o que um usuário deseja. Uma vez que a intenção foi corretamente identificada, o chatbot pode executar determinadas ações, como, por exemplo, invocar uma função que consulta um banco de dados para fornecer uma resposta.

Para que o <a href="https://docs.oracle.com/pt-br/iaas/Content/language/using/home.htm" target="_blank">OCI Language</a> possa identificar corretamente a intenção do usuário, é necessário treiná-lo com um conjunto de dados específico, comumente chamado de **Dados de Treinamento (dataset)**.

Neste caso, os dados de treinamento consistem em um conjunto de sentenças comuns, frequentemente utilizadas por usuários de uma pizzaria, como por exemplo:

![alt_text](./img/nlp-frase-3.png "NLP Frase #3")

![alt_text](./img/nlp-frase-4.png "NLP Frase #4")

Quanto maior e mais diversificado for o número de sentenças de exemplo, mais assertivo e preciso será o <a href="https://docs.oracle.com/pt-br/iaas/Content/language/using/home.htm" target="_blank">OCI Language</a> na identificação das intenções dos usuários.

!!! note "NOTA"
    Na verdade, o que se torna assertivo e preciso não é o <a href="https://docs.oracle.com/pt-br/iaas/Content/language/using/home.htm" target="_blank">OCI Language</a> em si, mas sim o modelo estatístico gerado a partir dos dados de treinamento que você fornece.

No diretório <a href="https://github.com/daniel-armbrust/ocn-ocipizza/tree/main/scripts/capitulo-4/data" target="_blank">"scripts/capitulo-4/data"</a> do <a href="https://github.com/daniel-armbrust/ocn-ocipizza" target="_blank">repositório de códigos</a> da aplicação **OCI PIZZA**, há dois arquivos que contêm sentenças de exemplo de interações típicas de usuários da pizzaria. São eles:

- <a href="https://github.com/daniel-armbrust/ocn-ocipizza/tree/main/scripts/capitulo-4/data/chatbot-train-intents.csv" target="_blank"><b>chatbot-train-intents.csv</b></a>
    - Arquivo que contém exemplos de sentenças que são utilizados no processo de treinamento.

- <a href="https://github.com/daniel-armbrust/ocn-ocipizza/tree/main/scripts/capitulo-4/data/chatbot-test-intents.csv" target="_blank"><b>chatbot-test-intents.csv</b></a>
    - Arquivo que contém exemplos de sentenças que são utilizados exclusivamente para testes.

!!! note "NOTA"
    A boa prática é separar 70% do conjunto total de dados para realizar o treinamento e reservar os 30% restantes para testes. É muito importante que esses 30% sejam dados que não foram utilizados no processo de treinamento.

### **Classificação de Texto**

<a href="https://docs.oracle.com/pt-br/iaas/Content/language/using/text-class.htm" target="_blank">Classificação de Texto</a> é uma técnica de aprendizagem supervisionada que usa dados previamente rotulados. 

O <a href="https://docs.oracle.com/pt-br/iaas/Content/language/using/home.htm" target="_blank">OCI Language</a> possui a funcionalidade para realizar a <a href="https://docs.oracle.com/pt-br/iaas/Content/language/using/text-class.htm" target="_blank">Classificação de Texto</a>, a qual retorna uma string específica — ou, nos termos do <a href="https://docs.oracle.com/pt-br/iaas/Content/language/using/home.htm" target="_blank">OCI Language</a>, um label ou categoria — com base em uma sentença ou texto de entrada.

Essa funcionalidade é extremamente útil em aplicações de chatbot, pois o objetivo é, a partir da sentença do usuário, retornar uma string que identifique uma intenção. Essa intenção pode ser então avaliada pela lógica da aplicação para gerar uma resposta apropriada.

Para tarefas de <a href="https://docs.oracle.com/pt-br/iaas/Content/language/using/text-class.htm" target="_blank">Classificação de Texto</a>, o arquivo que contém os dados de treinamento a serem enviados ao <a href="https://docs.oracle.com/pt-br/iaas/Content/language/using/home.htm" target="_blank">OCI Language</a> deve seguir a seguinte estrutura:

![alt_text](./img/text-classification-1.png "Classificação de Texto #1")

```bash linenums="1"
$ head -5 capitulo-4/data/chatbot-train-intents.csv
text,labels
"Errei o pedido, cancela por favor",cancelar_pedido
Gostaria de pedir uma pizza grande muçarela por favor,fazer_pedido
"Boa noite, obrigado",despedida
"Olá, gostaria de fazer um pedido",ver_cardapio
```

Alguns detalhes que devem ser levados em consideração ao criar um arquivo para <a href="https://docs.oracle.com/pt-br/iaas/Content/language/using/text-class.htm" target="_blank">Classificação de Texto</a> que são:

- `text,labels`
    - É obrigatório que a primeira linha do arquivo contenha as palavras `text` e `labels`, separadas por vírgula. Caso contrário, o processo de treinamento falhará.

- `text`
    - O texto das sentenças é de livre escolha e pode incluir letras maiúsculas, minúsculas, acentos e caracteres especiais. Como regra geral, se a sentença contiver uma vírgula, toda ela deve estar entre aspas duplas (`"texto, com, vírgula"`), caso contrário, o processo de treinamento falhará.

- `labels`
    - String que identifica a intenção com base na sentença contida na coluna `text`. O identificador de intenção pode ser multilabel e se este for o caso, deve seguir o formato `label_1|label_2|...`.

O conjunto de intenções que o chatbot do OCI PIZZA processa inclui:

- **saudacao**
- **fazer_pedido**
- **ver_cardapio**
- **confirmar_pedido**
- **cancelar_pedido**
- **agradecimento**

!!! note "NOTA"
    São necessárias, no mínimo, dez frases de exemplo para cada intenção. Essa é uma exigência do processo de treinamento realizado pelo serviço <a href="https://docs.oracle.com/pt-br/iaas/Content/language/using/home.htm" target="_blank">OCI Language</a>.

### **Treinamento**

Uma vez que existem dados previamente classificados, é possível iniciar a etapa de treinamento, que resulta na criação do que chamamos de modelo de Inteligência Artificial, ou simplesmente, modelo.

De maneira simplificada, um modelo é o resultado matemático do processo de treinamento, no qual "treinar" se refere à ação de "alimentar" algoritmos de Inteligência Artificial com uma grande quantidade de dados. Isso permite a criação de um modelo capaz de fazer previsões ou classificações sobre conjuntos de dados ainda não vistos. Em outras palavras, o modelo resultante do treinamento é capaz de realizar previsões.

!!! note "NOTA"
    Neste livro, não abordaremos em detalhes o que é Inteligência Artificial nem explicaremos seu funcionamento. A IA é uma área de estudos extremamente vasta e complexa. Aqui, apresentaremos apenas alguns aspectos básicos para que o leitor possa compreender temas relacionados à preparação do <a href="https://docs.oracle.com/pt-br/iaas/Content/language/using/home.htm" target="_blank">OCI Language</a> para ser utilizado em tarefas de classificação.

Para treinar um modelo no <a href="https://docs.oracle.com/pt-br/iaas/Content/language/using/home.htm" target="_blank">OCI Language</a> voltado para tarefas de <a href="https://docs.oracle.com/pt-br/iaas/Content/language/using/text-class.htm" target="_blank">Classificação de Texto</a>, é necessário, primeiramente, enviar os arquivos `chatbot-train-intents.csv` e `chatbot-test-intents.csv` para o [Object Storage](./object-storage.md). Isso irá permitir que o <a href="https://docs.oracle.com/pt-br/iaas/Content/language/using/home.htm" target="_blank">OCI Language</a> acesse esses dados e, a partir daí, crie, treine e teste o modelo que será utilizado pelo chatbot da aplicação **OCI PIZZA**.

O comando abaixo cria um bucket privado chamado `chatbot-data` na região `sa-saopaulo-1`, dentro da estrutura de [compartimento](../capitulo-3/iam-limites-cotas-e-audit.md#compartimentos) `cmp-prd:cmp-appl`, que será utilizado para o upload e armazenamento dos arquivos `chatbot-train-intents.csv` e `chatbot-test-intents.csv`:

```bash linenums="1"
$ oci os bucket create \
> --region "sa-saopaulo-1" \
> --compartment-id "ocid1.compartment.oc1..aaaaaaaaaaaaaaaabbbbbbbbccc" \
> --name "chatbot-data" \
> --public-access-type "NoPublicAccess"
```

Após a criação do bucket, é o momento de enviar os arquivos utilizando os comandos abaixo:

```bash linenums="1"
$ oci os object put \
> --region "sa-saopaulo-1" \
> --bucket-name "chatbot-data" \
> --file "data/chatbot-train-intents.csv" \
> --content-type "text/csv" \
> --verify-checksum \
> --force
```

```bash linenums="1"
$ oci os object put \
> --region "sa-saopaulo-1" \
> --bucket-name "chatbot-data" \
> --file "data/chatbot-test-intents.csv" \
> --content-type "text/csv" \
> --verify-checksum \
> --force
```

!!! note "NOTA"
    O script <a href="https://github.com/daniel-armbrust/ocn-ocipizza/blob/main/scripts/capitulo-4/bucket-chatbot-data.sh" target="_blank">"bucket-chatbot-data.sh"</a>, localizado no diretório <a href="https://github.com/daniel-armbrust/ocn-ocipizza/tree/main/scripts/capitulo-4" target="_blank">"scripts/capitulo-4"</a> do <a href="https://github.com/daniel-armbrust/ocn-ocipizza" target="_blank">repositório de códigos</a> da aplicação **OCI PIZZA**, cria os buckets e realiza o upload dos arquivos <a href="https://github.com/daniel-armbrust/ocn-ocipizza/tree/main/scripts/capitulo-4/data/chatbot-train-intents.csv" target="_blank">"chatbot-train-intents.csv"</a> e <a href="https://github.com/daniel-armbrust/ocn-ocipizza/tree/main/scripts/capitulo-4/data/chatbot-test-intents.csv" target="_blank">"chatbot-test-intents.csv"</a> nas regiões `sa-saopaulo-1` e `sa-vinhedo-1`.

Como última tarefa relacionada à disponibilização dos dados para treinamento, é necessário conceder acesso ao bucket `chatbot-data` ao <a href="https://docs.oracle.com/pt-br/iaas/Content/language/using/home.htm" target="_blank">OCI Language</a>. Esse acesso é concedido pela criação de um [Grupo Dinâmico](../capitulo-3/iam-limites-cotas-e-audit.md#363-grupos-dinâmicos) e uma [Política IAM](../capitulo-3/iam-limites-cotas-e-audit.md#políticas-de-acesso).

Para criar o [Grupo Dinâmico](../capitulo-3/iam-limites-cotas-e-audit.md#363-grupos-dinâmicos) que faz referência ao serviço <a href="https://docs.oracle.com/pt-br/iaas/Content/language/using/home.htm" target="_blank">OCI Language</a> e à [Política IAM](../capitulo-3/iam-limites-cotas-e-audit.md#políticas-de-acesso), utilize os comandos abaixo:

```bash linenums="1"
$ oci iam dynamic-group create \
> --compartment-id "ocid1.tenancy.oc1..aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa" \
> --name "language-dyngrp" \
> --description "Grupo dinâmico para o serviço OCI Language." \
> --matching-rule "ALL {resource.type='ailanguagemodel'}" \
> --wait-for-state "ACTIVE"
```

```bash linenums="1"
$ oci iam policy create \
> --compartment-id "ocid1.tenancy.oc1..aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa" \
> --name "language-policy" \
> --description "Políticas de Acesso para o Grupo Dinâmico \"language-dyngrp\" acessar os objetos do bucket \"chatbot-data\"." \
> --statements '["Allow dynamic-group language-dyngrp to manage objects in tenancy where target.bucket.name='chatbot-data'"]' \
> --wait-for-state "ACTIVE"
```

!!! note "NOTA"
    O script <a href="https://github.com/daniel-armbrust/ocn-ocipizza/blob/main/scripts/capitulo-4/language-policy.sh" target="_blank">"language-policy.sh"</a>, localizado no diretório <a href="https://github.com/daniel-armbrust/ocn-ocipizza/tree/main/scripts/capitulo-4" target="_blank">"scripts/capitulo-4"</a> do <a href="https://github.com/daniel-armbrust/ocn-ocipizza" target="_blank">repositório de códigos</a> da aplicação **OCI PIZZA**, contém os comandos necessários para a criação do [Grupo Dinâmico](../capitulo-3/iam-limites-cotas-e-audit.md#363-grupos-dinâmicos) e da [Política IAM](../capitulo-3/iam-limites-cotas-e-audit.md#políticas-de-acesso), que concedem acesso ao <a href="https://docs.oracle.com/pt-br/iaas/Content/language/using/home.htm" target="_blank">OCI Language</a> aos dados de treinamento.

Com os dados prontos, disponibilizados e o acesso concedido, chega o momento de treinar o modelo. Porém, antes disso, serão necessárias duas informações: o OCID do projeto recém-criado e o namespace do Object Storage. Ambas as informações serão utilizadas como parte do comando usado para treinar o modelo.

O comando abaixo retorna o [namespace](./object-storage.md#414-acessando-objetos) do [Object Storage](./object-storage.md):

```bash linenums="1"
$ oci os ns get
{
  "data": "WYYdXX82dnaS"
}
```

Já o comando abaixo retorna o OCID do projeto de <a href="https://docs.oracle.com/pt-br/iaas/Content/language/using/text-class.htm" target="_blank">Classificação de Texto</a> recém-criado:

```bash linenums="1"
$ oci ai language project list \
> --region "sa-saopaulo-1" \
> --compartment-id "ocid1.compartment.oc1..aaaaaaaaaaaaaaaabbbbbbbbccc" \
> --display-name "chatbot-project" \
> --lifecycle-state "ACTIVE" \
> --all \
> --query "data.items[].id"
[
  "ocid1.ailanguageproject.oc1.sa-saopaulo-1.abcdefghai"
]
```

Com as informações à disposição, é possível criar e treinar o modelo de <a href="https://docs.oracle.com/pt-br/iaas/Content/language/using/text-class.htm" target="_blank">Classificação de Texto</a> dentro da estrutura do compartimento `cmp-prd:cmp-appl`, na região `sa-saopaulo-1`, utilizando o comando abaixo:

```bash linenums="1"
$ oci ai language model create \
> --region "sa-saopaulo-1" \
> --compartment-id "ocid1.compartment.oc1..aaaaaaaaaaaaaaaabbbbbbbbccc" \
> --project-id "ocid1.ailanguageproject.oc1.sa-saopaulo-1.abcdefghai" \
> --display-name "model-text-classification" \
> --description "Modelo para Classificação de Texto." \
> --model-details "{
>    \"modelType\": \"TEXT_CLASSIFICATION\",
>    \"languageCode\": \"en\",
>    \"version\": \"V1.0\",
>    \"classificationMode\": { 
>        \"classificationMode\": \"MULTI_CLASS\" 
>    }
> }" \
> --training-dataset "{
>    \"locationDetails\": {
>        \"locationType\": \"OBJECT_LIST\",
>        \"bucketName\": \"chatbot-data\",
>        \"namespaceName\": \"WYYdXX82dnaS\",
>        \"objectNames\": [\"chatbot-train-intents.csv\"]
>    },
>    \"datasetType\": \"OBJECT_STORAGE\"
> }" \
> --test-strategy "{
>    \"testingDataset\": {
>        \"locationDetails\": {
>             \"locationType\": \"OBJECT_LIST\",
>             \"bucketName\": \"chatbot-data\",
>             \"namespaceName\": \"WYYdXX82dnaS\",
>             \"objectNames\": [\"chatbot-test-intents.csv\"]
>        },
>        \"datasetType\": \"OBJECT_STORAGE\"
>   },
>   \"strategyType\": \"TEST_AND_VALIDATION_DATASET\"
> }" \
> --wait-for-state "ACCEPTED"
```

!!! note "NOTA"
    O script <a href="https://github.com/daniel-armbrust/ocn-ocipizza/blob/main/scripts/capitulo-4/language-model.sh" target="_blank">"language-model.sh"</a>, localizado no diretório <a href="https://github.com/daniel-armbrust/ocn-ocipizza/tree/main/scripts/capitulo-4" target="_blank">"scripts/capitulo-4"</a> do <a href="https://github.com/daniel-armbrust/ocn-ocipizza" target="_blank">repositório de códigos</a> da aplicação **OCI PIZZA**, contém os comandos necessários para criar e treinar o modelo de <a href="https://docs.oracle.com/pt-br/iaas/Content/language/using/text-class.htm" target="_blank">Classificação de Texto</a> nas regiões `sa-saopaulo-1` e `sa-vinhedo-1`.