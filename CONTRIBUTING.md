# Contribuindo para o Gerador de Kits de Certificação

🎉 **Obrigado pelo seu interesse em contribuir!** Este projeto prospera com melhorias da comunidade.

---

## 🤝 Formas de Contribuir

### 1. 🐛 Reportar Bugs ou Problemas
Se você encontrou um problema com o template:
- **Verifique as issues existentes primeiro** para evitar duplicatas
- Abra uma nova issue com:
  - Título claro (ex: "Seção de diagnóstico gera formato de questão incorreto")
  - Passos para reproduzir
  - Comportamento esperado vs comportamento real
  - Suas variáveis (código do exame, vendor, etc.)
  - Arquivos gerados (se possível)

### 2. 💡 Sugerir Funcionalidades
Tem uma ideia para melhorar o template?
- Abra uma issue de **Feature Request**
- Explique o caso de uso e o benefício
- Forneça exemplos se possível

### 3. 📝 Melhorar Documentação
- Corrigir erros de digitação no README ou guias
- Adicionar esclarecimentos
- Traduzir documentação para outros idiomas
- Adicionar dicas de solução de problemas

### 4. 🛠️ Melhorar o Template
- Melhor engenharia de prompts
- Novos recursos (ex: rastreador de progresso, integração com plataformas de aprendizagem)
- Correções de bugs na lógica do template
- Adicionar suporte para novos tipos de certificação

---

## 📋 Processo de Pull Request

1. **Faça fork** deste repositório
2. **Crie um branch** para sua mudança:
   ```bash
   git checkout -b feat/nome-sua-funcionalidade
   # ou
   git checkout -b fix/sua-correcao-bug
   ```

3. **Faça suas alterações**
   - Siga o estilo/formato existente
   - Atualize a documentação se necessário
   - Teste suas mudanças (gere um kit com o template modificado)

4. **Commit** com commits convencionais:
   ```bash
   git commit -m "feat: adiciona suporte para certificações Kubernetes"
   git commit -m "fix: corrige formato de questão diagnóstica"
   git commit -m "docs: adiciona tradução em espanhol para README"
   git commit -m "chore: atualiza dependências"
   ```

5. **Push e abra PR**
   - Descreva o que mudou e por quê
   - Referencie issues relacionadas (ex: "Fixes #42")
   - Aguarde revisão

---

## ✅ Convenção de Mensagens de Commit

Use [Conventional Commits](https://www.conventionalcommits.org/):

- `feat:` — Nova funcionalidade
- `fix:` — Correção de bug
- `docs:` — Apenas documentação
- `style:` — Formatação (sem mudança de código)
- `refactor:` — Reestruturação de código (sem mudança de comportamento)
- `test:` — Adicionando testes
- `chore:` — Manutenção (dependências, configuração)

**Exemplos:**
```
feat: adiciona botão de clipboard mistake-log ao simulador
fix: corrige sintaxe Mermaid na geração de concept-map
docs: adiciona tradução README em português
```

---

## 🚫 O Que Não Aceitamos

### ❌ Fontes de Terceiros
- Links para cursos pagos
- Links para canais ou blogs não-oficiais
- Referências a "exam dumps" ou bancos de questões vazados
- Bancos de questões não-oficiais

**Por quê?** O template impõe **apenas fontes oficiais** para manter integridade e qualidade.

### ❌ Anúncios ou Auto-Promoção
- Não adicione links de afiliados
- Não promova seus cursos/produtos
- Não adicione pixels de rastreamento ou analytics

### ❌ Mudanças de Baixa Qualidade
- PRs automatizados em massa sem revisão
- Mudanças triviais (ex: adicionar um único espaço)
- PRs duplicados

---

## 🧪 Testando Suas Mudanças

Antes de enviar um PR que modifica `TEMPLATE.md`:

1. **Gere um kit de teste** usando seu template modificado
2. Verifique se todos os arquivos são criados corretamente
3. Verifique se os links apontam apenas para fontes oficiais
4. Teste o simulador HTML (abra e execute as questões)
5. Valide se os diagramas Mermaid renderizam corretamente

**Opcional mas apreciado:**
- Teste com múltiplos códigos de exame (Azure, AWS, GitHub, etc.)
- Teste com diferentes idiomas (pt-BR, es-ES, etc.)
- Documente quaisquer casos extremos que encontrou

---

## 📞 Dúvidas?

- **Perguntas gerais:** Abra uma [Discussion](https://github.com/YOUR-USERNAME/certification-kit-generator/discussions)
- **Bugs/funcionalidades:** Abra uma [Issue](https://github.com/YOUR-USERNAME/certification-kit-generator/issues)
- **Esclarecimentos rápidos:** Comente em issues/PRs existentes

---

## 📜 Código de Conduta

### Nosso Compromisso
Estamos comprometidos em fornecer uma comunidade acolhedora e inspiradora para todos.

### Nossos Padrões
- ✅ Seja respeitoso e inclusivo
- ✅ Dê boas-vindas a novatos e ajude-os a aprender
- ✅ Aceite críticas construtivas com elegância
- ✅ Foque no que é melhor para a comunidade

- ❌ Sem assédio, trolling ou discriminação
- ❌ Sem spam ou auto-promoção
- ❌ Sem conduta desrespeitosa ou não-profissional

### Aplicação
Violações podem ser reportadas para [MAINTAINER_EMAIL]. Todos os relatos serão revisados confidencialmente.

---

**Obrigado por tornar este projeto melhor!** 🙌

Cada contribuição, não importa quão pequena, ajuda estudantes em todo o mundo a alcançarem suas metas de certificação. 🎓🚀
