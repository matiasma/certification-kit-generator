# 🎓 Prompt Reutilizável v3 — Kit de Estudo para Certificações (foco INICIANTES)

> **v3 = otimizado para INICIANTES**, mantendo 100% dos guard rails de fonte oficial da v2. Adiciona 5 melhorias pedagógicas: diagnóstico inicial, primer de fundamentos, labs em modo dual (guiado + speedrun), glossário + mapa conceitual, e ciclo de active recall (flashcards + mistake log).
>
> **Diferença vs v2:** v2 assume conhecimento intermediário e otimiza para revisão. v3 calibra o ponto de partida do candidato e adiciona scaffolding pedagógico para quem nunca fez certificação ou está entrando na tecnologia.
>
> **Guard rails preservados:** zero referências a terceiros; apenas `<<OFFICIAL_DOCS_DOMAIN>>` e subdomínios oficiais do vendor; validação obrigatória via MCP.

---

## 📋 Variáveis

> 💡 **Otimizado para iniciantes:** você só precisa preencher **5 variáveis obrigatórias**. As demais têm valores padrão ou são descobertas automaticamente pelo agente.

### ✅ Obrigatórias — VOCÊ preenche

| Variável | Exemplo | Descrição |
|---|---|---|
| `<<EXAM_CODE>>` | `AZ-204`, `AWS-SAA-C03`, `CKA`, `GH-200`, `TF-Associate` | Código oficial do exame |
| `<<DAYS_AVAILABLE>>` | `7`, `15`, `30`, `flexível` | Dias até o exame |
| `<<HOURS_PER_DAY>>` | `1`, `2`, `4` | Horas de estudo por dia |
| `<<EXPERIENCE_LEVEL>>` | `iniciante absoluto`, `iniciante com base`, `intermediário` | Seu nível autodeclarado (o diagnóstico calibra no Dia 0) |
| `<<PREFERRED_LANGUAGE>>` | `pt-BR`, `en-US`, `es-ES` | Idioma de saída do kit |

### 🟡 Opcionais — preencha se souber (têm padrão sensato)

| Variável | Padrão | Exemplo |
|---|---|---|
| `<<EXAM_DATE>>` | `não marcada` | `2026-06-15` |
| `<<PRIOR_CERTS>>` | `nenhuma` | `AZ-900, AZ-104` |
| `<<STRONG_AREAS>>` | `desconhecido` | `redes, infra` |
| `<<WEAK_AREAS>>` | `desconhecido` | `segurança, bancos de dados` |
| `<<NOTE_TOOL>>` | `nenhum` | `OneNote`, `Notion`, `Obsidian` |
| `<<OUTPUT_FORMAT>>` | **`html`** | `html` \| `markdown` |

#### 📄 Sobre `<<OUTPUT_FORMAT>>` — qual escolher?

| Formato | Quando usar | Vantagens | Limitações | Custo de tokens (output) |
|---|---|---|---|---|
| **`html`** ⭐ (padrão) | Estudo no navegador, leitura offline, impressão, compartilhamento com não-devs | Visual rico (toggle de tema claro/escuro com persistência, TOC, syntax highlight), Mermaid renderiza nativo via CDN, busca no navegador (Ctrl+F), navegação clicável entre arquivos, abre com duplo-clique sem ferramentas, ideal para imprimir/salvar PDF | Diff de Git ruim, edição manual mais chata, importação em apps de notas (Obsidian/Notion) exige conversão | **Alto** — cada arquivo carrega ~80-150 linhas de scaffold (CSS, paletas dark/light, header sticky, script de toggle anti-FOUC, footer). Um kit de ~30 arquivos consome **~3x mais tokens de output** que a versão markdown e tipicamente força ≥1 compactação de contexto durante a geração. |
| **`markdown`** | Versionar no Git, importar em Obsidian/Notion/Logseq, editar com agente de IA, pipelines de docs | Diff limpo, editável em qualquer editor, compatível com ferramentas de notas, leve, fácil de pós-processar (scripts, conversores) | Sem estilização nativa, Mermaid depende do renderizador, abrir fora do VS Code/GitHub pede plugin | **Baixo** — só o conteúdo (headings, listas, tabelas, blocos de código). Tipicamente cabe na janela de contexto sem compactação para a maioria dos exames. |

> 💡 **Recomendação:** se você é iniciante e vai estudar abrindo arquivos no navegador, mantenha **`html`**. Se você usa Obsidian/Notion ou versiona no Git e revisa diffs, use **`markdown`**. Você sempre pode regerar trocando essa variável.
>
> ⚙️ **Nota sobre custo/contexto (LLMs):** o modo `html` é significativamente mais caro em tokens de saída por causa do scaffold embutido em cada arquivo (CSS dual-palette + script de toggle). Em modelos com janela menor ou cobrança por token de output, isso se traduz em geração mais lenta, compactações intermediárias da conversa e fatura maior. Se você só quer o **conteúdo** e tem orçamento de tokens apertado, use `markdown` e converta para HTML depois (ex.: `pandoc arquivo.md -o arquivo.html`). Se você prioriza a experiência final de leitura/PDF, mantenha `html` e aceite o custo. **Regra prática:** kit completo em html ≈ 80-120 mil tokens de output; em markdown ≈ 25-40 mil.

### 🤖 Auto-derivadas — o AGENTE descobre (não precisa preencher)

> Se você é iniciante, **não precisa saber** detalhes técnicos como o domínio oficial da documentação. O agente vai derivar a partir do `<<EXAM_CODE>>` consultando as fontes oficiais via MCP.

| Variável | Como o agente descobre |
|---|---|
| `<<EXAM_NAME>>` | Busca na página oficial do exame a partir do código |
| `<<EXAM_VENDOR>>` | Deriva do prefixo do código (ex: `AZ-` → Microsoft, `AWS-` → AWS, `CK` → CNCF, `GH-` → GitHub, `TF-` → HashiCorp) |
| `<<OFFICIAL_DOCS_DOMAIN>>` | Identifica o domínio canônico de docs do vendor (ex: `learn.microsoft.com`, `docs.aws.amazon.com`, `kubernetes.io`, `docs.github.com`, `developer.hashicorp.com`) |
| `<<VENDOR_LEARNING_PLATFORM>>` | Identifica a plataforma oficial de aprendizagem do vendor |

> Deixe esses campos com placeholders se preferir (`<<OFFICIAL_DOCS_DOMAIN>>`); o agente sobrescreve com os valores corretos antes de gerar conteúdo.

---

### Exemplo mínimo (só obrigatórias)

```
<<EXAM_CODE>> = AZ-204
<<DAYS_AVAILABLE>> = 15
<<HOURS_PER_DAY>> = 2
<<EXPERIENCE_LEVEL>> = iniciante com base
<<PREFERRED_LANGUAGE>> = pt-BR
```

Isso é suficiente. O agente descobre o resto e usa `<<OUTPUT_FORMAT>>=html` por padrão.

---

## 🚀 PROMPT — copie a partir daqui (entre as cercas)

<!-- AGENT_PROMPT_START -->
````
Você é um instrutor especialista em certificações técnicas, com foco pedagógico em CANDIDATOS INICIANTES. Crie, **dentro deste workspace**, um kit COMPLETO, executável, auto-contido e CALIBRADO ao nível real do candidato para a certificação abaixo.

## ⚙️ Passo 0 — Resolver variáveis auto-deriváveis (ANTES de gerar qualquer arquivo)

Para reduzir o atrito ao usuário iniciante, ele só preencheu as variáveis essenciais. **Você deve descobrir as demais** a partir do `<<EXAM_CODE>>` consultando fontes oficiais via MCP/fetch:

1. Identifique `<<EXAM_VENDOR>>` pelo prefixo/padrão do código (`AZ-`, `AI-`, `DP-`, `SC-`, `MS-`, `PL-` → Microsoft; `AWS-` ou `CLF-`, `SAA-`, `DVA-`, `SOA-` → AWS; `CKA`, `CKAD`, `CKS` → CNCF; `GH-` → GitHub; `TF-` → HashiCorp; `LFCS`, `LFCT` → Linux Foundation; outros: pesquise).
2. Determine `<<OFFICIAL_DOCS_DOMAIN>>` canônico do vendor (`learn.microsoft.com`, `docs.aws.amazon.com`, `kubernetes.io`, `docs.github.com`, `developer.hashicorp.com`, `docs.linuxfoundation.org`, etc.).
3. Determine `<<VENDOR_LEARNING_PLATFORM>>` (`learn.microsoft.com/training`, `aws.amazon.com/training`, `kubernetes.io/training`, `skills.github.com`, `developer.hashicorp.com/tutorials`, `training.linuxfoundation.org`, etc.).
4. Busque `<<EXAM_NAME>>` oficial na página do exame do vendor.
5. Para campos opcionais não preenchidos, aplique padrões: `<<EXAM_DATE>>=não marcada`, `<<PRIOR_CERTS>>=nenhuma`, `<<STRONG_AREAS>>=desconhecido`, `<<WEAK_AREAS>>=desconhecido`, `<<NOTE_TOOL>>=nenhum`, **`<<OUTPUT_FORMAT>>=html`**.
6. **Confirme os valores resolvidos** em uma mensagem curta antes de criar arquivos. Se não conseguir resolver com confiança (ex: código de exame ambíguo ou inválido), pergunte ao usuário. Sempre **anuncie explicitamente o formato de saída escolhido** (`html` ou `markdown`) para o usuário poder corrigir antes da geração.

A partir daqui, trate todas as variáveis como resolvidas e use seus valores reais em todo o conteúdo gerado.

## Contexto da certificação
- **Código / Nome / Vendor:** <<EXAM_CODE>> / <<EXAM_NAME>> / <<EXAM_VENDOR>>
- **Docs oficiais canônicas:** <<OFFICIAL_DOCS_DOMAIN>>
- **Plataforma oficial de aprendizagem do vendor:** <<VENDOR_LEARNING_PLATFORM>>

## Meu contexto
- **Exame em:** <<EXAM_DATE>> · **Tempo:** <<DAYS_AVAILABLE>> dias × <<HOURS_PER_DAY>>h/dia
- **Já tenho:** <<PRIOR_CERTS>> · **Forte em:** <<STRONG_AREAS>> · **Fraco em:** <<WEAK_AREAS>>
- **Nível autodeclarado:** <<EXPERIENCE_LEVEL>>
- **Idioma:** <<PREFERRED_LANGUAGE>> · **Notas:** <<NOTE_TOOL>>
- **Formato de saída:** <<OUTPUT_FORMAT>> (padrão `html`; alternativa `markdown`)

## 📄 Regra de formato de saída (CRÍTICA — aplica a TODOS os arquivos textuais)

A variável `<<OUTPUT_FORMAT>>` define a extensão e o formato de TODO arquivo textual do kit. Resolva da seguinte forma:

- **`<<OUTPUT_FORMAT>>=html` (padrão)**: gere os arquivos textuais como **`.html` em vez de `.md`**. Cada arquivo deve ser **single-file, sem build, sem dependências locais** (estilo `simulado.html`). Use:
  - `<!DOCTYPE html>`, `<html lang="...">`, `<head>` com `<meta charset="utf-8">`, `<meta name="viewport" content="width=device-width, initial-scale=1">`, `<title>` específico e `<style>` embutido com **temas dark (padrão) e claro** consistentes entre todos os arquivos (mesma paleta do `simulado.html`).
  - **🆕 Toggle de tema claro/escuro obrigatório em cada arquivo HTML**:
    - Defina CSS variables em `:root` (tema dark, padrão) e overrides em `:root[data-theme="light"]` (tema claro). Mantenha as **mesmas variáveis** em ambos os modos para o restante do CSS não saber qual tema está ativo.
    - Inclua um `<button id="theme-toggle">` no cabeçalho fixo de cada página (ícone `🌙` no dark, `☀️` no light, com `aria-label="Alternar tema claro/escuro"` e `title` descritivo).
    - Persista a escolha em `localStorage` com a chave fixa **`ckg-theme`** (mesma chave em TODOS os arquivos do kit, para o tema seguir o usuário ao navegar entre páginas).
    - Aplique o tema **antes do paint** via `<script>` inline no `<head>` (lê `localStorage` e seta `data-theme` em `<html>`) para evitar FOUC (flash do tema errado).
    - **Dark continua sendo o padrão** se não houver preferência salva. Não use `prefers-color-scheme` (mantém comportamento previsível: kit é dark até o usuário trocar explicitamente).
  - Tipografia limpa (system fonts), TOC interno no topo (`<nav>` com `<a href="#sec">`), cabeçalhos `<h1>`/`<h2>`/`<h3>` com `id` âncora, tabelas estilizadas, blocos `<pre><code>` para código (use `highlight.js` via CDN ou apenas `<code>` mono — escolha consistente).
  - Diagramas Mermaid: `<pre class="mermaid">…</pre>` + `<script type="module">import mermaid from 'https://cdn.jsdelivr.net/npm/mermaid@10/dist/mermaid.esm.min.mjs'; var mt=document.documentElement.getAttribute('data-theme')==='light'?'default':'dark'; mermaid.initialize({startOnLoad:true, theme:mt});</script>`. (Mermaid lê o tema atual no carregamento; ao alternar tema, a página precisa ser recarregada para os diagramas re-renderizarem — limitação aceitável; mencione isso no `concept-map.html`.)
  - **Navegação entre arquivos**: cabeçalho fixo ou rodapé com link `← Voltar ao índice (README.html)` em cada arquivo. O `README.html` lista todos os arquivos como cards/links clicáveis.
  - **Links externos** apontando para `<<OFFICIAL_DOCS_DOMAIN>>` abrem em nova aba (`target="_blank" rel="noopener"`).
  - Todos os arquivos devem **abrir com duplo-clique** no navegador, sem servidor.
  - Mantenha o **conteúdo idêntico** ao que seria em markdown — apenas a apresentação muda. Não corte material por causa do formato.
  - **Exceções que NÃO mudam de extensão**: `simulado.html` (já é HTML), `flashcards.csv` (formato de import obrigatório do Anki), `notes-template.<ext>` (segue ferramenta de notas — `.md` para Obsidian, `.one` placeholder para OneNote, etc.), e quaisquer **arquivos executáveis de labs** (`.py`, `.js`, `.sh`, `Dockerfile`, `requirements.txt`, `package.json`, `.env.example` — esses NUNCA viram HTML).
  - Arquivos de **README de labs** (`README-guided` e `README-speedrun`) seguem `<<OUTPUT_FORMAT>>` (viram `.html` no modo html).

- **`<<OUTPUT_FORMAT>>=markdown`**: gere todos os arquivos textuais como `.md` clássico (comportamento legado v3.0). Sem HTML wrapper. Mermaid em bloco ` ```mermaid `. Tudo renderiza no GitHub/VS Code.

**Onde quer que este prompt diga `.md`, substitua mentalmente pela extensão correta (`.html` ou `.md`) conforme `<<OUTPUT_FORMAT>>`.**

## Fontes (MCPs)

Antes de qualquer conteúdo técnico, consulte fontes oficiais via MCP. Não invente sintaxe, limites, versões ou keywords.

Configure `.vscode/mcp.json` conforme o vendor:
- **Microsoft / Azure:** `microsoft.docs.mcp` em `https://learn.microsoft.com/api/mcp` + `Azure` via `npx -y @azure/mcp@latest server start`
- **GitHub:** `github` em `https://api.githubcopilot.com/mcp/` (OAuth na 1ª chamada)
- **Outros vendors sem MCP dedicado:** `fetch_webpage` no domínio oficial

## ⚠️ REGRA CRÍTICA — Fontes permitidas (vale para TODOS os arquivos)

**Toda referência (link, citação, recomendação, simulado, flashcard, glossário) deve apontar exclusivamente para `<<OFFICIAL_DOCS_DOMAIN>>`, `<<VENDOR_LEARNING_PLATFORM>>` ou subdomínio oficial reconhecido do `<<EXAM_VENDOR>>`.** Qualquer outra fonte é **proibida**: cursos pagos/gratuitos de plataformas de e-learning não-vendor, vídeos no YouTube, blogs, canais de criadores independentes, agregadores ou bancos de questões/simulados de terceiros, repositórios comunitários no GitHub que não sejam do vendor oficial (ex: `github.com/<vendor>/*`), sites de "dumps". Para simulados: use **apenas o oficial do vendor**; se não existir, declare explicitamente em `mock-exam-plan.<EXT>` e dependa só do `simulado.html` deste kit. Se for citar número, limite, sintaxe ou keyword, **valide na fonte oficial primeiro** e linke a URL.

## Princípio pedagógico v3 (foco iniciante)

1. **Calibre antes de planejar:** o `diagnostic.<EXT>` define o plano, não a autoavaliação.
2. **Não pule fundamentos:** se o candidato não dominar pré-requisitos, o `fundamentals.<EXT>` precede o estudo do blueprint.
3. **Scaffolding progressivo:** labs em 2 modos (guiado → speedrun). Conceitos antes de aplicação.
4. **Vocabulário centralizado:** `glossary.<EXT>` e `concept-map.<EXT>` são consultados antes dos domínios.
5. **Active recall obrigatório:** `flashcards.<EXT>` (revisão diária) + `mistake-log.<EXT>` (após cada simulado).

## Entregáveis

Crie sob `<<EXAM_CODE>>/` (minúsculas), no idioma `<<PREFERRED_LANGUAGE>>`. Extensão dos arquivos textuais (`<EXT>`): **`html` se `<<OUTPUT_FORMAT>>=html` (padrão)**, `md` se `<<OUTPUT_FORMAT>>=markdown`.

```
<<EXAM_CODE>>/
├── README.<EXT>           # Índice + setup + roteiro Dia 0 → Dia N + checklist
├── diagnostic.<EXT>       # 🆕 Diagnóstico inicial (Dia 0) — calibra o plano
├── fundamentals.<EXT>     # 🆕 Primer de pré-requisitos (só vendor)
├── study-plan.<EXT>       # Cronograma dia-a-dia (gerado APÓS diagnóstico)
├── glossary.<EXT>         # 🆕 Termos A–Z, definição 1-2 linhas, link oficial
├── concept-map.<EXT>      # 🆕 Diagrama Mermaid de relações entre conceitos
├── domains/NN-<slug>.<EXT> # 1 por domínio do blueprint oficial
├── cheatsheet.<EXT>       # Referência rápida (TABULAR, sem prosa)
├── pegadinhas.<EXT>       # TOP 20 armadilhas + 10 heurísticas
├── exam-strategy.<EXT>    # Passes, gestão de tempo, flag/review
├── mock-exam-plan.<EXT>   # Cronograma de simulados (só oficial + simulado.html)
├── simulado.html          # 🔒 Sempre .html (single-file, sem build)
├── flashcards.<EXT>       # 🆕 TOP 50 cards (frente/verso) + export Anki
├── flashcards.csv         # 🔒 Sempre .csv (Anki-compatível: frente;verso;tag)
├── mistake-log.<EXT>      # 🆕 Template de rastreamento de erros
├── labs/NN-<slug>/        # 1 lab por domínio principal
│   ├── README-guided.<EXT>   # 🆕 Modo guiado (comentado, didático)
│   ├── README-speedrun.<EXT> # 🆕 Modo speedrun (esqueleto, retenção)
│   └── <arquivos executáveis>  # 🔒 sempre .py/.js/.sh/Dockerfile/etc.
└── notes-template.<ext>   # Omitir se <<NOTE_TOOL>>=nenhum (segue a ferramenta)
```

> **Legenda:** `<EXT>` = `html` ou `md` conforme `<<OUTPUT_FORMAT>>`. Itens marcados 🔒 mantêm sua extensão original em qualquer modo.

## Especificação por arquivo

**`README.<EXT>`** — Visão geral (duração, nº questões, score, custo, validade) · % por domínio do blueprint · setup (extensões, MCPs) · **roteiro Dia 0 obrigatório** (diagnostic → fundamentals se necessário → study-plan) · checklist macro. Inclui seção "Como usar este kit como iniciante" com fluxo recomendado. Se `<<OUTPUT_FORMAT>>=html`: este é o **hub navegacional** com grid de cards/links para todos os outros `.html`.

**`diagnostic.<EXT>` 🆕** — 20-25 questões diagnósticas:
- 5 questões de pré-requisitos (Git, YAML, HTTP, conceitos básicos do vendor)
- ~3-5 questões por domínio do blueprint (cobertura ampla, não profunda)
- Cada questão: enunciado + 4 alternativas + resposta correta + link oficial
- **Gabarito balanceado A/B/C/D:** cada letra 20–30% das corretas, máx 35%. Auditar e re-permutar antes de entregar.
- Tabela de auto-correção: `score 0-40% → modo aprofundado | 41-70% → cobertura padrão | 71-100% → comprimir`
- Output esperado: `score_per_domain.txt` que o `study-plan.<EXT>` consome
- **Executar antes de qualquer outro estudo (Dia 0, ~30min)**

**`fundamentals.<EXT>` 🆕** — Primer de pré-requisitos:
- Lista 10-15 conceitos absolutos pré-exame (Git, YAML, HTTP, JSON, conceitos básicos do vendor)
- Tabela "Você sabe?" — checklist auto-validável (sim/não)
- Para cada conceito: link para trilha oficial do vendor em `<<VENDOR_LEARNING_PLATFORM>>` (ex: GitHub Skills "Introduction to GitHub", Microsoft Learn "Azure Fundamentals path", AWS "Cloud Practitioner Essentials")
- Estimativa de horas por bloco
- **Obrigatório se diagnostic < 30% em pré-requisitos; opcional caso contrário**
- **NUNCA** linkar cursos de terceiros (Udemy, Coursera não-vendor, YouTube, blogs)

**`study-plan.<EXT>`** — Cronograma calibrado a `<<DAYS_AVAILABLE>>`×`<<HOURS_PER_DAY>>`h, **adaptado ao resultado do `diagnostic.<EXT>`**:
- Dia 0: diagnóstico (obrigatório) + leitura de `fundamentals.<EXT>` se score < 30% em pré-requisitos
- Dia 1+: cada dia tem tópicos, lab (modo guided no início, speedrun ao final), flashcards (15min/dia), simulado parcial, meta de retenção
- Para `<<WEAK_AREAS>>` identificadas pelo diagnóstico: alocar 1.5-2× o tempo padrão
- Para áreas com score alto: comprimir e usar tempo extra em fraquezas
- Último dia: revisão de flashcards + mistake-log + simulado final + descanso
- Reservar 15min/dia para `flashcards.<EXT>` e 30min/semana para revisar `mistake-log.<EXT>`

**`glossary.<EXT>` 🆕** — Termos A–Z do exame:
- 40-80 termos (proporcional ao escopo do exame)
- Cada entrada: `**Termo**: definição em 1-2 linhas. [doc](URL oficial)`
- Agrupado alfabeticamente
- Termos extraídos via MCP da doc oficial — não inventar
- Inclui apêndice "Acrônimos" se aplicável

**`concept-map.<EXT>` 🆕** — Mapa visual em Mermaid:
- Diagrama `graph LR` ou `flowchart TD` mostrando relações entre conceitos centrais
- Ex: `workflow → job → step → action; runner → environment → secrets; permissions → token → OIDC`
- Cada nó referencia entrada do `glossary.<EXT>`
- Validar via MCP que cada relação existe na doc oficial (não inventar associações)
- Renderizável diretamente: em `md`, no GitHub/VS Code via bloco ` ```mermaid `; em `html`, via `<pre class="mermaid">` + script CDN (tema `dark`)

**`domains/NN-<slug>.<EXT>`** — Estrutura: visão → conceitos-chave c/ exemplos → comandos/sintaxe críticos → tabelas comparativas → checklist → links para labs e flashcards relevantes. Cada afirmação técnica linkada a `<<OFFICIAL_DOCS_DOMAIN>>`. **Linkar para `glossary.<EXT>`** em primeira menção de termo técnico.

**`cheatsheet.<EXT>`** — **Tabelas e snippets, zero prosa.** Snippets, comandos CLI, atalhos, limites numéricos, defaults.

**`pegadinhas.<EXT>`** — TOP 20 armadilhas (parece-certo → é-certo → por-quê) + 10 heurísticas para eliminar alternativas.

**`exam-strategy.<EXT>`** — 3 passes (rápido/médio/revisão), minutos por questão, quando flagar, checklist véspera+dia.

**`mock-exam-plan.<EXT>`** — Cronograma de N simulados. Apenas oficiais do vendor + o `simulado.html` deste kit. (Ver REGRA CRÍTICA acima.) Inclui referência ao `mistake-log.<EXT>` como obrigatório após cada simulado.

**`simulado.html`** — **Sempre `.html`, independente de `<<OUTPUT_FORMAT>>`**. Single-file (HTML/CSS/JS vanilla, sem build, sem deps). Tema dark do vendor (em modo `html`, **reusa a mesma paleta** dos demais arquivos para coerência visual). Requisitos:
- **Quantidade = nº oficial de questões do exame** (validar via MCP). Se a fonte não publicar, fallback **50**. **Nunca menos, nunca mais que +20%.** Distribuir proporcionalmente aos pesos dos domínios.
- Cada questão: enunciado + (opcional) bloco de código + 4 alternativas. Mistura single/multi (badge para multi).
- **Gabarito balanceado A/B/C/D** (mesma regra do `diagnostic`; em multi, contar cada índice correto). Não delegar ao checkbox "embaralhar" do runtime.
- Botões por questão: **"💡 Revelar resposta"** (verde correta, vermelho erradas selecionadas, explicação por alternativa) e **"📖 Explicar geral"** (heurística + link doc oficial).
- **🆕 Botão "📝 Adicionar ao mistake-log"** — copia texto pré-formatado para clipboard, pronto para colar em `mistake-log.<EXT>` (em modo `html`, o texto colado deve ser HTML válido para o `<tbody>` da tabela; em `md`, linha de tabela markdown).
- Filtro por domínio · checkbox embaralhar · timer MM:SS · score final c/ breakdown por domínio + pass/fail (≥70%) · `localStorage` · botões Iniciar/Reiniciar/Finalizar/Revelar todas/Limpar.
- Cada questão DEVE ter `ref: { url, label }` apontando para `<<OFFICIAL_DOCS_DOMAIN>>` (validado).

##### ⚠️ Armadilhas JS obrigatórias de evitar no `simulado.html` (e em qualquer HTML interativo)

> Estes bugs já apareceram em iterações passadas e são proibidos. Aplique nos checkpoints de geração:

1. **Índice 0 é falsy.** Nunca escreva `var sel = state.answers[qi] || default;` para recuperar a alternativa marcada — se o usuário selecionou a **1ª alternativa** (índice `0`), `0 || default` retorna `default` e a UI mostra a opção como não-selecionada. Use sempre comparação explícita com `null`/`undefined`:
   ```js
   var a = state.answers[qi];
   var sel = (a === undefined || a === null) ? (q.t === 'multi' ? [] : null) : a;
   ```
   A mesma regra vale para qualquer contador, índice ou ID numérico que pode legitimamente ser `0`.
2. **Contagem de respondidas:** `if (state.answers[k]) ac++` está errado pelo mesmo motivo. Use `if (v !== null && v !== undefined && !(Array.isArray(v) && v.length === 0))`.
3. **Multi-select defensivo:** antes de chamar `sel.indexOf(i)`, valide `Array.isArray(sel)` — `state` recuperado de `localStorage` corrompido pode quebrar tudo.
4. **`onchange` em radios re-renderizados:** ao re-renderizar via `innerHTML`, o `<input checked>` precisa refletir o estado já gravado (não confiar só no DOM nativo); senão a marcação some no `goNext`/`goPrev`.
5. **Antes de entregar, faça um smoke test mental:** "se o usuário clicar na 1ª alternativa de Q1 e avançar para Q2, depois voltar para Q1, a 1ª alternativa ainda está destacada?". Se a resposta não for óbvia "sim" lendo o código, há bug.

**`flashcards.<EXT>` 🆕** — TOP 50 cards de active recall:
- Formato: `### Q: pergunta\n**A:** resposta\n**Ref:** [doc](URL oficial)`
- Cobertura: 10 por domínio (proporcional aos pesos)
- Foco em: limites numéricos, sintaxe exata, casos de uso, pegadinhas
- Tags por domínio (#D1, #D2, ...)
- **Revisão: 15min/dia** (15-20 cards/dia em rotação)

**`flashcards.csv` 🆕** — **Sempre `.csv`** (formato fixo p/ Anki). Export Anki-compatível:
- Formato: `frente;verso;tags` (separador `;` por compatibilidade Anki)
- Mesmo conteúdo de `flashcards.<EXT>`
- Importável direto no Anki/Mochi/RemNote

**`mistake-log.<EXT>` 🆕** — Template de rastreamento:
- Tabela: `Data | Simulado | # questão | Domínio | Categoria erro | Causa raiz | Ação corretiva | Revisado?`
- Categorias de erro pré-definidas: `sintaxe esquecida | conceito não entendido | pegadinha de UI | leitura apressada | dois plausíveis | desconhecia totalmente`
- Seção "Padrões semanais" — candidato resume tendências (ex: "70% dos erros em D3 são em JS actions → adicionar lab extra")
- Seção "Conceitos para flashcards novos" — alimenta `flashcards.<EXT>`
- Em modo `html`: a tabela é um `<table>` real, com `<tbody id="log">` para receber linhas coladas a partir do botão do `simulado.html`

**`labs/NN-<slug>/` 🆕 (modo dual)** — 1 lab executável por domínio principal, em DOIS modos:

- **`README-guided.<EXT>`** (modo didático para iniciante):
  - Objetivo + contexto (2-3 parágrafos curtos)
  - Pré-requisitos com links para `fundamentals.<EXT>` ou `glossary.<EXT>`
  - Passos numerados com **explicação de "por quê"** em cada step (não só "o que")
  - Comentários inline no código citando URL oficial para cada construct
  - Critério de sucesso descritivo
  - Troubleshooting expandido (5-10 cenários)
  - Pontos de exame ("O que isso ensina sobre o blueprint?")
  - Tempo estimado: 30-60min

- **`README-speedrun.<EXT>`** (modo retenção/v2-style):
  - Objetivo (1 linha) · pré-reqs (1 linha) · tempo: 10-20min
  - Passos numerados diretos, sem explicação
  - Tabela troubleshooting (3-5 linhas: erro | causa | fix)
  - Desafio extra (1 variação para auto-teste)

- **Arquivos executáveis** compartilhados entre os dois modos
- Lab dominado quando: ✅ guided completo + ✅ speedrun em <50% do tempo do guided

**`notes-template.<ext>`** — Template para `<<NOTE_TOOL>>`: 1 seção por domínio + 1 para pegadinhas + 1 para mistake-log. Omitir se `nenhum`.

## Critérios de qualidade

1. **Validar via MCP/docs oficiais** todo número, limite, versão, sintaxe, keyword — incluindo o **nº oficial de questões** (define tamanho do `simulado.html`; fallback 50) e **conceitos do glossary/concept-map** (não inventar relações).
2. **Cada afirmação técnica com link oficial.** Zero referências a terceiros em qualquer arquivo (ver REGRA CRÍTICA). Inclui `fundamentals`, `flashcards`, `glossary`, `concept-map` — todos os 4 arquivos novos seguem a mesma regra, independente do formato (`html` ou `md`).
3. Idioma `<<PREFERRED_LANGUAGE>>`, mas termos técnicos em inglês quando assim aparecem no exame.
4. Denso, prático, examinável. Sem fluff, sem repetição entre arquivos (referencie).
5. **Profundidade adaptada ao diagnóstico**: fundo onde score < 40%, comprimido onde > 70%. **Não usar autoavaliação como única base.**
6. Labs realmente executáveis localmente ou em sandbox gratuito do vendor. Modo guided **explica o porquê**, modo speedrun **testa retenção**.
7. `simulado.html` abre com duplo-clique, sem servidor. Inclui botão **"Adicionar ao mistake-log"**. **Bugs proibidos:** as 5 armadilhas JS listadas na seção do `simulado.html` (a #1 — "índice 0 falsy" — é a mais comum; revise o código antes de entregar).
7.1. **Gabarito balanceado A/B/C/D** em `diagnostic` e `simulado`: 20–30% por letra, máx 35%. Vetar entrega se exceder.
8. `concept-map` renderiza corretamente em Mermaid (testar mentalmente a sintaxe; em html usa CDN, em md usa bloco ` ```mermaid `).
9. `flashcards.csv` é importável em Anki sem ajustes manuais.
10. **Se `<<OUTPUT_FORMAT>>=html`**: tema dark consistente, todos os arquivos `.html` abrem isoladamente com duplo-clique, navegação entre arquivos funciona, links externos abrem em nova aba, conteúdo equivalente ao do modo markdown (sem perda).

## ✅ Checklist de Entregáveis Completos (use para validar)

> Substitua `<EXT>` por `html` ou `md` conforme `<<OUTPUT_FORMAT>>` (padrão `html`).

Antes de finalizar, verifique se TODOS estes arquivos existem:

**Arquivos Base (13):**
- [ ] `README.<EXT>` - Índice + setup + roteiro Dia 0
- [ ] `diagnostic.<EXT>` - 20-25 questões calibração
- [ ] `fundamentals.<EXT>` - Primer de pré-requisitos
- [ ] `glossary.<EXT>` - Termos A-Z
- [ ] `concept-map.<EXT>` - Diagramas Mermaid
- [ ] `study-plan.<EXT>` - Cronograma calibrado
- [ ] `cheatsheet.<EXT>` - Tabelas referência rápida
- [ ] `pegadinhas.<EXT>` - TOP 20 armadilhas
- [ ] `exam-strategy.<EXT>` - 3 passes + tempo
- [ ] `mock-exam-plan.<EXT>` - Cronograma simulados
- [ ] `simulado.html` - **OBRIGATÓRIO sempre .html** - Single-file com N questões. Antes de entregar, releia o JS e confirme as 5 armadilhas obrigatórias (em especial: nunca usar `state.answers[qi] || default` — índice 0 da 1ª alternativa é falsy).
- [ ] `flashcards.<EXT>` + `flashcards.csv` - TOP 50 Q/A (CSV sempre .csv)
- [ ] `mistake-log.<EXT>` - Template rastreamento

**Domínios (5):**
- [ ] `domains/01-*.<EXT>` - Domínio 1 completo
- [ ] `domains/02-*.<EXT>` - Domínio 2 completo
- [ ] `domains/03-*.<EXT>` - Domínio 3 completo
- [ ] `domains/04-*.<EXT>` - Domínio 4 completo
- [ ] `domains/05-*.<EXT>` - Domínio 5 completo (ajuste N conforme blueprint)

**Labs (mínimo 3-5, idealmente 1 por domínio principal):**
Para CADA lab, TODOS estes arquivos devem existir:
- [ ] `labs/01-*/README-guided.<EXT>` - Modo didático 30-60min
- [ ] `labs/01-*/README-speedrun.<EXT>` - Modo speedrun 10-20min
- [ ] `labs/01-*/<arquivos-executáveis>` - Código Python/JS/etc. rodável (extensão própria)
- [ ] `labs/01-*/requirements.txt` ou `package.json` - Dependências
- [ ] Repetir para labs 02, 03, 04, 05...

**Opcional:**
- [ ] `notes-template.<ext>` - Se `<<NOTE_TOOL>>` ≠ nenhum (extensão da ferramenta)

**Específico para `<<OUTPUT_FORMAT>>=html`:**
- [ ] Todos os arquivos `.html` abrem com **duplo-clique** sem servidor
- [ ] Tema dark **consistente** entre todos os arquivos (mesma paleta)
- [ ] 🆕 **Tema claro** também definido em `:root[data-theme="light"]` em todos os arquivos
- [ ] 🆕 **Botão de toggle (`#theme-toggle`)** presente e funcional no cabeçalho de **todos** os arquivos `.html`
- [ ] 🆕 **Tema escolhido persiste entre páginas** via `localStorage.ckg-theme` (mesma chave em todos os arquivos)
- [ ] 🆕 **Sem FOUC** ao carregar página (script inline no `<head>` aplica `data-theme` antes do paint)
- [ ] `README.html` é o hub com links clicáveis para todos os outros arquivos
- [ ] Cada arquivo tem link `← Voltar ao índice` para `README.html`
- [ ] `concept-map.html` renderiza Mermaid via CDN (testar com internet)
- [ ] Links externos para `<<OFFICIAL_DOCS_DOMAIN>>` abrem em nova aba
- [ ] TOC interno em arquivos longos (≥3 seções `<h2>`)

**CRÍTICO**: `simulado.html` com exatamente N questões (validar via MCP) NÃO é opcional. Labs SEM arquivos executáveis não contam como completos.

---

## Workflow de execução

1. Configure MCPs em `.vscode/mcp.json` para o vendor.
2. **Resolva `<<OUTPUT_FORMAT>>`** (padrão `html`) e anuncie ao usuário a extensão escolhida para os arquivos textuais (`.html` ou `.md`). Se `html`, defina **antecipadamente**:
   - As paletas de cores **dark (padrão) e light** (CSS variables em `:root` e `:root[data-theme="light"]`).
   - O snippet de cabeçalho com `<button id="theme-toggle">` e o snippet de rodapé.
   - O `<script>` inline de aplicação do tema **antes do paint** (lê `localStorage.ckg-theme`).
   - A função `toggleTheme()` (atualiza `data-theme`, salva em `localStorage`, alterna o ícone do botão).
   
   Reutilize **idênticos** em todos os arquivos para garantir consistência visual e persistência da escolha do usuário ao navegar entre páginas.
3. Busque blueprint oficial atual (domínios + pesos + **nº de questões**).
4. Crie estrutura de pastas: `<<EXAM_CODE>>/`, `domains/`, `labs/01-*/ labs/02-*/` etc.
5. Gere `README.<EXT>` com roteiro Dia 0 → Dia N explícito. Se `html`: este arquivo é o **hub navegável** com cards/links para todos os demais.
6. **Gere `diagnostic.<EXT>` PRIMEIRO** (antes do study-plan, porque o plano depende dele).
7. Gere `fundamentals.<EXT>` (primer de pré-requisitos com trilhas oficiais).
8. Gere `glossary.<EXT>` e `concept-map.<EXT>` (vocabulário e mapa, base para domains). Em `html`, o concept-map usa Mermaid via CDN.
9. Gere `study-plan.<EXT>` (instruindo o candidato a executar `diagnostic.<EXT>` antes; o plano traz placeholders condicionais que o candidato refina após o diagnóstico).
10. Para **CADA domínio** (01 até 05 ou N): gere `.<EXT>` consultando docs, linkando para `glossary.<EXT>` na 1ª menção de termos.
11. Gere `cheatsheet.<EXT>`, `pegadinhas.<EXT>`, `exam-strategy.<EXT>`, `mock-exam-plan.<EXT>`.
12. **Gere `simulado.html` COMPLETO** (sempre `.html`; validar N questões via MCP; incluir botão mistake-log; testar que abre com duplo-clique).
13. Gere `flashcards.<EXT>` + `flashcards.csv` (CSV sempre; TOP 50, distribuído proporcionalmente aos pesos dos domínios).
14. Gere `mistake-log.<EXT>` (template vazio com tabela e categorias pré-definidas).
15. **Para CADA lab (mínimo 3, idealmente 5):**
    - Crie pasta `labs/NN-<slug>/`
    - Gere `README-guided.<EXT>` (modo didático, 30-60min, explicações)
    - Gere `README-speedrun.<EXT>` (modo speedrun, 10-20min, comandos diretos)
    - Gere **TODOS os arquivos executáveis** (código Python/JS/Shell/etc. — extensão própria, nunca convertida)
    - Gere `requirements.txt` ou `package.json` (dependências)
    - Gere `.env.example` (configuração template)
    - **TESTE mentalmente se é executável** (não deixe só README sem código)
16. Gere notes-template (se aplicável), incluindo seção mistake-log.
17. **VALIDE contra checklist acima** - se faltar algo, crie antes de finalizar. Se `html`, abra mentalmente o `README.html` e verifique se todos os links internos resolvem.
18. Liste artefatos como links clicáveis no final (use links HTML se `<<OUTPUT_FORMAT>>=html`, markdown se `markdown`).

## Regras de execução

- Execute autonomamente, sem pedir confirmação a cada arquivo. Use TODO list para rastrear macro.
- Se um valor não for verificável, marque `<!-- TODO: validar em <URL> -->` em vez de chutar.
- Não duplique conteúdo entre arquivos. Não crie arquivos fora do escopo.
- **`diagnostic.<EXT>` e `fundamentals.<EXT>` são os primeiros entregáveis técnicos** depois do README — não pule.
- **Para o candidato:** instruir explicitamente no `README.<EXT>` a executar o diagnóstico no Dia 0 ANTES de seguir o `study-plan.<EXT>`.
- **Coerência de formato:** se `<<OUTPUT_FORMAT>>=html`, NÃO misture arquivos `.md` no kit textual (exceto `notes-template` se a ferramenta de notas exigir). Inversamente, se `markdown`, NÃO crie `.html` exceto `simulado.html`.

Comece agora: confirme os MCPs disponíveis para o vendor, **anuncie o `<<OUTPUT_FORMAT>>` resolvido**, depois execute todo o plano.
````
<!-- AGENT_PROMPT_END -->

---

## 💡 Dicas de uso (v3 específico)

1. **Workspace vazio + modo Agent** (não Ask).
2. **Escolha o formato cedo:** `<<OUTPUT_FORMAT>>=html` (padrão) para estudar lendo no navegador; `markdown` para versionar no Git ou importar em Obsidian/Notion. Não dá pra "converter no meio" — escolha antes de gerar.
3. **Dia 0 é sagrado:** abra `<<EXAM_CODE>>/diagnostic.<EXT>` e responda honestamente antes de tocar em qualquer outro arquivo. Sem isso, o `study-plan.<EXT>` está calibrado errado.
4. **Se score de pré-requisitos < 30%:** dedique 2-5 dias extras a `fundamentals.<EXT>` antes de iniciar o blueprint. Sem base, o resto não cola.
5. **Importe `flashcards.csv` no Anki** (ou app similar). Revise 15min/dia desde o Dia 1.
6. **Preencha `mistake-log.<EXT>` após CADA simulado.** O botão no `simulado.html` ajuda. Semanalmente, revise padrões.
7. **Labs sempre em duplo passo:** guided primeiro (entender), speedrun depois (retenção). Lab só é "feito" quando speedrun ≤ 50% do tempo do guided.
8. **MCPs pedem OAuth na 1ª chamada** — autorize.
9. **Se o agente alucinar:** *"valide esse limite em `<<OFFICIAL_DOCS_DOMAIN>>` via MCP"*.
10. **Iteração:** *"adicione 10 flashcards focando no domínio X"* / *"expanda o concept-map com a área Y"* / *"regere apenas em markdown para versionar"*.

## 🌐 Vendors

| Vendor | MCP / fonte docs | Plataforma oficial de aprendizagem |
|---|---|---|
| GitHub | `https://api.githubcopilot.com/mcp/` → `docs.github.com` | `skills.github.com` |
| Microsoft / Azure | `https://learn.microsoft.com/api/mcp` + `@azure/mcp` → `learn.microsoft.com` | `learn.microsoft.com/training` |
| AWS | `fetch_webpage` → `docs.aws.amazon.com` | `aws.amazon.com/training`, `skillbuilder.aws` |
| HashiCorp | `fetch_webpage` → `developer.hashicorp.com` | `developer.hashicorp.com/tutorials` |
| CNCF / Kubernetes | `fetch_webpage` → `kubernetes.io` | `kubernetes.io/training`, `training.linuxfoundation.org` |
| Google Cloud | `fetch_webpage` → `cloud.google.com/docs` | `cloud.google.com/learn` |

---

## 📌 Resumo das 5 melhorias v3 sobre v2

| # | Melhoria | Arquivos novos | Problema que resolve |
|---|---|---|---|
| 1 | **Diagnóstico inicial** | `diagnostic.<EXT>` | Calibração objetiva (não autoavaliação) |
| 2 | **Primer de fundamentos** | `fundamentals.<EXT>` | Iniciante sem base trava no Dia 1 |
| 3 | **Labs em modo dual** | `README-guided.<EXT>` + `README-speedrun.<EXT>` | Scaffolding pedagógico progressivo |
| 4 | **Glossário + mapa conceitual** | `glossary.<EXT>` + `concept-map.<EXT>` | Vocabulário e relações entre conceitos |
| 5 | **Active recall + feedback loop** | `flashcards.<EXT>` + `flashcards.csv` + `mistake-log.<EXT>` | Estudo passivo → ativo; erros viram dados |

> `<EXT>` = `html` (padrão) ou `md` conforme `<<OUTPUT_FORMAT>>` (variável adicionada em v3.1).

**Guard rails da v2 preservados 100%:** zero terceiros, validação MCP obrigatória, links exclusivos para `<<OFFICIAL_DOCS_DOMAIN>>` e `<<VENDOR_LEARNING_PLATFORM>>`.
