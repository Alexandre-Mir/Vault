# Blocos de Implementação - Roadmap COC 7e Character Sheet

## Bloco 1: Setup Inicial
**Status:** Concluído
**Descrição:** Configuração inicial do projeto

**Tarefas concluídas:**
- [x] Configurar Next.js com TypeScript
- [x] Configurar Tailwind CSS
- [x] Configurar Zustand para gerenciamento de estado
- [x] Configurar estrutura básica de pastas

**Dependências:** Nenhuma
**Pontos:** 3

---

## Bloco 2: [[Core Types]]
**Status:** Pendente
**Descrição:** Definição completa dos tipos TypeScript para COC 7e

**Sub-tarefas:**
- [ ] Definir interface `Investigator` como união discriminada por ruleset
- [ ] Criar tipos para características primárias com modificadores
- [ ] Implementar sistema de perícias com especializações
- [ ] Definir tipos para armas e combate
- [ ] Criar estrutura de inventário com encumbrance
- [ ] Implementar tipos para backstory e metadados
- [ ] Adicionar tipos para condições e estados
- [ ] Criar sistema de validação e integridade
- [ ] Implementar tipos para histórico e auditoria
- [ ] Adicionar suporte a homebrew e customização

**Dependências:** Bloco 1
**Pontos:** 8
**Critério de Aceitação:** Tipos compilam sem erros e cobrem 100% das regras do livro

---

## Bloco 3: [[Regras]]
**Status:** Pendente
**Descrição:** Implementação das regras de cálculo do COC 7e

**Sub-tarefas:**
- [ ] Implementar funções para cálculo de atributos derivados (HP, MP, SAN, Luck)
- [ ] Criar sistema de cálculo de Damage Bonus e Build
- [ ] Implementar regras de Dodge e Movement
- [ ] Criar funções para testes de perícia (roll d100)
- [ ] Implementar sistema de dano para armas
- [ ] Criar funções para condições (ferimentos, envenenamento, insanidade)
- [ ] Implementar regras de evolução de perícias
- [ ] Criar sistema de envelhecimento
- [ ] Implementar cálculos de encumbrance
- [ ] Adicionar suporte a regras Pulp Cthulhu

**Dependências:** Bloco 2
**Pontos:** 6
**Critério de Aceitação:** Todas as funções são puras e testáveis

---

## Bloco 4: Testes Unitários
**Status:** Pendente
**Descrição:** Testes para garantir a corretude das implementações

**Tarefas:**
- [ ] Configurar Vitest ou Jest
- [ ] Criar testes para todos os tipos Core
- [ ] Implementar testes para todas as funções de regras
- [ ] Adicionar testes de edge cases
- [ ] Criar fixtures para testes
- [ ] Implementar testes de performance

**Dependências:** Bloco 2, Bloco 3
**Pontos:** 5
**Critério de Aceitação:** 90%+ de cobertura de código

---

## Bloco 5: Banco de Dados (Dexie.js)
**Status:** Pendente
**Descrição:** Configuração do banco de dados local IndexedDB

**Tarefas:**
- [ ] Definir schema do Dexie para IInvestigator
- [ ] Implementar migrations entre versões de schema
- [ ] Criar repositório para operações CRUD
- [ ] Adicionar indexes para queries frequentes
- [ ] Implementar backup/restore automático
- [ ] Adicionar validação de dados na camada do DB

**Dependências:** Bloco 2
**Pontos:** 4
**Critério de Aceitação:** Schema suporta todas as propriedades do IInvestigator

---

## Bloco 6: Store (Zustand)
**Status:** Pendente
**Descrição:** Gerenciamento de estado global da aplicação

**Tarefas:**
- [ ] Criar store principal para o personagem atual
- [ ] Implementar actions para todas as operações de modificação
- [ ] Adicionar middleware para persistência automática
- [ ] Criar sistema de undo/redo
- [ ] Implementar seletores otimizados com memoization
- [ ] Adicionar validação de estado antes de salvar

**Dependências:** Bloco 2, Bloco 5
**Pontos:** 4
**Critério de Aceitação:** Store sincroniza corretamente com IndexedDB

---

## Bloco 7: Validação (Zod)
**Status:** Pendente
**Descrição:** Schemas de validação para todos os tipos

**Tarefas:**
- [ ] Criar schemas Zod que espelham os tipos TypeScript
- [ ] Implementar validação de regras de negócio nos schemas
- [ ] Adicionar transformações para valores padrão
- [ ] Criar schemas para import/export
- [ ] Implementar validação em runtime na store
- [ ] Adicionar mensagens de erro amigáveis

**Dependências:** Bloco 2
**Pontos:** 3
**Critério de Aceitação:** Schemas validam 100% das regras do livro

---

## Bloco 8: [[Criador de Personagens (Wizard)]]
**Status:** Pendente
**Descrição:** Fluxo guiado de criação de personagens

**Sub-tarefas:**
- [ ] **Passo 1: Atributos**
  - [ ] Componente para rolagem/compra de pontos
  - [ ] Visualização dos valores derivados em tempo real
  - [ ] Validação de limites mínimos/máximos
- [ ] **Passo 2: Ocupação**
  - [ ] Lista de ocupações com filtros
  - [ ] Detalhes da ocupação selecionada
  - [ ] Alocação automática de perícias de ocupação
  - [ ] Seleção de Credit Rating
- [ ] **Passo 3: Perícias**
  - [ ] Alocação de pontos de ocupação
  - [ ] Alocação de pontos de interesse
  - [ ] Visualização de custos e totais
  - [ ] Validação de limites de perícia
- [ ] **Passo 4: Detalhes**
  - [ ] Formulário de informações pessoais
  - [ ] Backstory (ideologia, pessoas importantes, etc.)
  - [ ] Seleção de imagem/retrato
- [ ] **Componentes compartilhados**
  - [ ] Stepper com progresso
  - [ ] Botões de navegação (voltar/próximo/salvar)
  - [ ] Modal de confirmação
  - [ ] Persistência automática entre passos

**Dependências:** Bloco 2, Bloco 3, Bloco 6, Bloco 7
**Pontos:** 7
**Critério de Aceitação:** Fluxo completo cria personagem válido

---

## Bloco 9: [[Ficha Interativa (Mobile-First)]]
**Status:** Pendente
**Descrição:** Interface principal de visualização e edição da ficha

**Sub-tarefas:**
- [ ] **App Shell**
  - [ ] Bottom Navigation com abas principais
  - [ ] Header com nome do personagem e ações
  - [ ] Sistema de temas (claro/escuro)
  - [ ] Menu de configurações
- [ ] **Aba: Status**
  - [ ] Cards para HP, MP, SAN, Luck
  - [ ] Barra de progresso visual para cada recurso
  - [ ] Lista de características primárias com modificadores
  - [ ] Funcionalidade click-to-roll para testes de atributo
  - [ ] Quick actions (curar, recuperar MP, etc.)
- [ ] **Aba: Perícias**
  - [ ] Lista filtrável por categoria (combate/social/acadêmica)
  - [ ] Barra de busca por nome
  - [ ] Indicador visual de evolução (checkbox)
  - [ ] Edição inline de valores
  - [ ] Botão de rolagem para cada perícia
  - [ ] Visualização de especializações
- [ ] **Aba: Combate**
  - [ ] Lista de armas equipadas
  - [ ] Dano e características de cada arma
  - [ ] Gerenciamento de munição
  - [ ] Ataques por rodada
  - [ ] Manobras de combate padrão
- [ ] **Drawers de Edição**
  - [ ] Sheet para edição detalhada de atributos
  - [ ] Sheet para edição detalhada de perícias
  - [ ] Sheet para edição de armas
  - [ ] Sheet para condições/efeitos
  - [ ] Sistema de notas por campo

**Dependências:** Bloco 8
**Pontos:** 10
**Critério de Aceitação:** Interface totalmente funcional em mobile

---

## Bloco 10: Inventário e Peso
**Status:** Pendente
**Descrição:** Sistema de inventário com cálculo automático de peso

**Tarefas:**
- [ ] Componente de lista de itens
- [ ] Formulário de adição/edição de itens
- [ ] Cálculo automático de encumbrance
- [ ] Indicador visual de carga (leve/médio/pesado)
- [ ] Efeitos de sobrecarga no MOV
- [ ] Sistema de containers (mochilas, bolsos)
- [ ] Itens equipados vs. na mochila

**Dependências:** Bloco 2, Bloco 3, Bloco 9
**Pontos:** 4
**Critério de Aceitação:** Peso calculado corretamente e afeta atributos

---

## Bloco 11: Dice Roller
**Status:** Pendente
**Descrição:** Sistema de rolagem de dados com feedback visual

**Tarefas:**
- [ ] Modal de resultado de rolagem
- [ ] Animações de dados rolando
- [ ] Cálculo automático de sucesso/fracasso
- [ ] Diferenciação por nível de sucesso (regular/hard/extreme)
- [ ] Histórico de rolagens
- [ ] Modificadores aplicáveis antes da rolagem
- [ ] Rolagem em lote para múltiplos testes

**Dependências:** Bloco 3, Bloco 9
**Pontos:** 3
**Critério de Aceitação:** Sistema de rolagem preciso e visualmente atrativo

---

## Bloco 12: Evolução de Perícias
**Status:** Pendente
**Descrição:** Sistema completo de evolução de perícias

**Tarefas:**
- [ ] Marcação de perícias para evolução (checkbox)
- [ ] Fase de desenvolvimento entre sessões
- [ ] Teste de melhoria (rolagem d100)
- [ ] Aumento automático de valor em caso de sucesso
- [ ] Registro de histórico de melhorias
- [ ] Limites de aumento por período

**Dependências:** Bloco 3, Bloco 9
**Pontos:** 3
**Critério de Aceitação:** Ciclo completo de evolução implementado

---

## Bloco 13: Import/Export JSON
**Status:** Pendente
**Descrição:** Funcionalidade de backup e compartilhamento

**Tarefas:**
- [ ] Botão de export para JSON
- [ ] Botão de import de JSON
- [ ] Validação de schema na importação
- [ ] Migração de versões diferentes
- [ ] Opção para incluir/excluir imagens
- [ ] Compressão de dados
- [ ] Geração de arquivo com timestamp

**Dependências:** Bloco 2, Bloco 7
**Pontos:** 3
**Critério de Aceitação:** Export/import roundtrip sem perda de dados

---

## Bloco 14: Configuração PWA
**Status:** Pendente
**Descrição:** Transformar aplicação em Progressive Web App

**Tarefas:**
- [ ] Configurar manifest.json
- [ ] Implementar Service Worker para cache
- [ ] Adicionar splash screens
- [ ] Configurar ícones para diferentes dispositivos
- [ ] Implementar atualizações em background
- [ ] Adicionar funcionalidade offline

**Dependências:** Bloco 9
**Pontos:** 3
**Critério de Aceitação:** Aplicação instala como PWA e funciona offline

---

## Bloco 15: Deploy na Vercel
**Status:** Pendente
**Descrição:** Implantação da aplicação em produção

**Tarefas:**
- [ ] Configurar ambiente de produção
- [ ] Setup de variáveis de ambiente
- [ ] Configurar domínio customizado
- [ ] Implementar analytics
- [ ] Setup de backup automático
- [ ] Monitoramento de erros

**Dependências:** Todos os blocos anteriores
**Pontos:** 2
**Critério de Aceitação:** Aplicação online e funcionando

---

## Bloco 16: Documentação
**Status:** Pendente
**Descrição:** Documentação do projeto

**Tarefas:**
- [ ] README com instruções de setup
- [ ] Documentação de arquitetura
- [ ] Guia de contribuição
- [ ] Documentação de APIs internas
- [ ] Exemplos de uso
- [ ] FAQ

**Dependências:** Todos os blocos anteriores
**Pontos:** 2
**Critério de Aceitação:** Documentação completa e atualizada

---

## Resumo de Dependências

```
Core Types (2) → Regras (3) → Testes Unitários (4)
Core Types (2) → Banco de Dados (5) → Store (6)
Core Types (2) → Validação (7)
Store (6) + Validação (7) + Regras (3) → Wizard (8)
Wizard (8) → Ficha Interativa (9)
Ficha Interativa (9) → Inventário (10) + Dice Roller (11) + Evolução (12)
Todos → Deploy (15) + Documentação (16)
```

**Total de Pontos Estimados:** 74 pontos  
**Ordem de Implementação Recomendada:** 
1. Core Types (2)
2. Regras (3) e Validação (7) em paralelo
3. Banco de Dados (5) → Store (6)
4. Testes Unitários (4)
5. Wizard (8)
6. Ficha Interativa (9)
7. Inventário (10), Dice Roller (11), Evolução (12)
8. Import/Export (13) e PWA (14)
9. Deploy (15) e Documentação (16)

**Blocos Críticos:** Core Types, Wizard, Ficha Interativa  
**Marcos Principais:**
- M1: Tipos definidos e testados (Bloco 2-4)
- M2: Criador de personagens funcional (Bloco 8)
- M3: Ficha interativa básica (Bloco 9)
- M4: MVP completo (Bloco 9 + 10 + 11)
- M5: Produção (Bloco 15)