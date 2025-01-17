# Biblivre5 - Docker
Configurações necessárias para executar o Biblivre 5 usando Docker

# Requisitos
[Docker] (https://www.docker.com/get-docker)
[Docker Compose] (https://docs.docker.com/compose/install)

## Baixando com o git
Execute:

```bash
git clone git@gitlab.com:jairo-tech/biblivre5.git
```

## Baixando arquivo zip
Baixe o [arquivo zip com o código](https://github.com/cleydyr/biblivre5-docker/archive/master.zip) e extraia.

## Executando o contêiner.

Acesse a pasta do projeto e execute os comandos:

1º:
```bash
docker build tomcat
```

2º:
```bash
docker-compose up -d
```

Em instantes sua instância do Biblivre 5 estará acessível.

Acesse: http://seudominio/Biblivre5.
