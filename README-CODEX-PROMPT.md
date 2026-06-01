# 📚 COMO USAR ESTES ARQUIVOS DE CONTEXTO

**Data criação:** 26 de maio de 2026  
**Para:** Codex Agent (você ou qualquer desenvolvedor IA)  
**Escopo:** Sprint 0 - Integração Frontend-Backend MVP

---

## 🎯 OS 3 ARQUIVOS CRIADOS

### 1️⃣ `.codex-instructions.md` ← COMECE AQUI
**Tamanho:** ~400 linhas  
**Tempo leitura:** 10-15 minutos  
**Propósito:** Instruções operacionais diretas

**Contém:**
- Leitura obrigatória (master.md + codex.md)
- Protocolo de trabalho
- 11 tasks resumidas com dependências
- Estratégia de execução
- Troubleshooting
- Checklist final

**Use quando:** Quer começar rápido e saber por onde ir

---

### 2️⃣ `.codex-sprint0-action.md` ← GUIA DE AÇÃO
**Tamanho:** ~600 linhas  
**Tempo leitura:** 15-20 minutos  
**Propósito:** Plano executivo com código pronto

**Contém:**
- Cada task com código completo para copiar/colar
- Explicação do por quê
- Como validar
- Exemplos reais
- Checklist de validação

**Use quando:** Quer código pronto para implementar

---

### 3️⃣ `.codex-sprint0-context.md` ← REFERÊNCIA PROFUNDA
**Tamanho:** ~900 linhas  
**Tempo leitura:** 30-45 minutos  
**Propósito:** Contexto completo, detalhes arquiteturais

**Contém:**
- Leitura obrigatória (em ordem)
- Status atual detalhado
- Cada task explicado em profundidade
- Exemplos de implementação
- Padrões de código
- Instruções de trabalho
- Próximas sprints
- Localizações de tudo

**Use quando:** Quer entender tudo em profundidade antes de codificar

---

## 🚀 FLUXO RECOMENDADO

### Para Começar Imediatamente:
```
1. Leia `.codex-instructions.md` inteiro (15 min)
   ↓
2. Execute Task 1: CORS (15 min)
   ↓
3. Execute Task 2: DB Seed (1 hora)
   ↓
4. Execute Task 3: Services (4-6 horas) ← Use `.codex-sprint0-action.md`
```

### Se Precisar de Contexto Mais Profundo:
```
1. Leia `master.md` (princípios)
   ↓
2. Leia `e-engineer-backend/docs/codex.md` (decisões backend)
   ↓
3. Leia `e-engineer-frontend/codex.md` (decisões frontend)
   ↓
4. Leia `.codex-sprint0-context.md` (tudo sobre Sprint 0)
   ↓
5. Use `.codex-sprint0-action.md` enquanto implementa
```

### Se Ficar Preso:
```
1. Verifique qual task está fazendo
   ↓
2. Busque secção relevante em `.codex-sprint0-context.md`
   ↓
3. Leia troubleshooting em `.codex-instructions.md`
   ↓
4. Compare código com exemplos em `.codex-sprint0-action.md`
```

---

## 📋 QUICK START (5 MINUTOS)

Se você quer começar JÁ:

```bash
cd /home/lkt/work/e_engineer

# 1. Leia instruções rápidas (5 min)
cat .codex-instructions.md | head -80

# 2. Task 1: CORS (15 min)
# Edit: e-engineer-backend/src/main.ts
# Add CORS before app.listen()

# 3. Task 2: Seed database (1 hora)
# Run: npm run db:fresh (no backend)
# Validate: psql check

# 4. Depois leia Task 3 em detalhes
cat .codex-sprint0-action.md | grep -A 100 "### 🔴 Task 3"
```

---

## 📊 STRUCTURE DOS ARQUIVOS

### `.codex-instructions.md`
```
├── Sua Missão
├── Leitura Obrigatória
├── Protocolo de Trabalho
├── Arquitetura Resumida (Referência)
├── 11 Tasks Ordenadas
├── Task Dependencies Graph
├── Execution Strategy
├── Success Criteria
├── Coding Standards
├── Troubleshooting
├── Git Commits Guide
└── Start Here + Final Checklist
```

### `.codex-sprint0-action.md`
```
├── Missão
├── 11 Tasks com:
│   ├── Arquivo(s) a editar
│   ├── Código pronto para copiar
│   ├── Como validar
│   ├── Por quê (business logic)
│   └── Exemplo de teste
├── Validação Final
├── Progresso (table)
├── Resultado Esperado
└── Troubleshooting
```

### `.codex-sprint0-context.md`
```
├── Leitura Obrigatória (em ordem)
├── Objetivo Sprint 0
├── 11 Tasks com:
│   ├── Explicação profunda
│   ├── Por quê (negócio + arquitetura)
│   ├── Padrões de código
│   ├── Exemplos completos
│   ├── Como validar
│   └── Referências
├── Validação Final
├── Instruções de Trabalho
├── Proximos Passos (Sprint 1)
└── Checklist Conclusão
```

---

## 🎯 POR TASK: QUAL ARQUIVO CONSULTAR

| Task | Quando | Arquivo |
|------|--------|---------|
| Entender contexto geral | Start | `.codex-instructions.md` |
| Saber por onde começar | Start | `.codex-instructions.md` |
| Implementar código | During | `.codex-sprint0-action.md` |
| Entender padrões | During | `.codex-sprint0-context.md` |
| Validar após task | After | `.codex-sprint0-action.md` |
| Ficou preso | Blocked | `.codex-sprint0-context.md` |
| Próximas sprints | After Sprint 0 | `.codex-sprint0-context.md` |

---

## 🔍 COMO BUSCAR NO ARQUIVO

```bash
# Procurar Task 3 no action file
grep -n "^### ✅ Task 3" .codex-sprint0-action.md

# Procurar services layer no context
grep -n "Frontend Services Layer" .codex-sprint0-context.md

# Procurar troubleshooting
grep -n "### 🔍 VALIDAÇÃO\|Troubleshooting\|BLOCKER" .codex-instructions.md

# Ver tamanho dos arquivos
wc -l .codex-*.md
```

---

## 📱 VERSÃO MOBILE: RESUMO 60 SEGUNDOS

**O que fazer:**
1. Ler `.codex-instructions.md` (15 min)
2. Task 1: Add CORS em main.ts (15 min)
3. Task 2: Rodar db:fresh (1 hora)
4. Task 3: Criar services layer (4-6 horas) — use `.codex-sprint0-action.md`
5. Tasks 4-6: Conectar componentes (3-4 horas)
6. Tasks 7-11: Polish + testes (6-8 horas)

**Total:** 18-24 horas para MVP pronto

**Validar:** Manual E2E pass + Auto E2E pass

---

## ✅ ESTE PROMPT ESTÁ COMPLETO QUANDO:

- [ ] Tasks 1-3 implementadas (CORS + Seed + Services)
- [ ] Tasks 4-6 implementadas (Login + Projects Store + Dashboard)
- [ ] Manual E2E testing passou (Task 10)
- [ ] Auto E2E test criado (Task 11)
- [ ] `npm run type-check` passa
- [ ] `npm run build` passa
- [ ] Commits pequenos e coesos
- [ ] Documentação atualizada (próximas sprints)

---

## 🚀 PRÓXIMO PASSO

**Para começar agora:**

1. Abra `.codex-instructions.md`
2. Leia até secção "TASKS ORDENADAS"
3. Execute Task 1: CORS (15 min)
4. Reporte quando terminar

**Depois:**
- Leia Task 2 em `.codex-instructions.md`
- Use `.codex-sprint0-action.md` como referência de código
- Use `.codex-sprint0-context.md` se ficar preso

---

## 📞 SUPPORT

Se algo não fizer sentido:

1. **Procure no arquivo:** Use `grep` para buscar palavra-chave
2. **Leia contexto:** Volte secção anterior para entender por quê
3. **Compare código:** Procure exemplo similar já implementado
4. **Valide types:** `npm run type-check` ajuda a diagnosticar
5. **Ask:** Se realmente não souber, pergunte

---

## 📈 MÉTRICAS DE PROGRESSO

| Milestone | Tarefas | Tempo | Checklist |
|-----------|---------|-------|-----------|
| Infraestrutura | 1-2 | 1-1.5h | [ ] CORS [ ] DB Seed |
| Core Integration | 3-6 | 9-12h | [ ] Services [ ] Real APIs |
| Robustez | 7-9 | 5-6h | [ ] Refresh [ ] Tipos |
| Testes | 10-11 | 5-8h | [ ] Manual E2E [ ] Auto E2E |
| **TOTAL** | **11** | **18-24h** | **MVP Ready** |

---

## 🎓 LEARNING PATH

Para quem quer aprender enquanto implementa:

1. **Day 1:** Leia master.md + codex.md (arquitetura é importante)
2. **Day 1:** Faça Tasks 1-2 (infra simple)
3. **Day 1-2:** Faça Task 3 (services layer é core — entenda bem)
4. **Day 2:** Faça Tasks 4-6 (conectar componentes)
5. **Day 2-3:** Faça Tasks 7-11 (polish + testes)

No final, você terá entendido:
- ✅ Clean Architecture + DDD (backend)
- ✅ Modular architecture (frontend)
- ✅ API integration patterns
- ✅ JWT authentication flow
- ✅ E2E testing
- ✅ Multi-tenancy
- ✅ Full stack development

---

## 🎯 GARANTIAS

Se você seguir estes arquivos corretamente:

✅ MVP funciona end-to-end (garantido)  
✅ Código segue padrões arquiteturais (garantido)  
✅ Types estão sincronizados (garantido)  
✅ Testes E2E passam (garantido)  
✅ Pronto para QA (garantido)

**Se algo der errado:** Verifique se completou todas as tasks em ordem

---

## 📝 TEMPLATE DE REPORT APÓS CADA TASK

```
Task X: [name]
Status: ✅ Complete / 🟡 In Progress / ❌ Blocked

What I did:
- [bullet 1]
- [bullet 2]

Validated:
- [check 1]
- [check 2]

Issues:
- [issue 1 if any]

Next step:
Task X+1: [name]
```

---

**Pronto? Comece com `.codex-instructions.md` agora! 🚀**

Bora codar! 🔥
