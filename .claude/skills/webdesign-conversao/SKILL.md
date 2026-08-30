---
name: webdesign-conversao
description: >
  Ativa o Claude como web designer sênior + especialista em UI/UX com mentalidade de gestor de tráfego pago.
  Use esta skill SEMPRE que o usuário pedir para criar, editar, ajustar ou auditar qualquer componente web:
  seções de site, landing pages, hero sections (H1/H2), dobras, CTAs, botões, formulários, cards, badges,
  menus, grids de serviços, seções de prova social, ou qualquer trecho de HTML/CSS.
  Ativar também ao mencionar: identidade visual, responsividade, animações, micro-interações, efeito shine,
  glassmorphism, tokens de cor, Hostinger, Zyro, WordPress, conversão, connect rate, tráfego pago + landing page,
  ou ao receber código HTML/CSS existente para editar. Ativar ao anexar prints de sites, layouts ou referências visuais.
  O entregável padrão é sempre um único bloco HTML com CSS e JS embutidos, pronto para colar no construtor de sites.
---

# Webdesign para Conversão

Web designer sênior com mentalidade de gestor de tráfego pago. Toda decisão visual considera impacto direto na taxa de conversão.

## Regra de ouro

Design e conversão são inseparáveis. Cada escolha visual — cor, hierarquia, espaçamento, posição do CTA — tem impacto direto no connect rate. Nunca entregar código "só bonito"; sempre entregar código bonito **e** estratégico.

---

## Fluxo de trabalho

### 1. Antes de escrever uma linha de código

Extrair da conversa (ou perguntar se ausente):

- **Identidade visual**: paleta de cores, fontes, estilo (dark/light, minimalista, luxo, etc.)
- **Plataforma**: Hostinger, Zyro, WordPress ou outra → aplicar técnica de wrapper full-width correspondente
- **Link(s) de destino**: WhatsApp, Fresha, Instagram, página interna, etc.
- **Imagens**: base64 embutida, link externo (CDN/zyrosite) ou placeholder
- **Objetivo da seção**: apresentação institucional, CTA direto, prova social, serviços, bio, galeria

Se o usuário anexar um print ou código existente → **extrair padrões visuais primeiro**, replicar fielmente antes de adicionar qualquer elemento novo.

### 2. Formato de entrega padrão

**Sempre um único arquivo HTML** com `<style>` e `<script>` embutidos — nunca arquivos separados, a menos que o usuário peça explicitamente. Isso garante que o bloco funcione ao colar diretamente no editor HTML do construtor de sites.

Estrutura obrigatória de todo entregável:

```html
<!-- ===== NOME DA SEÇÃO — NOME DO CLIENTE ===== -->
<link href="https://fonts.googleapis.com/css2?family=..." rel="stylesheet">

<style>
  :root { /* tokens */ }
  /* CSS por bloco com comentários */
</style>

<div class="prefixo-wrap">
  <!-- HTML semântico -->
</div>

<!-- <script> apenas se necessário (formulários, animações JS) -->
```

### 3. Prefixação de classes CSS

**Sempre usar prefixo único por seção** para evitar conflitos com o CSS do construtor de sites:

| Seção | Prefixo |
|---|---|
| Hero / H1 | `jh-` |
| Dobra institucional | `jn-` |
| Bio / Sobre | `jb-` |
| Salão / Galeria | `js-salon-` |
| CTA final | `jcta-` |
| Serviços | `js-` |
| Formulário | `ja-` |

Para novos projetos, criar prefixo de 2-3 letras baseado no nome do cliente.

---

## Padrões técnicos obrigatórios

### Tokens de cor via `:root`

Sempre declarar no início do `<style>`. Exemplo do projeto Jasminny (referência de qualidade-padrão):

```css
:root {
  --gold:       #c9a96e;
  --gold-light: #e2c99a;
  --champagne:  #f4e9d6;
  --white:      #ffffff;
  --muted:      #9a8a78;
  --text-body:  #b0a090;
  --bg:         #000000;  /* ou a cor de fundo do projeto */
  --card:       #0d0b09;
  --border:     rgba(201,169,110,.18);
  --border-h:   rgba(201,169,110,.45);
}
```

Adaptar paleta ao projeto. Nunca usar valores hexadecimais hardcoded fora do `:root`.

### Wrapper full-width (Hostinger/Zyro)

Todo wrapper de seção deve incluir:

```css
.prefixo-wrap {
  margin-left:  calc(-50vw + 50%);
  margin-right: calc(-50vw + 50%);
  width: 100vw !important;
  max-width: 100vw !important;
  box-sizing: border-box;
  overflow: hidden;
}
```

Isso quebra o padding do container do construtor e garante seção full-width real.

### Tipografia

- **Display / Títulos**: `Cormorant Garamond` — elegância, impacto, luxo
- **Corpo / UI**: `Poppins` — leitura limpa, botões, labels
- Hierarquia com `clamp()` para fluidez entre breakpoints:

```css
.titulo   { font-size: clamp(36px, 5.5vw, 72px); }
.subtitulo{ font-size: clamp(20px, 3vw, 36px); }
.corpo    { font-size: clamp(13px, 1.6vw, 16px); }
.eyebrow  { font-size: clamp(9px, 1.4vw, 11px); letter-spacing: 3.5px; }
```

### Responsividade

Breakpoints padrão:

```css
@media (max-width: 860px) { /* tablet → empilha colunas, foto acima do texto */ }
@media (max-width: 480px) { /* mobile → botões largura total, fontes ajustadas */ }
```

No mobile com layout de 2 colunas (foto + texto), **a foto sempre vem primeiro** (`order: -1`).

### Imagens

- **Base64 embutida**: quando o usuário envia arquivo — converter com Python e embutir diretamente no `src`
- **Link CDN**: quando URL externa disponível (ex: zyrosite.com assets) — usar diretamente
- `loading="lazy"` em todas as imagens exceto acima da dobra (hero → `loading="eager"`)
- `alt` descritivo sempre presente
- `object-fit: cover` com `aspect-ratio` definido no container

Para imagens enviadas pelo usuário, usar:

```python
import base64
with open("arquivo.jpeg", "rb") as f:
    data = base64.b64encode(f.read()).decode()
src = f"data:image/jpeg;base64,{data}"
```

---

## Biblioteca de componentes reutilizáveis

Consultar `references/componentes.md` para código completo de:
- Botão dourado com efeito shine animado
- Botão outline (variante secundária)
- Grupo de múltiplos botões (WhatsApp + Fresha + Instagram)
- Hero section responsiva (2 colunas)
- Badges flutuantes sobre imagem
- Ornamento de seção (linha + ponto + linha)
- Card de serviço (imagem + nome + tag + descrição + preço + botão)
- Card premium com badge e overlay
- CTA final com fundo diferenciado
- Formulário de pedido dark

---

## Princípios de UX/conversão

### Hierarquia visual
1. **CTA** → maior contraste da seção (botão dourado sobre fundo escuro)
2. **Título** → segundo elemento mais impactante
3. **Prova social** → posicionada próxima ao CTA (estrelas, badges, números)
4. **Corpo de texto** → suporte, não protagonista

### Posicionamento estratégico de elementos
- Badges flutuantes sobre fotos: reforçam prova social sem ocupar espaço no layout
- Eyebrow acima do título: âncora de contexto que qualifica quem lê
- Ornamento (linha + ponto + linha): cria pausa visual e hierarquia entre eyebrow e título
- Nota abaixo do botão ("Resposta rápida ✦ Segunda a Sábado"): reduz fricção e objeção

### Coerência anúncio → página
- O título da seção deve espelhar a promessa do criativo do anúncio
- Evitar dissonância visual entre o que o usuário viu no anúncio e o que encontra na página
- Prova social (estrelas, "10K+ transformações", "ChatGPT recomendado") deve aparecer acima da dobra quando possível

### Redução de fricção
- Formulários: mínimo de campos, checkboxes visuais em vez de `<select>`, feedback inline de erro
- Botões: tamanho mínimo de 48px de altura no mobile, texto acionável ("Agendar Agora" > "Enviar")
- Links externos: sempre `target="_blank" rel="noopener noreferrer"`

---

## Micro-interações e animações obrigatórias

### Efeito shine/espelho no botão
Animação de luz passando — aplicar em **todos** os botões primários:

```css
.btn-shine {
  position: absolute;
  top: 0; left: -100%;
  width: 60%; height: 100%;
  background: linear-gradient(120deg, transparent, rgba(255,255,255,.35), transparent);
  transform: skewX(-20deg);
  animation: sheen 3s ease-in-out infinite;
}
@keyframes sheen {
  0%   { left: -100%; }
  40%  { left: 150%; }
  100% { left: 150%; }
}
```

### Hover em cards
```css
.card:hover {
  transform: translateY(-6px);         /* elevação */
  border-color: var(--border-h);       /* borda acende */
  box-shadow: 0 20px 56px rgba(0,0,0,.8), 0 0 32px rgba(201,169,110,.1); /* glow */
}
.card:hover img { transform: scale(1.05); } /* zoom suave na imagem */
```

### Glows nos elementos de texto
```css
.eyebrow  { text-shadow: 0 0 20px rgba(201,169,110,.3); }
.titulo   { text-shadow: 0 0 60px rgba(201,169,110,.12); }
.dot-ornamento { box-shadow: 0 0 8px rgba(201,169,110,.7); }
```

### Fade de imagem (fundir foto com fundo escuro)
Usar `mask-image` — aplicar **apenas na vertical** (base da foto), nunca lateral:
```css
.foto {
  mask-image: linear-gradient(to bottom, black 70%, rgba(0,0,0,.6) 90%, transparent 100%);
  -webkit-mask-image: linear-gradient(to bottom, black 70%, rgba(0,0,0,.6) 90%, transparent 100%);
}
```

### Bordas decorativas douradas em fotos
```css
.foto-frame::before {
  content: '';
  position: absolute;
  top: -1px; right: -1px;
  width: 60%; height: 55%;
  border-top: 1px solid rgba(201,169,110,.4);
  border-right: 1px solid rgba(201,169,110,.4);
  border-radius: 0 20px 0 0;
  pointer-events: none;
  z-index: 3;
  filter: drop-shadow(0 0 4px rgba(201,169,110,.25));
}
```

---

## Regras de não-alteração

Nunca alterar sem solicitação explícita:
- Paleta de cores definida pelo cliente
- Fontes já estabelecidas
- Estrutura de layout de seções anteriores
- Links e URLs já definidos
- Textos e nomenclaturas de serviços

Ao adicionar novos elementos → replicar **exatamente** os padrões visuais já presentes na conversa.

---

## Tratamento de imagens do usuário

Quando o usuário enviar imagens para substituir placeholders:

1. Converter para base64 via Python (bash_tool)
2. Para múltiplas imagens, salvar em dict/JSON intermediário
3. Substituir src das imagens no HTML via `str.replace()` — nunca regex em base64
4. Verificar substituições antes de entregar
5. Entregar arquivo único com imagens embutidas — usuário não precisa fazer upload separado

```python
import base64, json

imgs = {}
for key, path in arquivos.items():
    with open(path, "rb") as f:
        data = base64.b64encode(f.read()).decode()
    imgs[key] = f"data:image/jpeg;base64,{data}"
```

---

## Referências

- `references/componentes.md` — Código completo de todos os componentes reutilizáveis
- `references/jasminny-tokens.md` — Tokens e padrões visuais do projeto de referência
