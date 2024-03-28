# Django-App-Documentation
## Criando um Ambiente Virtual

Irei criar um ambiente virtual (Virtual Environment) para armazenar todas as dependências de instalações necessárias. Ao fazer isso, evita-se que instalações de outros projetos conflitem com esse.

    $ python -m venv nameofvirtualenvironment

No meu caso:

    $ python -m venv .venv

O ```-m``` chama um módulo do python, no caso é ```venv```.

## Ativando o Ambiente Virtual

Não basta somente criar o ambiente, é necessário ativá-lo:
    
    $ source nome_do_ambiente_virtual/bin/activate

Caso o windows seja utilizado, para ativar o ambiente o comando se difere:

    $ nome_do_ambiente_virtual\Scripts\Activate

Agora podemos instalar as dependências sem que haja futuros conflitos, basta digitar ```pip install``` e o nome da biblioteca que deseja instalar.

## Instalando o Django

Para utilizar o Django é necessário que suas depêndencias sejam instaladas. Com o ```venv``` já ativado, realiza-se a instalação delas com o seguinte comando:

    $ pip install Django

O ```pip``` é o gerenciador de pacotes do python.

<hr>

## Criando um projeto

Use o seguinte código para criar uma estrutura de arquivos padrão para um projeto:

    $ django-admin startproject nameofproject

No meu caso:

    $ django-admin startproject mysite

Essa será a estrutura criada: 
```
mysite/
    manage.py
    mysite/
        __init__.py
        settings.py
        urls.py
        asgi.py
        wsgi.py
```
Refêrenciando a documentação do [Django](https://docs.djangoproject.com/pt-br/5.0/intro/tutorial01/) . Esses arquivos são:
- O diretório raiz ```mysite/``` é um contêiner para o seu projeto. Seu nome não importa para o Django; você pode renomeá-lo para qualquer nome que você quiser.
- ```manage.py```: um utilitário de linha de comando que permite a você interagir com esse projeto Django de várias maneiras. Você pode ler todos os detalhes sobre o ```manage.py``` em [django-admin and manage.py](https://docs.djangoproject.com/pt-br/5.0/ref/django-admin/).
- O diretório ```mysite/``` interior é o pacote Python para o seu projeto. Seu nome é o nome do pacote Python que você vai precisar usar para importar coisas do seu interior (por exemplo, ```mysite.urls```).
- ```mysite/__init__.py```: um arquivo vazio que diz ao Python que este diretório deve ser considerado um pacote Python. Se você é um iniciante Python, leia mais [sobre pacotes](https://docs.python.org/3/tutorial/modules.html#tut-packages) na documentação oficial do Python.
- ```mysite/settings.py```: configurações para este projeto Django. [Configurações do Django](https://docs.djangoproject.com/pt-br/5.0/topics/settings/) irá revelar para você tudo sobre o funcionamento do ```settings```.
- ```mysite/urls.py```: as declarações de URLs para este projeto Django; um “índice” de seu site movido a Django. Você pode ler mais sobre URLs em [Despachante de URL](https://docs.djangoproject.com/pt-br/5.0/topics/http/urls/).
- ```mysite/asgi.py```: um ponto de integração para servidores web compatíveis com ASGI usado para servir seu projeto. Veja [Como fazer o deploy com ASGI](https://docs.djangoproject.com/pt-br/5.0/howto/deployment/asgi/) para mais detalhes.
```mysite/wsgi.py```: um ponto de integração para servidores web compatíveis com WSGI usado para servir seu projeto. Veja [Como implementar com WSGI](https://docs.djangoproject.com/pt-br/5.0/howto/deployment/wsgi/) para mais detalhes.

<hr>

## Servidor de Desenvolvimento
Vamos verificar se ele funciona. Ative o ambiente virtual, caso não esteja ativo, vá para o diretório ```mysite```, se ainda não estiver nele, e execute o seguinte comando:

    $ python manage.py runserver

<b>Lembrando sempre de não utilizar</b> esse servidor em ambiente de produção. Ele foi planejado apenas para desenvolvimento. Essa ferramente foi incluída no Django para que possa desenvolver coisas rapidamente, sem ter que lidar com a configuração de um servidor de produção – como o Apache – até que esteja pronto para a produção.

Por padrão o comando ```runserver``` inicia o servidor dde desenvolvimento no IP interno da porta 8000. É possível mudar esse a porta passando ela na linha de comando como um argumento, logo após o comando.
Por exemplo:

    $ python manage.py runserver 8080

É possível alterar o IP, entretanto se torna um assunto mais avançado no qual acredito que não sejá necessário se aprofundar no momento.

<hr>

## Criando uma aplicação (App)
Uma app no Django é um pedaço do código, responsável por administrar um determinado contexto. Para definir uma app, é necessário se certificar de que esteja no mesmo diretório que ```manage.py```e logo após utilizar: 

    $ python manage.py startapp nameofapp

No meu caso:

    $ python manage.py startapp polls

Isto criará um diretório polls, com a seguinte estrutura:
```
polls/
    __init__.py
    admin.py
    apps.py
    migrations/
        __init__.py
    models.py
    tests.py
    views.py
```
Esta estrutura de diretório irá abrigar a aplicação de enquete.

<hr>

## Escrevendo a primeira View

Para criar uma View, é necessário adicionar o seguinte código dentro de ```polls/views.py```:

```
from django.http import HttpResponse


def index(request):
    return HttpResponse("Hello, world. You're at the polls index.")
```

Esta é a view mais simples possível no Django. Para chamar a view, é necessário mapear a URL - e para isto se torna preciso de uma URLconf.

Para criar uma URLconf no diretório polls, crie um arquivo chamado ```urls.py```. O diretório do seu app deverá ficar da seguinte forma:

```
polls/
    __init__.py
    admin.py
    apps.py
    migrations/
        __init__.py
    models.py
    tests.py
    urls.py
    views.py
```
No arquivo ```polls/urls.py``` inclua o seguinte código:

```
from django.urls import path

from . import views

urlpatterns = [
    path("", views.index, name="index"),
]
```
<hr>

## Configurando o Banco de Dados
Entrando no arquivo ```mysite/settings.py``` é possível visualizar diversas variáveis de módulo, elas representam as configurações do Django. Por padrão o banco de dados utiliza a configuração do SQLite, realizaremos a alteração para o PostgreSQL. 

Em ```DATABASES``` realizamos a seguinte alteração, alterando a ```ENGINE``` do Django e adicionando as demais varíaveis de ambiente necessárias para realizar a conexão com o banco de dados:

```
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql',
        'NAME': 'nameofdatabase',
        'USER': 'nameofuser',
        'PASSWORD': 'password',
        'HOST': '127.0.0.1orotherip',
        'PORT': "5432"
    }
}
```

## Configurando a TIME ZONE
Enquanto estiver editando ```mysite/settings.py```, realize a alteração de ```TIME_ZONE``` para o seu fuso horário.

## Entendendo Intalled Apps
Também observe a configuração do ```INSTALLED_APPS``` na parte superior do arquivo. Ela possui os nomes de todas as aplicações Django ativas para essa instância do Django. Aplicações podem ser usadas em múltiplos projetos, e você pode empacotá-las e distribuí-las para uso por outros em seus projetos.

- ```django.contrib.admin``` – O site de administração. Irá usar isso em breve.
- ```django.contrib.auth``` – Um sistema de autenticação.
- ```django.contrib.contenttypes``` – Um framework para tipos de conteúdo.
- ```django.contrib.sessions``` – Um framework de sessão.
- ```django.contrib.messages``` – Um framework de envio de mensagem.
- ```django.contrib.staticfiles``` – Um framework para gerenciamento de arquivos estáticos.

Algumas dessas aplicações fazem uso de pelo menos uma tabela no banco de dados, assim sendo, nós precisamos criar as tabelas no banco de dados antes que possamos utilizá-las. Para isso rode o seguinte comando:

    $ python manage.py migrate

<hr>

## Criando as Models

```
from django.db import models


class Question(models.Model):
    question_text = models.CharField(max_length=200)
    pub_date = models.DateTimeField("date published")


class Choice(models.Model):
    question = models.ForeignKey(Question, on_delete=models.CASCADE)
    choice_text = models.CharField(max_length=200)
    votes = models.IntegerField(default=0)
```

Aqui, cada modelo é representado por uma classe derivada da classe ```django.db.models.Model```. Cada modelo possui alguns atributos de classe, as quais por sua vez representa um campo do banco de dados no modelo.

Cada campo é representado por uma instância de uma classe ```Field``` – por exemplo, ```CharField``` para campos do tipo caractere e ```DateTimeField``` para data/hora. Isto diz ao Django qual tipo de dado cada campo contém.

O nome de cada instância ```Field``` (por exemplo ```question_text``` ou ```pub_date```) é o nome do campo, em formato amigável para a máquina. Você irá usar este valor no seu código Python, e seu banco de dados irá usá-lo como nome de coluna.

Você pode usar um argumento opcional na primeira posição de um ```Field``` para designar um nome legível para seres humanos o qual será usado em uma série de partes introspectivas do Django, e também servirá como documentação. Se esse argumento não for fornecido, o Django utilizará o nome legível para máquina. Neste exemplo nós definimos um nome legível para humanos apenas para ```Question.pub_date```. Para todos os outros campos neste modelo, o nome legível para máquina será utilizado como nome legível para humanos.

Algumas classes de Field possuem elementos obrigatórios. O ```CharField```, por exemplo, requer que você informe a ele um ```max_length``` que é usado não apenas no esquema do banco de dados, mas na validação, como nós veremos em breve.

Um ```Field``` pode ter vários argumentos opcionais; neste caso, definimos o valor ```default``` de votes para ```0```.

Finalmente, note que uma relação foi criada, usando ForeignKey. Isso diz ao Django que cada ```Choice``` está relacionada a uma única ```Question```. O Django oferece suporte para todos os relacionamentos comuns de um banco de dados: muitos-para-um, muitos-para-muitos e um-para-um.
