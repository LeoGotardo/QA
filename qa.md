# PLANO DE TESTES
## Sistema de Controle de Empréstimos Pessoais

**Projeto:** Controle de Empréstimos  
**Versão da Aplicação:** 1.0  
**Data do Plano:** 04/12/2024  
**Responsável pelos Testes:** [Seu Nome]  
**Tipo de Teste:** Funcional (Caixa Preta) + Usabilidade

---

## 1. OBJETIVO DOS TESTES

Validar se a aplicação atende a todos os requisitos funcionais e não-funcionais especificados, garantindo:
- ✅ Funcionalidades operando conforme esperado
- ✅ Interface intuitiva e responsiva
- ✅ Persistência correta dos dados
- ✅ Ausência de erros críticos

---

## 2. ESCOPO DOS TESTES

### 2.1 O que SERÁ testado:
- ✅ Todos os 9 Requisitos Funcionais (RF-001 a RF-009)
- ✅ Todos os 6 Requisitos Não-Funcionais (RNF-001 a RNF-006)
- ✅ Todas as 4 Regras de Negócio (RN-001 a RN-004)
- ✅ Compatibilidade entre navegadores
- ✅ Responsividade em diferentes telas

### 2.2 O que NÃO será testado:
- ❌ Testes de carga (não aplicável para LocalStorage)
- ❌ Testes de segurança avançados (fora do escopo)
- ❌ Testes automatizados (projeto acadêmico)

---

## 3. ESTRATÉGIA DE TESTES

### 3.1 Abordagem
- **Tipo:** Teste Manual Funcional
- **Técnica:** Caixa Preta (Black Box)
- **Método:** Partição de Equivalência + Análise de Valor Limite

### 3.2 Ambiente de Teste
- **Sistema Operacional:** Windows 10/11
- **Navegadores:**
  - Google Chrome (versão mais recente)
  - Mozilla Firefox (versão mais recente)
  - Microsoft Edge (versão mais recente)
- **Resoluções de Tela:**
  - Desktop: 1920x1080
  - Tablet: 768x1024
  - Mobile: 375x667

---

## 4. CASOS DE TESTE

---

### **CT-001: Cadastrar Empréstimo com Dados Válidos**
**Requisito:** RF-001, RN-001  
**Prioridade:** Alta  
**Pré-condição:** Aplicação aberta na aba "Novo Empréstimo"

| Passo | Ação | Resultado Esperado |
|-------|------|-------------------|
| 1 | Preencher "Nome do Item" com "Livro de Cálculo" | Campo aceita o texto |
| 2 | Preencher "Pessoa" com "Maria Silva" | Campo aceita o texto |
| 3 | Selecionar data de hoje | Data preenchida |
| 4 | Selecionar categoria "Livro" | Categoria selecionada |
| 5 | Preencher valor "150.00" | Valor aceito |
| 6 | Preencher observações "Capa azul" | Texto aceito |
| 7 | Clicar em "Cadastrar Empréstimo" | Alerta de sucesso aparece |
| 8 | Mudar para aba "Ativos" | Empréstimo aparece na lista |

**Critério de Aceitação:** Empréstimo cadastrado e visível na lista de ativos.

**Result:** Pass

---

### **CT-002: Validação de Campos Obrigatórios**
**Requisito:** RF-001, RN-001  
**Prioridade:** Alta  
**Pré-condição:** Aplicação aberta na aba "Novo Empréstimo"

| Passo | Ação | Resultado Esperado |
|-------|------|-------------------|
| 1 | Deixar "Nome do Item" em branco | Campo vazio |
| 2 | Deixar "Pessoa" em branco | Campo vazio |
| 3 | Deixar "Data" em branco | Campo vazio |
| 4 | Clicar em "Cadastrar Empréstimo" | Validação HTML5 impede envio |
| 5 | Mensagem de erro aparece | "Preencha este campo" exibido |

**Critério de Aceitação:** Formulário não permite envio sem campos obrigatórios.
**Result:** Pass

---

### **CT-003: Validação de Data Futura**
**Requisito:** RN-002  
**Prioridade:** Alta  
**Pré-condição:** Aplicação aberta na aba "Novo Empréstimo"

| Passo | Ação | Resultado Esperado |
|-------|------|-------------------|
| 1 | Preencher "Nome do Item" com "Tablet" | Campo aceita |
| 2 | Preencher "Pessoa" com "João" | Campo aceita |
| 3 | Selecionar data de amanhã (05/12/2024) | Data futura selecionada |
| 4 | Clicar em "Cadastrar Empréstimo" | Alerta "Data não pode ser futura!" |
| 5 | Empréstimo não é cadastrado | Lista permanece inalterada |

**Critério de Aceitação:** Sistema impede cadastro com data futura.

**Result:** Pass

---

### **CT-004: Listar Empréstimos Ativos**
**Requisito:** RF-002  
**Prioridade:** Alta  
**Pré-condição:** Pelo menos 2 empréstimos cadastrados

| Passo | Ação | Resultado Esperado |
|-------|------|-------------------|
| 1 | Navegar para aba "Ativos" | Aba exibida |
| 2 | Verificar lista de empréstimos | Todos ativos aparecem |
| 3 | Verificar informações exibidas | Item, pessoa, data, categoria, dias |
| 4 | Verificar cálculo de dias | Dias calculados corretamente |

**Critério de Aceitação:** Todos empréstimos não devolvidos aparecem com informações completas.

**Result:** Pass

---

### **CT-005: Cálculo Automático de Dias**
**Requisito:** RN-003  
**Prioridade:** Média  
**Pré-condição:** Empréstimo cadastrado há 5 dias

| Passo | Ação | Resultado Esperado |
|-------|------|-------------------|
| 1 | Cadastrar empréstimo com data de 5 dias atrás | Empréstimo criado |
| 2 | Verificar badge de dias na lista | Mostra "5 dias" |
| 3 | Cadastrar empréstimo de hoje | Empréstimo criado |
| 4 | Verificar badge de dias | Mostra "0 dias" |

**Critério de Aceitação:** Sistema calcula corretamente dias desde empréstimo.

**Result:** Pass

---

### **CT-006: Marcar Empréstimo como Devolvido**
**Requisito:** RF-003, RN-004  
**Prioridade:** Alta  
**Pré-condição:** Empréstimo ativo existente

| Passo | Ação | Resultado Esperado |
|-------|------|-------------------|
| 1 | Na aba "Ativos", localizar empréstimo | Empréstimo visível |
| 2 | Clicar em botão "✓ Devolvido" | Confirmação solicitada |
| 3 | Confirmar ação | Alerta de sucesso |
| 4 | Verificar lista de ativos | Empréstimo removido da lista |
| 5 | Navegar para aba "Histórico" | Empréstimo aparece com badge "Devolvido" |
| 6 | Verificar data de devolução | Data de hoje registrada |

**Critério de Aceitação:** Empréstimo movido para histórico com data de devolução.

**Result:** Pass

---

### **CT-007: Editar Empréstimo Ativo**
**Requisito:** RF-004  
**Prioridade:** Média  
**Pré-condição:** Empréstimo ativo existente

| Passo | Ação | Resultado Esperado |
|-------|------|-------------------|
| 1 | Clicar em botão "✎ Editar" | Modal de edição abre |
| 2 | Alterar "Nome do Item" para "Livro de Física" | Campo atualizado |
| 3 | Alterar categoria para "Livro" | Categoria alterada |
| 4 | Clicar em "Salvar" | Modal fecha |
| 5 | Verificar lista de ativos | Alterações refletidas |
| 6 | Verificar alerta de sucesso | Mensagem exibida |

**Critério de Aceitação:** Alterações são salvas e refletidas imediatamente.

**Result:** Pass

---

### **CT-008: Cancelar Edição**
**Requisito:** RF-004  
**Prioridade:** Baixa  
**Pré-condição:** Modal de edição aberto

| Passo | Ação | Resultado Esperado |
|-------|------|-------------------|
| 1 | Alterar campo "Nome do Item" | Campo modificado |
| 2 | Clicar em "Cancelar" | Modal fecha |
| 3 | Verificar empréstimo na lista | Dados originais mantidos |

**Critério de Aceitação:** Alterações são descartadas ao cancelar.

**Result:** Pass

---

### **CT-009: Excluir Empréstimo com Confirmação**
**Requisito:** RF-005  
**Prioridade:** Alta  
**Pré-condição:** Empréstimo ativo existente

| Passo | Ação | Resultado Esperado |
|-------|------|-------------------|
| 1 | Clicar em botão "✕ Excluir" | Confirmação aparece |
| 2 | Confirmar exclusão | Empréstimo removido |
| 3 | Verificar lista de ativos | Empréstimo não aparece mais |
| 4 | Verificar alerta | Mensagem de sucesso |

**Critério de Aceitação:** Empréstimo excluído permanentemente após confirmação.

**Result:** Pass

---

### **CT-010: Cancelar Exclusão**
**Requisito:** RF-005  
**Prioridade:** Média  
**Pré-condição:** Empréstimo ativo existente

| Passo | Ação | Resultado Esperado |
|-------|------|-------------------|
| 1 | Clicar em botão "✕ Excluir" | Confirmação aparece |
| 2 | Cancelar exclusão | Confirmação fecha |
| 3 | Verificar lista | Empréstimo permanece |

**Critério de Aceitação:** Empréstimo não é excluído ao cancelar.

**Result:** Pass

---

### **CT-011: Buscar Empréstimo por Nome do Item**
**Requisito:** RF-006  
**Prioridade:** Alta  
**Pré-condição:** 3+ empréstimos cadastrados

| Passo | Ação | Resultado Esperado |
|-------|------|-------------------|
| 1 | Na aba "Ativos", localizar caixa de busca | Campo visível |
| 2 | Digitar "Livro" | Busca em tempo real |
| 3 | Verificar resultados | Apenas itens com "Livro" aparecem |
| 4 | Digitar "xyz123" (não existe) | Mensagem "Nenhum empréstimo encontrado" |
| 5 | Limpar busca | Todos empréstimos voltam a aparecer |

**Critério de Aceitação:** Busca filtra resultados instantaneamente (case-insensitive).

**Result:** Pass

---

### **CT-012: Buscar Empréstimo por Nome da Pessoa**
**Requisito:** RF-006  
**Prioridade:** Alta  
**Pré-condição:** 3+ empréstimos cadastrados

| Passo | Ação | Resultado Esperado |
|-------|------|-------------------|
| 1 | Digitar "Maria" na busca | Filtro aplicado |
| 2 | Verificar resultados | Apenas empréstimos para "Maria" aparecem |

**Critério de Aceitação:** Busca funciona para nome da pessoa também.

**Result:** Pass

---

### **CT-013: Visualizar Histórico Completo**
**Requisito:** RF-007  
**Prioridade:** Média  
**Pré-condição:** Pelo menos 2 empréstimos devolvidos

| Passo | Ação | Resultado Esperado |
|-------|------|-------------------|
| 1 | Navegar para aba "Histórico" | Aba exibida |
| 2 | Verificar lista | Todos devolvidos aparecem |
| 3 | Verificar badge "Devolvido" | Badge verde visível |
| 4 | Verificar data de devolução | Data registrada corretamente |
| 5 | Verificar estilo visual | Cards com opacidade reduzida |

**Critério de Aceitação:** Histórico mostra apenas empréstimos devolvidos.

**Result:** Pass

---

### **CT-014: Categorizar Itens**
**Requisito:** RF-008  
**Prioridade:** Baixa  
**Pré-condição:** Formulário de cadastro aberto

| Passo | Ação | Resultado Esperado |
|-------|------|-------------------|
| 1 | Verificar campo "Categoria" | Select com opções visível |
| 2 | Clicar no select | Dropdown abre |
| 3 | Verificar opções disponíveis | Livro, Dinheiro, Eletrônico, Ferramenta, Jogo, Roupa, Outros |
| 4 | Selecionar "Eletrônico" | Opção selecionada |
| 5 | Cadastrar empréstimo | Badge "Eletrônico" aparece no card |

**Critério de Aceitação:** Sistema permite categorização com 7 opções predefinidas.

**Result:** Pass

---

### **CT-015: Adicionar Observações**
**Requisito:** RF-009  
**Prioridade:** Baixa  
**Pré-condição:** Formulário de cadastro aberto

| Passo | Ação | Resultado Esperado |
|-------|------|-------------------|
| 1 | Preencher campo "Observações" com texto longo (200 caracteres) | Texto aceito |
| 2 | Cadastrar empréstimo | Sucesso |
| 3 | Verificar card do empréstimo | Observação aparece com ícone 📝 |
| 4 | Deixar observações em branco | Campo opcional funciona |

**Critério de Aceitação:** Campo aceita texto livre e é opcional.

**Result:** Pass
---

### **CT-016: Persistência de Dados após Fechar Navegador**
**Requisito:** RNF-005  
**Prioridade:** Alta  
**Pré-condição:** 3 empréstimos cadastrados

| Passo | Ação | Resultado Esperado |
|-------|------|-------------------|
| 1 | Cadastrar 3 empréstimos | Sucesso |
| 2 | Fechar completamente o navegador | Navegador fechado |
| 3 | Reabrir o arquivo HTML | Aplicação carrega |
| 4 | Verificar lista de ativos | Todos os 3 empréstimos aparecem |
| 5 | Verificar dados | Todas informações intactas |

**Critério de Aceitação:** Dados persistem entre sessões via LocalStorage.

**Result:** Pass

---

### **CT-017: Estatísticas Atualizadas Automaticamente**
**Requisito:** RNF-001 (Usabilidade)  
**Prioridade:** Média  
**Pré-condição:** Aba "Ativos" aberta

| Passo | Ação | Resultado Esperado |
|-------|------|-------------------|
| 1 | Verificar "Empréstimos Ativos" | Contador mostra número correto |
| 2 | Verificar "Valor Total" | Soma de todos valores ativos |
| 3 | Cadastrar novo empréstimo de R$ 100 | Contador aumenta em 1 |
| 4 | Verificar valor total | Aumenta R$ 100,00 |
| 5 | Marcar um como devolvido | Contador diminui |
| 6 | Verificar valor total | Valor recalculado |

**Critério de Aceitação:** Dashboard atualiza em tempo real.

**Result:** Pass

---

### **CT-018: Performance com 100+ Registros**
**Requisito:** RNF-003  
**Prioridade:** Média  
**Pré-condição:** Nenhum empréstimo cadastrado

| Passo | Ação | Resultado Esperado |
|-------|------|-------------------|
| 1 | Cadastrar 100 empréstimos rapidamente | Sistema aceita todos |
| 2 | Navegar para aba "Ativos" | Lista carrega instantaneamente (<1s) |
| 3 | Usar busca | Filtro responde em tempo real |
| 4 | Marcar como devolvido | Ação executada rapidamente |
| 5 | Verificar histórico | Carregamento rápido |

**Critério de Aceitação:** Interface permanece responsiva com grande volume de dados.

**Result:** Pass

---

### **CT-019: Compatibilidade - Google Chrome**
**Requisito:** RNF-004  
**Prioridade:** Alta  
**Pré-condição:** Chrome instalado

| Passo | Ação | Resultado Esperado |
|-------|------|-------------------|
| 1 | Abrir aplicação no Chrome | Interface carrega corretamente |
| 2 | Testar todas funcionalidades | Tudo funciona |
| 3 | Verificar console (F12) | Sem erros JavaScript |
| 4 | Verificar layout | Design renderizado corretamente |

**Critério de Aceitação:** 100% funcional no Chrome.

**Result:** Pass

---

### **CT-020: Compatibilidade - Mozilla Firefox**
**Requisito:** RNF-004  
**Prioridade:** Alta  
**Pré-condição:** Firefox instalado

| Passo | Ação | Resultado Esperado |
|-------|------|-------------------|
| 1 | Abrir aplicação no Firefox | Interface carrega |
| 2 | Testar funcionalidades principais | Tudo funciona |
| 3 | Verificar LocalStorage | Dados persistem |
| 4 | Verificar console | Sem erros |

**Critério de Aceitação:** 100% funcional no Firefox.

**Result:** Pass

---

### **CT-021: Compatibilidade - Microsoft Edge**
**Requisito:** RNF-004  
**Prioridade:** Média  
**Pré-condição:** Edge instalado

| Passo | Ação | Resultado Esperado |
|-------|------|-------------------|
| 1 | Abrir aplicação no Edge | Interface carrega |
| 2 | Testar funcionalidades | Tudo funciona |
| 3 | Verificar compatibilidade CSS | Gradientes e estilos corretos |

**Critério de Aceitação:** 100% funcional no Edge.

**Result:** Pass

---

### **CT-022: Responsividade - Tela de Desktop (1920x1080)**
**Requisito:** RNF-001  
**Prioridade:** Alta  
**Pré-condição:** Navegador em tela cheia

| Passo | Ação | Resultado Esperado |
|-------|------|-------------------|
| 1 | Abrir aplicação | Layout otimizado para desktop |
| 2 | Verificar formulário | Campos bem espaçados |
| 3 | Verificar cards | Hover effects funcionando |
| 4 | Verificar estatísticas | Grid com 2 colunas |

**Critério de Aceitação:** Interface aproveitada bem espaço disponível.

**Result:** Pass

---

### **CT-023: Responsividade - Tela de Tablet (768x1024)**
**Requisito:** RNF-001  
**Prioridade:** Média  
**Pré-condição:** Navegador redimensionado

| Passo | Ação | Resultado Esperado |
|-------|------|-------------------|
| 1 | Redimensionar navegador para 768px largura | Layout adapta |
| 2 | Verificar formulário | Campos permanecem usáveis |
| 3 | Verificar cards | Botões acessíveis |
| 4 | Verificar estatísticas | Grid ajustado |

**Critério de Aceitação:** Interface utilizável em tablets.

**Result:** Pass

---

### **CT-024: Responsividade - Tela Mobile (375x667)**
**Requisito:** RNF-001  
**Prioridade:** Média  
**Pré-condição:** Modo de visualização mobile ativado (F12)

| Passo | Ação | Resultado Esperado |
|-------|------|-------------------|
| 1 | Ativar modo mobile no DevTools | Visualização mobile |
| 2 | Verificar menu de abas | Abas empilhadas se necessário |
| 3 | Verificar formulário | Campos ocupam largura total |
| 4 | Verificar botões | Tamanho adequado para toque |
| 5 | Verificar estatísticas | 1 coluna |

**Critério de Aceitação:** Interface funcional em telas pequenas.

**Result:** Pass

---

### **CT-025: Usabilidade - Feedback Visual**
**Requisito:** RNF-001, RNF-006  
**Prioridade:** Média  
**Pré-condição:** Aplicação aberta

| Passo | Ação | Resultado Esperado |
|-------|------|-------------------|
| 1 | Passar mouse sobre botão | Efeito hover visível |
| 2 | Clicar em botão | Efeito de clique (transform) |
| 3 | Cadastrar empréstimo | Alerta de sucesso aparece |
| 4 | Trocar de aba | Animação de fade-in |
| 5 | Passar mouse sobre card | Card move ligeiramente |

**Critério de Aceitação:** Aplicação fornece feedback visual constante.

**Result:** Pass

---

### **CT-026: Simplicidade da Interface**
**Requisito:** RNF-006  
**Prioridade:** Baixa  
**Pré-condição:** Primeira vez usando aplicação

| Passo | Ação | Resultado Esperado |
|-------|------|-------------------|
| 1 | Abrir aplicação sem instruções | Interface autoexplicativa |
| 2 | Tentar cadastrar empréstimo | Processo intuitivo |
| 3 | Localizar empréstimo ativo | Facilmente encontrado |
| 4 | Marcar como devolvido | Ação óbvia |

**Critério de Aceitação:** Usuário sem treinamento consegue usar.

**Result:** Pass

---

### **CT-027: Funcionamento Offline**
**Requisito:** RNF-002  
**Prioridade:** Alta  
**Pré-condição:** Aplicação já foi aberta uma vez

| Passo | Ação | Resultado Esperado |
|-------|------|-------------------|
| 1 | Desconectar internet | WiFi/cabo desconectado |
| 2 | Abrir arquivo HTML localmente | Aplicação carrega |
| 3 | Cadastrar empréstimo | Funciona normalmente |
| 4 | Marcar como devolvido | Funciona |
| 5 | Buscar empréstimos | Funciona |

**Critério de Aceitação:** 100% funcional sem internet.

**Result:** Pass

---

### **CT-028: Validação de Valor Negativo**
**Requisito:** RN-001  
**Prioridade:** Baixa  
**Pré-condição:** Formulário de cadastro aberto

| Passo | Ação | Resultado Esperado |
|-------|------|-------------------|
| 1 | Preencher campos obrigatórios | OK |
| 2 | Tentar inserir valor negativo "-50" | HTML5 impede (input type="number" min="0") |
| 3 | Verificar campo | Valor não aceito |

**Critério de Aceitação:** Sistema não permite valores negativos.

**Result:** Pass

---

### **CT-029: Teste de Limite - Texto Muito Longo**
**Requisito:** Geral  
**Prioridade:** Baixa  
**Pré-condição:** Formulário de cadastro aberto

| Passo | Ação | Resultado Esperado |
|-------|------|-------------------|
| 1 | Preencher "Nome do Item" com 500 caracteres | Texto aceito |
| 2 | Cadastrar empréstimo | Sucesso |
| 3 | Verificar card | Texto exibido sem quebrar layout |
| 4 | Preencher "Observações" com 1000 caracteres | Aceito |
| 5 | Verificar card | Observações visíveis sem quebrar |

**Critério de Aceitação:** Sistema lida com textos longos sem quebrar.

**Result:** Pass

---

### **CT-030: Teste de Caracteres Especiais**
**Requisito:** Geral  
**Prioridade:** Baixa  
**Pré-condição:** Formulário de cadastro aberto

| Passo | Ação | Resultado Esperado |
|-------|------|-------------------|
| 1 | Preencher "Nome" com "Livro <teste> & 'aspas'" | Aceito |
| 2 | Cadastrar | Sucesso |
| 3 | Verificar card | Caracteres exibidos corretamente (sem XSS) |

**Critério de Aceitação:** Caracteres especiais não causam problemas.

**Result:** Pass

---

## 5. DADOS DE TESTE

### 5.1 Massa de Dados para Testes

```
EMPRÉSTIMO 1:
- Item: Livro de Cálculo 2
- Pessoa: Maria Silva
- Data: [5 dias atrás]
- Categoria: Livro
- Valor: 150.00
- Observações: Capa azul, preciso para prova

EMPRÉSTIMO 2:
- Item: Carregador de Notebook Dell
- Pessoa: João Santos
- Data: [10 dias atrás]
- Categoria: Eletrônico
- Valor: 80.00
- Observações: (vazio)

EMPRÉSTIMO 3:
- Item: R$ 50,00
- Pessoa: Ana Costa
- Data: [2 dias atrás]
- Categoria: Dinheiro
- Valor: 50.00
- Observações: Para emergência médica

EMPRÉSTIMO 4 (para histórico):
- Item: Chave de Fenda
- Pessoa: Carlos Oliveira
- Data: [15 dias atrás]
- Categoria: Ferramenta
- Valor: 0
- Status: Devolvido (há 5 dias)
```

---

## 6. CRITÉRIOS DE ACEITAÇÃO GERAL

### ✅ APROVADO se:
- 100% dos casos de teste ALTA prioridade passarem
- 90%+ dos casos de teste MÉDIA prioridade passarem
- 80%+ dos casos de teste BAIXA prioridade passarem
- Nenhum bug crítico encontrado

### ❌ REPROVADO se:
- Qualquer RF não funcionar
- Dados forem perdidos
- Aplicação travar/crashar
- Incompatibilidade com navegadores principais

---

## 7. CRONOGRAMA DE EXECUÇÃO

| Fase | Duração Estimada |
|------|------------------|
| Preparação do ambiente | 10 minutos |
| Execução de CT-001 a CT-015 (Funcionais) | 45 minutos |
| Execução de CT-016 a CT-021 (Não-Funcionais) | 30 minutos |
| Execução de CT-022 a CT-030 (Extras) | 25 minutos |
| Documentação de resultados | 20 minutos |
| **TOTAL** | **~2 horas** |

---

## 8. ENTREGÁVEIS

Após execução, produzir:
1. ✅ Planilha/Documento com status de cada caso de teste
2. ✅ Screenshots de evidências
3. ✅ Lista de bugs encontrados (se houver)
4. ✅ Relatório de Testes completo

---

## 9. RESPONSABILIDADES

| Papel | Responsável |
|-------|-------------|
| Planejador de Testes | [Seu Nome] |
| Executor de Testes | [Seu Nome] |
| Revisor de Resultados | [Professor/Equipe] |

---

## 10. OBSERVAÇÕES FINAIS

- Testes devem ser executados **sequencialmente**
- Limpar LocalStorage entre baterias de teste para garantir ambiente limpo
- Anotar **qualquer comportamento inesperado**, mesmo que não seja bug
- Tirar screenshots de **todos os bugs** encontrados
- Se houver dúvidas durante execução, documentar para discussão

---

**FIM DO PLANO DE TESTES**

---

## PRÓXIMO PASSO: EXECUÇÃO

Agora você deve:
1. Abrir o arquivo HTML no navegador
2. Executar cada caso de teste acima
3. Anotar os resultados (PASSOU / FALHOU / BLOQUEADO)
4. Documentar bugs encontrados
5. Gerar o Relatório de Resultados dos Testes