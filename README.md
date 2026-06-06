# DSMeta

DSMeta e uma aplicacao full stack para consulta de desempenho de vendas por periodo, com envio de notificacao por SMS para destacar vendedores. O projeto foi desenvolvido no contexto da Semana Spring React da DevSuperior e combina uma API Java/Spring Boot com uma interface React.

## Funcionalidades

- Listagem paginada de vendas.
- Filtro de vendas por intervalo de datas.
- Ordenacao das vendas por maior valor total.
- Envio de SMS com destaque do vendedor usando Twilio.
- Interface web responsiva com seletores de data e tabela de resultados.
- Banco H2 em memoria para facilitar a execucao local.

## Tecnologias

### Backend

- Java 17
- Spring Boot 2.7.3
- Spring Web
- Spring Data JPA
- Spring Security
- H2 Database
- Twilio SDK
- Maven

### Frontend

- React 18
- TypeScript
- Vite
- Axios
- React Datepicker
- React Toastify
- Yarn

## Estrutura do projeto

```text
dsmeta/
+-- backend/   # API REST Spring Boot
+-- frontend/  # Aplicacao React com Vite
```

## Como executar localmente

### Pre-requisitos

- Java 17+
- Node.js 16+ ou superior
- Yarn
- Conta Twilio, caso queira testar o envio real de SMS

### Backend

Acesse a pasta do backend:

```bash
cd backend
```

Configure as variaveis de ambiente da Twilio, se quiser usar a notificacao por SMS:

```bash
TWILIO_SID=seu_account_sid
TWILIO_KEY=seu_auth_token
TWILIO_PHONE_FROM=seu_numero_twilio
TWILIO_PHONE_TO=numero_destino
```

Execute a API:

```bash
./mvnw spring-boot:run
```

No Windows:

```bash
mvnw.cmd spring-boot:run
```

A API ficara disponivel em:

```text
http://localhost:8080
```

O console do H2 fica em:

```text
http://localhost:8080/h2-console
```

Configuracao padrao do H2:

```text
JDBC URL: jdbc:h2:mem:testdb
User: sa
Password: vazio
```

### Frontend

Acesse a pasta do frontend:

```bash
cd frontend
```

Instale as dependencias:

```bash
yarn
```

Opcionalmente, configure a URL da API:

```bash
VITE_BACKEND_URL=http://localhost:8080
```

Execute a aplicacao:

```bash
yarn dev
```

O Vite informara a URL local da aplicacao, normalmente:

```text
http://localhost:5173
```

## Endpoints principais

### Listar vendas

```http
GET /sales?minDate=2022-01-01&maxDate=2022-12-31
```

Retorna uma pagina de vendas filtradas por periodo.

### Enviar notificacao SMS

```http
GET /sales/{id}/notification
```

Envia uma mensagem SMS informando que o vendedor da venda selecionada foi destaque no periodo.

## Dados iniciais

O arquivo `backend/src/main/resources/import.sql` carrega dados de exemplo automaticamente no banco H2 ao iniciar a aplicacao.

## Build

Para gerar o build do frontend:

```bash
cd frontend
yarn build
```

Para empacotar o backend:

```bash
cd backend
./mvnw package
```

No Windows:

```bash
mvnw.cmd package
```

## Observacoes

- As credenciais da Twilio devem ser configuradas por variaveis de ambiente.
- O backend permite CORS e deixa as rotas liberadas para facilitar a integracao com o frontend.
- O banco H2 e em memoria, portanto os dados criados em execucao local nao persistem apos reiniciar a aplicacao.
