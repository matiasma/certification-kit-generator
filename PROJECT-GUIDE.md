# 📘 Guia de Estrutura de Projeto e Manutenção

> **Para contribuidores e mantenedores do projeto Gerador de Kits de Certificação**

---

## 📁 Estrutura do Repositório

```
certification-kit-generator/
├── README.md                  # Página de destino principal (voltada ao usuário)
├── TEMPLATE.md                # O template de prompt real
├── QUICK-START.md             # Tutorial rápido de 4 passos
├── CONTRIBUTING.md            # Diretrizes de contribuição
├── PROMOTIONAL-POSTS.md       # Posts de mídia social para promoção
├── CHANGELOG.md               # Histórico de versões e roadmap
├── LICENSE                    # Licença MIT
├── .gitignore                 # Padrões de ignoração do Git
└── docs/ (futuro)             # Documentação detalhada
    ├── FAQ.md                 # Perguntas frequentes
    ├── USAGE.md               # Guia de uso detalhado
    └── CUSTOMIZATION.md       # Como customizar template
```

---

## 📝 Propósitos dos Arquivos

### Arquivos Principais (Voltados ao Usuário)

#### `README.md`
- **Propósito:** Página de destino de marketing, primeira impressão
- **Audiência:** Novos usuários descobrindo o projeto
- **Tom:** Empolgante, focado em benefícios, visual
- **Atualizações:** Ao adicionar recursos ou estatísticas
- **Tamanho:** ~10-12 min de leitura

#### `TEMPLATE.md`
- **Propósito:** O prompt real que usuários copiam/colam
- **Audiência:** Agentes de IA (GitHub Copilot, etc.)
- **Tom:** Técnico, preciso, instrucional
- **Atualizações:** Ao melhorar lógica de geração ou qualidade
- **Tamanho:** ~15 min de leitura para usuários (mas agentes o consomem)

#### `QUICK-START.md`
- **Propósito:** Caminho mais rápido para primeiro kit (minimizar atrito)
- **Audiência:** Usuários impacientes que querem resultados AGORA
- **Tom:** Orientado à ação, passo-a-passo, visual
- **Atualizações:** Quando o workflow muda ou bloqueios comuns são encontrados
- **Tamanho:** ~3-5 min de leitura

---

### Arquivos Meta (Voltados ao Contribuidor)

#### `CONTRIBUTING.md`
- **Propósito:** Diretrizes para contribuições da comunidade
- **Audiência:** Contribuidores, desenvolvedores
- **Tom:** Acolhedor mas com regras claras
- **Atualizações:** Ao aceitar novos tipos de contribuições
- **Tamanho:** ~8 min de leitura

#### `CHANGELOG.md`
- **Propósito:** Rastrear histórico de versões e roadmap
- **Audiência:** Usuários avançados, contribuidores, mantenedores
- **Tom:** Factual, cronológico, detalhado
- **Atualizações:** A cada lançamento, a cada mudança disruptiva
- **Tamanho:** Cresce com o tempo

#### `LICENSE`
- **Propósito:** Permissões legais (MIT)
- **Audiência:** Equipes jurídicas, usuários empresariais
- **Tom:** Jargão legal padrão
- **Atualizações:** Nunca (MIT é padrão)

---

### Arquivos de Marketing

#### `PROMOTIONAL-POSTS.md`
- **Propósito:** Posts de mídia social prontos para uso
- **Audiência:** Mantenedores de projeto, promotores da comunidade
- **Tom:** Focado em marketing, engajador
- **Atualizações:** Ao adicionar novas plataformas ou ângulos
- **Tamanho:** Material de referência (não destinado a leitura linear)

---

## 🔄 Workflow de Atualização

### Ao Adicionar um Recurso

1. **Atualize `TEMPLATE.md`**
   - Adicione as novas instruções de prompt
   - Teste que gera corretamente

2. **Atualize `CHANGELOG.md`**
   - Adicione entrada sob `[Não Lançado]`
   - Descreva o que mudou e por quê

3. **Atualize `README.md`**
   - Adicione recurso à seção "O Que é Gerado"
   - Atualize estatísticas (contagem de arquivos, recursos, etc.)

4. **Crie GitHub Release**
   - Marque versão (ex: `v3.1.0`)
   - Copie entrada do changelog para notas de lançamento

---

### Ao Corrigir um Bug

1. **Corrija em `TEMPLATE.md`**
2. **Atualize `CHANGELOG.md`**
   - Adicione à seção `Corrigido`
3. **Adicione ao FAQ** (se for um problema comum)

---

### Ao Adicionar Novo Suporte de Certificação

1. **Teste geração** com a nova cert
2. **Atualize "Certificações Suportadas" em `README.md`**
3. **Opcional:** Crie repositório de showcase

---

### Checklist de Manutenção Mensal

- [ ] Revisar issues abertas (responder em 48h)
- [ ] Verificar PRs (revisar em 1 semana)
- [ ] Atualizar estatísticas no README (downloads, stars, forks)
- [ ] Testar template com modelos de IA mais recentes
- [ ] Atualizar dependências (se houver)
- [ ] Verificar links quebrados

---

## 🧪 Protocolo de Testes

Antes de lançar uma nova versão:

### 1. Testes Funcionais
- [ ] Gerar kit para cert Azure (AZ-204) em **modo HTML padrão**
- [ ] Gerar kit para cert AWS (SAA-C03) em **modo Markdown** (`<<OUTPUT_FORMAT>>=markdown`)
- [ ] Gerar kit para Kubernetes (CKA)
- [ ] Gerar kit em idioma não-inglês (pt-BR)
- [ ] Verificar se todos os 30-35 arquivos foram criados na extensão correta (`.html` ou `.md`)
- [ ] Abrir `simulado.html` no navegador (funciona?)
- [ ] No modo HTML: abrir `README.html` e validar navegação clicável entre arquivos
- [ ] No modo HTML: validar que `concept-map.html` renderiza Mermaid via CDN
- [ ] 🆕 No modo HTML: clicar no botão de toggle de tema em pelo menos 3 arquivos diferentes e validar que (a) o tema alterna entre dark e light, (b) a escolha persiste ao navegar para outras páginas, (c) não há FOUC ao carregar páginas com tema light salvo
- [ ] Importar `flashcards.csv` para Anki (importa corretamente?)
- [ ] Executar pelo menos 1 lab (código executa?)

### 2. Testes de Qualidade
- [ ] Verificar se todos os links apontam para fontes oficiais
- [ ] Verificar se diagramas Mermaid renderizam (em md via GitHub/VS Code; em html via CDN)
- [ ] Verificar formatação (markdown puro ou HTML com tema dark/claro consistente e toggle funcional)
- [ ] Testar com diferentes níveis de experiência
- [ ] Testar com diferentes restrições de tempo
- [ ] Testar com `<<OUTPUT_FORMAT>>=html` e `<<OUTPUT_FORMAT>>=markdown`

### 3. Testes de Documentação
- [ ] Seguir QUICK-START.md passo-a-passo
- [ ] Verificar se instruções de CONTRIBUTING.md são claras

---

## 📊 Métricas para Rastrear

Monitore essas para entender a saúde do projeto:

### Métricas do GitHub
- **Stars:** Indicador de visibilidade
- **Forks:** Interesse em customização
- **Issues:** Carga de suporte
- **PRs:** Engajamento da comunidade

### Métricas de Uso (se analytics for adicionado depois)
- **Downloads de template:** Quantas pessoas tentam
- **Certificações geradas:** Quais certs são populares
- **Idiomas usados:** Prioridades de localização
- **Variáveis comuns:** Otimizar para casos de uso comuns

### Métricas da Comunidade
- **Histórias de sucesso:** Usuários que passaram em exames
- **Perguntas em Discussions:** Pontos de dor comuns

---

## 🎯 Padrões de Qualidade

### Para README.md
- ✅ Proposta de valor clara nas primeiras 3 linhas
- ✅ Elementos visuais (badges, emojis, tabelas)
- ✅ Amigável a mobile (testar no celular)
- ✅ Links funcionam (testar trimestralmente)

### Para TEMPLATE.md
- ✅ Gera todos os 30-35 arquivos consistentemente
- ✅ Todos os links apontam para fontes oficiais
- ✅ Lida com casos extremos (nível desconhecido, prazo apertado)
- ✅ Funciona com múltiplos agentes de IA (não apenas Copilot)
- ✅ Sem datas ou versões hardcoded (use "atual" ou valide)

---

## 🚨 O Que NÃO Aceitar

### Pull Requests
- ❌ Adicionar links de cursos de terceiros
- ❌ Adicionar links de afiliados
- ❌ Promover "exam dumps"
- ❌ Quebrar regras de validação de fonte
- ❌ Remover atribuição

### Issues
- ❌ "Como passo sem estudar?"
- ❌ "Pode compartilhar questões reais do exame?"
- ❌ Spam ou auto-promoção

### Suporte a Certificações
- ❌ Certificações sem docs oficiais
- ❌ Certificações não-técnicas
- ❌ Certificações que proíbem materiais de preparação

---

## 📜 Filosofia

Este projeto existe para:
1. **Democratizar preparação para certificação** — Ninguém deveria pagar R$ 2500 por docs públicos organizados
2. **Manter integridade** — Apenas fontes oficiais, sem atalhos
3. **Otimizar para aprendizado** — Não apenas passar, mas entender
4. **Permanecer aberto** — Licença MIT para sempre, orientado pela comunidade

**Nós não:**
- Competimos com treinamento oficial (fazemos referência a ele!)
- Oferecemos "garantias de aprovação" (ninguém pode)
- Aceitamos "exam dumps" ou questões reais
- Cobramos dinheiro (sempre gratuito)

---

**Dúvidas sobre este guia?**

Abra uma discussion: [GitHub Discussions](https://github.com/YOUR-USERNAME/certification-kit-generator/discussions)

---

**Última atualização:** 2026-05-15  
**Mantenedor:** [Seu Nome]
