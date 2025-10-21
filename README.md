# Portfólio Profissional de Desenvolvedor

Um portfólio web moderno, minimalista e profissional para um estudante de Engenharia de Software. Construído com React, Tailwind CSS, Flask e Supabase.

## 🎯 Características Principais

- **Single Page Application (SPA)**: Navegação fluida e responsiva
- **Design Minimalista**: Paleta de cores em preto, branco e cinza com azul escuro para interatividade
- **Gerenciamento Dinâmico**: Projetos e certificados gerenciados via API
- **Interface CRUD**: Painel de administração web para gerenciar dados
- **Contador de Visitas**: Rastreamento automático de visitantes
- **SEO Otimizado**: Metatags, sitemap e robots.txt
- **Responsivo**: Funciona perfeitamente em desktop, tablet e smartphone
- **Autenticação**: Sistema de autenticação simples para operações admin

## 📁 Estrutura do Projeto

```
portfolio/
├── portfolio-frontend/          # React + Tailwind CSS
│   ├── client/
│   │   ├── src/
│   │   │   ├── components/     # Componentes reutilizáveis
│   │   │   ├── pages/          # Páginas da aplicação
│   │   │   └── App.tsx         # Componente raiz
│   │   ├── public/             # Assets estáticos
│   │   └── package.json
│   └── vite.config.ts
│
├── portfolio-backend/           # Flask + Supabase
│   ├── app.py                   # API REST principal
│   ├── admin.py                 # Interface CRUD
│   ├── requirements.txt         # Dependências Python
│   ├── templates/               # Templates HTML
│   ├── static/                  # CSS e JavaScript
│   └── .env.example
│
├── QUICK_START.md              # Guia rápido (comece aqui!)
├── COMPLETE_SETUP_GUIDE.md     # Guia completo de setup
├── API_DOCUMENTATION.md        # Documentação da API
├── ADMIN_INTERFACE_GUIDE.md    # Guia da interface admin
└── SUPABASE_SETUP_GUIDE.md     # Configuração do Supabase
```

## 🚀 Quick Start

Para colocar o portfólio rodando em poucos minutos, siga o `QUICK_START.md`.

**Resumo rápido:**

```bash
# 1. Configurar Supabase (criar tabelas)
# Veja SUPABASE_SETUP_GUIDE.md

# 2. Backend
cd portfolio-backend
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt
cp .env.example .env
# Edite .env com suas credenciais
python app.py

# 3. Frontend (em outro terminal)
cd portfolio-frontend
npm install
cp .env.example .env.local
# Edite .env.local com suas credenciais
npm run dev

# 4. Abra no navegador
# Frontend: http://localhost:3000
# Admin: http://localhost:5001/admin
```

## 📚 Documentação

| Documento | Descrição |
|-----------|-----------|
| **QUICK_START.md** | Comece aqui! Setup em 5 minutos |
| **COMPLETE_SETUP_GUIDE.md** | Guia detalhado de configuração e deployment |
| **API_DOCUMENTATION.md** | Documentação completa dos endpoints da API |
| **ADMIN_INTERFACE_GUIDE.md** | Como usar o painel de administração |
| **SUPABASE_SETUP_GUIDE.md** | Configuração passo a passo do Supabase |

## 🛠️ Tecnologias Utilizadas

### Frontend
- **React 19**: Framework JavaScript para UI
- **Tailwind CSS**: Framework CSS utility-first
- **Vite**: Build tool rápido
- **TypeScript**: Tipagem estática
- **Wouter**: Roteamento leve
- **Lucide Icons**: Ícones SVG

### Backend
- **Flask**: Framework web Python
- **Flask-CORS**: Suporte a CORS
- **Supabase**: Backend as a Service (PostgreSQL)
- **Python-dotenv**: Gerenciamento de variáveis de ambiente

### Banco de Dados
- **Supabase (PostgreSQL)**: Banco de dados relacional
- **Tabelas**: projetos, certificados, visitas

### Deployment
- **Frontend**: Vercel, Netlify ou similar
- **Backend**: Render, Railway ou similar
- **Banco de Dados**: Supabase (hospedado)

## 📋 Seções do Portfólio

1. **Header**: Navegação fixa com links para todas as seções
2. **Hero Section**: Apresentação inicial com call-to-action
3. **Sobre Mim**: Biografia e links para redes sociais
4. **Projetos**: Galeria dinâmica de projetos (via API)
5. **Certificados**: Galeria de certificados com filtro por origem
6. **Currículo**: Seção para download do CV em PDF
7. **Contato**: Formulário de contato funcional
8. **Footer**: Rodapé com links e contador de visitas

## 🔐 Segurança

- Autenticação por senha para operações admin
- Variáveis de ambiente para credenciais sensíveis
- CORS configurado
- Validação de entrada no backend
- Recomendações de segurança em produção

## 🧪 Testes

Execute os testes unitários do backend:

```bash
cd portfolio-backend
pip install pytest pytest-cov
pytest test_app.py -v
```

## 📈 Performance e SEO

- **SEO**: Metatags, sitemap.xml, robots.txt
- **Performance**: Lazy loading, otimização de imagens
- **Responsividade**: Mobile-first design
- **Acessibilidade**: ARIA labels, semantic HTML

## 🎨 Customização

### Alterar Cores

Edite `portfolio-frontend/client/src/index.css`:

```css
:root {
  --primary: #003366;  /* Azul escuro */
  --secondary: #666666; /* Cinza */
}
```

### Alterar Informações Pessoais

Edite os componentes em `portfolio-frontend/client/src/components/`:

- `HeroSection.tsx`: Título e subtítulo
- `AboutSection.tsx`: Biografia e links sociais
- `Footer.tsx`: Informações de contato

## 📦 Variáveis de Ambiente

### Frontend (.env.local)

```env
VITE_SUPABASE_URL=https://seu-projeto.supabase.co
VITE_SUPABASE_ANON_KEY=sua-chave-anon-public
VITE_API_URL=http://localhost:5000
```

### Backend (.env)

```env
SUPABASE_URL=https://seu-projeto.supabase.co
SUPABASE_KEY=sua-chave-service-role-secret
ADMIN_PASSWORD=sua-senha-segura
FLASK_ENV=development
FLASK_DEBUG=True
```

## 🚢 Deployment

### Frontend (Vercel)

1. Faça push para GitHub
2. Conecte seu repositório no Vercel
3. Configure as variáveis de ambiente
4. Deploy automático

### Backend (Render)

1. Faça push para GitHub
2. Crie um novo Web Service no Render
3. Configure as variáveis de ambiente
4. Deploy automático

Veja `COMPLETE_SETUP_GUIDE.md` para instruções detalhadas.

## 🤝 Contribuindo

Sinta-se livre para fazer fork, modificar e melhorar este projeto!

## 📝 Licença

Este projeto é fornecido como está para uso pessoal e educacional.

## 💬 Suporte

Se encontrar problemas:

1. Consulte a documentação relevante
2. Verifique os logs do servidor
3. Abra uma issue no repositório

## 🎓 Sobre o Autor

**Lucas Toledo Cortonezi**

- 📍 São Paulo, Brasil
- 🎓 Estudante de Engenharia de Software na FIAP (2025-2028)
- 💻 Desenvolvedor apaixonado por tecnologia
- 🔗 [LinkedIn](https://br.linkedin.com/in/lucas-toledo-cortonezi-10a851350)
- 🔗 [GitHub](https://github.com/LucasToledoC)
- 🔗 [Instagram](https://www.instagram.com/alem4ao/)

## 📅 Changelog

### v1.0 (2025-01-15)
- Lançamento inicial
- Frontend React com Tailwind CSS
- Backend Flask com Supabase
- Interface CRUD de administração
- Documentação completa

## 🙏 Agradecimentos

Agradecimentos especiais a:

- React e comunidade
- Tailwind CSS
- Flask
- Supabase
- Vercel e Render
- Todos os contribuidores

---

**Pronto para colocar seu portfólio online? Comece com [QUICK_START.md](./QUICK_START.md)! 🚀**

