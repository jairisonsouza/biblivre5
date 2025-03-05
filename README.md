# Biblivre5 - Docker
Configurações necessárias para executar o Biblivre 5 usando Docker

# AMBIENTE LOCAL:

Para implamtar o sistema localmente basta executar o comando abaixo:

```
docker-compose -f docker-compose-localhost.yml up -d
```

Obs. Lembre-se de executar o comando na pasta raiz do projeto.

# AMBIENTE DE PRODUÇÃO:

## Dominio
Lembre de ter um dominio configurado para o IP da sua instância com as portas `80` e `443` habilitadas no firewall.

## Requisitos
[Docker] (https://www.docker.com/get-docker)
[Docker Compose] (https://docs.docker.com/compose/install)

* Para instalar o docker, execute:
```
sudo apt update
sudo apt install docker.io
```

* Para instalar o docker-compose, execute:
```
sudo apt install docker-compose
```

## Clonando o projeto
```
git clone https://github.com/jairisonsouza/biblivre5.git
```

## Configuração do domínio
Altere o arquivo `docker-compose.yml` e informe o seu domínio e seu e-mail nas linhas marcadas com `#`:

```
version: '3.9'
services:
  app:
    image: jairisondetran/tomcat:7-jdk8
    environment:
      - JAVA_OPTS="-agentlib:jdwp=transport=dt_socket,address=8000,server=y,suspend=n"
    depends_on:
     - "db"
    restart: always
    volumes:
      - type: bind
        source: ./tomcat/Biblivre5.war
        target: /usr/local/tomcat/webapps/Biblivre5.war
    networks:
      - biblivre5
    labels:
      - "traefik.enable=true"
      - "traefik.http.routers.biblivre.rule=Host(`seudominio.com.br`)" # Substitua pelo seu domínio
      - "traefik.http.routers.biblivre.entrypoints=websecure"
      - "traefik.http.routers.biblivre.tls.certresolver=myresolver"
      - "traefik.http.services.biblivre.loadbalancer.server.port=8080"

  db:
    image: postgres:10.3
    environment:
      POSTGRES_PASSWORD: abracadabra
      POSTGRES_USER: postgres
    volumes:
      - type: bind
        source: ./postgres/pg_hba.conf
        target: /etc/postgresql/pg_hba.conf
      - type: bind
        source: ./postgres/postgresql.conf
        target: /etc/postgresql/postgresql.conf
      - type: bind
        source: ./postgres/create-database.sh
        target: /docker-entrypoint-initdb.d/create-database.sh
      - type: bind
        source: ./postgres/sql/createdatabase.sql
        target: /docker-entrypoint-initdb.d/sql/createdatabase.sql
      - type: bind
        source: ./postgres/sql/biblivre4.sql
        target: /docker-entrypoint-initdb.d/sql/biblivre4.sql
    ports:
      - "5432:5432"
    networks:
      - biblivre5

  traefik:
    image: traefik:v2.10
    restart: always
    command:
      - "--api.insecure=true"
      - "--providers.docker=true"
      - "--entrypoints.web.address=:80"
      - "--entrypoints.websecure.address=:443"
      - "--entrypoints.web.http.redirections.entryPoint.to=websecure"
      - "--entrypoints.web.http.redirections.entryPoint.scheme=https"
      - "--entrypoints.web.http.redirections.entryPoint.permanent=true"
      - "--certificatesresolvers.myresolver.acme.tlschallenge=true"
      - "--certificatesresolvers.myresolver.acme.email=seuemail@dominio.com" # Substitua pelo seu e-mail
      - "--certificatesresolvers.myresolver.acme.storage=/letsencrypt/acme.json"
    ports:
      - "80:80"
      - "443:443"
    volumes:
      - "/var/run/docker.sock:/var/run/docker.sock:ro"
      - "traefik-data:/letsencrypt"
    networks:
      - biblivre5

networks:
  biblivre5:
    driver: bridge

volumes:
  traefik-data:

```

## Executando o contêiner.

Acesse a pasta do projeto e execute o comando:
```
docker-compose up -d
```

Em instantes sua instância do Biblivre 5 estará acessível.

Acesse: http://seudominio/Biblivre5.
