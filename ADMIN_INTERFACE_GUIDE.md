# Guia da Interface de Administração (CRUD)

## Visão Geral

A Interface de Administração é um painel web protegido por senha que permite gerenciar projetos, certificados e visualizar estatísticas de visitas do seu portfólio, sem necessidade de interagir diretamente com o banco de dados ou usar ferramentas como Postman.

## Acesso à Interface

### URL

```
http://localhost:5001/admin
```

Em produção, substitua `localhost:5001` pela URL do seu servidor.

### Login

1. Acesse a URL acima
2. Digite a senha de administrador configurada em `.env` (variável `ADMIN_PASSWORD`)
3. Clique em "Entrar"

**Nota:** A senha padrão é `admin123`. Altere-a em produção!

---

## Layout da Interface

A interface está dividida em três seções principais:

### Sidebar (Barra Lateral)

Na esquerda, você encontrará:

- **Logo**: "Portfolio Admin v1.0"
- **Menu de Navegação**: Links para as seções (Projetos, Certificados, Visitas)
- **Botão Sair**: Faz logout da interface

### Top Bar (Barra Superior)

No topo:

- **Título da Seção**: Mostra qual seção você está visualizando
- **Botão "+ Novo Item"**: Abre o formulário para criar um novo item (não aparece na seção Visitas)

### Área de Conteúdo

O conteúdo principal muda conforme a seção selecionada.

---

## Seção: Projetos

### Visualizar Projetos

Ao acessar a seção "Projetos", você verá uma grade com todos os seus projetos em formato de cards. Cada card exibe:

- **Título do Projeto**: Nome do projeto
- **Descrição**: Breve resumo do projeto
- **Tecnologias**: Tags com as tecnologias utilizadas
- **Botões de Ação**: "Editar" e "Deletar"

### Criar um Novo Projeto

1. Clique no botão **"+ Novo Item"**
2. Preencha o formulário:
   - **Título do Projeto** (obrigatório): Nome do projeto
   - **Descrição** (obrigatório): Descrição detalhada
   - **Tecnologias** (obrigatório): Tecnologias utilizadas, separadas por vírgula
   - **Link GitHub** (opcional): URL do repositório
   - **Link Deploy** (opcional): URL do projeto em produção

3. Clique em **"Salvar Projeto"**
4. Uma notificação de sucesso aparecerá

### Editar um Projeto

1. Clique no botão **"Editar"** no card do projeto
2. Modifique os campos desejados
3. Clique em **"Salvar Projeto"**
4. As alterações serão refletidas imediatamente

### Deletar um Projeto

1. Clique no botão **"Deletar"** no card do projeto
2. Uma janela de confirmação aparecerá
3. Clique em **"Excluir"** para confirmar
4. O projeto será removido permanentemente

---

## Seção: Certificados

### Visualizar Certificados

A seção "Certificados" exibe todos os seus certificados em uma grade. Cada card mostra:

- **Nome do Curso/Certificação**: Nome completo
- **Instituição**: Onde foi realizado
- **Origem**: Tag com a origem (ex: FIAP, Alura)
- **Data de Conclusão**: Quando foi concluído
- **Botões de Ação**: "Editar" e "Deletar"

### Filtrar por Origem

No topo da seção, você encontrará botões de filtro:

- **Todos**: Mostra todos os certificados
- **FIAP**: Mostra apenas certificados da FIAP
- **Alura**: Mostra apenas certificados da Alura
- **Coursera**: Mostra apenas certificados da Coursera
- **Udemy**: Mostra apenas certificados da Udemy
- **Outro**: Mostra certificados de outras origens

Clique em qualquer botão para filtrar os resultados.

### Criar um Novo Certificado

1. Clique no botão **"+ Novo Item"**
2. Preencha o formulário:
   - **Nome do Curso/Certificação** (obrigatório): Nome completo
   - **Instituição** (obrigatório): Onde foi realizado
   - **Origem** (opcional): Selecione de uma lista predefinida
   - **Data de Conclusão** (obrigatório): Data no formato DD/MM/YYYY
   - **Link do Certificado** (opcional): URL para visualizar o certificado

3. Clique em **"Salvar Certificado"**

### Editar um Certificado

1. Clique no botão **"Editar"** no card do certificado
2. Modifique os campos desejados
3. Clique em **"Salvar Certificado"**

### Deletar um Certificado

1. Clique no botão **"Deletar"** no card do certificado
2. Confirme a exclusão na janela que aparecerá

---

## Seção: Visitas

### Visualizar Contador de Visitas

A seção "Visitas" exibe um grande número representando o total de visitantes do seu portfólio.

### Resetar Contador

Se desejar resetar o contador de visitas para zero:

1. Clique no botão **"Resetar Contador"**
2. Uma confirmação será solicitada
3. Clique em **"OK"** para confirmar

**Nota:** Esta ação não pode ser desfeita!

---

## Notificações

A interface exibe notificações toast (pequenas mensagens) nos seguintes casos:

- **Sucesso (verde)**: Item criado, atualizado ou deletado com sucesso
- **Erro (vermelho)**: Ocorreu um erro ao processar a ação
- **Informação (azul)**: Mensagens informativas

As notificações desaparecem automaticamente após 3 segundos.

---

## Dicas e Boas Práticas

### Organização de Projetos

- Mantenha os títulos concisos e descritivos
- Use tecnologias separadas por vírgula (ex: "React, Node.js, MongoDB")
- Sempre forneça links para GitHub e Deploy quando possível
- Atualize as descrições conforme o projeto evolui

### Organização de Certificados

- Use a origem para categorizar seus certificados
- Mantenha as datas de conclusão atualizadas
- Adicione links para os certificados quando disponível
- Ordene por data de conclusão (mais recentes primeiro)

### Segurança

- **Altere a senha padrão**: Não deixe "admin123" em produção
- **Use senhas fortes**: Combine letras, números e símbolos
- **Não compartilhe a senha**: Mantenha a interface privada
- **Faça logout**: Sempre faça logout ao terminar

---

## Troubleshooting

### Erro: "Acesso Negado" ou "Senha Incorreta"

**Solução:**
- Verifique se a senha está correta
- Certifique-se de que está digitando a senha configurada em `.env`
- Tente limpar o cache do navegador

### Erro: "Falha ao Carregar Dados"

**Solução:**
- Verifique se o backend está rodando: `python admin.py`
- Confirme que o Supabase está acessível
- Verifique as credenciais do Supabase em `.env`

### Erro: "Falha ao Salvar Item"

**Solução:**
- Verifique se todos os campos obrigatórios foram preenchidos
- Confirme que o backend está rodando
- Tente novamente em alguns segundos

### Interface Lenta ou Não Responsiva

**Solução:**
- Verifique sua conexão com a internet
- Reinicie o servidor backend: `python admin.py`
- Limpe o cache do navegador
- Tente em outro navegador

---

## Fluxo de Trabalho Típico

### Adicionando um Novo Projeto

1. Termine de desenvolver o projeto
2. Faça push para o GitHub
3. Faça deploy em uma plataforma (Vercel, Netlify, etc.)
4. Acesse a interface de admin
5. Clique em "+ Novo Item"
6. Preencha os detalhes do projeto
7. Adicione os links do GitHub e Deploy
8. Clique em "Salvar Projeto"
9. Verifique se o projeto aparece no portfólio

### Adicionando um Novo Certificado

1. Conclua o curso ou certificação
2. Baixe o certificado (se disponível)
3. Acesse a interface de admin
4. Clique em "+ Novo Item"
5. Preencha os detalhes do certificado
6. Selecione a origem
7. Adicione o link do certificado (se disponível)
8. Clique em "Salvar Certificado"
9. Verifique se o certificado aparece no portfólio

---

## Recursos Avançados

### Edição em Massa

Para editar múltiplos itens rapidamente:

1. Edite o primeiro item
2. Clique em "Salvar"
3. Repita para os próximos itens

### Exportação de Dados

Atualmente, não há função de exportação integrada. Para exportar dados:

1. Use a API diretamente com curl ou Postman
2. Acesse o Supabase e exporte os dados lá
3. Considere implementar uma função de exportação customizada

### Backup de Dados

O Supabase oferece backups automáticos. Para mais informações:

1. Acesse seu projeto no Supabase
2. Vá para Settings → Backups
3. Configure a frequência de backup desejada

---

## Segurança e Privacidade

### Proteção de Dados

- A interface é protegida por senha
- Todos os dados são armazenados no Supabase (criptografado em repouso)
- As comunicações devem ser feitas via HTTPS em produção

### Conformidade

- Certifique-se de estar em conformidade com LGPD/GDPR se aplicável
- Implemente políticas de privacidade apropriadas
- Mantenha registros de acesso (logs) para auditoria

---

## Suporte

Se encontrar problemas com a interface de admin:

1. Consulte a seção [Troubleshooting](#troubleshooting)
2. Verifique os logs do backend
3. Abra uma issue no repositório
4. Entre em contato com o desenvolvedor

---

## Próximos Passos

- Customize a interface com suas cores e logo
- Implemente autenticação mais robusta (OAuth, JWT)
- Adicione funcionalidades de exportação
- Implemente controle de acesso baseado em papéis (RBAC)
- Adicione histórico de alterações (audit log)

---

**Parabéns! Agora você pode gerenciar seu portfólio facilmente! 🎉**

