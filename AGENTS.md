# AGENTS.md — SITE ALEX IMPORTS MT

> **Este arquivo é a fonte única de verdade da infraestrutura deste projeto.**
> Ele documenta onde o site está hospedado, como publicar, e o que fazer quando algo mudar.

---

## ⚠️ REGRA OBRIGATÓRIA DE ATUALIZAÇÃO DESTE ARQUIVO

**Este arquivo se auto-atualiza. É responsabilidade de qualquer inteligência artificial
(ou pessoa) que trabalhe neste projeto manter este arquivo sincronizado com a realidade.**

### Quando atualizar este arquivo

Atualize este arquivo **na mesma alteração** em que a infraestrutura mudar. Ou seja, se você:

- mudar de provedor de hospedagem, CDN, repositório ou domínio → atualize a seção correspondente;
- criar/renomear repositório, projeto, branch ou pasta de deploy → atualize;
- alterar nameservers, registros DNS, endereço de e-mail, telefone ou WhatsApp → atualize;
- adicionar/remover variáveis de ambiente, secrets, integrações ou serviços externos → atualize;
- criar novos comandos de build, deploy, preview ou validação → atualize;
- desativar um serviço, remover um domínio, encerrar um plano → atualize e marque como `DESATIVADO`;
- adicionar um novo passo obrigatório de publicação → atualize o fluxo de deploy.

### Como atualizar

1. Edite **apenas as seções afetadas** deste arquivo — não reescreva o documento inteiro.
2. Mantenha o formato e a estrutura existentes (tabelas, blocos de código, listas).
3. Se um serviço for desativado, **não apague o registro**: marque como `DESATIVADO` e mantenha a
   data e o motivo. Isso evita que alguém tente usar um serviço morto.
4. Se algo novo for criado (serviço, domínio, repositório, credencial), adicione-o na seção
   "Infraestrutura" **e** referencie-o no fluxo de deploy correspondente.
5. Ao final da alteração, confira que nenhum caminho, URL, ID ou comando ficou obsoleto.

### Checklist de consistência (rodar antes de considerar a tarefa concluída)

- [ ] Todos os repositórios/projetos citados existem e estão acessíveis?
- [ ] O domínio citado no arquivo é o mesmo que está em produção?
- [ ] Os nameservers registrados aqui são os que estão realmente configurados no Registro.br?
- [ ] O fluxo de deploy descrito funciona do zero (clone → build → deploy)?
- [ ] Nenhum segredo (senha, token, chave privada) foi escrito neste arquivo?

> **Regra de privacidade:** este arquivo é versionado no Git e pode ser público.
> **Nunca** escreva senhas, tokens, chaves de API, cookies ou documentos pessoais completos.
> Use apenas identificadores públicos (IDs de usuário, URLs, nomes de repositório) e
> ponteiros estáveis (ex.: "credencial guardada no gerenciador de senhas do titular").

---

## 1. Resumo do projeto

| Item | Valor |
|---|---|
| Nome do projeto | SITE ALEX IMPORTS MT |
| Empresa | Alex Imports MT |
| Tipo | Site institucional estático (HTML + CSS + JS em arquivo único) |
| Finalidade | Site de apresentação com canal de contato via WhatsApp |
| Workspace local | `C:\Users\rodri\OneDrive\Documents\SITE ALEX IMPORTS MT` |
| Repositório Git | `https://github.com/rodriguesalex999-u/aleximportsmt` |
| Deploy | Vercel (projeto `aleximportsmt`) |
| Domínio de produção | `https://aleximportsmt.com.br` |
| Contato principal | WhatsApp (65) 9294-2810 → `https://wa.me/556592942810` |

---

## 2. Infraestrutura

### 2.1 Registro de domínio — Registro.br (NIC.br)

| Item | Valor |
|---|---|
| Domínio | `aleximportsmt.com.br` |
| Registrador | Registro.br / NIC.br — `https://registro.br/` |
| Painel | `https://registro.br/painel/` |
| ID de usuário (código) | `ARFME44` |
| E-mail do cadastro | `rodriguesalex999@gmail.com` |
| Titular | Alex Rodrigues Fernandes de Melo (CPF `***.762.041-**`) |
| Status | Publicado / ativo |
| Expiração | 19/10/2027 |
| Nameservers **atuais** | `orbit.dns-parking.com`, `horizon.dns-parking.com` (Hostinger — DNS de parking) |
| Nameservers **alvo (Vercel)** | `ns1.vercel-dns.com`, `ns2.vercel-dns.com` |

**Como alterar nameservers (procedimento validado):**

1. Entrar em `https://registro.br/painel/` (login: código de usuário `ARFME44` + senha).
2. Menu **Painel → Domínios → "administrar aleximportsmt.com.br"**.
3. Aba **DNS / Nameservers** → substituir os 2 nameservers atuais pelos da Vercel.
4. Salvar e aguardar a propagação (pode levar até 24h; costuma resolver em minutos).
5. Confirmar propagação: `nslookup -type=NS aleximportsmt.com.br` (deve retornar `ns1/ns2.vercel-dns.com`).

**Recuperação de senha do Registro.br (se necessário):**

- Na tela de login, campo "Código, CPF, CNPJ, ou domínio" → digitar `ARFME44`.
- Link **"Não lembro ou não tenho a senha"** → resolve o desafio **"SOU HUMANO"** (CAPTCHA de imagem,
  precisa ser resolvido por uma pessoa) → clicar em **ENVIAR LEMBRETE**.
- O lembrete chega em `rodriguesalex999@gmail.com`.
- Se não houver mais acesso ao e-mail: procedimento de **reabilitação de conta** em
  `https://registro.br/ajuda/procedimentos-administrativos/alteracao-do-email/`
  (exige assinatura eletrônica gov.br + documento oficial com CPF; envio para `doc@registro.br`;
  análise em até 2 dias úteis).

### 2.2 GitHub — repositório e código

| Item | Valor |
|---|---|
| Conta | `rodriguesalex999-u` — `https://github.com/rodriguesalex999-u` |
| Repositório do site | `https://github.com/rodriguesalex999-u/aleximportsmt` |
| Branch de produção | `main` |
| Visibilidade | Pública |
| Autenticação | GitHub CLI (`gh`) autenticado no perfil `rodriguesalex999-u` |

**Comandos verificados:**

```bash
gh auth status
gh repo create aleximportsmt --public --source=. --remote=origin --push
git push origin main
```

### 2.3 Vercel — hospedagem e CDN

| Item | Valor |
|---|---|
| Conta | `rodriguesalex999-us` — `https://vercel.com/rodriguesalex999-us-projects` |
| Projeto | `aleximportsmt` |
| Dashboard | `https://vercel.com/rodriguesalex999-us-projects` |
| Integração | Repositório GitHub conectado (deploy automático a cada push em `main`) |
| Domínio no projeto | `aleximportsmt.com.br` (Settings → Domains) |
| Plano | Hobby (gratuito) — custo do domínio é o único |

**Fluxo de publicação (deploy automático):**

```
git push origin main  →  Vercel detecta o push  →  build  →  produção em aleximportsmt.com.br
```

**Publicar manualmente (quando o auto-deploy falhar):**

```bash
npx vercel --prod --yes
```

### 2.4 Hostinger — hPanel (serviço em desativação)

| Item | Valor |
|---|---|
| Painel | `https://hpanel.hostinger.com/` |
| Situação | **DESATIVADO** — plano Business Web Hosting expirado em 20/10/2026 |
| Sites no plano | `aleximportsmt.com.br`, `blue-beaver-675596.hostingersite.com`, `etevaldajoias.com` |
| Pedido pendente | Reativação Business Web Hosting 1 ano — **R$ 623,88** — **NÃO PAGAR** (criado por engano) |
| Link do pedido | `https://payments.hostinger.com/pay/f5b6dc12-e823-4785-97e7-202b597dbb41` |
| `etevaldajoias.com` | Expirado em 20/10/2026. **Não existe remoção manual** no hPanel; o Agente Hostinger confirmou que a remoção ocorre automaticamente ao fim do ciclo de expiração. Requer ticket para forçar. |

**Motivo da desativação:** o site passa a ser hospedado na Vercel (custo mínimo: apenas o domínio).
O DNS no Registro.br é migrado para `ns1/ns2.vercel-dns.com`, tornando o hPanel desnecessário.

> **Ação pendente:** abrir ticket no Agente Hostinger solicitando a remoção definitiva dos sites
> e o cancelamento do pedido de R$ 623,88. **Status: ainda não aberto** — usuário precisa acessar hPanel e solicitar via Agente Hostinger.
> **Nota 28/10/2026:** site corrigido (imagem removida, pronta entrega no Brasil); deploy Vercel feito (`aleximportsmt.vercel.app`); nameservers ainda precisam ser alterados no Registro.br; domínio `.com.br` ainda precisa ser adicionado no Vercel.

---

## 3. Estrutura do projeto

```
SITE ALEX IMPORTS MT/
├── AGENTS.md          ← este arquivo (fonte única de verdade; manter atualizado)
├── index.html         ← site completo: HTML + CSS + JS em arquivo único
├── README.md          ← instruções de publicação para humanos
├── .gitignore
└── .git/              ← repositório Git (remote: origin → GitHub)
```

**Decisão de arquitetura:** o site é um **arquivo HTML único** (`index.html`) com CSS e JS
embutidos. Isso mantém o deploy trivial (a Vercel serve o arquivo estático diretamente),
sem build step, sem dependências e sem risco de bundle quebrado.

---

## 4. Conteúdo do site

| Elemento | Valor |
|---|---|
| Nome exibido | Alex Imports MT |
| Seção de contato | **Fale Conosco** |
| WhatsApp | (65) 9294-2810 |
| Link WhatsApp | `https://wa.me/556592942810` |
| Link WhatsApp com mensagem | `https://wa.me/556592942810?text=Olá!%20Gostaria%20de%20um%20orçamento.` |
| Idioma | Português (pt-BR) |
| Paleta | Escuro premium com detalhes em dourado (`#d4af37` / `#f5d67b`) |
| Fontes | Google Fonts — `Playfair Display` (títulos) + `Inter` (corpo) |

---

## 5. Fluxo de deploy (passo a passo)

```bash
# 1. Conferir o que mudou
git status
git diff

# 2. Versionar
git add -A
git commit -m "descrição da mudança"

# 3. Publicar (dispara o deploy automático na Vercel)
git push origin main

# 4. Verificar
#    - build na Vercel: https://vercel.com/rodriguesalex999-us-projects
#    - site no ar:      https://aleximportsmt.com.br
```

**Validação local (opcional, sem servidor):** abrir `index.html` direto no navegador ou:

```bash
npx serve .          # http://localhost:3000
```

---

## 6. Checklist de publicação

- [ ] `index.html` abre sem erro no console do navegador
- [ ] Layout responsivo em 360px, 768px e 1440px
- [ ] Botão do WhatsApp abre `wa.me/556592942810` com número correto
- [ ] Seções "Fale Conosco" presentes e com CTA funcional
- [ ] `git status` limpo após commit
- [ ] Push para `main` feito
- [ ] Deploy verde na Vercel
- [ ] `https://aleximportsmt.com.br` respondendo com o novo conteúdo
- [ ] **Este `AGENTS.md` atualizado** com qualquer mudança de infraestrutura

---

## 7. Registro de alterações da infraestrutura

| Data | Alteração | Detalhe |
|---|---|---|
| 27/10/2026 | Criação do projeto | Site criado do zero; infraestrutura mapeada (Registro.br, GitHub, Vercel, Hostinger) |
| 27/10/2026 | Login no Registro.br | Acesso ao painel `ARFME44` recuperado com sucesso pelo titular |
| 27/10/2026 | Nameservers | Planejado: `orbit/horizon.dns-parking.com` → `ns1/ns2.vercel-dns.com` |
| 28/10/2026 | Vercel — domínio adicionado | `aleximportsmt.com.br` adicionado ao projeto Vercel; nameservers ainda precisam ser alterados no Registro.br |
| 28/10/2026 | Registro.br — login resolvido | CAPTCHA resolvido; usuário logado; nameservers ainda precisam ser alterados manualmente (seção DNS do domínio) |
| 28/10/2026 | Hostinger — chamado pendente | Ainda não aberto; usuário precisa acessar hPanel e solicitar via Agente Hostinger |
| 28/10/2026 | Site HTML criado | `index.html` elegante (Playfair + Inter, tema escuro dourado, Fale Conosco + WhatsApp 65 9294-2810) |

---

## 8. Notas e ressalvas

- **Vercel Hobby** permite apenas projetos pessoais/comerciais sem fins lucrativos amplos e
  impõe limite de 100 builds/dia. Para este site estático, o limite nunca é approached.
- **SSL/HTTPS** na Vercel é automático e gratuito (Let's Encrypt), emitido assim que os
  nameservers propagam.
- **Não pagar** o pedido de R$ 623,88 da Hostinger — ele foi criado por engano via Agente Hostinger.
- **Não usar** `etevaldajoias.com` em nenhum link, e-mail ou material de marketing: o domínio está
  expirado e em processo de remoção.
- **Credenciais:** nenhuma senha, token ou chave está neste arquivo. GitHub usa `gh auth`;
  Vercel usa a sessão já autenticada no navegador; Registro.br usa o código `ARFME44` + senha
  guardada no gerenciador de senhas do titular.
