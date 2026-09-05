# Stock Screen Backend — API REST para Triagem de Ações

![License](https://img.shields.io/badge/license-MIT-green)
![Java](https://img.shields.io/badge/Java-8-orange?logo=openjdk)
![Spring Boot](https://img.shields.io/badge/Spring%20Boot-2.4.6-brightgreen?logo=spring)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-Database-blue?logo=postgresql)
![Maven](https://img.shields.io/badge/Maven-Build-red?logo=apachemaven)
![Swagger](https://img.shields.io/badge/API%20Docs-Swagger%20UI-85EA2D?logo=swagger)

Backend Java/Spring Boot para aplicação de **triagem e análise de ações (stock screener)**, desenvolvido durante a **Santander Dev Week**. Fornece APIs REST para cadastro, consulta, filtragem e análise de dados de ações.

## 🎯 Sobre o Projeto

Este backend gerencia dados de cotações de ações, permitindo:
- Cadastro e atualização de ações
- Listagem completa com paginação
- Busca por ID ou data (cotações de hoje)
- Exclusão de registros
- Documentação automática via Swagger/OpenAPI

## 🏗️ Arquitetura

```
com.project.backend/
├── controller/          # REST Controllers (StockController)
├── service/             # Business logic (StockService)
├── repository/          # Data access (StockRepository - JPA)
├── model/
│   ├── Stock.java       # Entity JPA
│   └── dto/StockDTO.java # Data Transfer Object
├── mapper/              # Conversão Entity ↔ DTO (StockMapper)
├── exceptions/          # Global exception handling
│   ├── ExceptionsHandler.java  # @ControllerAdvice
│   ├── NotFoundException.java
│   ├── BusinessException.java
│   └── ExceptionResponse.java
├── util/                # Utilitários (MessageUtils)
└── BackendApplication.java     # Spring Boot main class
```

## 🛠️ Stack Tecnológica

| Camada | Tecnologia | Versão |
|--------|------------|--------|
| **Linguagem** | Java | 8 |
| **Framework** | Spring Boot | 2.4.6 |
| **Web** | Spring Web MVC | Incluído |
| **Validação** | Bean Validation (Hibernate Validator) | 2.2.5 |
| **Persistência** | Spring Data JPA + Hibernate | Incluído |
| **Banco** | PostgreSQL | Driver 42.x |
| **Build** | Maven Wrapper | 3.6+ |
| **Documentação** | SpringDoc OpenAPI UI (Swagger) | 1.2.32 |
| **Testes** | Spring Boot Test + JUnit 5 | Incluído |

## 🚀 Como Executar

### Pré-requisitos
- **Java JDK 8+** (recomendado JDK 11 ou 17 para compatibilidade)
- **PostgreSQL** (local ou remoto)
- **Maven 3.6+** (ou use o wrapper incluído)

### Configuração do Banco de Dados

O projeto usa PostgreSQL. Configure em `src/main/resources/application.yml`:

```yaml
spring:
  datasource:
    url: jdbc:postgresql://localhost:5432/stock_screen
    username: seu_usuario
    password: sua_senha
    driver-class-name: org.postgresql.Driver
  jpa:
    hibernate:
      ddl-auto: update  # create/update/validate/none
    show-sql: true
    database-platform: org.hibernate.dialect.PostgreSQLDialect
```

> ⚠️ **Segurança**: O `application.yml` original continha credenciais reais de um banco Heroku. **Nunca commite credenciais reais!** Use variáveis de ambiente ou `application-{profile}.yml` no `.gitignore`.

### Build e Execução

```bash
# 1. Clone o repositório
git clone https://github.com/paulorabelo/stock-screen-backend.git
cd stock-screen-backend

# 2. Configure o banco (application.yml ou variáveis de ambiente)

# 3. Build com Maven Wrapper (não precisa Maven instalado)
./mvnw clean install        # Linux/macOS
mvnw.cmd clean install      # Windows

# 4. Execute a aplicação
./mvnw spring-boot:run

# A API estará disponível em: http://localhost:8080/backend
```

### Executar JAR Gerado
```bash
# Após build bem-sucedido
java -jar target/backend-0.0.1-SNAPSHOT.jar
```

## 📚 API Endpoints

Base URL: `http://localhost:8080/backend/stock`

| Método | Endpoint | Descrição | Request Body |
|--------|----------|-----------|--------------|
| **POST** | `/stock` | Criar nova ação | `StockDTO` (JSON) |
| **PUT** | `/stock` | Atualizar ação existente | `StockDTO` (JSON) |
| **GET** | `/stock` | Listar todas as ações | — |
| **GET** | `/stock/{id}` | Buscar ação por ID | — |
| **DELETE** | `/stock/{id}` | Excluir ação por ID | — |
| **GET** | `/stock/today` | Listar cotações de hoje | — |

### Exemplo de StockDTO (JSON)
```json
{
  id: 1,
  name: Petrobras,
  symbol: PETR4.SA,
  price: 28.45,
  variation: 1.23,
  date: 2024-01-15
}
```

### Documentação Interativa (Swagger UI)
Após iniciar a aplicação, acesse:
- **Swagger UI**: http://localhost:8080/backend/swagger-ui.html
- **OpenAPI JSON**: http://localhost:8080/backend/v3/api-docs

## 🗄️ Modelo de Dados (Stock Entity)

| Campo | Tipo | Descrição |
|-------|------|-----------|
| `id` | Long | PK, auto-increment |
| `name` | String | Nome da empresa/ação |
| `symbol` | String | Ticker/símbolo (ex: PETR4.SA) |
| `price` | BigDecimal | Preço atual |
| `variation` | BigDecimal | Variação percentual |
| `date` | LocalDate | Data da cotação |

## 🔧 Configurações Importantes

### Perfis Maven
```bash
# Desenvolvimento (padrão)
./mvnw spring-boot:run

# Produção (exemplo)
./mvnw spring-boot:run -Dspring-boot.run.profiles=prod
```

### Variáveis de Ambiente Recomendadas
```bash
export DB_URL=jdbc:postgresql://host:5432/dbname
export DB_USERNAME=usuario
export DB_PASSWORD=senha_segura
export SERVER_PORT=8080
```

## 🧪 Testes
```bash
# Executar todos os testes
./mvnw test

# Testes com relatório
./mvnw test surefire-report:report
```

## 📦 Deploy

### Docker (Exemplo)
```dockerfile
FROM openjdk:17-jdk-slim
WORKDIR /app
COPY target/backend-0.0.1-SNAPSHOT.jar app.jar
EXPOSE 8080
ENTRYPOINT [java, -jar, app.jar]
```

### Heroku / Railway / Render
- Configure variáveis de ambiente para DB
- Build command: `./mvnw clean package -DskipTests`
- Start command: `java -jar target/backend-0.0.1-SNAPSHOT.jar`

## 🔗 Projetos Relacionados

| Projeto | Descrição | Link |
|---------|-----------|------|
| **project-stock-screen** | Full-stack version (este backend + Angular frontend) | [GitHub](https://github.com/paulorabelo/project-stock-screen) |
| **stock-screen-frontend** | Frontend Angular (dentro do project-stock-screen) | [GitHub](https://github.com/paulorabelo/project-stock-screen/tree/main/frontend) |

## 🤝 Contribuindo

1. Fork o projeto
2. Crie branch (`git checkout -b feature/nova-funcionalidade`)
3. Commit (`git commit -m 'feat: descrição'`)
4. Push (`git push origin feature/nova-funcionalidade`)
5. Pull Request

### Padrões de Commit (Conventional Commits)
- `feat:` nova funcionalidade
- `fix:` correção de bug
- `docs:` documentação
- `refactor:` refatoração
- `test:` testes

## 📄 Licença

Este projeto está sob a licença **MIT**. Veja [LICENSE](LICENSE).

## 👨‍💻 Autor

**Paulo Rabelo**
- GitHub: [@paulorabelo](https://github.com/paulorabelo)
- Blog: [blog.paulorabelo.dev.com.br](https://blog.paulorabelo.dev.com.br)
- LinkedIn: [Paulo Rabelo](https://www.linkedin.com/in/paulorabelooficial/)

---

*Desenvolvido durante a Santander Dev Week como parte do projeto de tela de cotações de ações.*
