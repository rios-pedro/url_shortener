# 🔗 URL Shortener

REST API para encurtar URL's em Base62

## 🚀 Tecnologias

- Java 17
- Spring Boot
- Spring Data JPA
- PostgreSQL
- SpringDoc OpenAPI (Swagger)
- Lombok
- Bean Validation

## 📋 Funcionalidades

- Listar todos os contatos ativos
- Buscar contato por ID
- Criar novo contato (com validação de idade mínima de 18 anos)
- Atualizar contato (incluindo ativação/desativação)
- Deletar contato

🏗️ Arquitetura

lient → POST /api/urls → Gera hash curto → Salva no PostgreSQL
Client → GET /{hash}   → Busca no banco → Incrementa contador → Redirect 302

## 🗂️ Estrutura do Projeto

```
com.seuapp.urlshortener
├── controller/
│   └── UrlController.java
├── service/
│   └── UrlService.java
├── repository/
│   └── UrlRepository.java
├── model/
│   └── Url.java
├── dto/
│   ├── CreateUrlRequest.java
│   └── CreateUrlResponse.java
└── exception/
    └── UrlNotFoundException.java
```

## ⚙️ Configuração

### Pré-requisitos

- Java 17+
- Maven

## 📖 Documentação da API

Com a aplicação rodando, acesse o Swagger em:

```
http://localhost:8080/swagger-ui.html
```

## 🔗 Endpoints

| Método | Rota | Descrição |
|--------|------|-----------|
| PUT | `/contacts/{id}` | Atualiza um contato |
| GET | `/{shortCode}` | Redireciona para a URL original |
| GET | `/api/urls/{shortCode}/stats` | Retorna métricas de acesso |

## ✅ Regras de negócio

– O shortCode será gerado com Base62 (a-z, A-Z, 0-9) com 6 caracteres
– Se a mesma URL longa já existir no banco, retorna o código existente (idempotência)
– Acesso a um código inexistente retorna 404 com mensagem clara
– O contador de acessos é incrementado a cada redirecionamento

## 👤 Autor

Pedro Rios — [@rios-pedro](https://github.com/rios-pedro)
