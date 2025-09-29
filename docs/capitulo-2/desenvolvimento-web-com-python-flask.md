---
hide:
  - toc
---

# Capítulo 2: Aplicação OCI PIZZA

# 2.3 Desenvolvimento Web com Python/Flask

## 2.3.1 Antes do Desenvolvimento

Após a definição dos requisitos, chega o momento de escolher a linguagem de programação, o framework e, o mais importante, definir de forma macro a arquitetura que será adotada inicialmente pela aplicação web para resolver o problema proposto.

Neste estágio, em que o foco é iniciar o desenvolvimento, diversas dúvidas podem surgir, como:

- Qual é a melhor linguagem de programação? 
- Qual é o melhor framework? 
- Qual é a arquitetura ideal para esta aplicação?

Essas questões são comuns no contexto do desenvolvimento de software, e a melhor resposta para elas é:

- Escolha a linguagem de programação e o framework que você mais conhece.
- Defina sua arquitetura de modo que ela resolva o seu problema da forma mais simples possível.

Para o desenvolvimento da aplicação **OCI PIZZA**, optou-se pela linguagem de programação <a href="https://www.python.org/" target="_blank">Python</a> e pelo microframework <a href="https://flask.palletsprojects.com" target="_blank">Flask</a> para a construção de aplicações web.

### **O Que É Framework?**

Um <a href="https://pt.wikipedia.org/wiki/Framework_para_aplica%C3%A7%C3%B5es_web" target="_blank">framework</a> é um conjunto de código e ferramentas desenvolvido para resolver problemas específicos, funcionando como uma _"caixa de ferramentas"_ para os desenvolvedores. Ele oferece códigos pré-definidos que economizam tempo e esforço durante o desenvolvimento de aplicações, além de incluir validações testadas e medidas de segurança, como a sanitização de dados, que protegem contra ataques, como <a href="https://pt.wikipedia.org/wiki/Inje%C3%A7%C3%A3o_de_SQL" target="_blank">SQL Injection</a>, por exemplo. Isso não apenas aumenta a segurança, mas também reduz o tempo de desenvolvimento, pois muitas funcionalidades já estão prontas para uso.

Geralmente, um <a href="https://pt.wikipedia.org/wiki/Framework_para_aplica%C3%A7%C3%B5es_web" target="_blank">framework</a> é composto por várias bibliotecas e outros <a href="https://pt.wikipedia.org/wiki/Framework_para_aplica%C3%A7%C3%B5es_web" target="_blank">frameworks</a>, como é o caso do <a href="https://flask.palletsprojects.com" target="_blank">Flask</a>, que utiliza <a href="https://jinja.palletsprojects.com/" target="_blank">Jinja</a>, <a href="https://palletsprojects.com/projects/click/" target="_blank">Click</a>, <a href="https://palletsprojects.com/projects/werkzeug/" target="_blank">Werkzeug</a> e <a href="https://palletsprojects.com/projects/itsdangerous/" target="_blank">ItsDangerous</a> em seu funcionamento interno.

Por fim, um <a href="https://pt.wikipedia.org/wiki/Framework_para_aplica%C3%A7%C3%B5es_web" target="_blank">framework</a> influencia diretamente a forma como a aplicação é escrita, estabelecendo um padrão de desenvolvimento. Por exemplo, em vez de escrever manualmente o código para abrir um <a href="https://pt.wikipedia.org/wiki/Soquete_de_rede" target="_blank">socket de rede</a> e interpretar comandos do protocolo <a href="https://pt.wikipedia.org/wiki/HTTP" target="_blank">HTTP</a>, um desenvolvedor pode usar um <a href="https://pt.wikipedia.org/wiki/Framework_para_aplica%C3%A7%C3%B5es_web" target="_blank">framework</a> que já realiza essas tarefas automaticamente.

Por exemplo, o código abaixo implementa o método `GET` do <a href="https://pt.wikipedia.org/wiki/HTTP" target="_blank">HTTP</a>: 

```python linenums="1"
import socket

def start_server():
    # Cria um socket TCP
    server_socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
    
    # Define o endereço e a porta do servidor
    server_socket.bind(('localhost', 5000))
    
    # Escuta por conexões
    server_socket.listen(1)
    print("Servidor rodando em http://localhost:5000")

    while True:
        # Aceita uma conexão
        client_socket, addr = server_socket.accept()
        print(f"Conexão recebida de {addr}")

        # Recebe a requisição do cliente
        request = client_socket.recv(1024).decode()
        print(f"Requisição recebida:\n{request}")

        # Monta a resposta HTTP
        response = "HTTP/1.1 200 OK\r\n"
        response += "Content-Type: text/plain\r\n"
        response += "Connection: close\r\n\r\n"
        response += "<p>Hello, World!</p>"

        # Envia a resposta ao cliente
        client_socket.sendall(response.encode())
        
        # Fecha a conexão com o cliente
        client_socket.close()

if __name__ == "__main__":
    start_server()
```

Ao utilizar um <a href="https://pt.wikipedia.org/wiki/Framework_para_aplica%C3%A7%C3%B5es_web" target="_blank">framework</a> como o <a href="https://flask.palletsprojects.com" target="_blank">Flask</a>, o código seria o seguinte:

```python linenums="1"
from flask import Flask

app = Flask(__name__)

@app.route('/')
def hello_world():
    return '<p>Hello World!</p>'
```

Observe que, ao utilizar o <a href="https://pt.wikipedia.org/wiki/Framework_para_aplica%C3%A7%C3%B5es_web" target="_blank">framework</a>, não foi necessário programar os detalhes relacionados ao <a href="https://pt.wikipedia.org/wiki/Soquete_de_rede" target="_blank">socket de rede</a> (`import socket`). O <a href="https://pt.wikipedia.org/wiki/Framework_para_aplica%C3%A7%C3%B5es_web" target="_blank">framework</a> abstrai todas essas complexidades, disponibilizando um decorador `@app.route('/')` que é aplicado sobre funções <a href="https://www.python.org/" target="_blank">Python</a>, com o objetivo de retornar um conteúdo <a href="https://pt.wikipedia.org/wiki/HTML" target="_blank">HTML</a> neste caso.

Ambos os códigos produzem como resultado o <a href="https://pt.wikipedia.org/wiki/HTML" target="_blank">HTML</a> `<p>Hello World!</p>`:

```bash linenums="1"
$ curl http://localhost:5000
<p>Hello, World!</p>
```

!!! note "NOTA"
    Utilizar um <a href="https://pt.wikipedia.org/wiki/Framework_para_aplica%C3%A7%C3%B5es_web" target="_blank">framework</a> realmente facilita o desenvolvimento de aplicações. No entanto, isso não significa que você, como desenvolvedor, não deva se preocupar com os detalhes que o <a href="https://pt.wikipedia.org/wiki/Framework_para_aplica%C3%A7%C3%B5es_web" target="_blank">framework</a> abstrai. É fundamental saber o que acontece _"debaixo do capô"_, pois esse conhecimento pode ser importante para resolver problemas obscuros que não são bem documentados pelo <a href="https://pt.wikipedia.org/wiki/Framework_para_aplica%C3%A7%C3%B5es_web" target="_blank">framework</a>, por exemplo.

Abaixo estão alguns outros exemplos de <a href="https://pt.wikipedia.org/wiki/Framework_para_aplica%C3%A7%C3%B5es_web" target="_blank">frameworks</a>:

- **<a href="https://www.djangoproject.com/" target="_blank">Django</a>**
    - Um framework web de alto nível para Python que promove o desenvolvimento rápido e limpo, seguindo o padrão MVC.

- **<a href="https://spring.io/projects/spring-boot" target="_blank">Spring Boot</a>**
    - Spring Boot é um framework Java construído sobre o Spring que simplifica o desenvolvimento de aplicações.

- **<a href="https://rubyonrails.org/" target="_blank">Ruby on Rails</a>**
    - Ruby on Rails é um framework de aplicação web do lado do servidor desenvolvido em Ruby.

- **<a href="https://expressjs.com/" target="_blank">Express.js</a>**
    - Express.js é um framework projetado para a construção de aplicações web e APIs desenvolvido em JavaScript.

- **<a href="https://gin-gonic.com/" target="_blank">Gin</a>**
    - Um framework web de alto desempenho para a linguagem de programação Go, projetado para simplificar o desenvolvimento de aplicações e APIs.

## 2.3.2 Introdução ao Microframework Flask

<a href="https://flask.palletsprojects.com" target="_blank">Flask</a> é um framework desenvolvido em <a href="https://www.python.org/" target="_blank">Python</a> utilizado para o desenvolvimento de aplicações web. É considerado um <i>"microframework"</i> devido ao seu tamanho reduzido, pois sua instalação padrão inclui apenas alguns componentes essenciais para a criação de aplicações web.

<a href="https://flask.palletsprojects.com/en/stable/" target="_blank">Flask</a> pode ser estendido por meio de componentes adicionais instalados separadamente, que acrescentam funcionalidades extras à sua aplicação. Por exemplo, a aplicação **OCI PIZZA** utiliza alguns componentes instalados à parte, como o <a href="https://jinja.palletsprojects.com/" target="_blank">Jinja</a>, que permite a utilização de templates <a href="https://pt.wikipedia.org/wiki/HTML" target="_blank">HTML</a>.

!!! note "NOTA"
    Este livro abordará apenas o básico sobre o framework <a href="https://flask.palletsprojects.com" target="_blank">Flask</a> referente ao seu uso no desenvolvimento da aplicação **OCI PIZZA**. Para obter mais informações, consulte a documentação disponível em sua página oficial: <a href="https://flask.palletsprojects.com" target="_blank">https://flask.palletsprojects.com</a>

### **Instalação do Flask**

A forma mais comum de instalar o <a href="https://flask.palletsprojects.com" target="_blank">Flask</a> é por meio de um <a href="https://docs.python.org/3/library/venv.html" target="_blank"><i>ambiente virtual Python (venv)</i></a>. Um <a href="https://docs.python.org/3/library/venv.html" target="_blank">ambiente virtual</a> é, basicamente, uma cópia isolada do interpretador <a href="https://www.python.org/" target="_blank">Python</a> que opera de maneira independente no sistema operacional. A principal vantagem de utilizar um <a href="https://docs.python.org/3/library/venv.html" target="_blank">ambiente virtual</a> é a possibilidade de agrupar sua aplicação e suas dependências em um único local, sem interferir na instalação global do <a href="https://www.python.org/" target="_blank">Python</a> no sistema operacional.

Para criar e ativar um <a href="https://docs.python.org/3/library/venv.html" target="_blank">ambiente virtual</a>, utilize os comandos a seguir:

```bash linenums="1"
$ python3 -m venv venv
$ source venv/bin/activate
(venv) $
```

Após criar o <a href="https://docs.python.org/3/library/venv.html" target="_blank">ambiente virtual</a>, você pode utilizar o comando `pip` para instalar o <a href="https://flask.palletsprojects.com" target="_blank">Flask</a> e outras bibliotecas, conforme demonstrado nos comandos a seguir:

```bash linenums="1"
(venv) $ pip install Flask
(venv) $ pip install Jinja2
```

!!! note "NOTA"
    O comando `pip` é o gerenciador de pacotes do <a href="https://www.python.org/" target="_blank">Python</a>, utilizado para instalar e gerenciar bibliotecas e dependências. Para mais informações, consulte o link: <a href="https://pypi.org/project/pip/" target="_blank">https://pypi.org/project/pip/</a>

Todas as bibliotecas ou pacotes instalados, juntamente com suas versões, podem ser visualizados utilizando o comando `pip freeze`:

```bash linenums="1"
(venv) $ pip freeze
blinker==1.8.2
click==8.1.8
flask==3.0.3
importlib-metadata==8.5.0
itsdangerous==2.2.0
jinja2==3.1.6
MarkupSafe==2.1.5
werkzeug==3.0.6
zipp==3.20.2
```

!!! note "NOTA"
    Observe que outras bibliotecas foram instaladas como parte da instalação do <a href="https://flask.palletsprojects.com" target="_blank">Flask</a> e do <a href="https://jinja.palletsprojects.com/" target="_blank">Jinja</a>. Isso ocorre porque esses pacotes dependem de outros pacotes para funcionar. O comando `pip` gerencia essas dependências automaticamente para você.

A finalidade do `pip freeze` não é apenas visualizar as bibliotecas e suas dependências instaladas no <a href="https://docs.python.org/3/library/venv.html" target="_blank">ambiente virtual</a>, mas também servir como um guia para a instalação das dependências do projeto.

Para aplicações escritas em <a href="https://www.python.org/" target="_blank">Python</a>, cria-se o arquivo `requirements.txt`, que conterá todas as dependências do projeto. Utilize o comando abaixo para gerar o arquivo `requirements.txt`: 

```bash linenums="1"
(venv) $ pip freeze > requirements.txt
```

Esse arquivo é útil caso você precise instalar seu projeto e suas dependências em outra máquina ou até mesmo na nuvem, utilizando o seguinte comando:

```bash linenums="1"
(venv) $ pip install -r requirements.txt
```

!!! note "NOTA"
    Ao versionar um projeto de software, nunca incluímos as bibliotecas instaladas. Em <a href="https://www.python.org/" target="_blank">Python</a>, a prática recomendada é manter as dependências do projeto listadas no arquivo `requirements.txt`, a partir do qual as dependências são instaladas. 

### **Bibliotecas e Dependências da Aplicação OCI PIZZA**

A seguir, estão algumas das bibliotecas externas ao <a href="https://flask.palletsprojects.com" target="_blank">Flask</a> que a aplicação **OCI PIZZA** utiliza:

- **<a href="https://flask-wtf.readthedocs.io/en/1.2.x/" target="_blank">Flask-WTF</a>**
    - <a href="https://flask-wtf.readthedocs.io/en/1.2.x/" target="_blank">Flask-WTF</a> é uma extensão do <a href="https://flask.palletsprojects.com" target="_blank">Flask</a> que integra o <a href="https://wtforms.readthedocs.io/en/3.2.x/" target="_blank">WTForms</a> com o objetivo de simplificar a criação e validação de formulários HTML.

- **<a href="https://pypi.org/project/Flask-Login/" target="_blank">Flask-Login</a>**
    - <a href="https://pypi.org/project/Flask-Login/" target="_blank">Flask-Login</a> é uma extensão do <a href="https://flask.palletsprojects.com" target="_blank">Flask</a> que simplifica a autenticação de usuários e o gerenciamento de sessões.

- **<a href="https://jinja.palletsprojects.com/" target="_blank">Jinja</a>**
    - <a href="https://jinja.palletsprojects.com/" target="_blank">Jinja</a> é uma biblioteca de template para <a href="https://www.python.org/" target="_blank">Python</a> que facilita a geração de HTML dinâmicos.

- **<a href="https://jinja.palletsprojects.com/" target="_blank">Flask-JWT-Extended</a>**
    - <a href="https://flask-jwt-extended.readthedocs.io/en/stable/" target="_blank">Flask-JWT-Extended</a> é uma extensão do <a href="https://flask.palletsprojects.com" target="_blank">Flask</a> que simplifica a autenticação baseada em <a href="https://pt.wikipedia.org/wiki/JSON_Web_Token" target="_blank">JSON Web Tokens (JWT)</a>.

- **<a href="https://flask-session.readthedocs.io/en/latest/" target="_blank">Flask-Session</a>**
    - <a href="(https://flask-session.readthedocs.io/en/latest/" target="_blank">Flask-Session</a> é uma extensão do <a href="https://flask.palletsprojects.com" target="_blank">Flask</a> que permite o gerenciamento de sessões do lado do servidor _(server-side sessions)_, oferecendo suporte a diferentes backends de armazenamento, como o <a href="https://redis.io/open-source/" target="_blank">Redis</a>.

- **<a href="https://gunicorn.org/" target="_blank">gunicorn</a>**
    - <a href="https://gunicorn.org/" target="_blank">Gunicorn</a> é um servidor _HTTP Python WSGI_ que permite a execução de aplicações web de forma eficiente e escalável. Ele é usado em aplicações web desenvolvidas em _Python/Flask_ pois dá suporte a gerenciar múltiplos processos para lidar com diversas requisições simultâneas.

- **<a href="https://pypi.org/project/borneo/" target="_blank">borneo</a>**
    - <a href="https://pypi.org/project/borneo/" target="_blank">Borneo</a> é uma biblioteca que permite a interação com o <a href="https://docs.oracle.com/en/database/other-databases/nosql-database/index.html" target="_blank">Oracle NoSQL Database</a> através da linguagem <a href="https://www.python.org/" target="_blank">Python</a>.

- **<a href="https://docs.oracle.com/en-us/iaas/Content/API/SDKDocs/pythonsdk.htm" target="_blank">OCI Python SDK</a>**
    - O <a href="https://docs.oracle.com/en-us/iaas/Content/API/SDKDocs/pythonsdk.htm" target="_blank">OCI Python SDK</a> é uma biblioteca que permite interagir com os serviços da <a href="https://ocn.dev.br/capitulo-3/">Oracle Cloud Infrastructure (OCI)</a> através da linguagem <a href="https://www.python.org/" target="_blank">Python</a>.

### **Hello World com Flask**

Uma aplicação básica em <a href="https://flask.palletsprojects.com" target="_blank">Flask</a> apresenta a seguinte estrutura:

```python linenums="1"
from flask import Flask

app = Flask(__name__)

@app.route('/')
def hello_world():
    return '<p>Hello World!</p>'
```

Algumas observações importantes sobre este trecho de código são:

**1.** `from flask import Flask` é uma instrução em <a href="https://www.python.org/" target="_blank">Python</a> que importa a classe <a href="https://flask.palletsprojects.com" target="_blank">Flask</a> do módulo flask.

**2.** A instrução `app = Flask(__name__)` cria uma instância da classe <a href="https://flask.palletsprojects.com" target="_blank">Flask</a> e a atribui à variável `app`. A partir de agora, todas as funcionalidades do <a href="https://flask.palletsprojects.com" target="_blank">Flask</a> estarão disponíveis através dessa variável.

**3.** A instrução `@app.route('/')` define uma rota web. Isso significa que, após a aplicação ser iniciada, toda requisição para a raiz (`/`) acionará a função `def hello_world()`, e o resultado da execução será retornado ao cliente através da instrução `return`.

!!! note "NOTA"
    Consulte a página de <a href="https://flask.palletsprojects.com/en/stable/tutorial/" target="_blank">Tutoriais</a> do <a href="https://flask.palletsprojects.com" target="_blank">Flask</a>, disponível em <a href="https://flask.palletsprojects.com/en/stable/tutorial/" target="_blank">https://flask.palletsprojects.com/en/stable/tutorial</a>, para obter mais exemplos de códigos em <a href="https://flask.palletsprojects.com" target="_blank">Flask</a>.

### **Execução do Flask**

Antes de executar a aplicação, o conteúdo do _Hello World_ apresentado na seção anterior deve ser salvo em um arquivo. Normalmente, para aplicações <a href="https://flask.palletsprojects.com" target="_blank">Flask</a>, utiliza-se o nome `app.py` ou `wsgi.py`, que se refere ao arquivo principal da aplicação web.

Para este exemplo de _Hello World_, será utilizado o arquivo `wsgi.py`:

```bash linenums="1"
(venv) $ cat wsgi.py
from flask import Flask

app = Flask(__name__)

@app.route('/')
def hello_world():
    return '<p>Hello World!</p>'
```

!!! note "NOTA"
    A aplicação **OCI PIZZA** também utiliza o arquivo `wsgi.py` como o arquivo principal da aplicação.

Por fim, para executar e disponibilizar a aplicação na rede, utilize o comando abaixo:

```bash linenums="1"
(venv) $ flask --app wsgi run --debug --reload --host 0.0.0.0 --port 5000
 * Serving Flask app 'wsgi'
 * Debug mode: on
WARNING: This is a development server. Do not use it in a production deployment. Use a production WSGI server instead.
 * Running on all addresses (0.0.0.0)
Press CTRL+C to quit
 * Restarting with stat
 * Debugger is active!
 * Debugger PIN: 140-307-595
```

!!! note "NOTA"
    Este comando inicia um servidor simples que deve ser utilizado apenas durante o desenvolvimento da aplicação (`--debug`).  Para executar a aplicação em produção, é recomendável utilizar um servidor WSGI dedicado, como o <a href="https://gunicorn.org/" target="_blank">gunicorn</a>. Para mais informações, consulte a seção <a href="https://flask.palletsprojects.com/en/stable/deploying/" target="_blank"><i>"Deploying to Production"</i></a> no seguinte link: <a href="https://flask.palletsprojects.com/en/stable/deploying/" target="_blank">https://flask.palletsprojects.com/en/stable/deploying/</a>.

A partir de outro terminal, é possível testar a aplicação utilizando o comando `curl`:

```bash linenums="1"
$ curl http://localhost:5000
<p>Hello World!</p>
```

## 2.3.3 JavaScript Vanilla 

## 2.3.4 Componentes Lógicos da Aplicação OCI PIZZA

### Flask Blueprints

### Organização do Código

#### Enpoint de Monitoração

TODO: Importante em ambientes CLOUD.
