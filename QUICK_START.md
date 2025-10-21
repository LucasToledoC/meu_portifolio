# Quick Start - Portfólio em 5 Minutos

Este guia rápido o ajudará a colocar seu portfólio funcionando em poucos minutos.

## Pré-requisitos Rápidos

Você precisa ter instalado:

- **Node.js** (com npm): [https://nodejs.org/](https://nodejs.org/)
- **Python 3.8+**: [https://www.python.org/](https://www.python.org/)
- **Uma conta Supabase gratuita**: [https://supabase.com](https://supabase.com)

## Passo 1: Configurar Supabase (2 minutos)

1. Crie uma conta em [https://supabase.com](https://supabase.com)
2. Crie um novo projeto
3. Vá para "SQL Editor" e execute este SQL:

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

4. Vá para Settings → API e copie:
   - **Project URL** (será seu `SUPABASE_URL`)
   - **service_role secret** (será seu `SUPABASE_KEY`)

## Passo 2: Configurar Backend (1 minuto)

```bash
cd portfolio-backend

# Criar ambiente virtual
python3 -m venv venv
source venv/bin/activate  # No Windows: venv\Scripts\activate

# Instalar dependências
pip install -r requirements.txt

# Criar arquivo .env
cp .env.example .env
```

Edite `.env` e adicione suas credenciais do Supabase:

```env
SUPABASE_URL=https://seu-projeto.supabase.co
SUPABASE_KEY=sua-chave-service-role-secret
ADMIN_PASSWORD=sua-senha-segura
```

## Passo 3: Configurar Frontend (1 minuto)

```bash
cd ../portfolio-frontend

# Instalar dependências
npm install

# Criar arquivo .env.local
cat > .env.local << EOF
VITE_SUPABASE_URL=https://seu-projeto.supabase.co
VITE_SUPABASE_ANON_KEY=sua-chave-anon-public
VITE_API_URL=http://localhost:5000
EOF
```

## Passo 4: Executar Localmente (1 minuto)

**Terminal 1 - Backend:**
```bash
cd portfolio-backend
source venv/bin/activate  # No Windows: venv\Scripts\activate
python app.py
```

**Terminal 2 - Frontend:**
```bash
cd portfolio-frontend
npm run dev
```

**Abra no navegador:**
- Frontend: `http://localhost:3000`
- Admin: `http://localhost:5001/admin` (senha: a que você configurou)

## Passo 5: Adicionar Seus Dados

1. Acesse `http://localhost:5001/admin`
2. Faça login com sua senha
3. Clique em "+ Novo Item" para adicionar projetos e certificados
4. Verifique em `http://localhost:3000` se aparecem

## Próximos Passos

- **Personalizar**: Edite cores e textos nos componentes React
- **Deploy**: Siga `COMPLETE_SETUP_GUIDE.md` para fazer deploy
- **Documentação Completa**: Veja `API_DOCUMENTATION.md` e `ADMIN_INTERFACE_GUIDE.md`

## Troubleshooting Rápido

| Problema | Solução |
|----------|---------|
| "Cannot find module" | Execute `npm install` ou `pip install -r requirements.txt` |
| "Connection refused" | Verifique se backend está rodando em outro terminal |
| "Invalid API Key" | Copie a chave correta do Supabase (service_role para backend) |
| "Table does not exist" | Execute o SQL do Passo 1 no Supabase |

## Dúvidas?

Consulte os guias detalhados:
- **Setup Completo**: `COMPLETE_SETUP_GUIDE.md`
- **API**: `API_DOCUMENTATION.md`
- **Admin Interface**: `ADMIN_INTERFACE_GUIDE.md`
- **Supabase**: `SUPABASE_SETUP_GUIDE.md`

---

**Pronto! Seu portfólio está rodando! 🚀**

