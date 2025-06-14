
# Projeto Java com Spring Boot e JWT

## Descrição

Este projeto é uma API RESTful desenvolvida para atividade acadêmica, baseada no enunciado "[Atividade Projeto Java com Spring Boot e JWT](Atividade%20Projeto%20Java%20com%20Spring%20Boot%20e%20JWT.pdf)", implementando autenticação JWT e controle de acesso por roles (**admin** e **user**).  
Permite cadastro, login e gerenciamento de usuários, com permissões diferenciadas para administradores e usuários comuns.

---

## Funcionalidades

- Cadastro de usuário com definição de papel (role)
- Login que retorna um token JWT
- Endpoints protegidos, acessíveis apenas com JWT válido
- Controle de acesso (admin vs user)
    - **Admin:** pode listar, editar e excluir qualquer usuário
    - **User:** pode visualizar e editar apenas seu próprio perfil

---

## Tecnologias Utilizadas

- Java 21
- Spring Boot
- Spring Security
- JWT (jjwt)
- MySQL (via Docker)
- Lombok

---

## Como Rodar o Projeto

### 1. Pré-requisitos

- JDK 21 ou superior
- Docker Desktop
- Maven

### 2. Subir o MySQL

No terminal, execute na pasta do projeto:

```bash
docker compose up -d
```

Banco disponível em `localhost:3306`, usuário `root`, senha `1234`, banco `jwtapp`.

### 3. Rodar o Projeto

```bash
mvn spring-boot:run
```

Acesse em: http://localhost:8080

---

## Endpoints e Exemplos de Teste

### 1. Cadastro

**POST /auth/register**  
Body:
```json
{
  "name": "Admin User",
  "email": "admin@email.com",
  "password": "1234",
  "role": "ADMIN"
}
```
ou
```json
{
  "name": "User Teste",
  "email": "user@email.com",
  "password": "1234",
  "role": "USER"
}
```

### 2. Login

**POST /auth/login**  
Body:
```json
{
  "email": "admin@email.com",
  "password": "1234"
}
```

Retorna um token JWT.

### 3. Autorização (Bearer Token)

No Postman/Insomnia, envie o token JWT em todas as rotas protegidas:  
`Authorization: Bearer SEU_TOKEN_AQUI`

### 4. Rotas do Usuário

- **GET /api/profile** — Dados do usuário autenticado
- **PUT /api/profile** — Editar nome do usuário autenticado  
  Body:
  ```json
  {
    "name": "Novo Nome"
  }
  ```

### 5. Rotas do Admin

- **GET /api/admin/users** — Listar todos usuários
- **PUT /api/admin/users/{id}** — Editar usuário pelo ID  
  Body:
  ```json
  {
    "name": "Nome Atualizado"
  }
  ```
- **DELETE /api/admin/users/{id}** — Deletar usuário pelo ID

---

## Regras de Permissão

- **USER:** só pode editar/visualizar seu perfil
- **ADMIN:** pode listar, editar e remover qualquer usuário

Tentativas de acesso sem permissão resultam em erro **403 Forbidden**.

---

Desenvolvido por Matheus Souza — Trabalho acadêmico.
    
