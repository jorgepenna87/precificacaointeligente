# Calculadora de Honorários — Arsenal Cálculo 200

Ferramenta web para alunos da pós-graduação **"Estratégia em Cálculos Trabalhistas"**.
O aluno preenche os dados do processo, vê o preço calculado em tempo real (com breakdown didático) e baixa uma proposta de honorários em formato `.docx` já preenchida.

## Como funciona

- Roda **100% no navegador**. Nenhum dado é enviado a servidor.
- Os dados do calculista (nome, documento, quantidade de cálculos, nomeações) ficam salvos no `localStorage` do navegador do aluno — preenche uma vez, nunca mais.
- Os dados do processo são pedidos a cada nova proposta.
- O histórico das **últimas 10 propostas geradas** fica salvo no navegador.
- A chave PIX **não é coletada nem armazenada** pelo app — o aluno preenche manualmente no Word depois de gerar o arquivo (segurança/privacidade).

## Estrutura

```
.
├── index.html       App completo (HTML + JS + Tailwind via CDN)
├── template.docx    Modelo Word com placeholders {variavel}
└── README.md        Este arquivo
```

## Como rodar localmente

⚠️ **Não funciona** abrindo `index.html` direto no navegador (o arquivo `template.docx` falha de carregar via `file://`).

Você precisa servir via HTTP local. **Não exige instalação se você tem Python**:

```bash
cd <pasta-do-projeto>
python3 -m http.server 8000
```

Depois abre no navegador: `http://localhost:8000`

> No GitHub Pages funciona direto, sem essa preocupação.

## Deploy no GitHub Pages (recomendado)

1. Criar conta em [github.com](https://github.com) (se não tiver)
2. Clicar em **"New repository"** → nome sugerido: `calculadora-honorarios` → marcar **Public** → criar
3. Fazer upload dos 3 arquivos (`index.html`, `template.docx`, `README.md`):
   - Na página do repo, clicar em **"uploading an existing file"**
   - Arrastar os 3 arquivos
   - Clicar em **"Commit changes"**
4. Ativar GitHub Pages:
   - Ir em **Settings** → **Pages** (menu lateral)
   - Em **Source**, escolher: **Deploy from a branch**, branch **main**, pasta `/ (root)`
   - **Save**
5. Aguardar 1-2 minutos. A URL vai aparecer no topo: `https://<seu-usuario>.github.io/calculadora-honorarios/`

## Embedar no site do curso

Cole o iframe abaixo (substituindo a URL pela sua do GitHub Pages) na página do curso:

```html
<iframe src="https://<seu-usuario>.github.io/calculadora-honorarios/"
        width="100%"
        height="1100"
        frameborder="0"
        style="border: 0;">
</iframe>
```

## Privacidade

- **Nenhum dado é enviado a qualquer servidor** — tudo roda localmente no navegador do aluno.
- Os dados ficam apenas no `localStorage` do navegador onde foram preenchidos.
- A **chave PIX nunca é solicitada nem salva** pelo app.
- O aluno pode limpar todos os dados zerando o `localStorage` (nas DevTools do navegador, ou simplesmente apagando o histórico do site).

## Stack técnica

- HTML/CSS/JavaScript vanilla (sem build, sem framework de CSS)
- CSS custom com paleta OKLCH (hue 215, azul oceano) e tipografia Inter
- Google Fonts: Inter (400/500/600/700)
- [PizZip](https://github.com/open-xmlformats/pizzip) + [docxtemplater](https://docxtemplater.com) — geração do .docx no navegador
- [FileSaver.js](https://github.com/eligrey/FileSaver.js) — download do arquivo
