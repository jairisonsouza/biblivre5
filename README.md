# Biblivre5 - Docker
Configurações necessárias para executar o Biblivre 5 usando Docker

# Dominio
Lembre de ter um dominio configurado para o IP da sua instância com as portas `80` e `443` habilitadas no firewall.

# Requisitos
[Docker] (https://www.docker.com/get-docker)
[Docker Compose] (https://docs.docker.com/compose/install)

Para instalar o docker, execute:
```bash
sudo apt update
sudo apt install docker.io
```

Para instalar o docker-compose, execute:
```bash
sudo apt install docker-compose
```

## Baixando com o git
Execute:

```bash
git clone https://github.com/jairisonsouza/biblivre5.git
```

## Configuração do domínio
Altere o arquivo docker-compose.yml para de acordo com o seu domínio, na linha 18:

```bash
"traefik.http.routers.biblivre.rule=Host(`biblivre.jairotech.com.br`)" # Substitua pelo seu domínio
```

Não faça nenhuma outra configuração.

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
