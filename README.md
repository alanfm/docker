# Descrição

Docker utilizando o compose, arquivo de configuração com variáveis de ambiente, criando um container nginx e um container php-fpm ligados através de um link e criando um container mysql.

## Configuração Container Nginx

1. Exposição de portas

	```80``` e ```443```

2. Volume (Obs: verificar se na configuração do docker -> drivers compartilhados, as unidades c: e/ou d: estão habilitadas)

	Aplicação: ```htdocs -> /var/www/html```
	
	Logs: ```nginx/logs -> /var/log/nginx```
	
	Virtual Host: ```nginx/sites -> /etc/nginx/conf.d```
	
3. Virtual Host

	Criação do vhost modelo http://api.local/ (vhost modificável)

## Configuração Container Php

1. Exposição de portas

	```9000```

2. Volume (Obs: verificar se na configuração do docker -> drivers compartilhados, as unidades c: e/ou d: estão habilitadas)

	Aplicação: ```htdocs -> /var/www/html```
	
3. Bibliotecas

	Habilitação de bibliotecas do php através de arquivo de configuração. Ex: MBSTRING, GD, MCRYPT, PDO_MYSQL, etc.
	
## Configuração Container Mysql

1. Exposição de portas

	```3306```

2. Volume (Obs: verificar se na configuração do docker -> drivers compartilhados, as unidades c: e/ou d: estão habilitadas)

	Aplicação: ```mysql/data -> /var/lib/mysql```

3. Configuração para conexão

	- ```MYSQL_DATABASE=default```

    - ```MYSQL_USER=default```

    - ```MYSQL_PASSWORD=secret```

    - ```MYSQL_ROOT_PASSWORD=root```

    - ```MYSQL_PORT=3306```
	
## Como utitilizar

1. Clone o repositório usando o comando:

   ```git clone https://github.com/alanfm/docker.git```

2. Entre na pasta ```docker``` e copie o arquivo ```example.env``` para ```.env```.

   ```cp example.env .env```

3. Rode seu container:

   ```docker-compose up -d```

4. Adicione os domínios no arquivo de hosts do windows.

   ```127.0.0.1	localhost```

   ```127.0.0.1	api.local```

5. Abra no navegador

   http://localhost/

   http://api.local/

6. Acessar o shell do container:
    
	```$ docker exec -it nginx bash```

	```$ docker exec -it php-fpm bash```
	
	```$ docker exec -it mysql bash```

7. Acessar o banco de dados dentro do container Mysql

	```mysql -u root -p```

8. Comandos básicos para utilizar o banco de dados

	```show databases;```

	```CREATE DATABASE teste;```
	
	```use teste;```
	
	```show tables;```

## Licença

MIT License