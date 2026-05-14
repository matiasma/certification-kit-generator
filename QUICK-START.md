# ⚡ Guia de Início Rápido

**Obtenha seu kit de estudos completo em 10 minutos!**

---

## 📋 Pré-requisitos

> ⚠️ **Ambiente testado:** **GitHub Copilot (Agent Mode) no VS Code**. Outros agentes (Cursor, Windsurf, Cline, Claude Desktop, etc.) podem funcionar, mas **não foram validados** — o resultado pode divergir. Veja a [seção completa de Requisitos no README](README.md#-requisitos-para-executar).

- ✅ **VS Code** (versão atual)
- ✅ **GitHub Copilot** + **GitHub Copilot Chat** (extensões instaladas e ativas)
- ✅ Plano **Pro, Business ou Enterprise** (Free pode esgotar mensagens)
- ✅ **Agent Mode** habilitado no Copilot Chat (não Ask/Edit Mode)
- ✅ **Modelo LLM** com janela ≥128k — recomendado: Claude Sonnet 4.5 ou GPT-5 (evite `mini`/`flash`/`haiku` na primeira execução)
- ✅ Permissão para uso de **MCPs/tools** quando o agente solicitar
- ✅ **5-15 minutos** de tempo + boa conexão de internet

> 💰 **Consumo médio de tokens por execução:** ~200-340k para certificações de tamanho médio (AZ-204, AWS-SAA, CKAD). Pode variar de ~110k (exames fundamentos) a ~550k (exames de arquitetura). Veja a tabela completa no [README](README.md#-estimativa-de-consumo-de-tokens). Usando GitHub Copilot, o consumo entra na sua assinatura mensal.

---

## 🚀 4 Passos para Seu Kit de Estudos

### Passo 1: Baixe o Template

**Opção A:** Clone este repositório
```bash
git clone https://github.com/YOUR-USERNAME/certification-kit-generator.git
cd certification-kit-generator
```

**Opção B:** Baixe apenas o template
- Vá para [`TEMPLATE.md`](TEMPLATE.md)
- Clique no botão **Raw**
- Copie todo o conteúdo (Ctrl+A, Ctrl+C)

---

### Passo 2: Preencha Suas Variáveis

> 🎯 **Para iniciantes:** você só precisa preencher **5 variáveis obrigatórias**. As demais têm padrão ou são descobertas automaticamente pelo agente.

Abra `TEMPLATE.md` e localize a seção **Variáveis** no topo.

#### ✅ Obrigatórias (você preenche)

```markdown
<<EXAM_CODE>>           = AZ-204           # código oficial do exame
<<DAYS_AVAILABLE>>      = 15               # dias até o exame (ou "flexível")
<<HOURS_PER_DAY>>       = 2                # horas de estudo por dia
<<EXPERIENCE_LEVEL>>    = iniciante        # iniciante absoluto | iniciante com base | intermediário
<<PREFERRED_LANGUAGE>>  = pt-BR            # pt-BR | en-US | es-ES | ...
```

#### 🟡 Opcionais (têm padrão sensato — preencha se souber)

```markdown
<<EXAM_DATE>>     = 2026-06-15      # padrão: "não marcada"
<<PRIOR_CERTS>>   = AZ-900           # padrão: "nenhuma"
<<STRONG_AREAS>>  = redes, C#        # padrão: "desconhecido" (diagnóstico calibra)
<<WEAK_AREAS>>    = segurança        # padrão: "desconhecido" (diagnóstico calibra)
<<NOTE_TOOL>>     = Notion           # padrão: "nenhum"
```

#### 🤖 Auto-derivadas (o agente descobre — **você NÃO precisa saber**)

Estas variáveis técnicas são resolvidas automaticamente a partir do `<<EXAM_CODE>>` consultando docs oficiais via MCP:

- `<<EXAM_NAME>>` — nome oficial do exame
- `<<EXAM_VENDOR>>` — vendor (Microsoft, AWS, CNCF, etc.)
- `<<OFFICIAL_DOCS_DOMAIN>>` — domínio canônico de documentação
- `<<VENDOR_LEARNING_PLATFORM>>` — plataforma oficial de aprendizagem

Você pode deixar esses campos com os placeholders originais — o agente sobrescreve antes de gerar o kit.

**Como editar:**
- Use **Localizar e Substituir** (Ctrl+H no VS Code) para trocar cada `<<VARIAVEL>>` pelo seu valor
- Ou edite manualmente as 5 linhas obrigatórias

---

### Passo 3: Crie um Workspace Vazio

**Importante:** Comece com uma pasta de workspace **limpa e vazia**!

```bash
# Crie uma nova pasta para seu kit
mkdir meu-kit-az-204
cd meu-kit-az-204

# Abra no VS Code
code .
```

**Por que vazio?** O template criará 30-35 arquivos. Começar em uma pasta vazia mantém tudo organizado.

---

### Passo 4: Execute em um Agente de IA

#### Usando GitHub Copilot:

1. **Abra o Copilot Chat** (Ctrl+I ou clique no ícone de chat)
2. **Cole o template preenchido** (tudo, incluindo a seção de prompt entre as cercas)
3. **Pressione Enter** ⏎
4. **Aguarde 5-15 minutos** ⏱️

Você verá o agente:
- ✅ Criando estrutura de pastas
- ✅ Consultando docs oficiais (via MCP)
- ✅ Gerando questões diagnósticas
- ✅ Criando guias de estudo
- ✅ Construindo labs
- ✅ Gerando simulador HTML
- ✅ Criando flashcards

#### Usando outros agentes (não testados oficialmente):

> ⚠️ Cursor, Windsurf, Cline, Claude Desktop, ChatGPT etc. **não foram validados**. Pode funcionar, mas o resultado pode divergir (arquivos faltando, links inválidos, conteúdo truncado). Use por sua conta e risco e valide o material contra a documentação oficial do vendor.

Se ainda assim quiser tentar:
1. Abra o chat do agente em um workspace vazio
2. Garanta que ele tenha permissão para criar arquivos e usar tools (MCP ou `fetch`)
3. Cole o template preenchido
4. Aguarde a conclusão

---

## ✅ Verifique Seu Kit

Após a conclusão da geração, sua pasta deve parecer assim:

```
meu-kit-az-204/
├── README.md              ✅
├── diagnostic.md          ✅
├── fundamentals.md        ✅
├── glossary.md            ✅
├── concept-map.md         ✅
├── study-plan.md          ✅
├── cheatsheet.md          ✅
├── pegadinhas.md          ✅
├── exam-strategy.md       ✅
├── mock-exam-plan.md      ✅
├── simulado.html          ✅ (Abra isso no navegador!)
├── flashcards.md          ✅
├── flashcards.csv         ✅
├── mistake-log.md         ✅
├── domains/
│   ├── 01-*.md            ✅
│   ├── 02-*.md            ✅
│   ├── ...
└── labs/
    ├── 01-*/              ✅
    │   ├── README-guided.md
    │   ├── README-speedrun.md
    │   └── <arquivos de código>
    └── ...
```

**Esperado:**
- **~35 arquivos** no total
- **50.000-70.000 palavras** de conteúdo
- **3-5 labs** com código executável
- **50 flashcards** em markdown + CSV
- **Quiz HTML interativo** (duplo-clique para abrir)

---

## 🎯 O Que Fazer a Seguir

### Dia 0 (30 minutos)
1. **Leia `README.md`** — Entenda a estrutura
2. **Faça `diagnostic.md`** — Calibre seu nível
3. **Verifique os resultados** — Veja se você precisa de `fundamentals.md`

### Dia 1+ (Siga `study-plan.md`)
- Cada dia tem leitura atribuída, labs e flashcards
- Acompanhe progresso em `mistake-log.md`
- Revise `pegadinhas.md` regularmente

### Última Semana
- Complete `simulado.html` (simulação completa do exame)
- Revise `exam-strategy.md` (técnica dos 3 passes)
- Revisão de última hora com `cheatsheet.md`

---

## ❓ Solução de Problemas

### "O agente continua pedindo esclarecimentos"
- Certifique-se de ter preenchido **todas as variáveis** (nenhum `<<PLACEHOLDER>>` restante)
- Verifique se o código do exame está correto (ex: `az-204`, não `AZ204`)

### "O agente parou no meio"
- Alguns agentes têm limites de tokens — apenas diga "continue" ou "termine"
- Se persistir, divida em requisições menores (ex: "termine os domínios primeiro")

### "O conteúdo gerado está no idioma errado"
- Verifique se `<<PREFERRED_LANGUAGE>>` está configurado corretamente (ex: `pt-BR`, não `portuguese`)
- Regenere do zero com a variável corrigida

### "O simulador HTML não funciona"
- Certifique-se de que `simulado.html` foi totalmente gerado (verifique tamanho do arquivo >100KB)
- Abra diretamente no navegador (Firefox, Chrome, Edge)
- Verifique o console do navegador para erros (F12)

### "Os labs não executam"
- Verifique se todos os arquivos de código foram gerados (não apenas READMEs)
- Instale dependências (`requirements.txt`, `package.json`)
- Verifique se você tem as ferramentas necessárias (Docker, Python, Node, etc.)

---

## 💡 Dicas Profissionais

### ⚡ Acelere a Geração
- Use um **modelo LLM atual com janela ampla** (Claude Sonnet 4.5, GPT-5 ou Gemini 2.5 Pro)
- Garanta boa internet (consultas MCP precisam dela)
- Execute em horários fora de pico se estiver usando serviço de IA compartilhado

### 💰 Controle de Consumo de Tokens
- Um kit médio consome **~200-340k tokens** por execução (entrada + saída)
- Exames pequenos (AZ-900, GH-Foundations) ficam em ~110-170k
- Exames grandes (AZ-305, AWS-SAP) podem chegar a ~550k
- Se o agente parar no meio, peça para **continuar** em vez de regerar tudo

### 🎨 Customize Após a Geração
- Todos os arquivos são markdown — edite livremente!
- Adicione notas pessoais
- Faça fork e customize para sua equipe

### 🔄 Regenere se Necessário
- Não ficou satisfeito com os resultados? **Ajuste variáveis e regenere**
- Exemplo: Aumente `<<HOURS_PER_DAY>>` para conteúdo mais detalhado

### 📦 Compartilhe Seu Kit
- Publique no GitHub (é tudo markdown + HTML)
- Adicione um disclaimer de que é educacional
- Faça link para este template para que outros possam gerar o próprio

### 🧪 Teste Antes de Estudar
- Abra `simulado.html` — certifique-se de que funciona
- Tente um lab — verifique se o código roda
- Importe `flashcards.csv` para o Anki — verifique o formato

---

## 🎓 Checklist de Sucesso

Use isso para verificar se você está pronto para começar a estudar:

- [ ] Kit gerado com sucesso (30-35 arquivos)
- [ ] `README.md` explica a estrutura
- [ ] `diagnostic.md` concluído (pontuado por domínio)
- [ ] `fundamentals.md` revisado (se necessário)
- [ ] `study-plan.md` faz sentido para minha agenda
- [ ] `simulado.html` abre e funciona no navegador
- [ ] Pelo menos 1 lab roda com sucesso
- [ ] Flashcards importados para Anki (opcional)
- [ ] `mistake-log.md` pronto para uso

---

## 🆘 Precisa de Ajuda?

- **Problemas com template:** [Abra uma issue](https://github.com/YOUR-USERNAME/certification-kit-generator/issues)
- **Dúvidas de uso:** [GitHub Discussions](https://github.com/YOUR-USERNAME/certification-kit-generator/discussions)

---

## 🎉 Você Está Pronto!

Você agora tem:
- ✅ Materiais de estudo completos (30-35 arquivos)
- ✅ Personalizados para SEU nível e cronograma
- ✅ 100% baseado em docs oficiais do vendor
- ✅ Gratuito e open-source

**Próximo:** Abra `README.md` no seu kit gerado e comece o Dia 0!

---

**Tempo investido:** 10 minutos  
**Valor recebido:** 40+ horas de material de estudo organizado  
**Custo:** Apenas o consumo de tokens

**Boa sorte com sua certificação!** 🚀🎓

---

**⭐ Se isso ajudou você, dê uma estrela no repositório!** Isso ajuda outras pessoas a descobrirem esta ferramenta.

[⬅️ Voltar para README Principal](README.md) | [🎯 Template Completo](TEMPLATE.md)
