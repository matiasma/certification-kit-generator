# Histórico de Alterações

Todas as mudanças notáveis no template Gerador de Kits de Certificação serão documentadas neste arquivo.

O formato é baseado em [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
e este projeto segue [Versionamento Semântico](https://semver.org/spec/v2.0.0.html).

---

## [3.2.2] - 2026-05-19

### Adicionado
- **🆕 Regra de gabarito balanceado A/B/C/D** em `diagnostic` e `simulado`: 20–30% por letra, máx 35%. Item 7.1 em `## Critérios de qualidade`.

---

## [3.2.1] - 2026-05-15

### Corrigido
- **🐛 Bug crítico no `simulado.html`** — a primeira alternativa (índice `0`) de cada questão **nunca parecia selecionada** no UI ao ser clicada. Causa: padrão `var sel = state.answers[qi] || default` — em JavaScript, `0 || x === x` porque `0` é falsy. O estado era gravado e contabilizado corretamente, mas o destaque visual sumia. Aplicado fix no kit `AZ305/simulado.html` substituindo o `||` por checagem explícita contra `null`/`undefined`.

### Adicionado
- **🆕 Seção "Armadilhas JS obrigatórias de evitar"** no `TEMPLATE.md` (bloco do `simulado.html`) com 5 regras defensivas: (1) índice 0 falsy, (2) contagem de respondidas, (3) multi-select defensivo, (4) `onchange` em radios re-renderizados, (5) smoke test mental obrigatório antes de entregar.
- **🆕 Item de checklist** em `## Critérios de qualidade` e em `## ✅ Checklist de Entregáveis` referenciando explicitamente o bug "índice 0 falsy" para evitar reincidência.

---

## [3.2.0] - 2026-05-15

### 🆕 Toggle de tema claro/escuro em todos os arquivos HTML gerados

Kits no modo `html` agora incluem um botão de alternar entre tema escuro (padrão) e claro em **cada** arquivo gerado. A preferência do usuário persiste entre páginas via `localStorage`.

### Adicionado
- **🆕 Botão `#theme-toggle`** obrigatório no cabeçalho fixo de cada arquivo `.html` do kit (ícone `🌙` em dark, `☀️` em light, com `aria-label` acessível).
- **🆕 Paleta de tema claro** definida em `:root[data-theme="light"]` em todos os arquivos, espelhando as mesmas CSS variables do tema dark.
- **🆕 Persistência entre páginas** via `localStorage` com chave fixa **`ckg-theme`** — a escolha do usuário segue ao navegar entre `README.html`, `domains/*.html`, `labs/**`, etc.
- **🆕 Script anti-FOUC inline no `<head>`** que aplica `data-theme` em `<html>` antes do paint, evitando o flash de tema errado em recarregamentos.
- **🆕 Mermaid dinâmico**: o tema do Mermaid (`dark` ou `default`) é escolhido com base no `data-theme` ativo no carregamento da página (limitação documentada: trocar tema requer reload para re-renderizar diagramas).
- **🆕 4 novos itens no checklist HTML** do template: toggle presente em todos os arquivos, paleta light definida, persistência via `localStorage.ckg-theme`, sem FOUC.

### Alterado
- **Passo 2 do workflow** (`TEMPLATE.md`) agora exige que o agente defina antecipadamente **ambas as paletas** (dark + light), o snippet do botão `#theme-toggle`, e o script anti-FOUC — reutilizados idênticos em todos os arquivos.
- **Tabela comparativa HTML vs Markdown** (no `TEMPLATE.md`, `README.md` e `QUICK-START.md`) atualizada para destacar o toggle de tema como vantagem do modo HTML.
- **Protocolo de testes** (`PROJECT-GUIDE.md`) inclui validação do toggle em múltiplos arquivos e da persistência entre páginas.

### Preservado
- **Dark continua padrão** se não houver preferência salva (não usamos `prefers-color-scheme` para manter comportamento previsível).
- Modo `markdown` inalterado.
- Todas as regras de fontes oficiais e validação MCP.

---

## [3.1.0] - 2026-05-15

### 🆕 Suporte a HTML como formato de saída padrão

Os kits agora podem ser gerados como `.html` single-file (padrão) ou `.md` clássico, escolha via nova variável.

### Adicionado
- **🆕 Variável `<<OUTPUT_FORMAT>>`** (opcional, padrão `html`) — define a extensão de todos os arquivos textuais do kit. Valores aceitos: `html` (padrão) ou `markdown`.
- **🆕 Modo HTML**: todos os arquivos textuais viram `.html` single-file (sem build, sem dependências locais), com:
  - Tema dark consistente entre todos os arquivos (mesma paleta do `simulado.html`)
  - TOC interno, navegação clicável entre arquivos (`README.html` é o hub)
  - Mermaid renderizado nativamente via CDN (sem precisar de plugin)
  - Tabelas estilizadas, blocos de código com formatação
  - Links externos abrem em nova aba (`target="_blank"`)
  - Abrem com duplo-clique no navegador, sem servidor
- **🆕 Tabela comparativa HTML vs Markdown** no `TEMPLATE.md`, `README.md` e `QUICK-START.md` explicando o caso de uso de cada formato.
- **🆕 Critérios de qualidade específicos para HTML** no checklist do template (consistência visual, navegação, renderização Mermaid).
- **🆕 Passo 2 do workflow** instrui o agente a anunciar o `<<OUTPUT_FORMAT>>` resolvido ao usuário e definir paleta CSS reutilizável antes de gerar arquivos.

### Alterado
- **Especificação de entregáveis**: todas as extensões `.md` viraram `.<EXT>` no `TEMPLATE.md` (resolvido para `html` ou `md` conforme `<<OUTPUT_FORMAT>>`). `simulado.html` e `flashcards.csv` mantêm extensão fixa em ambos os modos.
- **Documentação atualizada** (`README.md`, `QUICK-START.md`, `PROJECT-GUIDE.md`) para refletir o formato configurável e o padrão HTML.
- **Protocolo de testes**: agora cobre validação em ambos os modos (HTML e Markdown).

### Preservado
- Comportamento markdown clássico (v3.0) disponível via `<<OUTPUT_FORMAT>>=markdown`.
- Todas as regras de fontes oficiais e validação MCP da v3.0.
- Compatibilidade total com Anki (`flashcards.csv` sempre CSV) e ferramentas executáveis dos labs (arquivos `.py`, `.js`, `Dockerfile`, etc. mantêm extensão própria).

---

## [3.0.0] - 2026-05-13

### 🎉 Lançamento Público Inicial (v3)

Reescrita completa do template gerador de kits de estudo para certificação, otimizado para **iniciantes**.

### Adicionado
- **⚙️ Seção de Requisitos para Executar** - Bloco explícito no topo do README definindo **GitHub Copilot (Agent Mode) no VS Code** como ambiente oficialmente testado, com aviso de que outros agentes (Cursor, Windsurf, Cline, etc.) não foram validados
- **🧠 Recomendações de modelo LLM** - Tabela com modelos recomendados por provedor (Copilot, Anthropic, OpenAI, Google) e aviso para evitar modelos pequenos/rápidos na primeira execução
- **💰 Estimativa de consumo de tokens** - Tabela por tamanho de certificação (pequena/média/grande) com fatores que afetam o consumo
- **🎯 Modelo simplificado de variáveis** - Apenas 5 obrigatórias (`EXAM_CODE`, `DAYS_AVAILABLE`, `HOURS_PER_DAY`, `EXPERIENCE_LEVEL`, `PREFERRED_LANGUAGE`); 5 opcionais com padrões sensatos; 4 auto-derivadas pelo agente (vendor, domínio de docs, plataforma de aprendizagem, nome oficial do exame)
- **🤖 Passo 0 do agente** - Resolução automática de metadados técnicos via MCP a partir do código do exame, removendo a necessidade de o iniciante conhecer detalhes como `OFFICIAL_DOCS_DOMAIN`
- **📋 Avaliação diagnóstica** (20-25 questões) - Calibra plano de estudos ao nível real
- **📚 Primer de fundamentos** - Guia de pré-requisitos para scores diagnósticos <30%
- **📖 Glossário** (40-80 termos) - Termos técnicos A-Z com links oficiais
- **🗺️ Mapas conceituais** - Diagramas Mermaid mostrando relações entre conceitos
- **🧪 Labs em modo dual** - Modos Guiado (30-60min) + Speedrun (10-20min)
- **🎴 Sistema de flashcards** - TOP 50 Q&A + export CSV compatível com Anki
- **📝 Log de erros** - Template para rastrear erros com categorias
- **🎯 Simulador HTML** - Quiz interativo completo com cronômetro e explicações
- **🔒 Validação de fontes** - Impõe 100% docs oficiais do vendor (sem terceiros)
- **🌍 Suporte multi-idioma** - Gere em qualquer idioma (pt-BR, es-ES, etc.)
- **📊 Rastreamento de progresso** - Checklist no README e plano de estudos

### Alterado
- **Geração de plano de estudos** - Agora se adapta aos resultados diagnósticos (não apenas autoavaliação)
- **Estrutura de labs** - Dividido em modos guiado (aprendizagem) e speedrun (retenção)
- **Formato de quiz** - De markdown para HTML interativo com cronômetro
- **Documentação** - Instruções mais claras para iniciantes

### Melhorado
- **Foco em iniciantes** - Assume menos conhecimento prévio, adiciona scaffolding
- **Active recall** - Flashcards e rastreamento de erros para retenção
- **Calibração** - Avaliação diagnóstica garante dificuldade realística
- **Ética** - Imposição mais forte de apenas fontes oficiais

---

## [2.0.0] - 2026-03-XX (Interno)

### Adicionado
- Estrutura multi-domínio
- Cheatsheets de comandos CLI
- Guia de estratégia de exame
- Plano de simulados

### Alterado
- Assumia nível intermediário (sem suporte para iniciantes)
- Modo único de lab (sem divisão guiado/speedrun)
- Autoavaliação manual (sem diagnóstico)

### Problemas Conhecidos
- Requeria ajuste manual se iniciante
- Sem primer de vocabulário
- Sem ferramentas de retenção (flashcards)

---

## [1.0.0] - 2025-XX-XX (Interno)

### Adicionado
- Estrutura inicial do template
- Gerador básico de plano de estudos
- Guias de domínio
- Quiz simples em markdown

### Problemas Conhecidos
- Sem sistema de calibração
- Sem labs
- Customização limitada
- Apenas inglês

---

## Roadmap

### [3.3.0] - Planejado (Q3 2026)

**Recursos em consideração:**
- [ ] **Diagnóstico adaptativo** - Dificuldade das questões se ajusta com base nas respostas
- [ ] **Repetição espaçada** - Algoritmo SM-2 integrado para flashcards
- [ ] **Dashboard de progresso** - Página HTML rastreando conclusão
- [ ] **Export para PDF** - Export de guia de estudos com um clique
- [ ] **Simulador mobile-friendly** - Design responsivo para celular/tablet
- [ ] **Flashcards por voz** - Text-to-speech para revisão hands-free
- [ ] **Banco de questões da comunidade** - Extensão opcional com questões verificadas

**Documentação:**
- [ ] Tutorial em vídeo (YouTube)
- [ ] Demo interativo (teste antes de gerar)
- [ ] Expansão de FAQ
- [ ] Guia de solução de problemas

**Suporte de plataforma:**
- [ ] Extensão VSCode (geração com um clique)
- [ ] Ferramenta CLI (`npx cert-kit-gen`)
- [ ] Interface web (sem instalação local necessária)

---

## Histórico de Versões

| Versão | Data de Lançamento | Destaques |
|---------|--------------|----------|
| **v3.2.0** | 2026-05-15 | 🆕 Toggle de tema claro/escuro persistente em todos os HTML |
| **v3.1.0** | 2026-05-15 | 🆕 Suporte a HTML como formato de saída padrão |
| **v3.0.0** | 2026-05-13 | 🎉 Lançamento público, otimizado para iniciantes |
| v2.0.0 | 2026-03-XX | Interno, foco intermediário |
| v1.0.0 | 2025-XX-XX | Interno, MVP |

---

## Mudanças Disruptivas

### v3.0.0 (de v2.0.0)

**Mudanças de estrutura:**
- Adicionado `diagnostic.md` (agora obrigatório Dia 0)
- Adicionado `fundamentals.md` (condicional ao diagnóstico)
- Adicionado `glossary.md` e `concept-map.md`
- Adicionado `flashcards.csv` (além do `.md`)
- Adicionado `mistake-log.md`
- Labs divididos em 2 READMEs (`-guided.md` + `-speedrun.md`)

**Mudanças de variáveis:**
- Adicionado `<<EXPERIENCE_LEVEL>>` (obrigatório)
- Adicionado `<<PREFERRED_LANGUAGE>>` (obrigatório)
- Adicionado `<<WEAK_AREAS>>` / `<<STRONG_AREAS>>` (obrigatório)

**Mudanças de conteúdo:**
- `study-plan.md` agora referencia resultados diagnósticos
- `simulado.html` agora inclui botão mistake-log
- Todos os arquivos devem linkar para fontes oficiais (imposto)

**Migração da v2:**
Se você usou v2, regenere do zero com v3. Migração manual não é recomendada.

---

## Contribuindo para o Changelog

Ao enviar PRs que mudam funcionalidade:

1. Adicione entrada sob a seção **[Não Lançado]**
2. Use categorias: Adicionado, Alterado, Descontinuado, Removido, Corrigido, Segurança
3. Linke para issue/PR: `- Corrigido bug de pontuação diagnóstica (#42)`
4. Siga o formato: `- **Nome da funcionalidade** - Descrição`

---

## Dúvidas?

- **Sobre lançamentos:** Confira [GitHub Releases](../../releases)
- **Sobre roadmap:** Participe das [Discussions](../../discussions)
- **Reportar bugs:** [Abra uma issue](../../issues)

---

**Última atualização:** 2026-05-13  
**Versão estável atual:** v3.0.0  
**Licença:** MIT
