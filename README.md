# Casco Digital - Site com Formulario de Contato

Site institucional da Casco Digital com formulario de contato funcional usando Cloudflare Pages Functions e Resend.

## Estrutura de Arquivos

```
casco-digital-site/
├── index.html                  # Pagina principal do site
├── functions/
│   └── api/
│       └── contact.js          # Endpoint POST /api/contact
├── assets/
│   └── images/                 # Imagens usadas no site
└── README.md                   # Este arquivo
```

## Funcionalidades

- Design responsivo moderno
- Navbar com links rapidos (Suporte Remoto, Portal de Chamados)
# - Formulario de contato com validacao visual
- Backend serverless (Cloudflare Pages Functions)
- Envio de email via Resend
- Dois emails por envio:
  - Um para a Casco Digital (notificacao interna)
  - Um de confirmacao para o cliente

## Setup - Cloudflare Pages

### 1. Repositorio Git

Repo ja esta com a estrutura correta.
Para reutilizar este projeto, faca um fork ou clone deste repositorio para a sua conta e conecte esse repo no Cloudflare Pages.

### 2. Criar Projeto no Cloudflare Pages

1. Acesse https://dash.cloudflare.com/ e va em **Pages**.
2. Clique em **Create a project** > **Connect to Git**.
3. Selecione o repositorio acima.
4. Configuracao de build:
   - **Framework preset**: None
   - **Build command**: (deixe vazio)
   - **Build output directory**: `/`
   - **Root directory**: `/`
5. Clique em **Save and Deploy**.

### 3. Configurar Resend

1. Crie conta em https://resend.com.
2. Va em **Domains** e adicione/verifique seu dominio ou subdominio.
3. Autorize os registros DNS no Cloudflare quando solicitado.
4. Gere uma API Key em **API Keys** > **Create API Key**.
5. Use essa chave como valor de `EMAIL_API_KEY` no Cloudflare Pages.

### 4. Configurar Variaveis de Ambiente

Apos o primeiro deploy:

1. Va em **Settings** > **Variables and Secrets** > **Production**.
2. Adicione as 4 variaveis abaixo:

#### EMAIL_API_KEY (tipo: Secret)
- Clique em **Add variable**.
- Type: **Secret**
- Variable name: `EMAIL_API_KEY`
- Value: Sua API key do Resend (comeca com `re_...`)
- Clique em **Add variable**.

#### EMAIL_API_URL (tipo: Text)
- Clique em **Add variable**.
- Type: **Text**
- Variable name: `EMAIL_API_URL`
- Value: `https://api.resend.com/emails`
- Clique em **Add variable**.

#### EMAIL_FROM (tipo: Text)
- Clique em **Add variable**.
- Type: **Text**
- Variable name: `EMAIL_FROM`
- Value: Email/dominio verificado no Resend
  - Exemplo: `no-reply@dominio.com.br`
- Clique em **Add variable**.

#### EMAIL_TO (tipo: Text)
- Clique em **Add variable**.
- Type: **Text**
- Variable name: `EMAIL_TO`
- Value: Email que recebe os contatos do site
  - Exemplo: `destino@dominio.com.br`
- Clique em **Add variable**.


### 5. Redeploy

Apos configurar as variaveis:

1. Va em **Deployments**.
2. Clique nos 3 pontinhos do ultimo deploy.
3. Escolha **Retry deployment**.

Pronto! Site disponivel em na URL que cloudflare fornece



## Personalizacao

### Alterar destinatario dos emails

Edite a variavel `EMAIL_TO` em **Settings** > **Variables and Secrets** no Cloudflare Pages.

### Customizar texto dos emails

Edite os templates `internalPayload` e `clientPayload` em `functions/api/contact.js`:

- `internalPayload`: email que voce recebe
- `clientPayload`: email de confirmacao enviado ao cliente

---

**Casco Digital**  
Consultoria em M365, PowerShell e Infraestrutura  
suporte@cascodigital.com.br  
https://cascodigital.com.br
