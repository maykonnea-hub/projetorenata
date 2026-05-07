# Detox Emocional — Página de Vendas

Landing page do desafio "Detox Emocional" da Renata. HTML estático + Tailwind CSS, hospedado no Vercel.

## Estrutura

```
.
├── index.html      # Página principal (9 seções)
├── obrigado.html   # Página pós-compra (link do Telegram)
├── vercel.json     # Config do Vercel (URLs limpas)
└── README.md
```

## Antes de publicar — preencher placeholders

Edite `index.html` e `obrigado.html` substituindo:

| Placeholder | Onde | O que colocar |
|---|---|---|
| `SEU_LINK_AQUI` | `index.html` (3 botões CTA) | Link de checkout do Hotmart (`https://pay.hotmart.com/...`) |
| `SEU_LINK_DO_TELEGRAM` | `obrigado.html` | Link de convite do grupo Telegram (`https://t.me/+...`) |
| `SEU_PIXEL_ID` | ambos os arquivos (descomente as 2 linhas) | ID do Pixel Meta |
| Imagens Unsplash | `index.html` (hero e seção sobre) | Fotos reais da Renata |
| `og-image.jpg` | `<meta property="og:image">` | Imagem 1200x630 pra preview no WhatsApp/Instagram |

## Deploy no Vercel — passo a passo

### Opção 1: via interface (mais simples, sem terminal)

1. Crie conta em https://vercel.com (login com GitHub)
2. No painel: **Add New** → **Project**
3. **Import** o repositório (precisa estar no GitHub primeiro — veja "subir pro GitHub" abaixo)
4. **Deploy** — pronto, no ar em ~30 segundos

### Opção 2: via Vercel CLI (mais rápido depois do primeiro deploy)

```powershell
npm i -g vercel
vercel login
vercel --prod
```

### Subir pro GitHub primeiro

```powershell
git add .
git commit -m "feat: landing page detox emocional"
gh repo create detox-emocional --public --source=. --push
```

(Se não tiver `gh`: instale com `winget install GitHub.cli` e faça `gh auth login`.)

## Domínio personalizado

1. Compre `detoxemocional.com.br` no [Registro.br](https://registro.br) (~R$ 40/ano)
2. No Vercel: projeto → **Settings** → **Domains** → adicione o domínio
3. O Vercel mostra os registros DNS — vá no Registro.br → **DNS** → adicione os registros (geralmente um `A` apontando pra `76.76.21.21` e um `CNAME` `www → cname.vercel-dns.com`)
4. Aguarde 5–30 min pra propagar. HTTPS é automático.

## Configurar Hotmart

1. Crie conta produtor em https://hotmart.com
2. **Novo produto** → tipo **Curso Online**
3. Preço: **R$ 19,90** com parcelamento em 2x
4. Em **Página de Obrigado**: aponte pra `https://detoxemocional.com.br/obrigado` (ou use a do Hotmart)
5. **Garantia:** 7 dias
6. Em **Tracking → Pixel**: cole o mesmo ID do Pixel Meta (Hotmart dispara `Purchase` server-side)
7. Copie o **link de checkout** e cole nos 3 botões do `index.html`

## Pixel Meta — checklist

- [ ] Pixel criado no [Gerenciador de Eventos](https://business.facebook.com/events_manager)
- [ ] `SEU_PIXEL_ID` substituído nos dois arquivos (e linhas `fbq('init')` e `fbq('track')` descomentadas)
- [ ] Testado com [Meta Pixel Helper](https://chrome.google.com/webstore/detail/meta-pixel-helper/fdgfkebogiimcoedlicjlajpkdmockpc) no Chrome
- [ ] `InitiateCheckout` dispara ao clicar no botão (já configurado no onclick)
- [ ] `Purchase` configurado no Hotmart (Tracking → Pixel)

## Editar a página

Tudo é HTML puro com classes Tailwind. Pra trocar texto: abra `index.html` em qualquer editor (VS Code recomendado), edite e dê commit. O Vercel publica automático em cada push pro GitHub.

## Testar localmente

Abra `index.html` direto no navegador (Ctrl+O), ou:

```powershell
# se tiver Node instalado
npx serve
```

E acesse http://localhost:3000.
