# Tokens e Padrões Visuais — Kikuchi Engenharia (Fábio Kikuchi)

Extraído da LP real **"Eberick Protendido — Lajes e Vigas"** (Hotmart, engenharia estrutural).
Cliente: Eng. Fábio Kikuchi Yamura — cursos técnicos para engenheiros/calculistas (Eberick, concreto armado/protendido/metálica).
Usar como segunda referência de qualidade-padrão ao lado de `jasminny-tokens.md`, para o **nicho técnico/B2B** (em vez do nicho estética/luxo do Jasminny).

---

## Contexto de marca

Diferente do Jasminny (dourado/luxo/feminino), a identidade Kikuchi é **técnica, séria, escura, com acento terracota** — fala com engenheiro, não com consumidor final. Tom de copy: direto, quantificado (R$, %, anos), sem adjetivo vazio.

---

## Tokens de cor via `:root`

```css
:root {
  --bg:  #0a0908;   /* fundo base, quase preto */
  --sf:  #110f0d;   /* fundo de seção alternada (sc-alt) */
  --cd:  #171412;   /* fundo de card */
  --bd:  #2a2420;   /* bordas sutis */
  --ac:  #C85A28;   /* acento terracota — CTA, links, destaques */
  --ac2: #e0692f;   /* acento hover */
  --acd: rgba(200,90,40,.12); /* fundo de tag/badge sobre --ac */
  --acg: rgba(200,90,40,.08); /* glow radial de fundo */
  --wt:  #f0ece8;   /* texto branco/títulos */
  --mt:  #6b6158;   /* texto mudo/legenda — ⚠️ ver nota de contraste abaixo */
  --tx:  #c0b5a8;   /* texto de corpo */
  --ok:  #7cb342;   /* verde de confirmação (lista "para quem é") */
  --fd:  'Cormorant Garamond', serif;  /* display/títulos */
  --fb:  'Poppins', sans-serif;        /* corpo/UI */
}
```

**Nota de contraste**: `--mt` sobre `--cd`/`--sf` fica perto do limite WCAG AA em textos pequenos (10-14px, ex. `.cost-desc`, `.foot-sub`). Ao reaproveitar, testar contraste antes de usar `--mt` abaixo de 14px — se falhar, subir para `--tx` ou aumentar a fonte.

---

## Tipografia

Mesma dupla-padrão da skill (Cormorant Garamond + Poppins), com `clamp()` em toda a hierarquia:

```css
.h1  { font-size: clamp(2.8rem, 5.8vw, 4.8rem); font-family: var(--fd); font-weight: 300; }
.t2  { font-size: clamp(2rem, 4vw, 3.2rem);     font-family: var(--fd); font-weight: 300; }
.ey  { font-size: 11px; letter-spacing: .22em; text-transform: uppercase; } /* eyebrow */
```

Itálico no `<span>` de destaque dentro de títulos (`.h1 span { font-style: italic; color: var(--ac) }`) — mesma técnica do Jasminny, adaptada à cor de marca.

---

## ⚠️ Convenção de classes desta página (ler antes de reaproveitar)

Esta LP **não segue** o prefixo de 2-3 letras por seção documentado no `SKILL.md` principal. Em vez disso, usa:
- Um único wrapper `.ep` (Eberick Protendido) envolvendo a página inteira;
- Classes curtas e genéricas dentro dele: `.hero`, `.cta`, `.sc`, `.mod`, `.faq`, `.offer`...

Isso funciona **porque é uma landing page mono-bloco** (um scroll único, nada mais na página). **Risco real**: se este padrão for copiado para um site institucional com múltiplos blocos HTML independentes na mesma página, `.hero`/`.cta`/`.mod` têm nome comum o suficiente para colidir com CSS de outro bloco.

**Regra para novos projetos**: se for landing page única e completa → pode usar wrapper único + classes curtas (mais legível). Se for seção avulsa dentro de um site maior → usar prefixo dedicado (ex. `kk-` para Kikuchi) conforme o padrão do `SKILL.md`.

---

## Componentes específicos deste projeto

### 1. Card de custo/dado (3 colunas, número grande + descrição)

```html
<div class="cost-grid">
  <div class="cost-card">
    <div class="cost-val">R$ 5k–15k</div>
    <div class="cost-desc">Honorário médio de um único projeto protendido de laje + vigas</div>
  </div>
  <!-- repetir -->
</div>
```

```css
.cost-grid { display:grid; grid-template-columns:repeat(3,1fr); gap:1.25rem; max-width:900px; margin:0 auto 2.5rem; }
.cost-card { background:var(--cd); border:1px solid var(--bd); border-radius:4px; padding:2rem 1.5rem; text-align:center; transition:border-color .3s; }
.cost-card:hover { border-color:rgba(200,90,40,.3); }
.cost-val { font-family:var(--fd); font-size:2.4rem; font-weight:300; color:var(--ac); font-style:italic; line-height:1; margin-bottom:8px; }
.cost-desc { font-size:14px; color:var(--mt); font-weight:300; line-height:1.6; }
```
Uso: quantificar dor/custo de oportunidade com números concretos — reaproveitar sempre que o produto tiver ROI mensurável (cursos técnicos, consultorias, B2B).

### 2. Box de reframe (virada de chave, com glow radial)

```css
.reframe { background:var(--cd); border:1px solid rgba(200,90,40,.2); border-radius:4px; padding:3.5rem; text-align:center; max-width:900px; margin:0 auto; position:relative; overflow:hidden; }
.reframe-glow { position:absolute; inset:0; background:radial-gradient(ellipse at center,var(--acg) 0%,transparent 70%); pointer-events:none; }
.reframe-acc { display:block; margin-top:2rem; font-family:var(--fd); font-style:italic; color:var(--ac); font-size:clamp(1.2rem,2.4vw,1.8rem); }
```
Mesmo padrão serve para `.more` (reforço) e `.offer` (oferta) — é o "box de destaque com glow" genérico da paleta Kikuchi.

### 3. Grid "para quem é / não é" (qualificação binária)

```css
.whom-grid { display:grid; grid-template-columns:1fr 1fr; gap:1.5rem; max-width:900px; margin:0 auto; }
.whom-col  { background:var(--cd); border:1px solid var(--bd); border-radius:4px; padding:2rem; }
.whom-yes h3 { color:var(--ok); }
.whom-no h3  { color:#e57373; }
.whom-yes li::before { content:'\2713'; color:var(--ok); font-weight:700; }
.whom-no li::before  { content:'\2717'; color:#e57373; font-weight:700; }
```
Reaproveitar em qualquer produto/infoproduto para pré-qualificar lead e reduzir reembolso — funciona bem antes da seção de oferta.

### 4. Card de módulo/curso com accordion nativo (sem JS)

```html
<div class="mod">
  <img src="..." alt="Módulo 01" loading="lazy">
  <div class="mod-ct">
    <div class="mod-num">01</div>
    <span class="mod-tag">10 aulas</span>
    <div class="mod-name">Nome do Módulo</div>
    <div class="mod-desc">Descrição curta do módulo.</div>
    <details>
      <summary>Ver aulas do módulo</summary>
      <ul class="mod-lessons">
        <li class="mod-lesson"><span class="mod-lesson-n">01</span>Nome da aula</li>
      </ul>
    </details>
  </div>
</div>
```

```css
.mod summary { list-style:none; cursor:pointer; display:flex; justify-content:space-between; }
.mod summary::-webkit-details-marker { display:none; }
.mod summary::after { content:'+'; font-family:var(--fd); }
.mod details[open] summary::after { content:'\2212'; }
```

**Padrão importante a padronizar em todos os projetos**: usar `<details>/<summary>` nativo para qualquer accordion (FAQ, grade de curso, especificações) em vez de JS. Vantagens: zero dependência de JavaScript do construtor de sites, acessível por teclado por padrão, funciona mesmo se o site travar algum script. Único cuidado: sempre remover o marcador nativo do navegador via `summary::-webkit-details-marker{display:none}` e criar o `+`/`−` custom via `::after`.

### 5. Ancoragem de preço por comparação real (não inflada)

```html
<div class="price-compare">
  <div class="price-alt">
    <div class="price-alt-name">Pós-Graduação em Estruturas</div>
    <div class="price-alt-val">R$ 8.000+</div>
  </div>
  <div class="price-alt">
    <div class="price-alt-name">Consultoria particular</div>
    <div class="price-alt-val">R$ 3.000+</div>
  </div>
</div>
```

```css
.price-compare { display:grid; grid-template-columns:1fr 1fr; gap:1rem; max-width:480px; margin:0 auto 1.5rem; text-align:left; }
.price-alt { background:rgba(255,255,255,.02); border:1px solid var(--bd); border-radius:4px; padding:14px 18px; }
.price-alt-val { font-family:var(--fd); font-style:italic; text-decoration:line-through; color:var(--mt); }
```

Preferir **sempre** este padrão de ancoragem (comparar com alternativas reais do mercado) em vez de "de R$X por R$Y" com valor "de" inflado artificialmente — mais crível para público técnico/cético, e replicável em qualquer nicho B2B/profissional liberal.

### 6. Lista de dor (`.pains`) e lista de stack/oferta (`.stack`)

Mesmo componente-base (lista com borda, separador entre itens, ícone antes do texto), reaproveitado em dois contextos:

```css
.pains, .stack, .faq, .sol-list { border:1px solid var(--bd); border-radius:4px; overflow:hidden; }
.pain, .stack li, .sol-li { border-bottom:1px solid var(--bd); padding:1.4rem 1.75rem; }
.pain:last-child, .stack li:last-child { border-bottom:none; }
```
Esse "container com lista + separadores + borda" é o padrão-base para: dores, itens do que está incluso, bullets de solução, FAQ. Um único bloco de CSS serve para os quatro usos — vale generalizar como classe utilitária `.bordered-list` em projetos futuros.

---

## Responsivo (breakpoints usados)

```css
@media (max-width: 920px) { /* grids 2-col → 1-col, imagem primeiro (order:-1) */ }
@media (max-width: 700px) { /* grids 3-col → 1-col */ }
@media (max-width: 520px) { /* mobile: CTA full-width, paddings reduzidos */ }
```
Três breakpoints (920/700/520) em vez dos dois padrão (860/480) do `SKILL.md` — mais granular para grids de 3 colunas (`.cost-grid`, `.proofs`). Adotar 3 breakpoints sempre que houver grid de 3+ colunas no design.

---

## Checklist de débito técnico identificado (corrigir ao reaproveitar)

- [ ] **Imagens em base64 são pesadas** (nesta LP, 7 imagens somaram ~450KB decodificados = ~93% do peso da página). Preferir comprimir para WebP e/ou hospedar como URL externa quando o arquivo final ultrapassar ~200-300KB total — página lenta mata connect rate de tráfego pago.
- [ ] Definir `aspect-ratio` nos containers de imagem (`.capa`, `.sol-img`, `.mod img`) para evitar layout shift — não foi feito nesta LP.
- [ ] Testar contraste de `--mt` em fontes pequenas antes de usar como texto principal.
- [ ] Elementos como `.mod-name` e `.auth-name` deveriam ser `<h3>`, não `<div>`, para manter hierarquia semântica de heading.
