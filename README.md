# Django-App-Documentation
## Criando um Ambiente Virtual

Irei criar um ambiente virtual (Virtual Environment) para armazenar todas as dependências de instalações necessárias. Ao fazer isso, evita-se que instalações de outros projetos conflitem com esse.
```
$ python -m venv nameofvirtualenvironment
```
No meu caso:
```
$ python -m venv .venv
```
O ```-m``` chama um módulo do python, no caso é ```venv```.

## Ativando o Ambiente Virtual

Não basta somente criar o ambiente, é necessário ativá-lo:
```
$ source nome_do_ambiente_virtual/bin/activate
```
Caso o windows seja utilizado, para ativar o ambiente o comando se difere:
```
$ nome_do_ambiente_virtual\Scripts\Activate
```
Agora podemos instalar as dependências sem que haja futuros conflitos, basta digitar ```pip install``` e o nome da biblioteca que deseja instalar.

## Instalando o Django

Para utilizar o Django é necessário que suas depêndencias sejam instaladas. Com o ```venv``` já ativado, realiza-se a instalação delas com o seguinte comando:

```
$ pip install Django
```

O ```pip``` é o gerenciador de pacotes do python.

## Criando um projeto

Use o seguinte código para criar uma estrutura de arquivos padrão para um projeto:

```
$ django-admin startproject nameofproject
```
No meu caso:
```
$ django-admin startproject mysite
```
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

## Servidor de Desenvolvimento
Vamos verificar se ele funciona. Ative o ambiente virtual, caso não esteja ativo, vá para o diretório ```mysite```, se ainda não estiver nele, e execute o seguinte comando:
```
$ python manage.py runserver
```
<b>Lembrando sempre de não utilizar</b> esse servidor em ambiente de produção. Ele foi planejado apenas para desenvolvimento. Essa ferramente foi incluída no Django para que possa desenvolver coisas rapidamente, sem ter que lidar com a configuração de um servidor de produção – como o Apache – até que esteja pronto para a produção.

Por padrão o comando ```runserver``` inicia o servidor dde desenvolvimento no IP interno da porta 8000. É possível mudar esse a porta passando ela na linha de comando como um argumento, logo após o comando.
Por exemplo:
```
$ python manage.py runserver 8080
```
É possível alterar o IP, entretanto se torna um assunto mais avançado no qual acredito que não sejá necessário se aprofundar no momento.
