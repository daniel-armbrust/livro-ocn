---
hide:
  - toc
---

# Capítulo 4: Serviços Auxiliares e Persistência de Dados

# 4.4 Chatbot com OCI Language

## 4.4.1 O que é um Chatbot?

Um **Chatbot**, também conhecido como **Assistente Virtual Inteligente (AVI)**, é um programa de computador projetado para interagir e auxiliar os clientes de uma empresa. Ele é desenvolvido para interpretar a linguagem natural, possibilitando simular uma conversa humana com os usuários por meio de interfaces de chat. Essas interfaces podem ser integradas de diversas maneiras, como em páginas da web, assistentes de voz como a Amazon Alexa, ou em aplicativos de mensagens, incluindo WhatsApp, Telegram, Facebook ou Instagram Messenger.

Uma vez que o chatbot pode interpretar e _"entender"_ a linguagem humana, ou seja, a linguagem que os humanos utilizam no dia a dia, ele pode ser programado, por exemplo, para realizar ações como fornecer informações sobre produtos e serviços e manter diálogos complexos com os usuários.

No caso da aplicação **OCI PIZZA**, o chatbot tem a função de auxiliar os clientes da pizzaria em diversas questões, como:

- Fazer pedidos de pizza
- Verificar o andamento de um pedido já realizado
- Cancelar um pedido
- Consultar o cardápio e preços
- Verificar a viabilidade de entrega no endereço solicitado

Para compreender melhor o funcionamento de um chatbot, seus conceitos e como ele pode ser desenvolvido, é necessário entender como as máquinas interpretam palavras, frases e expressões por meio do **Processamento de Linguagem Natural**, tema que será abordado a seguir.

## 4.4.2 Processamento de Linguagem Natural

Um computador é uma máquina projetada para processar números, o que significa que ele não consegue interpretar ou processar letras, palavras ou textos nativamente. Em outras palavras, o computador não consegue, por conta própria, compreender a linguagem humana.

Por exemplo, como fazer com que o computador compreenda a ação presente em uma frase que solicita a entrega de uma pizza em um determinado endereço?

![alt_text](./img/nlp-frase-1.png "NLP Frase #1")

No contexto de uma pizzaria, é possível desenvolver um código que verifique que qualquer texto que siga as palavras "Rua" ou "Avenida", tem alta probabilidade de indicar uma solicitação para entrega de pizza em um endereço específico. 

Dessa forma, conseguimos reduzir a ambiguidade e os limites de interpretação, considerando que a palavra "Aparecida" faz referência exclusiva a uma "Rua" ou "Avenida", e não a uma cidade, verbo ou qualquer outro significado.

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
    <a href="https://github.com/wadetb/eliza" target="_blank">ELIZA</a> foi um dos primeiros chatbots, desenvolvido na década de 1960, projetado para simular uma conversa entre uma pessoa e seu terapeuta. Seu funcionamento baseava-se em uma simples árvore de decisão `IF-ELSE`, onde o programa extraía palavras-chave do texto de entrada do usuário e consultava um arquivo de respostas pré-definidas para determinar a resposta a ser retornada. Você pode conferir a implementação em Python do chatbot <a href="https://github.com/wadetb/eliza" target="_blank">ELIZA</a> no seguinte link: <a href="https://github.com/wadetb/eliza" target="_blank">https://github.com/wadetb/eliza</a>

No entanto, com o tempo, novas possibilidades de diálogo surgem, exigindo mais código e estruturas `IF-ELSE` para executar ações de correspondência. Com mais código, aumentam as chances de bugs e, ao interpretar a linguagem humana, a probabilidade de erros de interpretação também cresce. 

Imagine desenvolver um chatbot que possa interpretar contextos mais amplos, além do ambiente de uma pizzaria. Nesse caso, a palavra "Aparecida" pode ter diversos significados, como:

1. Nome próprio feminino comum no Brasil.
2. Pode se referir a uma localidade, como a cidade de Aparecida do Norte.
3. Verbo "aparecer", significando que algo ou alguém tornou-se visível. 

Para superar as limitações que levam a erros de interpretação ao processar a linguagem humana, é necessário converter esses textos em representações numéricas por meio de um conjunto de técnicas conhecidas como **Processamento de Linguagem Natural**.

**Processamento de Linguagem Natural (PLN)**, ou em inglês, **Natural Language Processing (NLP)**, é uma subárea da **Inteligência Artificial (IA)** voltada para o processamento e análise de dados em linguagem natural.

Aplicações que utilizam técnicas de **Processamento de Linguagem Natural** podem "entender" sentenças faladas e escritas por humanos, ou seja, em linguagem natural. Elas são capazes de gerar respostas úteis e manter diálogos complexos.

Não se programam regras gramaticais. Em vez disso, são desenvolvidos modelos estatísticos que permitem identificar as probabilidades entre as palavras de um texto. Isso torna o processo muito mais assertivo ao programar algo capaz de "entender" e "responder" em linguagem humana, sem recorrer a um monte de `IF-ELSE`.

Para construir um chatbot eficaz, é fundamental, em primeiro lugar, conhecer as técnicas e implementações que viabilizam o **Processamento de Linguagem Natural**. Isso, antes de tudo, prepara os textos utilizados no treinamento de modelos estatísticos, os quais ajudarão o chatbot a responder perguntas de forma eficiente.