# Django-App-Documentation
## Criando um Ambiente Virtual

Irei criar um ambiente virtual (Virtual Environment) para armazenar todas as dependências de instalações necessárias. Ao fazer isso, evita-se que instalações de outros projetos conflitem com esse.
```
python -m venv nameofvirtualenvironment
```
No meu caso:
```
python -m venv .venv
```
O ```-m``` chama um módulo do python, no caso é ```venv ```.

## Ativando o Ambiente Virtual

Não basta somente criar o ambiente, é necessário ativá-lo:
```
source nome_do_ambiente_virtual/bin/activate
```
Caso o windows seja utilizado, para ativar o ambiente o comando se difere:
```
nome_do_ambiente_virtual\Scripts\Activate
```
Agora podemos instalar as dependências sem que haja futuros conflitos, basta digitar ```pip install``` e o nome da biblioteca que deseja instalar.

