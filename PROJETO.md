# Site Alex Imports MT — Guia do Projeto

> Leia este arquivo antes de mexer no site. Ele explica o que é o projeto, o design aprovado
> e as regras para cadastrar produtos e tratar imagens. Vale para qualquer pessoa ou IA.

## 1. O que é
- Loja online **multiprodutos** da **Alex Imports MT** (Cuiabá · MT).
- Referência de experiência: página "Ofertas do dia / SuperOfertas" do AliExpress,
  mas com a identidade da Alex Imports MT e o objetivo de ser **melhor e mais simples** que ela.
- **Sem login e sem senha**: o cliente escolhe, coloca no carrinho e compra.
- Futuro (ainda não feito): forma de pagamento e uma IA dentro do site que mostra ao
  cliente o que ele provavelmente procura.

## 2. Arquivos
| Arquivo / pasta | O que é |
|---|---|
| `index.html` | O site inteiro (HTML + CSS + JS num arquivo só). |
| `vercel.json` | Links próprios de categoria (`/c/...`) e produto (`/p/...`) e cache das mídias. |
| `AGENTS.md` | Infraestrutura (domínio, GitHub, Vercel). Ler antes de publicar. |
| `imagens/` | Cópia das fotos já tratadas, usadas na prévia. |
| `videos/` | Vídeos já comprimidos dos produtos. |
| `PROJETO.md` | Este guia. |

Fotos de origem dos produtos: `G:\Meu Drive\CADASTRO PRODUTOS\...`
(ex.: `JUMP NAUTICA\ALEX TREINAMENTO\IMPACTO PECAS` e `...\RELOGIO MASCULINO`).
O nome do arquivo de origem traz o nome do produto e o preço (ex.: `...-78.00`).

## 3. Design aprovado (versão 1 — aprovado pelo Alex em 01/11/2026)
- **Cores**: azul-marinho `#0b1f3a` (marca, cabeçalho, rodapé) · laranja `#ff6a00` (ação, destaque)
  · dourado `#f5b301` (detalhe na faixa) · fundo `#f4f5f7` · verde `#0a9f5a` (confirmações).
- **Fonte**: Outfit (Google Fonts), pesos 400–800.
- **Logo**: quadrado azul-marinho com "AI" + bolinha laranja; texto "Alex **Imports**" e "MATO GROSSO".
- **Estrutura da página**, de cima para baixo:
  1. Cabeçalho fixo: logo · busca grande arredondada · "Enviamos de Cuiabá · MT" · carrinho com contador.
  2. Faixa azul: compra sem cadastro · envio para todo o Brasil · atendimento direto.
  3. Banner laranja "SuperOfertas Alex Imports" com 3 cartões de vantagens.
  4. "Compre por categoria" (cartões com foto + quantidade de produtos).
  5. "Ofertas do dia" com abas de categoria (Recomendado + cada categoria) e grade de produtos.
  6. Faixa de confiança (4 cartões) e rodapé azul.
- **Cartão de produto**: foto quadrada (troca para a 2ª foto ao passar o mouse), selo no canto,
  botão redondo de carrinho, categoria em laranja, nome em 2 linhas, preço grande.
- **Página do produto** (janela): galeria com miniaturas, preço em caixa laranja clara,
  destaques com ✓, quantidade, botões "Comprar agora" e "Adicionar ao carrinho", descrição.
- **Carrinho**: gaveta lateral, guardado no navegador do cliente. "Finalizar pelo WhatsApp" abre o
  WhatsApp da loja (65) 9294-2810 com a lista do pedido e o total já escritos.
- **Celular (prioridade, tráfego pago)**: o produto abre em tela cheia como app; fotos e vídeo
  deslizam para o lado com contador (1/5); barra fixa embaixo com carrinho e "Comprar agora · preço";
  ao rolar para baixo aparece "Você também pode gostar" com os outros produtos (mesma categoria
  primeiro); o botão Voltar do celular fecha o produto; abas de categoria ficam fixas no topo.
- **Links próprios** (para mandar ao cliente ou usar em anúncio):
  - Categoria: `https://aleximportsmt.com.br/c/<id-da-categoria>` (ex.: `/c/relogio-masculino`)
  - Produto: `https://aleximportsmt.com.br/p/<id-do-produto>`
  - Na página da categoria há o botão "Copiar link desta categoria".
- **Regra de honestidade**: não colocar preço "de/por", avaliações, estrelas ou "vendidos"
  inventados. Só com dados reais.

## 4. Como cadastrar um produto
No `index.html`, no bloco `PRODUTOS`, copiar um produto e trocar:
`id`, `nome`, `categoria` (id de `CATEGORIAS`), `preco`, `selo`, `imagens`, `destaques`, `descricao`.
Categoria nova: adicionar em `CATEGORIAS` (`id`, `nome`, `icone`).

Categorias atuais: **Junta Motor** (`junta-motor`) e **Relógio Masculino** (`relogio-masculino`).

## 5. Padrão de imagens (obrigatório)
1. **Quadrada 1080 × 1080**, preenchendo tudo: **sem borda branca nem preta**. A foto é ampliada e
   as sobras são cortadas. Antes de cortar, conferir se o produto não fica cortado.
2. **Melhorar a qualidade** quando a foto for menor que 1080: ampliar com IA de super-resolução
   (EDSR ×2) e aplicar leve nitidez.
3. **Formato WebP, leve**: até ~150 KB por foto.
4. **Substituir a original**: a versão tratada vai para a mesma pasta de origem, com o mesmo nome
   (extensão `.webp`), no lugar da original. Assim a pasta fica só com fotos no padrão.
5. **Link**: subir no Cloudflare R2, bucket **`alex-imports-mt`** (separado do `etevalda`), e usar o link
   público no site. Trocar `IMG_BASE` no `index.html` pelo endereço público do bucket.

## 6. Padrão de vídeos (quando o produto tiver vídeo)
- O vídeo é a **primeira mídia** na página do produto: toca sozinho, sem som e em repetição,
  com botão "Ativar som". No cartão da grade aparece o selo "▶ Vídeo".
- **Leve**: 720 × 720, H.264 (MP4), 30 qps, áudio 64 kbps, `faststart`. Ex.: 50 MB → 2,9 MB.
  O vídeo só baixa quando o cliente abre o produto, então a página inicial continua rápida.
- **Hospedagem: DECISÃO TOMADA — Cloudflare R2** (bucket `alex-imports-mt`, pastas `imagens/` e `videos/`).
  Plano grátis: 10 GB de armazenamento, 1 milhão de envios e 10 milhões de leituras por mês,
  sem cobrança de tráfego. Enquanto o link público do R2 não estiver ativo, as mídias são
  servidas pela própria Vercel (pastas `imagens/` e `videos/` do repositório).
- **Reserva**: o campo `youtube` (ID do vídeo) é usado só se o arquivo não carregar.
- O vídeo original fica na pasta de origem; a versão leve vai para `videos/` do site.
- No produto: `video: "nome.mp4"` e, se tiver, `youtube: "ID"`.

## 7. Situação atual
- [x] Versão 1 do site com 2 categorias e 3 produtos (1 com vídeo).
- [x] Experiência de celular tipo app, links por categoria/produto, pedido pelo WhatsApp.
- [x] Publicado no GitHub `rodriguesalex999-u/aleximportsmt` (Vercel publica sozinha).
- [x] Bucket R2 `alex-imports-mt` criado.
- [ ] Ativar o link público do bucket e subir as fotos (precisa do Alex).
- [ ] Trocar `IMG_BASE` para o link do R2.
- [ ] Pagamento.
- [ ] IA de recomendação dentro do site.
