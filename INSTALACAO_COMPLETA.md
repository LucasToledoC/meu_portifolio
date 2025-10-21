# 🚀 Guia Completo de Instalação - Portfólio na Sua Máquina

Este é um guia passo a passo para você baixar e configurar o portfólio completo na sua máquina local.

---

## 📋 Pré-requisitos (Instale Primeiro!)

Você precisa ter instalado na sua máquina:

### 1. **Node.js** (inclui npm)
- Acesse: https://nodejs.org/
- Baixe a versão **LTS** (recomendado)
- Instale normalmente
- Verifique no terminal:
  ```bash
  node --version
  npm --version
  ```

### 2. **Python 3.8+**
- Acesse: https://www.python.org/
- Baixe a versão 3.8 ou superior
- **IMPORTANTE**: Marque a opção "Add Python to PATH" durante a instalação
- Verifique no terminal:
  ```bash
  python --version
  # ou
  python3 --version
  ```

### 3. **Git** (opcional, mas recomendado)
- Acesse: https://git-scm.com/
- Instale normalmente
- Verifique no terminal:
  ```bash
  git --version
  ```

### 4. **Conta Supabase Gratuita**
- Acesse: https://supabase.com
- Clique em "Sign Up"
- Crie uma conta com seu email
- Crie um novo projeto

---

## 📥 Passo 1: Baixar os Arquivos do Projeto

### Opção A: Usando Git (Recomendado)

Se você recebeu links dos repositórios:

```bash
# Crie uma pasta para o projeto
mkdir meu-portfolio
cd meu-portfolio

# Clone o frontend
git clone <URL-DO-REPOSITORIO-FRONTEND> portfolio-frontend

# Clone o backend
git clone <URL-DO-REPOSITORIO-BACKEND> portfolio-backend
```

### Opção B: Baixando como ZIP

Se você recebeu os arquivos como ZIP:

1. Extraia os arquivos em uma pasta chamada `meu-portfolio`
2. Você deve ter duas pastas:
   - `portfolio-frontend/`
   - `portfolio-backend/`

---

## 🗄️ Passo 2: Configurar o Supabase (Banco de Dados)

Este é o passo **mais importante**! O Supabase armazena seus projetos e certificados.

### 2.1: Criar Tabelas no Supabase

1. Acesse https://supabase.com e faça login
2. Clique no seu projeto
3. No menu esquerdo, clique em **"SQL Editor"**
4. Clique em **"New Query"**
5. **Cole este código SQL inteiro**:

```sql
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

CREATE TABLE visitas (
  id BIGINT PRIMARY KEY GENERATED ALWAYS AS IDENTITY,
  total BIGINT DEFAULT 0,
  created_at TIMESTAMP DEFAULT NOW(),
  updated_at TIMESTAMP DEFAULT NOW()
);

INSERT INTO visitas (total) VALUES (0);
```

6. Clique em **"Run"** (botão azul)
7. Pronto! As tabelas foram criadas

### 2.2: Obter as Credenciais do Supabase

1. No menu esquerdo do Supabase, clique em **"Settings"**
2. Clique em **"API"**
3. Você verá:
   - **Project URL** → copie e guarde (será seu `SUPABASE_URL`)
   - **Project API keys** → procure por **"service_role secret"** → copie e guarde (será seu `SUPABASE_KEY`)

**Guarde esses valores! Você vai precisar deles.**

---

## ⚙️ Passo 3: Configurar o Backend (Flask)

### 3.1: Abrir Terminal na Pasta do Backend

```bash
# Navegue para a pasta do backend
cd portfolio-backend
```

### 3.2: Criar Ambiente Virtual Python

```bash
# Windows
python -m venv venv
venv\Scripts\activate

# Mac/Linux
python3 -m venv venv
source venv/bin/activate
```

Você saberá que funcionou quando aparecer `(venv)` no início da linha do terminal.

### 3.3: Instalar Dependências

```bash
pip install -r requirements.txt
```

Isso vai baixar todas as bibliotecas necessárias (pode levar alguns minutos).

### 3.4: Criar Arquivo .env

1. Na pasta `portfolio-backend`, crie um arquivo chamado `.env`
2. Abra com um editor de texto (Notepad, VS Code, etc.)
3. **Cole este conteúdo**:

```env
SUPABASE_URL=https://seu-projeto.supabase.co
SUPABASE_KEY=sua-chave-service-role-secret
ADMIN_PASSWORD=escolha-uma-senha-segura
FLASK_ENV=development
FLASK_DEBUG=True
```

4. **Substitua os valores**:
   - `https://seu-projeto.supabase.co` → Cole a URL do Supabase que você copiou
   - `sua-chave-service-role-secret` → Cole a chave do Supabase que você copiou
   - `escolha-uma-senha-segura` → Crie uma senha (ex: `minha-senha-123`)

5. **Salve o arquivo**

### 3.5: Testar o Backend

```bash
# Certifique-se de que o ambiente virtual está ativado (venv)
python app.py
```

Você deve ver algo como:
```
 * Running on http://127.0.0.1:5000
```

**Deixe este terminal aberto!** Você vai precisar dele rodando.

---

## ⚛️ Passo 4: Configurar o Frontend (React)

### 4.1: Abrir Novo Terminal na Pasta do Frontend

```bash
# Em um NOVO terminal (deixe o anterior aberto)
cd portfolio-frontend
```

### 4.2: Instalar Dependências

```bash
npm install
```

Isso vai baixar todas as bibliotecas do React (pode levar alguns minutos).

### 4.3: Criar Arquivo .env.local

1. Na pasta `portfolio-frontend`, crie um arquivo chamado `.env.local`
2. Abra com um editor de texto
3. **Cole este conteúdo**:

```env
VITE_SUPABASE_URL=https://seu-projeto.supabase.co
VITE_SUPABASE_ANON_KEY=sua-chave-anon-public
VITE_API_URL=http://localhost:5000
```

4. **Substitua os valores**:
   - `https://seu-projeto.supabase.co` → Cole a URL do Supabase
   - `sua-chave-anon-public` → Volte ao Supabase, em Settings → API, procure por **"anon public"** e copie
   - `http://localhost:5000` → Deixe como está (é o endereço do backend)

5. **Salve o arquivo**

### 4.4: Iniciar o Frontend

```bash
# Certifique-se de estar na pasta portfolio-frontend
npm run dev
```

Você deve ver algo como:
```
➜  Local:   http://localhost:3000/
```

---

## 🎉 Passo 5: Acessar o Portfólio

Agora você tem dois servidores rodando:

### Frontend (Portfólio)
- **URL**: http://localhost:3000
- Abra no navegador
- Você deve ver o portfólio com fundo preto

### Admin (Gerenciar Dados)
- **URL**: http://localhost:5001/admin
- Faça login com a senha que você criou no `.env`
- Aqui você pode adicionar projetos e certificados

---

## 📝 Passo 6: Adicionar Seus Dados

### Adicionar Projetos

1. Acesse http://localhost:5001/admin
2. Faça login com sua senha
3. Clique em "+ Novo Item"
4. Preencha:
   - **Título do Projeto**: Nome do seu projeto
   - **Descrição**: O que o projeto faz
   - **Tecnologias**: React, Node.js, MongoDB (separadas por vírgula)
   - **Link GitHub**: https://github.com/seu-usuario/seu-projeto
   - **Link Deploy**: https://seu-projeto.com
5. Clique em "Salvar Projeto"
6. Volte para http://localhost:3000 e veja seu projeto aparecer!

### Adicionar Certificados

1. No admin, clique em "Certificados"
2. Clique em "+ Novo Item"
3. Preencha:
   - **Nome do Curso**: Ex: "Engenharia de Software"
   - **Instituição**: Ex: "FIAP"
   - **Origem**: Selecione FIAP, Alura, etc.
   - **Data de Conclusão**: DD/MM/YYYY
   - **Link do Certificado**: URL do certificado (opcional)
4. Clique em "Salvar Certificado"

---

## 🛑 Parar os Servidores

Quando quiser parar:

1. **Backend**: No terminal do backend, pressione `Ctrl + C`
2. **Frontend**: No terminal do frontend, pressione `Ctrl + C`

---

## 🔄 Próxima Vez que Quiser Rodar

Você não precisa instalar tudo de novo! Apenas:

```bash
# Terminal 1 - Backend
cd portfolio-backend
source venv/bin/activate  # (ou venv\Scripts\activate no Windows)
python app.py

# Terminal 2 - Frontend
cd portfolio-frontend
npm run dev
```

---

## ❌ Troubleshooting (Problemas Comuns)

### Erro: "command not found: python"
- **Solução**: Python não está instalado ou não está no PATH
- Reinstale Python e marque "Add Python to PATH"

### Erro: "command not found: node"
- **Solução**: Node.js não está instalado
- Instale em https://nodejs.org/

### Erro: "Cannot find module"
```bash
# Solução:
npm install  # para frontend
pip install -r requirements.txt  # para backend
```

### Erro: "Connection refused" ou "Cannot connect to API"
- **Solução**: O backend não está rodando
- Certifique-se de que o terminal do backend está aberto e mostra "Running on http://127.0.0.1:5000"

### Erro: "Invalid API Key" ou "Table does not exist"
- **Solução**: Verifique se copiou as credenciais corretas do Supabase
- Verifique se criou as tabelas (Passo 2.1)

### Erro: "CORS error"
- **Solução**: O backend não está rodando ou `VITE_API_URL` está incorreto
- Verifique se é `http://localhost:5000` (sem barra no final)

### Porta 3000 ou 5000 já está em uso
```bash
# Mude a porta do frontend
npm run dev -- --port 3001

# Mude a porta do backend (edite app.py)
# Procure por: app.run(debug=True, port=5000)
# Mude para: app.run(debug=True, port=5001)
```

---

## 📚 Próximos Passos

### Personalizar o Portfólio

1. **Alterar nome/texto**: Edite os arquivos em `portfolio-frontend/client/src/components/`
2. **Alterar cores**: Edite `portfolio-frontend/client/src/index.css`
3. **Adicionar seu CV**: Coloque um arquivo `resume.pdf` em `portfolio-frontend/client/public/`

### Fazer Deploy (Colocar Online)

Quando quiser colocar seu portfólio na internet:

1. **Frontend**: Faça deploy em Vercel ou Netlify
2. **Backend**: Faça deploy em Render ou Railway
3. **Banco de Dados**: Supabase já está online

Veja `COMPLETE_SETUP_GUIDE.md` para instruções detalhadas.

---

## 💡 Dicas Importantes

1. **Guarde suas credenciais do Supabase**: Você vai precisar delas
2. **Não compartilhe o arquivo `.env`**: Contém senhas e chaves secretas
3. **Use senhas fortes**: Não use "123456" como senha de admin
4. **Deixe os terminais abertos**: Enquanto estiver desenvolvendo

---

## 📞 Precisa de Ajuda?

Se tiver problemas:

1. Verifique a seção "Troubleshooting" acima
2. Leia a documentação em `COMPLETE_SETUP_GUIDE.md`
3. Verifique se todos os pré-requisitos estão instalados
4. Tente fechar e abrir os terminais de novo

---

**Parabéns! Você está pronto para começar! 🎉**

Qualquer dúvida, consulte este guia ou os outros arquivos de documentação.

