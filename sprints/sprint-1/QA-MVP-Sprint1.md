# QA - MVP Sprint 1

**Objetivo:** Checklist e passos de QA para validar o MVP mínimo (Sprint 1)

## Preparação
- Rodar `docker-compose up` no root do projeto
- Rodar `npm run dev` no frontend
- Verificar `npm run type-check` e `npm run build`

## Cenários principais

### 1. Login / Sessão
- [ ] Login com `admin@engflow.local` funciona
- [ ] Token salvo em localStorage
- [ ] Token renova via refresh automaticamente

### 2. Projects UI (Vuetify)
- [ ] Projects page usa Vuetify components
- [ ] Lista mostra projetos reais
- [ ] Filtros (name/status) funcionam
- [ ] Loading states durante requests
- [ ] Mensagens de erro amigáveis ao criar/editar

### 3. Error Handling
- [ ] 400 validation errors mostram detalhes
- [ ] 401 redireciona para login quando necessário
- [ ] 500 mostra toast com "Erro interno"

### 4. Tests
- [ ] Backend: testes unitários relevantes passam
- [ ] Frontend: testes unitários das views críticas passam

### 5. Regression
- [ ] Navegar entre páginas sem console errors
- [ ] Criar projeto e confirmar persistência

---

## Relatório de bugs
- Registrar: passo, input, resultado esperado, resultado real, logs do browser

---

**Fim do QA**
