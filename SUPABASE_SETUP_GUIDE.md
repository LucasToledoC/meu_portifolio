# Guia Completo: Configuração do Supabase para o Portfólio

Este guia fornece instruções passo a passo para configurar o Supabase, criar as tabelas necessárias e obter as credenciais para integração com o backend Flask.

## Pré-requisitos

- Uma conta de email válida
- Acesso à internet
- Navegador web moderno (Chrome, Firefox, Safari, Edge)

## Passo 1: Criar uma Conta no Supabase

1. Acesse [https://supabase.com](https://supabase.com)
2. Clique no botão **"Start your project"** ou **"Sign Up"**
3. Escolha uma opção de login:
   - **GitHub** (recomendado para desenvolvedores)
   - **Google**
   - **Email e Senha**
4. Siga o processo de autenticação
5. Verifique seu email se necessário

## Passo 2: Criar um Novo Projeto

1. Após fazer login, você será levado ao dashboard do Supabase
2. Clique no botão **"New Project"** ou **"Create a new project"**
3. Preencha os detalhes do projeto:
   - **Project Name**: `portfolio` (ou outro nome de sua preferência)
   - **Database Password**: Crie uma senha forte (você precisará dela)
   - **Region**: Escolha a região mais próxima de você (ex: `South America (São Paulo)` para Brasil)
   - **Pricing Plan**: Selecione **Free** para começar

4. Clique em **"Create new project"** e aguarde a criação (pode levar alguns minutos)

## Passo 3: Acessar o Painel de Controle do Projeto

1. Quando o projeto estiver pronto, você será redirecionado para o painel
2. No menu lateral esquerdo, você verá várias opções:
   - **Home**
   - **SQL Editor**
   - **Table Editor**
   - **Auth**
   - **Storage**
   - **Realtime**
   - **Settings**

## Passo 4: Criar as Tabelas do Banco de Dados

Você tem duas opções para criar as tabelas: usando o **SQL Editor** (recomendado) ou o **Table Editor**.

### Opção A: Usando o SQL Editor (Recomendado)

1. No menu lateral, clique em **"SQL Editor"**
2. Clique no botão **"New Query"** ou **"+"**
3. Cole o seguinte código SQL:

```sql
-- Criar tabela de projetos
CREATE TABLE projetos (
  id BIGINT PRIMARY KEY GENERATED ALWAYS AS IDENTITY,
  titulo VARCHAR(255) NOT NULL,
  descricao TEXT NOT NULL,
  tecnologias TEXT NOT NULL,
  link_github VARCHAR(255),
  link_deploy VARCHAR(255),
  created_at TIMESTAMP DEFAULT NOW(),
  updated_at TIMESTAMP DEFAULT NOW()
);

-- Criar tabela de certificados
CREATE TABLE certificados (
  id BIGINT PRIMARY KEY GENERATED ALWAYS AS IDENTITY,
  nome VARCHAR(255) NOT NULL,
  instituicao VARCHAR(255) NOT NULL,
  origem VARCHAR(100),
  data_conclusao DATE NOT NULL,
  link_certificado VARCHAR(255),
  created_at TIMESTAMP DEFAULT NOW(),
  updated_at TIMESTAMP DEFAULT NOW()
);

-- Criar tabela de visitas
CREATE TABLE visitas (
  id BIGINT PRIMARY KEY GENERATED ALWAYS AS IDENTITY,
  total BIGINT DEFAULT 0,
  created_at TIMESTAMP DEFAULT NOW(),
  updated_at TIMESTAMP DEFAULT NOW()
);

-- Inserir um registro inicial na tabela de visitas
INSERT INTO visitas (total) VALUES (0);
```

4. Clique no botão **"Run"** (ou pressione `Ctrl+Enter`)
5. Você verá uma mensagem de sucesso confirmando a criação das tabelas

### Opção B: Usando o Table Editor

Se preferir uma abordagem visual:

1. No menu lateral, clique em **"Table Editor"**
2. Clique no botão **"Create a new table"**
3. Para cada tabela (projetos, certificados, visitas), preencha:
   - **Table Name**: Nome da tabela
   - **Columns**: Adicione as colunas conforme especificado abaixo

**Tabela: projetos**
| Coluna | Tipo | Obrigatório | Padrão |
|--------|------|-------------|--------|
| id | bigint | Sim | Auto-incremento |
| titulo | varchar(255) | Sim | - |
| descricao | text | Sim | - |
| tecnologias | text | Sim | - |
| link_github | varchar(255) | Não | - |
| link_deploy | varchar(255) | Não | - |
| created_at | timestamp | Não | now() |
| updated_at | timestamp | Não | now() |

**Tabela: certificados**
| Coluna | Tipo | Obrigatório | Padrão |
|--------|------|-------------|--------|
| id | bigint | Sim | Auto-incremento |
| nome | varchar(255) | Sim | - |
| instituicao | varchar(255) | Sim | - |
| origem | varchar(100) | Não | - |
| data_conclusao | date | Sim | - |
| link_certificado | varchar(255) | Não | - |
| created_at | timestamp | Não | now() |
| updated_at | timestamp | Não | now() |

**Tabela: visitas**
| Coluna | Tipo | Obrigatório | Padrão |
|--------|------|-------------|--------|
| id | bigint | Sim | Auto-incremento |
| total | bigint | Não | 0 |
| created_at | timestamp | Não | now() |
| updated_at | timestamp | Não | now() |

## Passo 5: Obter as Credenciais de API

1. No menu lateral, clique em **"Settings"** (ícone de engrenagem)
2. Clique em **"API"**
3. Você verá duas informações importantes:
   - **Project URL**: Copie este valor (será seu `SUPABASE_URL`)
   - **API Keys**: Você verá várias chaves:
     - **anon public**: Use esta para o frontend
     - **service_role secret**: Use esta para o backend (mantenha segura!)

4. Copie o **Project URL** e a chave **service_role secret**
5. Guarde estas informações em um local seguro

## Passo 6: Configurar o Arquivo .env do Backend

1. No diretório `portfolio-backend`, abra o arquivo `.env` (ou crie um baseado em `.env.example`)
2. Preencha com as credenciais obtidas:

```
SUPABASE_URL=https://seu-projeto.supabase.co
SUPABASE_KEY=sua-chave-service-role-secret-aqui
ADMIN_PASSWORD=escolha-uma-senha-segura
FLASK_ENV=development
FLASK_DEBUG=True
```

## Passo 7: Configurar o Arquivo .env do Frontend

1. No diretório `portfolio-frontend`, crie um arquivo `.env.local`
2. Adicione as credenciais do Supabase (use a chave `anon public` para o frontend):

```
VITE_SUPABASE_URL=https://seu-projeto.supabase.co
VITE_SUPABASE_ANON_KEY=sua-chave-anon-public-aqui
VITE_API_URL=http://localhost:5000
```

## Passo 8: Testar a Conexão

### Teste 1: Verificar Tabelas no Supabase

1. Volte ao painel do Supabase
2. Clique em **"Table Editor"**
3. Você deve ver as três tabelas criadas: `projetos`, `certificados`, `visitas`
4. Clique em cada uma para verificar se as colunas estão corretas

### Teste 2: Testar a API do Backend

1. Abra um terminal e navegue até `portfolio-backend`
2. Ative o ambiente virtual: `source venv/bin/activate` (ou `venv\Scripts\activate` no Windows)
3. Inicie o servidor Flask: `python app.py`
4. Abra outro terminal e teste um endpoint:

```bash
# Teste GET /api/projetos
curl http://localhost:5000/api/projetos

# Você deve receber uma resposta JSON vazia: []
```

## Passo 9: Adicionar Dados de Teste (Opcional)

Para testar o frontend com dados reais, você pode adicionar alguns projetos e certificados de teste:

### Adicionar um Projeto de Teste

```bash
curl -X POST http://localhost:5000/api/projetos \
  -H "Authorization: Bearer sua_admin_password" \
  -H "Content-Type: application/json" \
  -d '{
    "titulo": "Portfólio Pessoal",
    "descricao": "Um site de portfólio moderno e minimalista",
    "tecnologias": "React, Tailwind CSS, Flask, Supabase",
    "link_github": "https://github.com/LucasToledoC/portfolio",
    "link_deploy": "https://portfolio.com"
  }'
```

### Adicionar um Certificado de Teste

```bash
curl -X POST http://localhost:5000/api/certificados \
  -H "Authorization: Bearer sua_admin_password" \
  -H "Content-Type: application/json" \
  -d '{
    "nome": "Engenharia de Software",
    "instituicao": "FIAP",
    "origem": "FIAP",
    "data_conclusao": "2028-12-31"
  }'
```

## Segurança: Boas Práticas

1. **Nunca compartilhe suas credenciais**: Mantenha o arquivo `.env` seguro e não o commite no Git
2. **Use a chave correta**: Use `service_role secret` apenas no backend; use `anon public` no frontend
3. **Altere a senha do admin**: Não use a senha padrão em produção
4. **Ative autenticação no Supabase**: Considere adicionar Row Level Security (RLS) para proteger suas tabelas
5. **Faça backup regularmente**: Supabase oferece backups automáticos no plano pago

## Troubleshooting

### Erro: "Invalid API Key"
- Verifique se você copiou a chave correta (service_role secret para backend)
- Certifique-se de que não há espaços extras

### Erro: "Table does not exist"
- Verifique se as tabelas foram criadas corretamente no SQL Editor
- Tente recarregar a página do Supabase

### Erro: "CORS error"
- Certifique-se de que o backend tem CORS habilitado (já está no código)
- Verifique se o `VITE_API_URL` no frontend está correto

### Erro: "Connection refused"
- Verifique se o backend está rodando: `python app.py`
- Certifique-se de que as credenciais do Supabase estão corretas no `.env`

## Próximos Passos

1. Teste a API com ferramentas como Postman ou Insomnia
2. Configure o frontend React para consumir a API
3. Implemente a interface de administração (CRUD)
4. Faça deploy do backend em plataformas como Render ou Railway
5. Faça deploy do frontend em Vercel ou Netlify

## Referências

- [Documentação do Supabase](https://supabase.com/docs)
- [Guia de Início Rápido do Supabase](https://supabase.com/docs/guides/getting-started)
- [Supabase Python Client](https://supabase.com/docs/reference/python/introduction)

---

**Nota**: Este guia foi criado para ajudar na configuração inicial. Para mais detalhes, consulte a documentação oficial do Supabase.

