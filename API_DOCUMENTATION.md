# Documentação da API - Portfólio

## Visão Geral

A API do Portfólio é uma REST API desenvolvida em Flask que fornece endpoints para gerenciar projetos, certificados e rastrear visitas ao portfólio. A API utiliza autenticação baseada em token (Bearer Token) para operações protegidas.

## Base URL

```
http://localhost:5000
```

Em produção, substitua `localhost:5000` pela URL do seu servidor.

## Autenticação

Endpoints protegidos requerem um header `Authorization` com o formato:

```
Authorization: Bearer <admin_password>
```

**Exemplo com curl:**
```bash
curl -X POST http://localhost:5000/api/projetos \
  -H "Authorization: Bearer sua_senha_admin" \
  -H "Content-Type: application/json" \
  -d '{"titulo": "Meu Projeto", ...}'
```

## Endpoints

### Health Check

#### GET /health

Verifica se a API está rodando.

**Resposta (200 OK):**
```json
{
  "status": "ok",
  "message": "Portfolio API is running"
}
```

---

### Projetos

#### GET /api/projetos

Recupera todos os projetos.

**Resposta (200 OK):**
```json
[
  {
    "id": 1,
    "titulo": "Portfólio Pessoal",
    "descricao": "Um site de portfólio moderno e minimalista",
    "tecnologias": "React, Tailwind CSS, Flask",
    "link_github": "https://github.com/...",
    "link_deploy": "https://portfolio.com",
    "created_at": "2025-01-15T10:30:00",
    "updated_at": "2025-01-15T10:30:00"
  }
]
```

---

#### POST /api/projetos

Cria um novo projeto. **Requer autenticação.**

**Headers:**
```
Authorization: Bearer <admin_password>
Content-Type: application/json
```

**Body (obrigatório):**
```json
{
  "titulo": "Meu Projeto",
  "descricao": "Descrição do projeto",
  "tecnologias": "React, Node.js",
  "link_github": "https://github.com/...",
  "link_deploy": "https://..."
}
```

**Campos obrigatórios:**
- `titulo` (string, max 255 caracteres)
- `descricao` (string)
- `tecnologias` (string)

**Campos opcionais:**
- `link_github` (URL)
- `link_deploy` (URL)

**Resposta (201 Created):**
```json
[
  {
    "id": 2,
    "titulo": "Meu Projeto",
    "descricao": "Descrição do projeto",
    "tecnologias": "React, Node.js",
    "link_github": "https://github.com/...",
    "link_deploy": "https://...",
    "created_at": "2025-01-15T10:35:00",
    "updated_at": "2025-01-15T10:35:00"
  }
]
```

**Erros:**
- 400 Bad Request: Campos obrigatórios faltando
- 401 Unauthorized: Senha incorreta ou faltando
- 500 Internal Server Error: Erro no servidor

---

#### GET /api/projetos/{id}

Recupera um projeto específico.

**Resposta (200 OK):**
```json
{
  "id": 1,
  "titulo": "Portfólio Pessoal",
  "descricao": "Um site de portfólio moderno e minimalista",
  "tecnologias": "React, Tailwind CSS, Flask",
  "link_github": "https://github.com/...",
  "link_deploy": "https://portfolio.com",
  "created_at": "2025-01-15T10:30:00",
  "updated_at": "2025-01-15T10:30:00"
}
```

**Erros:**
- 404 Not Found: Projeto não encontrado

---

#### PUT /api/projetos/{id}

Atualiza um projeto. **Requer autenticação.**

**Headers:**
```
Authorization: Bearer <admin_password>
Content-Type: application/json
```

**Body:**
```json
{
  "titulo": "Novo Título",
  "descricao": "Nova descrição",
  "tecnologias": "React, Node.js, MongoDB"
}
```

**Resposta (200 OK):**
```json
{
  "id": 1,
  "titulo": "Novo Título",
  "descricao": "Nova descrição",
  "tecnologias": "React, Node.js, MongoDB",
  "link_github": "https://github.com/...",
  "link_deploy": "https://portfolio.com",
  "created_at": "2025-01-15T10:30:00",
  "updated_at": "2025-01-15T10:40:00"
}
```

---

#### DELETE /api/projetos/{id}

Deleta um projeto. **Requer autenticação.**

**Headers:**
```
Authorization: Bearer <admin_password>
```

**Resposta (200 OK):**
```json
{
  "message": "Project deleted successfully"
}
```

---

### Certificados

#### GET /api/certificados

Recupera todos os certificados. Suporta filtro por origem.

**Query Parameters:**
- `origem` (opcional): Filtra por origem (ex: "FIAP", "Alura")

**Exemplos:**
```
GET /api/certificados
GET /api/certificados?origem=FIAP
```

**Resposta (200 OK):**
```json
[
  {
    "id": 1,
    "nome": "Engenharia de Software",
    "instituicao": "FIAP",
    "origem": "FIAP",
    "data_conclusao": "2028-12-31",
    "link_certificado": "https://...",
    "created_at": "2025-01-15T10:30:00",
    "updated_at": "2025-01-15T10:30:00"
  }
]
```

---

#### POST /api/certificados

Cria um novo certificado. **Requer autenticação.**

**Headers:**
```
Authorization: Bearer <admin_password>
Content-Type: application/json
```

**Body (obrigatório):**
```json
{
  "nome": "Curso de React",
  "instituicao": "Alura",
  "origem": "Alura",
  "data_conclusao": "2025-01-15",
  "link_certificado": "https://..."
}
```

**Campos obrigatórios:**
- `nome` (string, max 255 caracteres)
- `instituicao` (string, max 255 caracteres)
- `data_conclusao` (date, formato: YYYY-MM-DD)

**Campos opcionais:**
- `origem` (string, max 100 caracteres)
- `link_certificado` (URL)

**Resposta (201 Created):**
```json
[
  {
    "id": 2,
    "nome": "Curso de React",
    "instituicao": "Alura",
    "origem": "Alura",
    "data_conclusao": "2025-01-15",
    "link_certificado": "https://...",
    "created_at": "2025-01-15T10:35:00",
    "updated_at": "2025-01-15T10:35:00"
  }
]
```

---

#### GET /api/certificados/{id}

Recupera um certificado específico.

**Resposta (200 OK):**
```json
{
  "id": 1,
  "nome": "Engenharia de Software",
  "instituicao": "FIAP",
  "origem": "FIAP",
  "data_conclusao": "2028-12-31",
  "link_certificado": "https://...",
  "created_at": "2025-01-15T10:30:00",
  "updated_at": "2025-01-15T10:30:00"
}
```

---

#### PUT /api/certificados/{id}

Atualiza um certificado. **Requer autenticação.**

**Headers:**
```
Authorization: Bearer <admin_password>
Content-Type: application/json
```

**Body:**
```json
{
  "nome": "Novo Nome",
  "instituicao": "Nova Instituição"
}
```

**Resposta (200 OK):**
```json
{
  "id": 1,
  "nome": "Novo Nome",
  "instituicao": "Nova Instituição",
  "origem": "FIAP",
  "data_conclusao": "2028-12-31",
  "link_certificado": "https://...",
  "created_at": "2025-01-15T10:30:00",
  "updated_at": "2025-01-15T10:45:00"
}
```

---

#### DELETE /api/certificados/{id}

Deleta um certificado. **Requer autenticação.**

**Headers:**
```
Authorization: Bearer <admin_password>
```

**Resposta (200 OK):**
```json
{
  "message": "Certificate deleted successfully"
}
```

---

### Visitas

#### GET /api/visitas

Recupera o número total de visitas.

**Resposta (200 OK):**
```json
{
  "total": 42
}
```

---

#### POST /api/visitas

Incrementa o contador de visitas. **Sem autenticação necessária.**

**Resposta (200 OK):**
```json
{
  "total": 43
}
```

---

## Códigos de Status HTTP

| Código | Significado |
|--------|-------------|
| 200 | OK - Requisição bem-sucedida |
| 201 | Created - Recurso criado com sucesso |
| 400 | Bad Request - Requisição inválida |
| 401 | Unauthorized - Autenticação falhou |
| 404 | Not Found - Recurso não encontrado |
| 500 | Internal Server Error - Erro no servidor |

---

## Exemplos de Uso

### Criar um Projeto com curl

```bash
curl -X POST http://localhost:5000/api/projetos \
  -H "Authorization: Bearer admin123" \
  -H "Content-Type: application/json" \
  -d '{
    "titulo": "E-commerce Platform",
    "descricao": "Uma plataforma de e-commerce completa com React e Node.js",
    "tecnologias": "React, Node.js, MongoDB, Stripe",
    "link_github": "https://github.com/LucasToledoC/ecommerce",
    "link_deploy": "https://ecommerce.com"
  }'
```

### Obter Certificados da FIAP

```bash
curl http://localhost:5000/api/certificados?origem=FIAP
```

### Incrementar Contador de Visitas

```bash
curl -X POST http://localhost:5000/api/visitas
```

---

## CORS

A API tem CORS habilitado para permitir requisições do frontend. Os seguintes headers são permitidos:

```
Access-Control-Allow-Origin: *
Access-Control-Allow-Methods: GET, POST, PUT, DELETE, OPTIONS
Access-Control-Allow-Headers: Content-Type, Authorization
```

---

## Rate Limiting

Não há rate limiting implementado por padrão. Para produção, considere adicionar rate limiting usando bibliotecas como `Flask-Limiter`.

---

## Segurança

### Recomendações para Produção

1. **Use HTTPS**: Sempre use HTTPS em produção
2. **Altere a senha padrão**: Não use "admin123" em produção
3. **Use variáveis de ambiente**: Armazene senhas em `.env`, nunca no código
4. **Implemente Rate Limiting**: Proteja contra brute force
5. **Validação de entrada**: Valide todos os dados de entrada
6. **CORS restritivo**: Especifique apenas os domínios permitidos
7. **Logging e monitoramento**: Implemente logging adequado

---

## Suporte

Para dúvidas ou problemas, consulte a documentação do Flask ou abra uma issue no repositório.

