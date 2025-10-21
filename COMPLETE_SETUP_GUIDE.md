# Guia Completo: Setup e Deployment do Portfólio

Este guia fornece instruções passo a passo para configurar, testar e fazer deploy do seu portfólio completo.

## Índice

1. [Pré-requisitos](#pré-requisitos)
2. [Estrutura do Projeto](#estrutura-do-projeto)
3. [Setup Local](#setup-local)
4. [Configuração do Supabase](#configuração-do-supabase)
5. [Executar Localmente](#executar-localmente)
6. [Testes](#testes)
7. [Deployment](#deployment)
8. [Troubleshooting](#troubleshooting)

---

## Pré-requisitos

Antes de começar, certifique-se de ter instalado:

- **Node.js** (v16+): [https://nodejs.org/](https://nodejs.org/)
- **Python** (v3.8+): [https://www.python.org/](https://www.python.org/)
- **Git**: [https://git-scm.com/](https://git-scm.com/)
- **npm** ou **pnpm**: Gerenciador de pacotes (npm vem com Node.js)
- **Conta Supabase**: [https://supabase.com](https://supabase.com)

### Verificar Instalação

```bash
# Verificar Node.js
node --version
npm --version

# Verificar Python
python3 --version

# Verificar Git
git --version
```

---

## Estrutura do Projeto

Seu projeto está organizado em dois repositórios principais:

```
portfolio/
├── portfolio-frontend/          # React + Tailwind CSS
│   ├── client/
│   │   ├── src/
│   │   │   ├── components/     # Componentes React
│   │   │   ├── pages/          # Páginas
│   │   │   ├── App.tsx
│   │   │   └── main.tsx
│   │   ├── public/             # Assets estáticos
│   │   └── package.json
│   └── vite.config.ts
│
└── portfolio-backend/           # Flask + Supabase
    ├── app.py                   # API principal
    ├── admin.py                 # Interface CRUD
    ├── requirements.txt         # Dependências Python
    ├── templates/               # Templates HTML
    ├── static/                  # CSS e JavaScript
    └── .env.example
```

---

## Setup Local

### Passo 1: Clonar ou Preparar o Projeto

Se você recebeu o projeto como arquivos:

```bash
# Criar diretório do projeto
mkdir portfolio
cd portfolio

# Os arquivos já devem estar nos diretórios:
# - portfolio-frontend/
# - portfolio-backend/
```

Se estiver usando Git:

```bash
git clone <seu-repositorio-frontend> portfolio-frontend
git clone <seu-repositorio-backend> portfolio-backend
```

### Passo 2: Setup do Frontend

```bash
cd portfolio-frontend

# Instalar dependências
npm install --legacy-peer-deps
# ou
pnpm install

# Criar arquivo .env.local
cp .env.example .env.local
```

Edite `.env.local`:

```env
VITE_SUPABASE_URL=https://seu-projeto.supabase.co
VITE_SUPABASE_ANON_KEY=sua-chave-anon-public
VITE_API_URL=http://localhost:5000
```

### Passo 3: Setup do Backend

```bash
cd ../portfolio-backend

# Criar ambiente virtual Python
python -m venv venv

# Ativar ambiente virtual
# No Linux/Mac:
source venv/bin/activate
# No Windows (Git Bash):
source venv/Scripts/activate
# No Windows (Command Prompt):
venv\Scripts\activate

# IMPORTANTE: Verificar se está no ambiente virtual correto
# Você deve ver (venv) no início do prompt
which python  # Deve mostrar o caminho para venv/Scripts/python
python --version

# Instalar dependências (certifique-se que está no ambiente virtual)
pip install -r requirements.txt

# Criar arquivo .env (se não existir)
cp .env.example .env
# Ou no Windows:
# copy .env.example .env
```

**⚠️ Importante:** Sempre verifique se você está no ambiente virtual antes de executar comandos Python. O prompt deve mostrar `(venv)` no início.

Edite `.env`:

```env
SUPABASE_URL=https://seu-projeto.supabase.co
SUPABASE_KEY=sua-chave-service-role-secret
ADMIN_PASSWORD=escolha-uma-senha-segura
FLASK_ENV=development
FLASK_DEBUG=True
```

---

## Configuração do Supabase

Siga o guia detalhado em `SUPABASE_SETUP_GUIDE.md` para:

1. Criar conta e projeto no Supabase
2. Criar as tabelas (`projetos`, `certificados`, `visitas`)
3. Obter as credenciais de API
4. Adicionar dados de teste

---

## Executar Localmente

### Terminal 1: Backend

```bash
cd portfolio-backend

# Ativar ambiente virtual (se não estiver ativado)
# No Linux/Mac:
source venv/bin/activate
# No Windows (Git Bash):
source venv/Scripts/activate
# No Windows (Command Prompt):
venv/Scripts/activate

# IMPORTANTE: Verificar se está no ambiente virtual
# Você deve ver (venv) no início do prompt

# Iniciar servidor Flask
python app.py

# Saída esperada:
# * Serving Flask app 'app'
# * Debug mode: on
# * Running on http://127.0.0.1:5000
```

### Terminal 2: Admin Interface (Opcional)

```bash
cd portfolio-backend

# Ativar ambiente virtual
# No Linux/Mac:
source venv/bin/activate
# No Windows (Git Bash):
source venv/Scripts/activate

# Iniciar interface CRUD
python admin.py

# Saída esperada:
# * Running on http://127.0.0.1:5001
```

Acesse: `http://localhost:5001/admin`

### Terminal 3: Frontend

```bash
cd portfolio-frontend

# Iniciar servidor de desenvolvimento
npm run dev
# ou
pnpm dev

# Saída esperada:
# ➜  Local:   http://localhost:3000/
```

Acesse: `http://localhost:3000`

---

## Testes

### Testar API com curl

```bash
# Health check
curl http://localhost:5000/health

# Obter todos os projetos
curl http://localhost:5000/api/projetos

# Criar um projeto (requer autenticação)
curl -X POST http://localhost:5000/api/projetos \
  -H "Authorization: Bearer sua_senha_admin" \
  -H "Content-Type: application/json" \
  -d '{
    "titulo": "Teste",
    "descricao": "Projeto de teste",
    "tecnologias": "React, Node.js"
  }'

# Obter contador de visitas
curl http://localhost:5000/api/visitas

# Incrementar visitas
curl -X POST http://localhost:5000/api/visitas
```

### Testar Frontend

1. Abra `http://localhost:3000` no navegador
2. Verifique se todas as seções carregam corretamente
3. Teste os links de navegação
4. Verifique se os projetos e certificados aparecem (se tiver adicionado dados)
5. Teste o formulário de contato

### Testar Admin Interface

1. Acesse `http://localhost:5001/admin`
2. Faça login com a senha configurada
3. Teste CRUD de projetos e certificados
4. Verifique se os dados aparecem no frontend

---

## Deployment

### Deploy do Frontend (Vercel)

**Opção 1: Via GitHub**

1. Faça push do código para GitHub
2. Acesse [https://vercel.com](https://vercel.com) e faça login
3. Clique em "New Project"
4. Selecione seu repositório `portfolio-frontend`
5. Configure as variáveis de ambiente:
   - `VITE_SUPABASE_URL`
   - `VITE_SUPABASE_ANON_KEY`
   - `VITE_API_URL` (URL do seu backend em produção)
6. Clique em "Deploy"

**Opção 2: Via Netlify**

1. Acesse [https://netlify.com](https://netlify.com) e faça login
2. Clique em "Add new site" → "Import an existing project"
3. Conecte seu GitHub
4. Selecione o repositório
5. Configure:
   - Build command: `npm run build`
   - Publish directory: `dist`
   - Variáveis de ambiente (conforme acima)
6. Clique em "Deploy site"

### Deploy do Backend (Render)

1. Acesse [https://render.com](https://render.com) e faça login
2. Clique em "New +" → "Web Service"
3. Conecte seu GitHub
4. Selecione o repositório `portfolio-backend`
5. Configure:
   - **Name**: `portfolio-api`
   - **Runtime**: `Python 3`
   - **Build Command**: `pip install -r requirements.txt`
   - **Start Command**: `gunicorn -w 4 -b 0.0.0.0:$PORT app:app`
6. Adicione variáveis de ambiente:
   - `SUPABASE_URL`
   - `SUPABASE_KEY`
   - `ADMIN_PASSWORD`
   - `FLASK_ENV=production`
7. Clique em "Create Web Service"

### Deploy do Backend (Railway)

1. Acesse [https://railway.app](https://railway.app) e faça login
2. Clique em "New Project"
3. Selecione "Deploy from GitHub"
4. Conecte seu GitHub e selecione o repositório
5. Configure as variáveis de ambiente
6. Railway detectará automaticamente que é um projeto Python
7. Clique em "Deploy"

### Atualizar URL da API no Frontend

Após fazer deploy do backend, atualize a variável `VITE_API_URL` no frontend com a URL de produção:

```env
VITE_API_URL=https://seu-backend.onrender.com
```

---

## Variáveis de Ambiente

### Frontend (.env.local)

| Variável | Descrição | Exemplo |
|----------|-----------|---------|
| `VITE_SUPABASE_URL` | URL do projeto Supabase | `https://xxxxx.supabase.co` |
| `VITE_SUPABASE_ANON_KEY` | Chave pública do Supabase | `eyJhbGc...` |
| `VITE_API_URL` | URL da API backend | `http://localhost:5000` |

### Backend (.env)

| Variável | Descrição | Exemplo |
|----------|-----------|---------|
| `SUPABASE_URL` | URL do projeto Supabase | `https://xxxxx.supabase.co` |
| `SUPABASE_KEY` | Chave service_role do Supabase | `eyJhbGc...` |
| `ADMIN_PASSWORD` | Senha para operações admin | `senha_segura_123` |
| `FLASK_ENV` | Ambiente (development/production) | `production` |
| `FLASK_DEBUG` | Ativar modo debug | `False` |

---

## Personalização

### Alterar Cores

Edite `portfolio-frontend/client/src/index.css`:

```css
:root {
  --primary: #003366;  /* Azul escuro */
  --secondary: #666666; /* Cinza */
  /* ... outras cores ... */
}
```

### Alterar Fontes

Edite `portfolio-frontend/client/src/index.css`:

```css
@import url('https://fonts.googleapis.com/css2?family=Lora:wght@400;700&family=Inter:wght@400;500;600;700&display=swap');

body {
  font-family: 'Inter', sans-serif;
}

h1, h2, h3 {
  font-family: 'Lora', serif;
}
```

### Alterar Informações Pessoais

Edite os componentes:

- **Nome**: `portfolio-frontend/client/src/components/HeroSection.tsx`
- **Sobre Mim**: `portfolio-frontend/client/src/components/AboutSection.tsx`
- **Links Sociais**: Atualize URLs em `AboutSection.tsx` e `Footer.tsx`

---

## Troubleshooting

### Erro: "ModuleNotFoundError: No module named 'flask'"

**Problema:** Você não está no ambiente virtual correto ou as dependências não foram instaladas.

**Solução:**
```bash
# 1. Ativar o ambiente virtual
cd portfolio-backend
source venv/Scripts/activate  # Git Bash no Windows
# ou
venv\Scripts\activate        # Command Prompt no Windows

# 2. Verificar se está no ambiente correto
which python  # Deve mostrar caminho para venv/Scripts/python
python --version

# 3. Instalar dependências
pip install -r requirements.txt

# 4. Executar o app
python app.py
```

### Erro: "Cannot find module"

**Solução:**
```bash
# Reinstalar dependências
npm install
# ou
pip install -r requirements.txt
```

### Erro: "CORS error"

**Solução:**
- Verifique se o backend está rodando
- Confirme que `VITE_API_URL` está correto
- Verifique se CORS está habilitado no backend

### Erro: "Connection refused"

**Solução:**
- Certifique-se de que backend está rodando: `python app.py`
- Verifique se as credenciais do Supabase estão corretas

### Erro: "Invalid API Key"

**Problema:** A chave do Supabase está incorreta ou mal formatada.

**Solução:**
1. Acesse seu projeto no [Supabase](https://supabase.com)
2. Vá em "Settings" → "API"
3. Copie a chave **"service_role"** (não a "anon public")
4. Substitua no arquivo `.env`:
```env
SUPABASE_KEY=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...
```
- Certifique-se de que não há espaços extras

### Erro: "Table does not exist"

**Solução:**
- Verifique se as tabelas foram criadas no Supabase
- Consulte `SUPABASE_SETUP_GUIDE.md`

### Erro: "bash: venvScriptsactivate: command not found"

**Problema:** Você está usando barras invertidas em bash.

**Solução:**
```bash
# Use barras normais no Git Bash
source venv/Scripts/activate
# NÃO use: venv\Scripts\activate
```

---

## Próximos Passos

1. **Adicionar dados reais**: Use a interface CRUD para adicionar seus projetos e certificados
2. **Customizar design**: Altere cores, fontes e layout conforme desejar
3. **Adicionar mais funcionalidades**: Implemente novas seções ou recursos
4. **Otimizar performance**: Adicione caching, lazy loading, etc.
5. **Configurar domínio customizado**: Aponte seu domínio para o frontend
6. **Implementar analytics**: Adicione Google Analytics ou similar

---

## Suporte e Recursos

- **Documentação React**: [https://react.dev](https://react.dev)
- **Documentação Tailwind CSS**: [https://tailwindcss.com](https://tailwindcss.com)
- **Documentação Flask**: [https://flask.palletsprojects.com](https://flask.palletsprojects.com)
- **Documentação Supabase**: [https://supabase.com/docs](https://supabase.com/docs)
- **Documentação Vercel**: [https://vercel.com/docs](https://vercel.com/docs)
- **Documentação Render**: [https://render.com/docs](https://render.com/docs)

---

**Parabéns! Seu portfólio está pronto para o mundo! 🚀**

