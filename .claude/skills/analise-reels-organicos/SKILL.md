---
name: analise-reels-organicos
description: >
  Analisa os últimos Reels orgânicos do Instagram via Meta Graph API (alcance, engajamento, watch time,
  viralidade), classifica cada Reel por desempenho, identifica padrões de conteúdo de alta e baixa
  performance, recomenda quais Reels impulsionar e sugere 3 novos roteiros com copy pronta. Use esta
  skill SEMPRE que o usuário pedir análise de Reels, performance de conteúdo orgânico no Instagram,
  estratégia de conteúdo, recomendação de impulsionamento de Reels, ou invocar /analise-reels-organico.
---

# Analise de Reels Organicos + Estrategia de Conteudo

## Requisitos para Execucao

Antes de rodar esta analise, voce precisa ter:

- **Conta Meta/Instagram conectada** com token valido (`credentials/meta.env`)
- **IG User ID** da conta a ser analisada (em `CLAUDE.md` ou `CLIENT.md`)
- **Permissoes da API**: `instagram_basic`, `instagram_manage_insights`, `pages_read_engagement`
- **Meta Graph API v21.0** ou superior
- Pelo menos **7 Reels publicados** na conta

> Execute `/conectar-meta` caso ainda nao tenha configurado a conexao.

> **Skill disponivel**: Execute `/analise-reels-organico` para rodar toda esta analise automaticamente com dashboard HTML interativo.

---

## 1. Coleta de Dados

Puxe os **ultimos N Reels organicos** (padrao: 7) do Instagram via Meta Graph API:

| Metrica | Campo API | Nota |
|---------|-----------|------|
| Titulo / Legenda | `caption` | Via fields |
| Data de publicacao | `timestamp` | Via fields |
| Thumbnail | `thumbnail_url` | Via fields |
| Link permanente | `permalink` | Via fields |
| Alcance | `reach` | Via insights |
| Curtidas | `like_count` | Via fields (NAO insights) |
| Comentarios | `comments_count` | Via fields (NAO insights) |
| Compartilhamentos | `shares` | Via insights |
| Salvamentos | `saved` | Via insights |
| Interacoes totais | `total_interactions` | Via insights |
| Watch time medio | `ig_reels_avg_watch_time` | Milissegundos — dividir por 1000 |
| View time total | `ig_reels_video_view_total_time` | Milissegundos — converter para horas |

**IMPORTANTE**: A metrica `plays` foi descontinuada na v22.0+. NAO usar.

### Formulas calculadas

```
Engagement Rate = (likes + comments + shares + saves) / reach * 100
Watch Time (s)  = ig_reels_avg_watch_time / 1000
View Time (h)   = ig_reels_video_view_total_time / 3600000
Coef. Viralidade = shares / reach * 100
```

---

## 2. Analise de Performance

Para cada Reel, classifique como **TOP**, **Alto**, **Medio** ou **Baixo** desempenho:

| Classificacao | Criterio |
|---------------|----------|
| **TOP** | Melhor Reel do periodo (eng rate mais alto) |
| **ALTO** | Eng rate > media + 20% |
| **MEDIO** | Dentro de +-20% da media |
| **BAIXO** | Eng rate < media - 30% |

Indicadores secundarios:
- Compartilhamentos e salvamentos (indicadores de valor percebido)
- Relacao shares/alcance (coeficiente de viralidade — acima de 4% = viral)
- Watch time medio vs. media do periodo

**Saida esperada:** Tabela comparativa ranqueando os Reels do melhor ao pior, com todas as metricas e badge de classificacao.

---

## 3. Identificacao de Padroes

Identifique padroes nos Reels de melhor performance:

- **Tipo de conteudo**: educativo, bastidores, antes/depois, depoimento, trend, humor
- **Duracao do video**: correlacao com retencao
- **Gancho nos primeiros 3 segundos**: qual frase ou elemento visual prendeu atencao
- **CTA utilizado**: comentar palavra-chave, salvar, seguir, link bio
- **Horario e dia de publicacao**: correlacao com alcance
- **Formato da legenda**: curta vs. longa, com ou sem estrutura (problema + resultado + CTA)

**Saida esperada:** Dois blocos contrastantes:
1. **O que funciona** (padroes dos Reels TOP/ALTO) — bullets com evidencias
2. **O que NAO funciona** (padroes dos Reels BAIXO) — bullets com evidencias

---

## 4. Recomendacao de Impulsionamento

Indique **quais Reels valem a pena impulsionar** com prioridade:

**Criterios de selecao:**
- Alto engajamento organico (acima da media)
- Tema alinhado com conversao / objetivo do negocio
- Boa retencao (watch time acima da media)
- Coeficiente de viralidade alto (shares/reach)

**Para cada Reel recomendado, incluir:**

| Campo | Descricao |
|-------|-----------|
| Prioridade | 1 (investir agora), 2 (segunda onda), 3 (monitorar) |
| Por que este | Justificativa com metricas concretas |
| Publico-alvo | Lookalike, interesses, retargeting |
| Objetivo | Alcance, engajamento, trafego |
| Orcamento | R$/dia x N dias |

Indicar tambem quais Reels NAO impulsionar e justificar.

---

## 5. Sugestao de 3 Novos Reels

Proponha **3 roteiros de Reels** baseados nos padroes identificados na Secao 3:

| Item | Descricao |
|------|-----------|
| **Tema** | Assunto principal |
| **Formato** | Educativo, trend, bastidores, etc. |
| **Duracao sugerida** | Em segundos |
| **Gancho (0-3s)** | Frase ou acao que abre o video |
| **Estrutura** | Passo a passo do conteudo |
| **CTA final** | O que o espectador deve fazer |
| **Por que funciona** | Conexao com os padroes de alto desempenho |

---

## 6. Copy para Cada Reel Sugerido

Para cada um dos 3 Reels propostos, escreva:

- **Legenda completa**: gancho + corpo + CTA
- **5 hashtags** relevantes ao nicho
- **Texto de capa** (se aplicavel)

---

## Formato de Saida

### Texto (padrao)
Relatorio organizado em secoes com:
- Tabelas comparativas de metricas
- Ranking de performance
- Recomendacoes acionaveis e objetivas
- Roteiros prontos para producao

### HTML (recomendado)
Dashboard interativo seguindo `reports/STYLE-GUIDE.md`:
- Dark/light toggle
- KPI cards, graficos Chart.js, thumbnails
- Cards com border-left colorido por classificacao
- Dados embarcados como JSON, renderizados via JavaScript
- Responsivo (desktop, tablet, mobile)

> Use `/analise-reels-organico` para gerar automaticamente o dashboard HTML completo.
