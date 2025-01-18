# Biblivre5 - Docker
Configurações necessárias para executar o Biblivre 5 usando Docker

# Dominio
Lembre de ter um dominio configurado para o IP da sua instância com as portas `80` e `443` habilitadas no firewall.

# Requisitos
[Docker] (https://www.docker.com/get-docker)
[Docker Compose] (https://docs.docker.com/compose/install)

## Baixando com o git
Execute:

```bash
https://github.com/jairisonsouza/biblivre5.git
```

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
