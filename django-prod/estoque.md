# Instalando Estoque em desenvolvimento (dev) e produção (prod)

## 1. Criando usuario para o ambiente dev/prod

```bash
# cria usuario
 sudo adduser estoque

# adiciona usuario ao grupo existente sudo 
 sudo usermod -aG sudo estoque
```

## 2. Instalando python 3.7.4 com pyenv

- Referências:
  - https://github.com/pyenv/pyenv-installer
  - https://github.com/pyenv/pyenv/wiki/common-build-problems

```bash
# dependências
sudo apt-get install -y make build-essential libssl-dev zlib1g-dev libbz2-dev \
libreadline-dev libsqlite3-dev wget curl llvm libncurses5-dev libncursesw5-dev \
xz-utils tk-dev libffi-dev liblzma-dev python-openssl git

# instalando o pyenv
curl https://pyenv.run | bash

# adicionar no final do arquivo .bashrc
vi ~/.bashrc 

export PATH="/home/estoque/.pyenv/bin:$PATH"
eval "$(pyenv init -)"
eval "$(pyenv virtualenv-init -)"

## Instalando ultima versao do python
# update de lista
pyenv update

# lista versoes
pyenv install -l

# instala a versão python 3.7.4
pyenv install 3.7.4

# selecionar versão 3.7.4
pyenv local 3.7.4

## Verificando versão python
python -V
    Python 3.7.4
```

## 3. Baixando à aplicação estoque do site github e criando ambiente de desenvolvimento(dev) e produção(prod).

```bash
su estoque -
cd ~
git clone https://github.com/rg3915/estoque.git dev
cd ~
git clone https://github.com/rg3915/estoque.git prod
```

## 4. Criando ambiente python em desenvolvimento(dev)
```python
# Instalando Desenvolvimento
cd ~/dev
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
python contrib/env_gen.py
python manage.py migrate
python manage.py createsuperuser

# adicionado o ip do servidor no .env_gen
vi /home/estoque/dev/.env

DEBUG=False
ALLOWED_HOSTS=127.0.0.1, .localhost, <IP DO SERVIDOR>

# rodando a aplicação modo dev
python manage.py runserver 0.0.0.0:8000

# SE tudo estiver funcionado pressionar CTRL+C
deactivate
```

## 5. Criando banco de produção(prod) - PostgreSQL

```bash
# Instalando dependências validas para o postgresql
sudo apt install -pip python3-dev libpq-dev postgresql postgresql-contrib nginx curl

# Fazendo login no usuario bash do postgresql
estoque@eclipse210:~$ sudo -u postgres psql
[sudo] password for estoque:
psql (10.10 (Ubuntu 10.10-0ubuntu0.18.04.1))
Type "help" for help.

postgres=# CREATE DATABASE estoque;
CREATE DATABASE

# Criando usuario
postgres=# CREATE USER estoqueuser WITH PASSWORD '12345';
CREATE ROLE

#Alterando as ROLE
postgres=# ALTER ROLE estoqueuser SET client_encoding TO 'utf8';
ALTER ROLE
postgres=# ALTER ROLE estoqueuser SET default_transaction_isolation TO 'read committed';
ALTER ROLE
postgres=# ALTER ROLE estoqueuser SET timezone TO 'UTC';
ALTER ROLE

# Dando direio total ao usuario estoqueuser ao banco estoque
postgres=# GRANT ALL PRIVILEGES ON DATABASE estoque TO estoqueuser;

# Fechando o prompt do postgresql e gravando as configurações.
postgres=# \q
```

## 6. Configurando ambiente de produção(prod) para python

```python
su estoque -
cd ~

# atualizando o pip
sudo -H pip3 install --upgrade pip

# Instalando Desenvolvimento
cd ~prod/
python3 -m venv .venv
source .venv/bin/activate

# Criar arquivo prod.txt
cat prod.txt
-r requirements.txt
gunicorn==19.9.0
psycopg2-binary==2.8.3

# instalar as bibliotecas python
pip install --upgrade pip
pip install -r prod.txt

#Rodas o programa 
python contrib/env_gen.py

# Editar o arquivo .env
vi .env
ALLOWED_HOSTS=127.0.0.1, .localhost, <IP DO SERVIDOR>
DATABASE_URL=postgres://estoqueuser:12345@localhost:5432/estoque

# Comentar/Editar o texto abaixo:
vi ~/prod/projeto/settings.py
de:
#comentar
#DATABASES = {
#    'default': {
#        'ENGINE': 'django.db.backends.sqlite3',
#        'NAME': os.path.join(BASE_DIR, 'db.sqlite3'),
#    }
#}

para:
default_dburl = 'sqlite:///' + os.path.join(BASE_DIR, 'db.sqlite3')
DATABASES = {
       'default': config('DATABASE_URL', default=default_dburl, cast=dburl),
}


# Adicionar no começo do arquivo:
vi ~/prod/projeto/settings.py
....
from dj_database_url import parse as dburl

# Alterar 
vi ~/prod/projeto/settings.py
de:
STATIC_ROOT = os.path.join(BASE_DIR, 'staticfiles/')

para:
STATIC_ROOT = os.path.join(BASE_DIR, 'static/')                                     │

# Atualizando o banco e cache:
python manage.py migrate
python manage.py createsuperuser
python manage.py collectstatic

# Ajustando firewall
su -
sudo ufw allow 8000

# Rodando o aplicação 
python manage.py runserver 0.0.0.0:8000
```

## 7. Configurando o guncorn

```bash
# Habilitando ambiente virtual de produção(prod)
cd /home/estoque/prod
source .venv/bin/activate

# Testand o gunicorn com projeto. (dentro diretorio manage.py)
(.venv) estoque@eclipse210:~/prod$ gunicorn --bind 0.0.0.0:8000 projeto.wsgi
[2019-10-02 21:47:33 +0000] [2620] [INFO] Starting gunicorn 19.9.0
[2019-10-02 21:47:33 +0000] [2620] [INFO] Listening at: http://0.0.0.0:8000 (2620)
[2019-10-02 21:47:33 +0000] [2620] [INFO] Using worker: sync
[2019-10-02 21:47:33 +0000] [2623] [INFO] Booting worker with pid: 2623
# CTRL + C

# Criado o socket
sudo vi /etc/systemd/system/gunicorn.socket

[Unit]
Description=gunicorn socket

[Socket]
ListenStream=/run/gunicorn.sock

[Install]
WantedBy=sockets.target


# Criando o serviço
sudo vi /etc/systemd/system/gunicorn.service

[Unit]
Description=gunicorn daemon
Requires=gunicorn.socket
After=network.target

[Service]
User=estoque
Group=www-data
WorkingDirectory=/home/estoque/prod
ExecStart=/home/estoque/prod/.venv/bin/gunicorn \
          --access-logfile - \
          --workers 3 \
          --bind unix:/run/gunicorn.sock \
          projeto.wsgi:applicationt

[Install]
WantedBy=multi-user.target

#Habilitando o serviço
sudo systemctl start gunicorn.socket
sudo systemctl enable gunicorn.socket

# Verificando se o socket esta ok.(vai listar o esqueleto do conteudo da pagina principal)
curl --unix-socket /run/gunicorn.sock localhost


#
● gunicorn.service - gunicorn daemon
   Loaded: loaded (/etc/systemd/system/gunicorn.service; disabled; vendor preset: enabled)
   Active: active (running) since Wed 2019-10-02 22:25:21 UTC; 2min 55s ago
 Main PID: 4328 (gunicorn)
    Tasks: 4 (limit: 4660)
   CGroup: /system.slice/gunicorn.service
           ├─4328 /home/estoque/prod/.venv/bin/python3 /home/estoque/prod/.venv/bin/gunicorn --access-logfile - --workers 3 --bind unix:/run/gunicorn.sock projeto.wsgi:
           ├─4345 /home/estoque/prod/.venv/bin/python3 /home/estoque/prod/.venv/bin/gunicorn --access-logfile - --workers 3 --bind unix:/run/gunicorn.sock projeto.wsgi:
           ├─4347 /home/estoque/prod/.venv/bin/python3 /home/estoque/prod/.venv/bin/gunicorn --access-logfile - --workers 3 --bind unix:/run/gunicorn.sock projeto.wsgi:
           └─4348 /home/estoque/prod/.venv/bin/python3 /home/estoque/prod/.venv/bin/gunicorn --access-logfile - --workers 3 --bind unix:/run/gunicorn.sock projeto.wsgi:

# Lista o servico
sudo systemctl status gunicorn

#Output:
● gunicorn.service - gunicorn daemon
   Loaded: loaded (/etc/systemd/system/gunicorn.service; disabled; vendor preset: enabled)
   Active: active (running) since Wed 2019-10-02 22:25:21 UTC; 2min 55s ago
 Main PID: 4328 (gunicorn)
    Tasks: 4 (limit: 4660)
   CGroup: /system.slice/gunicorn.service
           ├─4328 /home/estoque/prod/.venv/bin/python3 /home/estoque/prod/.venv/bin/gunicorn --access-logfile - --workers 3 --bind unix:/run/gunicorn.sock projeto.wsgi:
           ├─4345 /home/estoque/prod/.venv/bin/python3 /home/estoque/prod/.venv/bin/gunicorn --access-logfile - --workers 3 --bind unix:/run/gunicorn.sock projeto.wsgi:
           ├─4347 /home/estoque/prod/.venv/bin/python3 /home/estoque/prod/.venv/bin/gunicorn --access-logfile - --workers 3 --bind unix:/run/gunicorn.sock projeto.wsgi:
           └─4348 /home/estoque/prod/.venv/bin/python3 /home/estoque/prod/.venv/bin/gunicorn --access-logfile - --workers 3 --bind unix:/run/gunicorn.sock projeto.wsgi:

Oct 02 22:25:21 eclipse210 systemd[1]: Started gunicorn daemon.
Oct 02 22:25:21 eclipse210 gunicorn[4328]: [2019-10-02 22:25:21 +0000] [4328] [INFO] Starting gunicorn 19.9.0
Oct 02 22:25:21 eclipse210 gunicorn[4328]: [2019-10-02 22:25:21 +0000] [4328] [INFO] Listening at: unix:/run/gunicorn.sock (4328)
Oct 02 22:25:21 eclipse210 gunicorn[4328]: [2019-10-02 22:25:21 +0000] [4328] [INFO] Using worker: sync
Oct 02 22:25:21 eclipse210 gunicorn[4328]: [2019-10-02 22:25:21 +0000] [4345] [INFO] Booting worker with pid: 4345
Oct 02 22:25:21 eclipse210 gunicorn[4328]: [2019-10-02 22:25:21 +0000] [4347] [INFO] Booting worker with pid: 4347
Oct 02 22:25:21 eclipse210 gunicorn[4328]: [2019-10-02 22:25:21 +0000] [4348] [INFO] Booting worker with pid: 4348
Oct 02 22:25:21 eclipse210 gunicorn[4328]:  - - [02/Oct/2019:19:25:21 -0300] "GET / HTTP/1.1" 200 3830 "-" "curl/7.58.0"
```

## 8. Configurando NGinx

```python
 # Adicionar a linha no arquivo hosts
 vi /etc/hosts 
192.168.12.32 eclipse210.marvels.corp estoque.marvels.corp estoque eclipse210


# Criar o arquivo estoque-prod
sudo vi /etc/nginx/sites-available/estoque-prod
server {
    listen 80;
    server_name 192.168.12.32;

    location = /favicon.ico { access_log off; log_not_found off; }
    location /static/ {
        root /home/estoque/prod;
    }

    location / {
        include proxy_params;
        proxy_pass http://unix:/run/gunicorn.sock;
    }
}


# Faendo link simbolico da aplicacao e testando
sudo ln -s /etc/nginx/sites-available/estoque-prod /etc/nginx/sites-enabled
sudo nginx -t

# Ajustando o firewall
sudo ufw delete allow 8000
sudo ufw allow 'Nginx Full'

#Ajustando o banco
sudo systemctl status postgresql
sudo systemctl start postgresql
sudo systemctl enable postgresql

#caso faça update no sistema:
sudo systemctl restart gunicorn
sudo systemctl daemon-reload
sudo systemctl restart gunicorn.socket gunicorn.service
sudo nginx -t && sudo systemctl restart nginx

Referencia:
https://www.digitalocean.com/community/tutorials/how-to-set-up-django-with-postgres-nginx-and-gunicorn-on-ubuntu-18-04

```

## Instalando certficado local

```python
# Gerando chave
mkdir /home/estoque/ssl-estoque
cd /home/estoque/ssl-estoque
openssl req -newkey rsa:2048 -nodes -keyout estoque.marvels.corp.key -out estoque.marvels.corp.csr

# O que digitei neste exemplo o dominio: marvels.corp
# Gerando chave RSA para criação de certificado Raiz:
openssl genrsa -des3 -out ca.key 2048

# Gerando certificado Raiz a partir da chave RSA:
openssl req -x509 -new -nodes -key ca.key -sha256 -days 2048 -out ca.pem

Country Name (2 letter code) [AU]:BR
State or Province Name (full name) [Some-State]:Sao Paulo
Locality Name (eg, city) []:Bauru
Organization Name (eg, company) [Internet Widgits Pty Ltd]:Marvels Corp
Organizational Unit Name (eg, section) []:TI
Common Name (e.g. server FQDN or YOUR name) []:marvels.corp
Email Address []:rootzen@marvels.corp


#Criando uma chave do certificado usando as configurações do file.csr.conf
# Antes, precisamos criar 2 arquivos com informações para criação do certificado, isso substitui você escrever tudo na linha de comando.
#Arquivo 1: file.csr.conf
[req]
default_bits = 2048
prompt = no
default_md = sha256
distinguished_name = dn

[dn]
C=BR
ST=Sao Paulo
L=Bauru
O=marvels.corp
OU=TI
emailAddress=lscosta@marvels.corp
CN = estoque.marvels.corp


# Arquivo 2: x509.conf
authorityKeyIdentifier=keyid,issuer
basicConstraints=CA:FALSE
keyUsage = digitalSignature, nonRepudiation, keyEncipherment, dataEncipherment
subjectAltName = @alt_names

[alt_names]
DNS.1 = teste.com

# Criando uma chave do certificado usando as configurações do file.csr.conf
openssl req -new -sha256 -nodes -out server.csr -newkey rsa:2048 -keyout server.key -config <( cat file.csr.conf )

# Solicitando assinatura a partir da CA:
openssl x509 -req -in server.csr -CA ca.pem -CAkey ca.key -CAcreateserial -out server.crt -days 1024 -sha256 -extfile x509.conf


# Configuracao do NGinx SSL
 sudo rm /etc/nginx/sites-enabled/default
Alterar o arquivo => /etc/nginx/sites-enabled/estoque-prod
 cat /etc/nginx/sites-enabled/estoque-prod
server {
   # listen 80;
    listen 443 ssl;
    server_name estoque.marvels.corp;
    ssl_certificate /home/estoque/ssl-estoque/server.crt;
    ssl_certificate_key /home/estoque/ssl-estoque/server.key;

    location = /favicon.ico { access_log off; log_not_found off; }
    location /staticfiles/ {
        root /home/estoque/prod;
    }

    location / {
        include proxy_params;
        proxy_pass http://unix:/run/gunicorn.sock;
    }
}

(.venv) estoque@eclipse210:~$

# Windows 10 cliente adicionar o nome para acesso via ssl => C:\Windows\System32\drivers\etc\hosts

# Copyright (c) 1993-2009 Microsoft Corp.
#
# This is a sample HOSTS file used by Microsoft TCP/IP for Windows.
#
# This file contains the mappings of IP addresses to host names. Each
# entry should be kept on an individual line. The IP address should
# be placed in the first column followed by the corresponding host name.
# The IP address and the host name should be separated by at least one
# space.
#
# Additionally, comments (such as these) may be inserted on individual
# lines or following the machine name denoted by a '#' symbol.
#
# For example:
#
#      102.54.94.97     rhino.acme.com          # source server
#       38.25.63.10     x.acme.com              # x client host

# localhost name resolution is handled within DNS itself.
#	127.0.0.1       localhost
#	::1             localhost
192.168.12.32	estoque.marvels.corp







# Acessando pelo browser  do windows
https://192.168.12.32





Referencia:
https://www.organicadigital.com/blog/configurando-ssl-com-nginx/
https://consultalinux.org/blog/ler_post.php?id=131

```

