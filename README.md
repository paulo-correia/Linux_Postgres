# Postgres

![](http://)

PostgreSQL é um sistema gerenciador de banco de dados objeto relacional (SGBDOR), desenvolvido como projeto de código aberto.

## Instalação

Toda a instalação é feita como **root**

### Debian

Instale o pacote do posgresql com o comando:

 `apt-get install postgresql`

### CentOS

Instale o pacote do posgresql com o comando:

 `yum -y install postgresql-server`

Inicialize o banco de dados com o comando:

 `service postgresql initdb`

Edite o arquivo /var/lib/pgsql/data/postgresql.conf

Altere a linha:

 `#listen_addresses = 'localhost' `

Para:

 `listen_addresses = '*' `

Altere a linha:

 `#log_line_prefix = ' '`

Para:

 `log_line_prefix = '%t %u %d'`

Salve o arquivo e saia

Inicie o serviço com o comando:

 `service postgresql start`

Coloque o serviço para ser carregado no boot com o comando:

 `chkconfig postgresql on`

## phpPgAdmin

### Debian

Instale o wget com o comando:

 `apt-get install wget`

### CentOS

Instale o wget com o comando:

 `yum -y install wget`

### Comum a ambos

Entre no diretório /var/www/html com o comando:

 `cd /var/www/html`

Baixe o phppgadmin com o comando:

`wget http://downloads.sourceforge.net/phppgadmin/phpPgAdmin-5.1.tar.gz?download`

renomeie o arquivo phpPgAdmin-5.1.tar.gz?download com o comando:

 `mv phpPgAdmin-5.1.tar.gz?download phpPgAdmin-5.1.tar.gz`

Extraia o conteúdo do arquivo com o comando:

 `>tar -xvzf phpPgAdmin-5.1.tar.gz`

Renomeie a pasta phpPgAdmin-5.1 com o comando:

 `mv phpPgAdmin-5.1 phpPgAdmin`

### Debian

Instale o php-pgsql com o comando:

 `apt-get install php-pgsql `

Reinicie o apache com o comando:

 `service apache2 restart `

### CentOS

Instale o php-pgsql com o comando:

 `yum -y install php-pgsql`

Reinicie o httpd com o comando:

 `service httpd restart`

## Configurações para o phpPgAdmin

Atribua uma senha UNIX para o usuário postgres com o comando:

 `passwd postgres`

Logue como ousuário postgres com o comando:

 `su postgres`

Chame o postgres com o comando:

 `psql`

Altere a senha do postgres no banco de dados com o comando:

 `ALTER USER postgres WITH PASSWORD 'senha';``

De o comando \\q para sair

Edite o arquivo /var/www/html/phppgadmin/conf:

Altere a linha:

 `$conf['servers'][0]['host'] = 'localhost';`

Para:

 `$conf['servers'][0]['host'] = 'ip do servidor';`

Altere a linha:

 `$conf['extra_login_security'] = true;`

Para:

 `$conf['extra_login_security'] = false;`

Salve e saia do editor

Edite o arquivo /etc/postgresql/9.4/main/pg\_hba.conf ou /var/lib/pgsql/data/pg\_hba.conf:

Insira uma linha abaixo de:

 `# hostnossl`

E coloque o seguinte conteúdo:

host all all ip da rede/24 md5

Salve e saia do editor

Edite o arquivo /etc/postgresql/9.4/main/postgresql.conf: ou /var/lib/pgsql/data/postgresql.conf:

Comente a linha colocando um # antes:

 `listen_addresses = 'localhost'`

Insira uma linha abaixo desta linha e coloque o seguinte conteúdo:

 `listen_addresses = 'ip do servidor'`

Salve e saia do editor

Reinicie o serviço do postgresql com o comando:

 `service postgresql restart`

Crie um link simbólico da pasta /usr/share/phppgadmin com o comando:

 `ln -s  /usr/share/phppgadmin /var/www/html/pgadmin`

**Obs:** Verifique se não há necessidade de mudar dono e grupo da pasta /usr/share/phppgadmin, se tiver o comando é **chown -R www-data.www-data /usr/share/phppgadmin**

Testes
------

Teste abrindo ip do servidor/pgadmin no navegador