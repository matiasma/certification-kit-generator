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

Isso é suficiente. O agente descobre o resto.

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
5. Para campos opcionais não preenchidos, aplique padrões: `<<EXAM_DATE>>=não marcada`, `<<PRIOR_CERTS>>=nenhuma`, `<<STRONG_AREAS>>=desconhecido`, `<<WEAK_AREAS>>=desconhecido`, `<<NOTE_TOOL>>=nenhum`.
6. **Confirme os valores resolvidos** em uma mensagem curta antes de criar arquivos. Se não conseguir resolver com confiança (ex: código de exame ambíguo ou inválido), pergunte ao usuário.

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

## Fontes (MCPs)

Antes de qualquer conteúdo técnico, consulte fontes oficiais via MCP. Não invente sintaxe, limites, versões ou keywords.

Configure `.vscode/mcp.json` conforme o vendor:
- **Microsoft / Azure:** `microsoft.docs.mcp` em `https://learn.microsoft.com/api/mcp` + `Azure` via `npx -y @azure/mcp@latest server start`
- **GitHub:** `github` em `https://api.githubcopilot.com/mcp/` (OAuth na 1ª chamada)
- **Outros vendors sem MCP dedicado:** `fetch_webpage` no domínio oficial

## ⚠️ REGRA CRÍTICA — Fontes permitidas (vale para TODOS os arquivos)

**Toda referência (link, citação, recomendação, simulado, flashcard, glossário) deve apontar exclusivamente para `<<OFFICIAL_DOCS_DOMAIN>>`, `<<VENDOR_LEARNING_PLATFORM>>` ou subdomínio oficial reconhecido do `<<EXAM_VENDOR>>`.** Qualquer outra fonte é **proibida**: cursos pagos/gratuitos de plataformas de e-learning não-vendor, vídeos no YouTube, blogs, canais de criadores independentes, agregadores ou bancos de questões/simulados de terceiros, repositórios comunitários no GitHub que não sejam do vendor oficial (ex: `github.com/<vendor>/*`), sites de "dumps". Para simulados: use **apenas o oficial do vendor**; se não existir, declare explicitamente em `mock-exam-plan.md` e dependa só do `simulado.html` deste kit. Se for citar número, limite, sintaxe ou keyword, **valide na fonte oficial primeiro** e linke a URL.

## Princípio pedagógico v3 (foco iniciante)

1. **Calibre antes de planejar:** o `diagnostic.md` define o plano, não a autoavaliação.
2. **Não pule fundamentos:** se o candidato não dominar pré-requisitos, o `fundamentals.md` precede o estudo do blueprint.
3. **Scaffolding progressivo:** labs em 2 modos (guiado → speedrun). Conceitos antes de aplicação.
4. **Vocabulário centralizado:** `glossary.md` e `concept-map.md` são consultados antes dos domínios.
5. **Active recall obrigatório:** `flashcards.md` (revisão diária) + `mistake-log.md` (após cada simulado).

## Entregáveis

Crie sob `<<EXAM_CODE>>/` (minúsculas), no idioma `<<PREFERRED_LANGUAGE>>`:

```
<<EXAM_CODE>>/
├── README.md              # Índice + setup + roteiro Dia 0 → Dia N + checklist
├── diagnostic.md          # 🆕 Diagnóstico inicial (Dia 0) — calibra o plano
├── fundamentals.md        # 🆕 Primer de pré-requisitos (só vendor)
├── study-plan.md          # Cronograma dia-a-dia (gerado APÓS diagnóstico)
├── glossary.md            # 🆕 Termos A–Z, definição 1-2 linhas, link oficial
├── concept-map.md         # 🆕 Diagrama Mermaid de relações entre conceitos
├── domains/NN-<slug>.md   # 1 por domínio do blueprint oficial
├── cheatsheet.md          # Referência rápida (TABULAR, sem prosa)
├── pegadinhas.md          # TOP 20 armadilhas + 10 heurísticas
├── exam-strategy.md       # Passes, gestão de tempo, flag/review
├── mock-exam-plan.md      # Cronograma de simulados (só oficial + simulado.html)
├── simulado.html          # Single-file, sem build
├── flashcards.md          # 🆕 TOP 50 cards (frente/verso) + export Anki
├── flashcards.csv         # 🆕 Export Anki-compatível (frente;verso;tag)
├── mistake-log.md         # 🆕 Template de rastreamento de erros
├── labs/NN-<slug>/        # 1 lab por domínio principal
│   ├── README-guided.md   # 🆕 Modo guiado (comentado, didático)
│   ├── README-speedrun.md # 🆕 Modo speedrun (esqueleto, retenção)
│   └── <arquivos executáveis>
└── notes-template.<ext>   # Omitir se <<NOTE_TOOL>>=nenhum
```

## Especificação por arquivo

**`README.md`** — Visão geral (duração, nº questões, score, custo, validade) · % por domínio do blueprint · setup (extensões, MCPs) · **roteiro Dia 0 obrigatório** (diagnostic → fundamentals se necessário → study-plan) · checklist macro. Inclui seção "Como usar este kit como iniciante" com fluxo recomendado.

**`diagnostic.md` 🆕** — 20-25 questões diagnósticas:
- 5 questões de pré-requisitos (Git, YAML, HTTP, conceitos básicos do vendor)
- ~3-5 questões por domínio do blueprint (cobertura ampla, não profunda)
- Cada questão: enunciado + 4 alternativas + resposta correta + link oficial
- Tabela de auto-correção: `score 0-40% → modo aprofundado | 41-70% → cobertura padrão | 71-100% → comprimir`
- Output esperado: `score_per_domain.txt` que o `study-plan.md` consome
- **Executar antes de qualquer outro estudo (Dia 0, ~30min)**

**`fundamentals.md` 🆕** — Primer de pré-requisitos:
- Lista 10-15 conceitos absolutos pré-exame (Git, YAML, HTTP, JSON, conceitos básicos do vendor)
- Tabela "Você sabe?" — checklist auto-validável (sim/não)
- Para cada conceito: link para trilha oficial do vendor em `<<VENDOR_LEARNING_PLATFORM>>` (ex: GitHub Skills "Introduction to GitHub", Microsoft Learn "Azure Fundamentals path", AWS "Cloud Practitioner Essentials")
- Estimativa de horas por bloco
- **Obrigatório se diagnostic < 30% em pré-requisitos; opcional caso contrário**
- **NUNCA** linkar cursos de terceiros (Udemy, Coursera não-vendor, YouTube, blogs)

**`study-plan.md`** — Cronograma calibrado a `<<DAYS_AVAILABLE>>`×`<<HOURS_PER_DAY>>`h, **adaptado ao resultado do `diagnostic.md`**:
- Dia 0: diagnóstico (obrigatório) + leitura de `fundamentals.md` se score < 30% em pré-requisitos
- Dia 1+: cada dia tem tópicos, lab (modo guided no início, speedrun ao final), flashcards (15min/dia), simulado parcial, meta de retenção
- Para `<<WEAK_AREAS>>` identificadas pelo diagnóstico: alocar 1.5-2× o tempo padrão
- Para áreas com score alto: comprimir e usar tempo extra em fraquezas
- Último dia: revisão de flashcards + mistake-log + simulado final + descanso
- Reservar 15min/dia para `flashcards.md` e 30min/semana para revisar `mistake-log.md`

**`glossary.md` 🆕** — Termos A–Z do exame:
- 40-80 termos (proporcional ao escopo do exame)
- Cada entrada: `**Termo**: definição em 1-2 linhas. [doc](URL oficial)`
- Agrupado alfabeticamente
- Termos extraídos via MCP da doc oficial — não inventar
- Inclui apêndice "Acrônimos" se aplicável

**`concept-map.md` 🆕** — Mapa visual em Mermaid:
- Diagrama `graph LR` ou `flowchart TD` mostrando relações entre conceitos centrais
- Ex: `workflow → job → step → action; runner → environment → secrets; permissions → token → OIDC`
- Cada nó referencia entrada do `glossary.md`
- Validar via MCP que cada relação existe na doc oficial (não inventar associações)
- Renderizável diretamente no GitHub/VS Code

**`domains/NN-<slug>.md`** — Estrutura: visão → conceitos-chave c/ exemplos → comandos/sintaxe críticos → tabelas comparativas → checklist → links para labs e flashcards relevantes. Cada afirmação técnica linkada a `<<OFFICIAL_DOCS_DOMAIN>>`. **Linkar para `glossary.md`** em primeira menção de termo técnico.

**`cheatsheet.md`** — **Tabelas e snippets, zero prosa.** Snippets, comandos CLI, atalhos, limites numéricos, defaults.

**`pegadinhas.md`** — TOP 20 armadilhas (parece-certo → é-certo → por-quê) + 10 heurísticas para eliminar alternativas.

**`exam-strategy.md`** — 3 passes (rápido/médio/revisão), minutos por questão, quando flagar, checklist véspera+dia.

**`mock-exam-plan.md`** — Cronograma de N simulados. Apenas oficiais do vendor + o `simulado.html` deste kit. (Ver REGRA CRÍTICA acima.) Inclui referência ao `mistake-log.md` como obrigatório após cada simulado.

**`simulado.html`** — Single-file (HTML/CSS/JS vanilla, sem build, sem deps). Tema dark do vendor. Requisitos:
- **Quantidade = nº oficial de questões do exame** (validar via MCP). Se a fonte não publicar, fallback **50**. **Nunca menos, nunca mais que +20%.** Distribuir proporcionalmente aos pesos dos domínios.
- Cada questão: enunciado + (opcional) bloco de código + 4 alternativas. Mistura single/multi (badge para multi).
- Botões por questão: **"💡 Revelar resposta"** (verde correta, vermelho erradas selecionadas, explicação por alternativa) e **"📖 Explicar geral"** (heurística + link doc oficial).
- **🆕 Botão "📝 Adicionar ao mistake-log"** — copia texto pré-formatado para clipboard, pronto para colar em `mistake-log.md`.
- Filtro por domínio · checkbox embaralhar · timer MM:SS · score final c/ breakdown por domínio + pass/fail (≥70%) · `localStorage` · botões Iniciar/Reiniciar/Finalizar/Revelar todas/Limpar.
- Cada questão DEVE ter `ref: { url, label }` apontando para `<<OFFICIAL_DOCS_DOMAIN>>` (validado).

**`flashcards.md` 🆕** — TOP 50 cards de active recall:
- Formato: `### Q: pergunta\n**A:** resposta\n**Ref:** [doc](URL oficial)`
- Cobertura: 10 por domínio (proporcional aos pesos)
- Foco em: limites numéricos, sintaxe exata, casos de uso, pegadinhas
- Tags por domínio (#D1, #D2, ...)
- **Revisão: 15min/dia** (15-20 cards/dia em rotação)

**`flashcards.csv` 🆕** — Export Anki-compatível:
- Formato: `frente;verso;tags` (separador `;` por compatibilidade Anki)
- Mesmo conteúdo de `flashcards.md`
- Importável direto no Anki/Mochi/RemNote

**`mistake-log.md` 🆕** — Template de rastreamento:
- Tabela: `Data | Simulado | # questão | Domínio | Categoria erro | Causa raiz | Ação corretiva | Revisado?`
- Categorias de erro pré-definidas: `sintaxe esquecida | conceito não entendido | pegadinha de UI | leitura apressada | dois plausíveis | desconhecia totalmente`
- Seção "Padrões semanais" — candidato resume tendências (ex: "70% dos erros em D3 são em JS actions → adicionar lab extra")
- Seção "Conceitos para flashcards novos" — alimenta `flashcards.md`

**`labs/NN-<slug>/` 🆕 (modo dual)** — 1 lab executável por domínio principal, em DOIS modos:

- **`README-guided.md`** (modo didático para iniciante):
  - Objetivo + contexto (2-3 parágrafos curtos)
  - Pré-requisitos com links para `fundamentals.md` ou `glossary.md`
  - Passos numerados com **explicação de "por quê"** em cada step (não só "o que")
  - Comentários inline no código citando URL oficial para cada construct
  - Critério de sucesso descritivo
  - Troubleshooting expandido (5-10 cenários)
  - Pontos de exame ("O que isso ensina sobre o blueprint?")
  - Tempo estimado: 30-60min

- **`README-speedrun.md`** (modo retenção/v2-style):
  - Objetivo (1 linha) · pré-reqs (1 linha) · tempo: 10-20min
  - Passos numerados diretos, sem explicação
  - Tabela troubleshooting (3-5 linhas: erro | causa | fix)
  - Desafio extra (1 variação para auto-teste)

- **Arquivos executáveis** compartilhados entre os dois modos
- Lab dominado quando: ✅ guided completo + ✅ speedrun em <50% do tempo do guided

**`notes-template.<ext>`** — Template para `<<NOTE_TOOL>>`: 1 seção por domínio + 1 para pegadinhas + 1 para mistake-log. Omitir se `nenhum`.

## Critérios de qualidade

1. **Validar via MCP/docs oficiais** todo número, limite, versão, sintaxe, keyword — incluindo o **nº oficial de questões** (define tamanho do `simulado.html`; fallback 50) e **conceitos do glossary/concept-map** (não inventar relações).
2. **Cada afirmação técnica com link oficial.** Zero referências a terceiros em qualquer arquivo (ver REGRA CRÍTICA). Inclui `fundamentals.md`, `flashcards.md`, `glossary.md`, `concept-map.md` — todos os 4 arquivos novos seguem a mesma regra.
3. Idioma `<<PREFERRED_LANGUAGE>>`, mas termos técnicos em inglês quando assim aparecem no exame.
4. Denso, prático, examinável. Sem fluff, sem repetição entre arquivos (referencie).
5. **Profundidade adaptada ao diagnóstico**: fundo onde score < 40%, comprimido onde > 70%. **Não usar autoavaliação como única base.**
6. Labs realmente executáveis localmente ou em sandbox gratuito do vendor. Modo guided **explica o porquê**, modo speedrun **testa retenção**.
7. `simulado.html` abre com duplo-clique, sem servidor. Inclui botão **"Adicionar ao mistake-log"**.
8. `concept-map.md` renderiza corretamente em Mermaid (testar mentalmente a sintaxe).
9. `flashcards.csv` é importável em Anki sem ajustes manuais.

## ✅ Checklist de Entregáveis Completos (use para validar)

Antes de finalizar, verifique se TODOS estes arquivos existem:

**Arquivos Base (13):**
- [ ] `README.md` - Índice + setup + roteiro Dia 0
- [ ] `diagnostic.md` - 20-25 questões calibração
- [ ] `fundamentals.md` - Primer de pré-requisitos
- [ ] `glossary.md` - Termos A-Z
- [ ] `concept-map.md` - Diagramas Mermaid
- [ ] `study-plan.md` - Cronograma calibrado
- [ ] `cheatsheet.md` - Tabelas referência rápida
- [ ] `pegadinhas.md` - TOP 20 armadilhas
- [ ] `exam-strategy.md` - 3 passes + tempo
- [ ] `mock-exam-plan.md` - Cronograma simulados
- [ ] `simulado.html` - **OBRIGATÓRIO** - Single-file com N questões
- [ ] `flashcards.md` + `flashcards.csv` - TOP 50 Q/A
- [ ] `mistake-log.md` - Template rastreamento

**Domínios (5):**
- [ ] `domains/01-*.md` - Domínio 1 completo
- [ ] `domains/02-*.md` - Domínio 2 completo
- [ ] `domains/03-*.md` - Domínio 3 completo
- [ ] `domains/04-*.md` - Domínio 4 completo
- [ ] `domains/05-*.md` - Domínio 5 completo (ajuste N conforme blueprint)

**Labs (mínimo 3-5, idealmente 1 por domínio principal):**
Para CADA lab, TODOS estes arquivos devem existir:
- [ ] `labs/01-*/README-guided.md` - Modo didático 30-60min
- [ ] `labs/01-*/README-speedrun.md` - Modo speedrun 10-20min
- [ ] `labs/01-*/<arquivos-executáveis>` - Código Python/JS/etc. rodável
- [ ] `labs/01-*/requirements.txt` ou `package.json` - Dependências
- [ ] Repetir para labs 02, 03, 04, 05...

**Opcional:**
- [ ] `notes-template.<ext>` - Se `<<NOTE_TOOL>>` ≠ nenhum

**CRÍTICO**: `simulado.html` com exatamente N questões (validar via MCP) NÃO é opcional. Labs SEM arquivos executáveis não contam como completos.

---

## Workflow de execução

1. Configure MCPs em `.vscode/mcp.json` para o vendor.
2. Busque blueprint oficial atual (domínios + pesos + **nº de questões**).
3. Crie estrutura de pastas: `<<EXAM_CODE>>/`, `domains/`, `labs/01-*/ labs/02-*/` etc.
4. Gere `README.md` com roteiro Dia 0 → Dia N explícito.
5. **Gere `diagnostic.md` PRIMEIRO** (antes do study-plan, porque o plano depende dele).
6. Gere `fundamentals.md` (primer de pré-requisitos com trilhas oficiais).
7. Gere `glossary.md` e `concept-map.md` (vocabulário e mapa, base para domains).
8. Gere `study-plan.md` (instruindo o candidato a executar `diagnostic.md` antes; o plano traz placeholders condicionais que o candidato refina após o diagnóstico).
9. Para **CADA domínio** (01 até 05 ou N): gere `.md` consultando docs, linkando para `glossary.md` na 1ª menção de termos.
10. Gere `cheatsheet.md`, `pegadinhas.md`, `exam-strategy.md`, `mock-exam-plan.md`.
11. **Gere `simulado.html` COMPLETO** (validar N questões via MCP; incluir botão mistake-log; testar que abre com duplo-clique).
12. Gere `flashcards.md` + `flashcards.csv` (TOP 50, distribuído proporcionalmente aos pesos dos domínios).
13. Gere `mistake-log.md` (template vazio com tabela e categorias pré-definidas).
14. **Para CADA lab (mínimo 3, idealmente 5):**
    - Crie pasta `labs/NN-<slug>/`
    - Gere `README-guided.md` (modo didático, 30-60min, explicações)
    - Gere `README-speedrun.md` (modo speedrun, 10-20min, comandos diretos)
    - Gere **TODOS os arquivos executáveis** (código Python/JS/Shell/etc.)
    - Gere `requirements.txt` ou `package.json` (dependências)
    - Gere `.env.example` (configuração template)
    - **TESTE mentalmente se é executável** (não deixe só README sem código)
15. Gere notes-template (se aplicável), incluindo seção mistake-log.
16. **VALIDE contra checklist acima** - se faltar algo, crie antes de finalizar.
17. Liste artefatos como links markdown clicáveis no final.

## Regras de execução

- Execute autonomamente, sem pedir confirmação a cada arquivo. Use TODO list para rastrear macro.
- Se um valor não for verificável, marque `<!-- TODO: validar em <URL> -->` em vez de chutar.
- Não duplique conteúdo entre arquivos. Não crie arquivos fora do escopo.
- **`diagnostic.md` e `fundamentals.md` são os primeiros entregáveis técnicos** depois do README — não pule.
- **Para o candidato:** instruir explicitamente no `README.md` a executar o diagnóstico no Dia 0 ANTES de seguir o `study-plan.md`.

Comece agora: confirme os MCPs disponíveis para o vendor, depois execute todo o plano.
````
<!-- AGENT_PROMPT_END -->

---

## 💡 Dicas de uso (v3 específico)

1. **Workspace vazio + modo Agent** (não Ask).
2. **Dia 0 é sagrado:** abra `<<EXAM_CODE>>/diagnostic.md` e responda honestamente antes de tocar em qualquer outro arquivo. Sem isso, o `study-plan.md` está calibrado errado.
3. **Se score de pré-requisitos < 30%:** dedique 2-5 dias extras a `fundamentals.md` antes de iniciar o blueprint. Sem base, o resto não cola.
4. **Importe `flashcards.csv` no Anki** (ou app similar). Revise 15min/dia desde o Dia 1.
5. **Preencha `mistake-log.md` após CADA simulado.** O botão no `simulado.html` ajuda. Semanalmente, revise padrões.
6. **Labs sempre em duplo passo:** guided primeiro (entender), speedrun depois (retenção). Lab só é "feito" quando speedrun ≤ 50% do tempo do guided.
7. **MCPs pedem OAuth na 1ª chamada** — autorize.
8. **Se o agente alucinar:** *"valide esse limite em `<<OFFICIAL_DOCS_DOMAIN>>` via MCP"*.
9. **Iteração:** *"adicione 10 flashcards focando no domínio X"* / *"expanda o concept-map com a área Y"*.

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
| 1 | **Diagnóstico inicial** | `diagnostic.md` | Calibração objetiva (não autoavaliação) |
| 2 | **Primer de fundamentos** | `fundamentals.md` | Iniciante sem base trava no Dia 1 |
| 3 | **Labs em modo dual** | `README-guided.md` + `README-speedrun.md` | Scaffolding pedagógico progressivo |
| 4 | **Glossário + mapa conceitual** | `glossary.md` + `concept-map.md` | Vocabulário e relações entre conceitos |
| 5 | **Active recall + feedback loop** | `flashcards.md` + `flashcards.csv` + `mistake-log.md` | Estudo passivo → ativo; erros viram dados |

**Guard rails da v2 preservados 100%:** zero terceiros, validação MCP obrigatória, links exclusivos para `<<OFFICIAL_DOCS_DOMAIN>>` e `<<VENDOR_LEARNING_PLATFORM>>`.
