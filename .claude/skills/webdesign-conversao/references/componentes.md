# Componentes Reutilizáveis — Webdesign para Conversão

Código extraído do projeto real Jasminny Amorim Concept Beauty. Adaptar tokens e textos a cada novo projeto.

---

## 1. Botão Primário (dourado com shine)

```html
<a href="URL" target="_blank" rel="noopener noreferrer" class="btn btn--gold">
  <span class="btn-shine"></span>
  Texto do Botão
</a>
```

```css
.btn {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  gap: 10px;
  position: relative;
  overflow: hidden;
  border-radius: 999px;
  font-family: 'Poppins', sans-serif;
  font-size: clamp(12px, 1.5vw, 14px);
  font-weight: 700;
  letter-spacing: 1.5px;
  text-transform: uppercase;
  padding: 16px 40px;
  cursor: pointer;
  text-decoration: none;
  transition: transform .2s, box-shadow .2s, filter .2s;
  -webkit-tap-highlight-color: transparent;
}
.btn--gold {
  background: linear-gradient(135deg, var(--gold) 0%, #a07840 100%);
  color: #080706;
  border: 1px solid rgba(201,169,110,.5);
  box-shadow: 0 8px 32px rgba(201,169,110,.35), 0 0 0 1px rgba(201,169,110,.4);
}
.btn--gold:hover {
  transform: translateY(-2px);
  box-shadow: 0 14px 44px rgba(201,169,110,.5), 0 0 0 1px rgba(201,169,110,.6);
  filter: brightness(1.08);
}
.btn--gold:active { transform: translateY(0); }

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

---

## 2. Botão Outline (secundário)

```html
<a href="URL" target="_blank" rel="noopener noreferrer" class="btn btn--outline">
  <svg><!-- ícone --></svg>
  Texto
</a>
```

```css
.btn--outline {
  background: transparent;
  color: var(--gold-light);
  border: 1px solid rgba(201,169,110,.4);
  box-shadow: 0 4px 16px rgba(0,0,0,.3), inset 0 1px 0 rgba(201,169,110,.1);
}
.btn--outline:hover {
  background: rgba(201,169,110,.08);
  border-color: rgba(201,169,110,.7);
  box-shadow: 0 8px 28px rgba(201,169,110,.2);
  color: var(--champagne);
  transform: translateY(-2px);
}
```

---

## 3. Grupo de 3 botões (WhatsApp + Fresha + Instagram)

```html
<div class="btn-group">
  <a href="https://api.whatsapp.com/send?phone=NUMERO&text=TEXTO"
     target="_blank" rel="noopener noreferrer" class="btn btn--gold">
    <span class="btn-shine"></span>
    <svg viewBox="0 0 24 24" fill="currentColor" width="17" height="17">
      <path d="M17.472 14.382c-.297-.149-1.758-.867-2.03-.967-.273-.099-.471-.148-.67.15-.197.297-.767.966-.94 1.164-.173.199-.347.223-.644.075-.297-.15-1.255-.463-2.39-1.475-.883-.788-1.48-1.761-1.653-2.059-.173-.297-.018-.458.13-.606.134-.133.298-.347.446-.52.149-.174.198-.298.298-.497.099-.198.05-.371-.025-.52-.075-.149-.669-1.612-.916-2.207-.242-.579-.487-.5-.669-.51a12.8 12.8 0 00-.57-.01c-.198 0-.52.074-.792.372-.272.297-1.04 1.016-1.04 2.479 0 1.462 1.065 2.875 1.213 3.074.149.198 2.096 3.2 5.077 4.487.709.306 1.262.489 1.694.625.712.227 1.36.195 1.871.118.571-.085 1.758-.719 2.006-1.413.248-.694.248-1.289.173-1.413-.074-.124-.272-.198-.57-.347m-5.421 7.403h-.004a9.87 9.87 0 01-5.031-1.378l-.361-.214-3.741.982.998-3.648-.235-.374a9.86 9.86 0 01-1.51-5.26c.001-5.45 4.436-9.884 9.888-9.884 2.64 0 5.122 1.03 6.988 2.898a9.825 9.825 0 012.893 6.994c-.003 5.45-4.437 9.884-9.885 9.884m8.413-18.297A11.815 11.815 0 0012.05 0C5.495 0 .16 5.335.157 11.892c0 2.096.547 4.142 1.588 5.945L.057 24l6.305-1.654a11.882 11.882 0 005.683 1.448h.005c6.554 0 11.89-5.335 11.893-11.893a11.821 11.821 0 00-3.48-8.413z"/>
    </svg>
    Agendar
  </a>

  <a href="URL_FRESHA" target="_blank" rel="noopener noreferrer" class="btn btn--outline">
    <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" width="17" height="17">
      <rect x="3" y="4" width="18" height="17" rx="2"/>
      <path d="M3 9h18M8 2v4M16 2v4"/>
    </svg>
    Fresha
  </a>

  <a href="URL_INSTAGRAM" target="_blank" rel="noopener noreferrer" class="btn btn--outline">
    <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" width="17" height="17">
      <rect x="2" y="2" width="20" height="20" rx="5"/>
      <circle cx="12" cy="12" r="5"/>
      <circle cx="17.5" cy="6.5" r="1" fill="currentColor" stroke="none"/>
    </svg>
    Instagram
  </a>
</div>
```

```css
.btn-group {
  display: flex;
  flex-wrap: wrap;
  gap: 14px;
  align-items: center;
}
@media (max-width: 480px) {
  .btn-group { flex-direction: column; }
  .btn-group .btn { width: 100%; justify-content: center; }
}
```

---

## 4. Ornamento de seção (linha + ponto + linha)

```html
<div class="ornament">
  <span class="ornament-line"></span>
  <span class="ornament-dot"></span>
  <span class="ornament-line ornament-line--rev"></span>
</div>
```

```css
.ornament {
  display: flex;
  align-items: center;
  gap: 12px;
  margin: 20px 0 28px;
}
.ornament-line {
  display: block;
  height: 1px;
  width: 48px;
  background: linear-gradient(90deg, var(--gold), transparent);
}
.ornament-line--rev {
  background: linear-gradient(90deg, transparent, var(--gold));
}
.ornament-dot {
  width: 4px; height: 4px;
  border-radius: 50%;
  background: var(--gold);
  flex-shrink: 0;
  box-shadow: 0 0 8px rgba(201,169,110,.7);
}
```

---

## 5. Eyebrow + Título de seção

```html
<div class="section-line"></div>
<p class="eyebrow">Texto do eyebrow</p>
<h2 class="titulo">
  Título principal<br>
  <em>com itálico dourado</em>
</h2>
```

```css
.section-line {
  width: 48px; height: 2px;
  background: var(--gold);
  margin-bottom: 20px;
}
.eyebrow {
  font-size: clamp(9px, 1.4vw, 11px);
  font-weight: 600;
  letter-spacing: 3.5px;
  text-transform: uppercase;
  color: var(--gold);
  margin-bottom: 16px;
  text-shadow: 0 0 20px rgba(201,169,110,.3);
}
.titulo {
  font-family: 'Cormorant Garamond', serif;
  font-size: clamp(34px, 5vw, 68px);
  font-weight: 300;
  line-height: 1.08;
  color: var(--white);
  margin-bottom: 24px;
  text-shadow: 0 0 60px rgba(201,169,110,.12);
}
.titulo em {
  font-style: italic;
  color: var(--gold-light);
  font-weight: 400;
}
```

---

## 6. Frame de foto com bordas decorativas

```html
<div class="foto-frame">
  <img class="foto" src="URL" alt="Descrição" loading="lazy">
  <!-- badges opcionais aqui -->
</div>
```

```css
.foto-frame {
  position: relative;
  border-radius: 20px;
  overflow: hidden;
  box-shadow:
    0 0 0 1px rgba(201,169,110,.15),
    0 24px 60px rgba(0,0,0,.8),
    0 0 48px rgba(201,169,110,.08);
}
/* Borda decorativa superior direita */
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
/* Borda decorativa inferior esquerda */
.foto-frame::after {
  content: '';
  position: absolute;
  bottom: -1px; left: -1px;
  width: 35%; height: 35%;
  border-bottom: 1px solid rgba(201,169,110,.25);
  border-left: 1px solid rgba(201,169,110,.25);
  pointer-events: none;
  z-index: 3;
}
.foto {
  width: 100%;
  display: block;
  object-fit: cover;
  border-radius: 20px;
  transition: transform .6s ease;
}
.foto-frame:hover .foto { transform: scale(1.04); }
```

---

## 7. Badge flutuante sobre foto

```html
<!-- Badge de número/estatística (canto inferior esquerdo) -->
<div class="badge-stat">
  <span class="badge-num">10K+</span>
  <span class="badge-label">Transformações</span>
</div>

<!-- Badge de texto (canto superior direito) -->
<div class="badge-text">
  <span>★★★★★</span>
  <span class="badge-sub">5 estrelas</span>
</div>
```

```css
.badge-stat, .badge-text {
  position: absolute;
  z-index: 4;
  background: #0a0906;
  border: 1px solid rgba(201,169,110,.3);
  border-radius: 12px;
  padding: 12px 18px;
  box-shadow:
    0 8px 32px rgba(0,0,0,.8),
    0 0 16px rgba(201,169,110,.1),
    inset 0 1px 0 rgba(201,169,110,.1);
}
.badge-stat { bottom: 28px; left: -16px; }
.badge-text { top: 20px; right: -16px; display: flex; flex-direction: column; align-items: center; gap: 4px; }

.badge-num {
  font-family: 'Cormorant Garamond', serif;
  font-size: clamp(26px, 3vw, 36px);
  font-weight: 600;
  color: var(--gold-light);
  display: block;
  text-shadow: 0 0 20px rgba(201,169,110,.4);
}
.badge-label, .badge-sub {
  font-size: 9px;
  font-weight: 600;
  letter-spacing: 2px;
  text-transform: uppercase;
  color: var(--muted);
}
```

---

## 8. Card de serviço

```html
<div class="service-card">
  <div class="service-card-img">
    <img src="URL" alt="Nome do serviço" loading="lazy">
  </div>
  <div class="service-card-body">
    <h4 class="service-name">Nome do Serviço</h4>
    <p class="service-tag">Para quem quer X</p>
    <p class="service-desc">Descrição curta e sofisticada do serviço.</p>
    <div class="service-footer">
      <span class="service-price">99€</span>
      <a href="URL" target="_blank" rel="noopener noreferrer" class="btn btn--gold btn--sm">
        <span class="btn-shine"></span>Agendar
      </a>
    </div>
  </div>
</div>
```

```css
.service-card {
  background: var(--card);
  border: 1px solid var(--border);
  border-radius: 16px;
  overflow: hidden;
  display: flex;
  flex-direction: column;
  transition: transform .3s, border-color .3s, box-shadow .3s;
  box-shadow: 0 4px 20px rgba(0,0,0,.4);
}
.service-card:hover {
  transform: translateY(-5px);
  border-color: var(--border-h);
  box-shadow: 0 14px 40px rgba(0,0,0,.55), 0 0 20px rgba(201,169,110,.08);
}
.service-card-img { aspect-ratio: 16/9; overflow: hidden; }
.service-card-img img {
  width: 100%; height: 100%;
  object-fit: cover; display: block;
  transition: transform .5s ease;
}
.service-card:hover .service-card-img img { transform: scale(1.07); }

.service-card-body {
  padding: clamp(16px, 3vw, 22px);
  display: flex; flex-direction: column; flex: 1;
}
.service-name {
  font-family: 'Cormorant Garamond', serif;
  font-size: clamp(18px, 2.5vw, 22px);
  font-weight: 400;
  color: var(--champagne);
  margin-bottom: 6px;
}
.service-tag {
  font-size: clamp(11px, 1.5vw, 12px);
  font-weight: 300;
  color: var(--gold-light);
  font-style: italic;
  margin-bottom: 8px;
}
.service-desc {
  font-size: clamp(11px, 1.8vw, 13px);
  font-weight: 300;
  line-height: 1.7;
  color: var(--muted);
  flex: 1;
  margin-bottom: 16px;
}
.service-footer {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 10px;
  flex-wrap: wrap;
}
.service-price {
  font-family: 'Cormorant Garamond', serif;
  font-size: clamp(20px, 2.5vw, 26px);
  font-weight: 500;
  color: var(--gold-light);
}
.btn--sm { padding: 10px 22px; font-size: clamp(10px, 2vw, 12px); }

@media (max-width: 480px) {
  .service-footer { flex-direction: column; align-items: flex-start; }
  .service-footer .btn { width: 100%; justify-content: center; }
}
```

---

## 9. Layout hero 2 colunas (foto + texto)

```html
<div class="hero-wrap">
  <div class="hero-inner">
    <div class="hero-content">
      <!-- eyebrow, título, ornamento, texto, botões -->
    </div>
    <div class="hero-photo-col">
      <div class="foto-frame">
        <img class="foto" src="URL" alt="Alt" loading="eager">
        <!-- badges flutuantes opcionais -->
      </div>
    </div>
  </div>
</div>
```

```css
.hero-wrap {
  /* wrapper full-width */
  margin-left: calc(-50vw + 50%);
  margin-right: calc(-50vw + 50%);
  width: 100vw !important;
  max-width: 100vw !important;
  background: var(--bg);
  overflow: hidden;
}
.hero-inner {
  max-width: 1280px;
  margin: 0 auto;
  display: grid;
  grid-template-columns: 1fr 1fr;
  align-items: center;
  gap: clamp(40px, 6vw, 80px);
  padding: clamp(72px, 10vw, 130px) clamp(24px, 5vw, 80px);
}
@media (max-width: 860px) {
  .hero-inner {
    grid-template-columns: 1fr;
    padding: 60px 20px 56px;
  }
  .hero-photo-col { order: -1; } /* foto acima no mobile */
}
```

---

## 10. Formulário de pedido dark (WhatsApp)

Padrão de formulário com checkboxes visuais, envio via WhatsApp. Consultar código completo no arquivo `jasminny-formulario.html` produzido na conversa de referência. Elementos-chave:

- Input de nome com `font-size: max(16px, ...)` para evitar zoom automático no iOS
- Checkboxes customizados com `display: none` + label visual
- Validação inline antes do envio
- Mensagem formatada com markdown WhatsApp (`*bold*`) gerada por JS
- Abertura via `window.open(url, '_blank')`

---

## Tokens de referência — Projeto Jasminny (dark luxury)

```css
:root {
  --gold:        #c9a96e;
  --gold-light:  #e2c99a;
  --champagne:   #f4e9d6;
  --white:       #ffffff;
  --muted:       #9a8a78;
  --text-body:   #b0a090;
  --bg:          #000000;
  --card:        #13110e;
  --card2:       #1a1612;
  --border:      rgba(185,155,100,.18);
  --border-h:    rgba(201,169,110,.45);
}
/* Fontes: Cormorant Garamond (display) + Poppins (UI) */
```

**Outros perfis de paleta para adaptar:**

| Estilo | Bg | Primária | Texto |
|---|---|---|---|
| Light luxury | `#faf8f5` | `#b89660` | `#2e2420` |
| Dark luxury (Jasminny) | `#000000` | `#c9a96e` | `#f4e9d6` |
| Clínica/clean | `#f5f5f5` | `#4a7c6f` | `#1a1a1a` |
| Bold/moderno | `#0d0d0d` | `#e63946` | `#ffffff` |
