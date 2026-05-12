# bss-forms-editor-criativos

Página de vaga + formulário de candidatura (Typeform-style) para Editor de Criativo da **BSS Performance Marketing**.

## Rotas
- `/editor-criativos` — landing page da vaga.
- `/forms-editor-criativos` — formulário de candidatura (uma pergunta por vez).
- `/` redireciona para `/editor-criativos`.

## Stack
- React 18 via CDN (UMD) + Babel Standalone — arquivo único `index.html`, sem build step.
- Tema dark: fundo preto, texto branco, botões laranja.
- Deploy: site estático (Netlify ready).

## Captura dos dados
O submit do formulário envia o payload em paralelo para:

1. **Netlify Forms** — formulário `candidatura-editor-criativos` (visível no painel do Netlify, exporta CSV, envia notificações).
2. **Webhook n8n** — `https://n8n-n8n.7b7hsj.easypanel.host/webhook/formulario` (JSON).

O sucesso é considerado se **qualquer um dos dois** capturar. Isso garante que dados não sejam perdidos se o workflow do n8n estiver inativo.

## Campos enviados (15)
`nome_completo, cpf, idade, email, celular, expectativa_remuneracao, nivel_ingles, nivel_experiencia, tipos_video, softwares_edicao, inteligencias_artificiais, cursos_mentorias, portfolio, linkedin, origem_vaga`

## Deploy no Netlify
1. Conectar este repo no Netlify.
2. Build command: vazio. Publish directory: `.` (raiz).
3. Após o primeiro deploy, o formulário `candidatura-editor-criativos` aparece em **Forms** no painel do Netlify.

## Desenvolvimento local
Abrir `index.html` direto no navegador, ou:
```
python -m http.server 8000
```
Para testar as rotas localmente, navegue para `http://localhost:8000/editor-criativos` (o roteamento JS cuida do resto).
