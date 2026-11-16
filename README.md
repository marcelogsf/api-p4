# 🏥 Voll.med API - Projeto P4 (Back-End)

API REST desenvolvida em **Java 21** e **Spring Boot 3**, contendo controle de acesso, autenticação via **JWT (JSON Web Token)**, CRUD completo de médicos e pacientes, validações de negócio, migrations com **Flyway**, e documentação interativa com **Swagger OpenAPI**.

---

## 🚀 Acesso Rápido à Documentação (Swagger UI)

Com a aplicação em execução, acesse a documentação interativa para testar todos os endpoints diretamente no navegador:

👉 **[http://localhost:8080/swagger-ui/index.html](http://localhost:8080/swagger-ui/index.html)**

> **Especificação OpenAPI (JSON):** [http://localhost:8080/v3/api-docs](http://localhost:8080/v3/api-docs)

---

## 🔐 Como se Autenticar no Swagger

As rotas de Médicos e Pacientes são protegidas por autenticação Stateless via JWT. Para testá-las:

1. Acesse o endpoint **`POST /login`** no Swagger.
2. Utilize as credenciais padrão de teste:
   ```json
   {
     "login": "marcelo",
     "senha": "123456"
   }
   ```
   *(Ou: `"login": "ana.souza@voll.med"`, `"senha": "123456"`)*
3. Execute a requisição e **copie o token gerado** no corpo da resposta:
   ```json
   {
     "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..."
   }
   ```
4. Suba até o topo da página do Swagger e clique no botão verde **Authorize 🔓**.
5. No campo **Value:**, cole o token JWT e clique em **Authorize**. O cadeado ficará fechado **🔒**.
6. Pronto! Agora todas as rotas protegidas (`/medicos`, `/pacientes`) responderão com **`200 OK`**.

---

## 🛠️ Tecnologias Utilizadas

- **Java 21** & **Spring Boot 3.4.3**
- **Spring Security 6** (Autenticação Stateless via JWT com Auth0)
- **Spring Data JPA** & **Hibernate**
- **MySQL 8.0**
- **Flyway Migration** (Versionamento e criação automatizada do banco de dados)
- **SpringDoc OpenAPI 2.8.5** & **Swagger UI**
- **Lombok** & **Bean Validation**
- **Maven** (Gerenciamento de dependências e build)

---

## 📌 Principais Endpoints

### 🔑 Autenticação & Usuários (Rotas Públicas)
| Método | Endpoint | Descrição |
|---|---|---|
| `POST` | `/login` | Autentica o usuário e devolve o Token JWT |
| `POST` | `/usuarios` | Cadastra um novo usuário com senha criptografada em BCrypt |

### 👨‍⚕️ Médicos (Requer Token JWT)
| Método | Endpoint | Descrição |
|---|---|---|
| `GET` | `/medicos` | Lista médicos ativos com paginação e ordenação |
| `GET` | `/medicos/{id}` | Detalha as informações de um médico específico |
| `POST` | `/medicos` | Cadastra um novo médico e endereço completo |
| `PUT` | `/medicos` | Atualiza dados (nome, telefone, endereço) |
| `DELETE` | `/medicos/{id}` | Inativação lógica (*Soft Delete* setando `ativo = false`) |

### 🧑‍💼 Pacientes (Requer Token JWT)
| Método | Endpoint | Descrição |
|---|---|---|
| `GET` | `/pacientes` | Lista pacientes ativos com paginação |
| `POST` | `/pacientes` | Cadastra um novo paciente |
| `PUT` | `/pacientes` | Atualiza dados do paciente |
| `DELETE` | `/pacientes/{id}` | Inativação lógica do paciente |

---

## ⚙️ Configuração e Execução

### 1. Pré-requisitos
- JDK 21 instalado e configurado no `JAVA_HOME`.
- Servidor MySQL rodando na porta `3306` com database `p4_back_2026`.

### 2. Rodar pelo IntelliJ IDEA
Execute a classe principal [`ApiApplication.java`](src/main/java/med/voll/api/ApiApplication.java). O Flyway criará e migrará todas as tabelas automaticamente.

### 3. Rodar via Maven Terminal
```bash
./mvnw clean spring-boot:run
```

### 4. Build de Produção (.jar)
Para gerar o executável com perfil de produção parametrizável:
```bash
./mvnw clean package
```
O arquivo será gerado em `target/api-0.0.1-SNAPSHOT.jar`.
