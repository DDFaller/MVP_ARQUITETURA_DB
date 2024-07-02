
# MVP Arquitetura Database

Este repositório contém a configuração e scripts do banco de dados para a aplicação MVP Arquitetura.

## Sumário

- [Instalação](#instalação)
- [Configuração](#configuração)
- [Uso](#uso)
- [Docker](#docker)

## Instalação

### Pré-requisitos

- Docker
- Docker Compose

### Passos

1. Clone o repositório:

```bash
git clone https://github.com/DDFaller/MVP_Arquitetura_DB.git
cd MVP_Arquitetura_DB
```

## Configuração

Certifique-se de que o arquivo `docker-compose.yml` está corretamente configurado para seu ambiente. Você pode configurar variáveis como nome do banco de dados, usuário e senha.

Exemplo de `docker-compose.yml`:

```yaml
version: '3.8'
services:
  db:
    image: postgres:13
    environment:
      POSTGRES_DB: mvp
      POSTGRES_USER: postgres
      POSTGRES_PASSWORD: 0812
    ports:
      - "5432:5432"
    volumes:
      - db_data:/var/lib/postgresql/data
      - db-init:/docker-entrypoint-initdb.d
```

## Uso

### Iniciar o Banco de Dados

Inicie o container do banco de dados usando Docker Compose:

```bash
docker-compose up -d
```

### Executar Scripts SQL

Você pode executar scripts SQL para criar tabelas, inserir dados iniciais, etc. Coloque seus scripts na pasta `db-init` dentro do arquivo `create-database.sql` e execute-os conforme necessário. 

Exemplo de script SQL para criar tabelas:

```sql
CREATE DATABASE mvp;

\connect mvp

CREATE SCHEMA models;
CREATE SCHEMA "user";

CREATE TABLE "models".clothes(

  id SERIAL PRIMARY KEY,
  user_id INTEGER NOT NULL,
  model_name VARCHAR(140) NOT NULL,
  model_url VARCHAR(40)
);


CREATE TABLE "user".user_data(
  id SERIAL PRIMARY KEY,
  cpf VARCHAR(40) NOT NULL,
  password VARCHAR(40) NOT NULL
);



```

Para executar o script:
Adicione o volume db-init conforme demonstrado no arquivo compose

## Docker

### Construir a Imagem

Não é necessário construir uma imagem para o banco de dados, já que estamos utilizando a imagem oficial do PostgreSQL. 

### Executar o Container

Para iniciar o container, use:

```bash
docker-compose up -d
```

### Parar o Container

Para parar o container, use:

```bash
docker-compose down
```