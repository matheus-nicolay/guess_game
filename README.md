## Design e Arquitetura

### Estrutura de Serviços

O projeto é dividido em três principais serviços:

1. **Backend**: Implementado em Flask, que lida com a lógica de negócio e interações com o banco de dados.
2. **Frontend**: Criado com React, que fornece a interface do usuário.
3. **Banco de Dados**: Usamos PostgreSQL como sistema de gerenciamento de banco de dados.

### Volumes e Persistência de Dados

Os volumes são utilizados para garantir a persistência dos dados do banco de dados, permitindo que os dados sejam mantidos mesmo após a reinicialização dos contêineres. O volume `db_data` armazena os dados do PostgreSQL.

### Redes

O Docker Compose cria uma rede padrão onde todos os serviços podem se comunicar entre si usando seus nomes de serviço. Isso simplifica a configuração, permitindo que o backend se conecte ao banco de dados usando o nome do serviço `db`.

### Balanceamento de Carga

Embora o projeto atual não implemente balanceamento de carga, a estrutura permite a adição de múltiplas instâncias do backend em uma futura estrutura de produção (Utilizando Docker Swarm ou Kubernetes, por exemplo), pois existe balanceamento de carga sendo efetuado pelo proxy do NGINX.

## Instalação

Para instalar e configurar o projeto localmente, siga as etapas abaixo:

### Pré-requisitos

- Docker
- Docker Compose

### Passo a Passo

1. **Clone o repositório:**

   ```bash
   git clone https://github.com/matheus-nicolay/guess_game.git
   cd guess_game
   docker-compose up -d --build
   ```

2. **Acesse a aplicação**

Após a construção e inicialização, a aplicação estará disponível em http://localhost.

## Atualizando Serviços

A estrutura foi projetada para facilitar a atualização de qualquer componente do sistema. Você pode atualizar serviços trocando a versão da imagem Docker ou ajustando o Dockerfile correspondente. Aqui estão as etapas para atualizar um serviço:

### Atualização do Banco de Dados

Para atualizar a versão do PostgreSQL, edite a tag no docker-compose.yml:

```
db:
  image: postgres:14  # Atualize a versão conforme necessário
```

### Atualização do Backend

Para atualizar o backend, altere o Dockerfile ou as dependências no requirements.txt, e depois execute:

```
docker-compose up --build backend
```

### Atualização do Frontend

Similarmente, para atualizar o frontend, você pode modificar o Dockerfile ou as dependências no package.json, e então executar:

```
docker-compose up --build frontend
```