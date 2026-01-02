Definir as interfaces TS definitivas para CoC 7e

# Blocos de Implementação - Tipagem COC 7e

## Bloco 1: Identificadores e Meta
**Descrição:** Estrutura básica de identificação e metadados da ficha

**Tarefas:**
- [x] Definir interface `IInvestigatorMeta` com `id` (uuid), `createdAt`, `updatedAt`
- [x] Adicionar `schemaVersion` para controle de migrações
- [x] Implementar `ownerId` e `playerName` 
- [x] Criar enum `Provenance` (imported, created, duplicated)
- [x] Adicionar campo `ruleset` obrigatório (classic, pulp)
- [x] Incluir `agingApplied: IAgingApplication` para rastreamento de envelhecimento
- [x] Criar `occupationSnapshot: IOccupationSnapshot` imutável

**Dependências:** Nenhuma
**Estimativa:** 2 pontos
**Critério de Aceitação:** Interface compila sem erros, suporta todos os valores de ruleset

---
ANTES DE PROSSEGUIR PARA O PRÓXIMO BLOCO, DEVE SER FEITA UMA REVISÃO DO BLOCO ANTERIOR
## Bloco 2: Características Primárias
**Descrição:** Atributos principais do personagem com modificadores e rastreamento

**Tarefas:**
- [x] Criar enum `PrimaryCharacteristic` (STR, DEX, CON, APP, POW, SIZ, INT, EDU)
- [x] Definir `PrimaryCharacteristic` com `baseValue`, `temporaryModifier`, `permanentModifier`
- [x] Implementar `CharacteristicModification` com `source`, `value`, `appliedAt`, `reason`
- [x] Criar `lastModifiedCharacteristic` para auditoria
- [x] Adicionar suporte para `baseFormula` em características derivadas
- [ ] Implementar validação de domínio (valores entre 0-100)

**Dependências:** Bloco 1
**Estimativa:** 3 pontos
**Critério de Aceitação:** Modificadores podem ser rastreados até sua origem

---

## Bloco 3: Estatísticas Derivadas
**Descrição:** Valores calculados a partir das características primárias

**Tarefas:**
- [ ] Criar `IDerivedStat` base com `current`, `max`, `calculatedAt`
- [ ] Implementar `IHitPoints` com `temp`, `isMajorWound`, `majorWoundDate`, `permanentReduction`
- [ ] Definir `ISanity` com `dailyLoss`, `permanentLoss`, `isIndefinitelyInsane`, `temporaryLossEvents[]`
- [ ] Criar `ILuck` com métodos de recuperação/uso
- [ ] Implementar `IDerivedCombatStats` (Dodge, Damage Bonus, Build, MOV)
- [ ] Adicionar `derivedFrom: string` (enum ou fórmula parseável)

**Dependências:** Bloco 2
**Estimativa:** 4 pontos
**Critério de Aceitação:** Campos derivados têm referência clara à fórmula de cálculo

---

## Bloco 4: Perícias (ISkill)
**Descrição:** Sistema completo de perícias com especializações e evolução

**Tarefas:**
- [ ] Definir `ISkill` com `name`, `subName`, `category`, `baseValue`, `value`
- [ ] Implementar `occupationPoints`, `interestPoints`, `trainingSource`
- [ ] Criar sistema de evolução: `isChecked`, `checkedAt`, `successCount`, `improvementHistory[]`
- [ ] Adicionar `baseFormula` para perícias dinâmicas (ex: `DEX_HALF`)
- [ ] Implementar `specializations[]` para múltiplas especializações
- [ ] Criar `rollHistory[]` para auditoria de testes
- [ ] Adicionar validação de domínio (0-100)

**Dependências:** Bloco 2
**Estimativa:** 5 pontos
**Critério de Aceitação:** Perícias dinâmicas recalculam automaticamente ao mudar atributos

---

## Bloco 5: Combate e Armas (IWeapon)
**Descrição:** Sistema de armas e combate com todas as características

**Tarefas:**
- [ ] Definir `IWeapon` com `name`, `skillUsed` (referência a ISkill)
- [ ] Implementar `damage` como estrutura separada (dice, bonus, type)
- [ ] Criar `IAmmo` com `current`, `capacity`, `malfunctionRange`
- [ ] Adicionar `traits[]` (automatic, twoHanded, etc.)
- [ ] Implementar `condition`/`durability`, `isJammed`
- [ ] Criar `wieldSlot` e `equipped` flag
- [ ] Adicionar `damageType` e `AP` para regras avançadas

**Dependências:** Bloco 4
**Estimativa:** 3 pontos
**Critério de Aceitação:** Armas podem ser vinculadas a perícias específicas

---

## Bloco 6: Inventário e Itens
**Descrição:** Sistema de inventário com encumbrance e containers

**Tarefas:**
- [ ] Definir `IGear` com `id`, `name`, `quantity`, `weight`
- [ ] Implementar `isEquipped`, `slot`, `container`/`location`
- [ ] Criar cálculo de `Encumbrance` baseado em `carryingWeight` e `Build`/`SIZ`
- [ ] Adicionar propriedades dinâmicas (bateria com carga, etc.)
- [ ] Implementar `IInventoryContainer` para organização hierárquica
- [ ] Criar validação de peso máximo

**Dependências:** Bloco 2, Bloco 3
**Estimativa:** 4 pontos
**Critério de Aceitação:** Sistema calcula encumbrance automaticamente

---

## Bloco 7: Moeda e Crédito
**Descrição:** Sistema econômico e reputação do investigador

**Tarefas:**
- [ ] Definir `ICurrency` com `type`, `amount`, `exchangeRate`
- [ ] Implementar `cash` e `currencies[]` para múltiplas moedas
- [ ] Criar `ICreditRating` com `value`, `reputationNotes`
- [ ] Adicionar validação baseada no `occupationSnapshot`
- [ ] Implementar conversão automática entre moedas
- [ ] Criar histórico de transações financeiras

**Dependências:** Bloco 1
**Estimativa:** 2 pontos
**Critério de Aceitação:** Credit Rating valida contra limites da ocupação

---

## Bloco 8: Backstory e Metadados
**Descrição:** Informações pessoais e história do personagem

**Tarefas:**
- [ ] Definir `IPersonalInfo` com `name`, `age`, `occupation`, `residence`
- [ ] Implementar `IBackstory` com `ideology`, `importantPeople[]`, `places[]`
- [ ] Adicionar `valuedPossessions[]`, `traits[]`
- [ ] Criar `IPortrait` com `url`, `privacyFlag`, `metadata`
- [ ] Implementar `languageProficiencies[]`
- [ ] Adicionar campos para `personalDescription`, `appearance`

**Dependências:** Bloco 1
**Estimativa:** 3 pontos
**Critério de Aceitação:** Todas as seções do backstory do livro estão representadas

---

## Bloco 9: Flags de Estado
**Descrição:** Condições temporárias e estado do personagem

**Tarefas:**
- [ ] Definir `ICharacterState` com `isDead`, `isUnconscious`, `isStabilized`
- [ ] Criar enum `ConditionType` (bleeding, stunned, poisoned, etc.)
- [ ] Implementar `ICondition` com `expiresAt`, `stacks`, `severity`
- [ ] Adicionar `restrictions[]` (unableToAct, restrained, etc.)
- [ ] Criar sistema de expiração automática de condições
- [ ] Implementar `isProne` e efeitos relacionados

**Dependências:** Bloco 3
**Estimativa:** 3 pontos
**Critério de Aceitação:** Condições afetam automaticamente os testes apropriados

---

## Bloco 10: Validação e Integridade
**Descrição:** Sistema de validação da ficha

**Tarefas:**
- [ ] Definir `IValidationResult` com `isValid`, `errors[]`, `warnings[]`
- [ ] Implementar validação de campos obrigatórios
- [ ] Criar validação de regras específicas (SAN ≤ 99, etc.)
- [ ] Adicionar validação contra `occupationSnapshot`
- [ ] Implementar `validateInvestigator()` função principal
- [ ] Criar sistema de "fixes" automáticos para problemas comuns

**Dependências:** Todos os blocos anteriores
**Estimativa:** 4 pontos
**Critério de Aceitação:** Detecta todas as inconsistências de regras listadas

---

## Bloco 11: Histórico e Auditoria
**Descrição:** Sistema completo de auditoria e histórico

**Tarefas:**
- [ ] Definir `IChangeLog` com `field`, `oldValue`, `newValue`, `timestamp`, `source`
- [ ] Implementar `rollHistory[]` para todos os testes
- [ ] Criar `IAuditTrail` para modificações importantes
- [ ] Adicionar `snapshots[]` para versionamento da ficha
- [ ] Implementar função `getHistory(field)` para auditoria específica
- [ ] Criar sistema de replay para sequências de testes

**Dependências:** Bloco 1
**Estimativa:** 4 pontos
**Critério de Aceitação:** Todas as modificações podem ser rastreadas

---

## Bloco 12: Customização e Homebrew
**Descrição:** Suporte a regras da casa e personalização

**Tarefas:**
- [ ] Definir `IHouseRule` com `name`, `description`, `effect`
- [ ] Implementar `customSkills[]` com definição completa
- [ ] Criar `ICustomTrait` para características personalizadas
- [ ] Adicionar `variantRules` para regras opcionais do livro
- [ ] Implementar sistema de ativação/desativação de homebrew
- [ ] Criar validação para homebrew

**Dependências:** Bloco 4
**Estimativa:** 3 pontos
**Critério de Aceitação:** Homebrew não quebra validação básica

---

## Bloco 13: Salvamento e Serialização
**Descrição:** Sistema de exportação/importação

**Tarefas:**
- [ ] Definir `IExportMetadata` com `hash`, `exportedAt`, `version`
- [ ] Implementar `exportInvestigator(options)` com opções de privacidade
- [ ] Criar `importInvestigator(data, validationStrictness)`
- [ ] Adicionar suporte a imagens (embed vs reference)
- [ ] Implementar migração entre versões de schema
- [ ] Criar formato de snapshot para diffs

**Dependências:** Bloco 1, Bloco 10
**Estimativa:** 5 pontos
**Critério de Aceitação:** Export/import roundtrip sem perda de dados

---

## Bloco 14: Permissões e Compartilhamento
**Descrição:** Controle de acesso e colaboração

**Tarefas:**
- [ ] Definir `ISharingPermission` (read, write, admin)
- [ ] Implementar `sharedWith[]` com `userId`, `permission`, `sharedAt`
- [ ] Adicionar `isPublic` flag e controles de visibilidade
- [ ] Criar sistema de convites e solicitações de acesso
- [ ] Implementar validação de permissões por operação
- [ ] Adicionar histórico de compartilhamento

**Dependências:** Bloco 1
**Estimativa:** 3 pontos
**Critério de Aceitação:** Permissões são verificadas em todas as operações

---

## Bloco 15: Localização e Internacionalização
**Descrição:** Suporte a múltiplos idiomas

**Tarefas:**
- [ ] Definir `ILocalizedString` com `[locale]: string`
- [ ] Implementar `displayNames` para skills, traits, etc.
- [ ] Criar `localeNames` no investigador para nomes alternativos
- [ ] Adicionar suporte a `languageProficiencies` com níveis
- [ ] Implementar sistema de fallback de locale
- [ ] Criar dicionário de termos do jogo por idioma

**Dependências:** Bloco 4, Bloco 8
**Estimativa:** 3 pontos
**Critério de Aceitação:** Interface pode ser totalmente traduzida

---

## Bloco 16: Testes e Fixtures
**Descrição:** Dados de teste e casos extremos

**Tarefas:**
- [ ] Criar fixtures para todos os rulesets (classic, pulp)
- [ ] Implementar personagens com valores extremos (0, 1, 100+)
- [ ] Adicionar fixtures com ferimentos graves ativos
- [ ] Criar personagens com todas as condições possíveis
- [ ] Implementar fixtures para testes de migração
- [ ] Adicionar personagens com homebrew complexo

**Dependências:** Todos os blocos anteriores
**Estimativa:** 4 pontos
**Critério de Aceitação:** Cobre 100% dos casos de borda listados

---

## Bloco 17: Regras Críticas - Ferimento e Cura
**Descrição:** Implementação detalhada das regras de ferimentos

**Tarefas:**
- [ ] Implementar `isMajorWound` com todas as consequências
- [ ] Criar `majorWoundDate` e `preventsNaturalHealing`
- [ ] Adicionar `permanentHPReduction` tracker
- [ ] Implementar regras de cicatrização natural
- [ ] Criar sistema de primeiros socorros e tratamento médico
- [ ] Adicionar efeitos de ferimentos por localização (opcional)

**Dependências:** Bloco 3
**Estimativa:** 3 pontos
**Critério de Aceitação:** Ferimentos graves impedem cura natural corretamente

---

## Bloco 18: Regras Críticas - Sanidade
**Descrição:** Sistema completo de sanidade com todos os efeitos

**Tarefas:**
- [ ] Implementar `temporarySanLossEvents[]` com rastreamento completo
- [ ] Criar sistema de `dailyLoss` acumulável
- [ ] Adicionar trigger automático para `isIndefinitelyInsane`
- [ ] Implementar fases de insanidade temporária
- [ ] Criar efeitos de sanidade 0 e sanidade máxima
- [ ] Adicionar terapias e recuperação de sanidade

**Dependências:** Bloco 3
**Estimativa:** 4 pontos
**Critério de Aceitação:** Insanidade indefinida é acionada nas condições corretas

---

## Bloco 19: Regras Críticas - Perícias Baseadas em Atributo
**Descrição:** Sistema robusto para perícias derivadas

**Tarefas:**
- [ ] Definir enum `BaseFormula` com todas as fórmulas do livro
- [ ] Implementar `recalculateDerivedSkills()` função
- [ ] Criar cache de valores derivados com invalidação
- [ ] Adicionar `derivedFrom` em todas as perícias derivadas
- [ ] Implementar sistema de notificação de mudanças
- [ ] Criar testes para todas as fórmulas de atributo

**Dependências:** Bloco 2, Bloco 4
**Estimativa:** 3 pontos
**Critério de Aceitação:** Mudança em atributo atualiza todas as perícias derivadas

---

## Bloco 20: Regras Críticas - Evolução de Perícias
**Descrição:** Sistema de XP e melhoria de perícias

**Tarefas:**
- [ ] Implementar `xpSpent` tracker por perícia
- [ ] Criar `improvementHistory[]` com detalhes completos
- [ ] Adicionar sistema de `checkedAt` e resgate de testes
- [ ] Implementar regras de melhoria por uso
- [ ] Criar sistema de treinamento e estudo
- [ ] Adicionar limites de melhoria por período

**Dependências:** Bloco 4
**Estimativa:** 3 pontos
**Critério de Aceitação:** Perícias podem ser marcadas para evolução corretamente

---

## Bloco 21: Regras de Arredondamento
**Descrição:** Sistema consistente de arredondamento

**Tarefas:**
- [ ] Definir `RoundingRule` (floor, round, ceil)
- [ ] Implementar `applyRounding(value, rule)` função utilitária
- [ ] Criar configuração por ruleset (classic vs pulp)
- [ ] Adicionar `roundingRules` no investigador
- [ ] Implementar testes para todas as operações de arredondamento
- [ ] Criar sistema de override por house rule

**Dependências:** Bloco 3
**Estimativa:** 2 pontos
**Critério de Aceitação:** Cálculos são consistentes em todas as plataformas

---

## Bloco 22: Sistema de Unidades
**Descrição:** Suporte a múltiplos sistemas de medida

**Tarefas:**
- [ ] Definir `UnitSystem` (metric, imperial)
- [ ] Implementar `IWeight` com valor e unidade
- [ ] Criar `IDistance` com valor e unidade
- [ ] Adicionar conversão automática entre sistemas
- [ ] Implementar preferência por investigador
- [ ] Criar formatação localizada de unidades

**Dependências:** Bloco 6
**Estimativa:** 3 pontos
**Critério de Aceitação:** Peso e distância podem ser exibidos em qualquer sistema

---

## Bloco 23: Arquitetura de Tipos
**Descrição:** Separação entre dados e regras

**Tarefas:**
- [ ] Definir `src/types/` para todas as interfaces
- [ ] Criar `src/lib/coc-rules.ts` para funções puras
- [ ] Implementar `src/lib/calculations.ts` para fórmulas
- [ ] Adicionar `src/lib/validations.ts` para regras de negócio
- [ ] Criar sistema de injecão de dependência para regras
- [ ] Implementar testes unitários para todas as funções

**Dependências:** Todos os blocos de tipos
**Estimativa:** 5 pontos
**Critério de Aceitação:** Nenhuma regra de negócio nas interfaces

---

## Bloco 24: Compatibilidade e Migração
**Descrição:** Sistema robusto de migração entre versões

**Tarefas:**
- [ ] Implementar `schemaVersion` com semver
- [ ] Criar `migrationNotes[]` para cada versão
- [ ] Adicionar `IMigrationStep` para transformações
- [ ] Implementar `migrateInvestigator(data, targetVersion)`
- [ ] Criar testes para todas as migrações possíveis
- [ ] Adicionar rollback seguro

**Dependências:** Bloco 1, Bloco 13
**Estimativa:** 4 pontos
**Critério de Aceitação:** Fichas antigas podem ser migradas sem perda

---

## Bloco 25: Performance e Cache
**Descrição:** Otimização de cálculos pesados

**Tarefas:**
- [ ] Implementar `cachedDerivedValues` com timestamp
- [ ] Criar sistema de invalidação de cache por evento
- [ ] Adicionar `shouldRecalculate()` lógica
- [ ] Implementar memoization para funções caras
- [ ] Criar cache por sessão para valores estáticos
- [ ] Adicionar métricas de performance

**Dependências:** Bloco 3, Bloco 19
**Estimativa:** 3 pontos
**Critério de Aceitação:** Cálculos não são repetidos desnecessariamente

---

## Bloco 26: Segurança e Privacidade
**Descrição:** Proteção de dados sensíveis

**Tarefas:**
- [ ] Implementar `privacy` flags em todos os campos sensíveis
- [ ] Criar `exportOptions` com `includeSensitiveData`
- [ ] Adicionar criptografia para dados pessoais
- [ ] Implementar sanitização para compartilhamento público
- [ ] Criar sistema de consentimento para dados
- [ ] Adicionar logs de acesso a dados sensíveis

**Dependências:** Bloco 8, Bloco 13
**Estimativa:** 4 pontos
**Critério de Aceitação:** Dados pessoais não vazam em exports públicos

---

## Bloco 27: Envelhecimento Canônico
**Descrição:** Implementação das regras de envelhecimento do livro

**Tarefas:**
- [ ] Definir `IAgingApplication` imutável
- [ ] Implementar `applyAging(investigator, age)` função
- [ ] Criar validação de aplicação única
- [ ] Adicionar `agingEffects[]` para rastreamento
- [ ] Implementar regras específicas por década
- [ ] Criar sistema de reversão (se permitido por house rule)

**Dependências:** Bloco 2
**Estimativa:** 3 pontos
**Critério de Aceitação:** Envelhecimento aplica exatamente uma vez

---

## Bloco 28: Ocupação como Snapshot
**Descrição:** Congelamento das regras de criação

**Tarefas:**
- [ ] Definir `IOccupationSnapshot` imutável
- [ ] Implementar `eligibleSkills[]` com pontos alocados
- [ ] Adicionar `creditRatingRange` (min, max)
- [ ] Criar `creationDate` e `ruleSource`
- [ ] Implementar validação contra snapshot
- [ ] Adicionar migração para fichas antigas

**Dependências:** Bloco 1, Bloco 4
**Estimativa:** 3 pontos
**Critério de Aceitação:** Snapshot persiste após mudanças no catálogo

---

## Bloco 29: Ruleset como Discriminador
**Descrição:** Sistema de uniões discriminadas por ruleset

**Tarefas:**
- [ ] Definir `IInvestigator` como união discriminada
- [ ] Criar `IClassicInvestigator` com campos específicos
- [ ] Implementar `IPulpInvestigator` com talentos e arquétipos
- [ ] Adicionar `IDeltaGreenInvestigator` se aplicável
- [ ] Criar type guards para cada ruleset
- [ ] Implementar funções específicas por ruleset

**Dependências:** Todos os blocos anteriores
**Estimativa:** 5 pontos
**Critério de Aceitação:** TypeScript impede estados inválidos por ruleset

---

## Bloco 30: Testes de Integração
**Descrição:** Testes completos do sistema

**Tarefas:**
- [ ] Criar testes para todas as funções de regras
- [ ] Implementar testes de migração entre versões
- [ ] Adicionar testes de performance
- [ ] Criar testes de validação de regras
- [ ] Implementar testes de serialização roundtrip
- [ ] Adicionar testes de casos de borda extremos

**Dependências:** Todos os blocos
**Estimativa:** 8 pontos
**Critério de Aceitação:** 100% de cobertura das regras críticas

---

## Bloco 31: Documentação dos Tipos
**Descrição:** Documentação completa da API de tipos

**Tarefas:**
- [ ] Gerar documentação automática dos tipos
- [ ] Adicionar exemplos de uso para cada interface
- [ ] Criar guia de migração para consumidores
- [ ] Documentar todas as enums e valores possíveis
- [ ] Adicionar advertências e boas práticas
- [ ] Criar cheatsheet para desenvolvedores

**Dependências:** Todos os blocos
**Estimativa:** 4 pontos
**Critério de Aceitação:** Documentação cobre 100% das interfaces públicas

---

## Checklist Final de Verificação
**Descrição:** Validação final antes do fechamento

**Tarefas:**
- [ ] Verificar que todas as regras do livro estão representadas
- [ ] Confirmar suporte a Classic, Pulp e variantes
- [ ] Validar sistema de envelhecimento de aplicação única
- [ ] Testar occupation snapshot imutável
- [ ] Verificar uniões discriminadas por ruleset
- [ ] Confirmar validação de domínio em todos os campos
- [ ] Testar migração de versões anteriores
- [ ] Validar export/import com todas as opções
- [ ] Testar performance com fichas complexas
- [ ] Confirmar cobertura de testes completa

**Dependências:** Todos os blocos
**Estimativa:** 2 pontos
**Critério de Aceitação:** Tipagem considerada "canônica" e pronta para produção

---

**Total de Pontos Estimados:** 99 pontos  
**Ordem Recomendada:** Seguir numeração dos blocos  
**Blocos Críticos:** 1, 2, 3, 4, 27, 28, 29 (devem ser implementados primeiro)  
**Entregável:** Interface TypeScript completa e testada para COC 7e

- [ ] **Identificadores e meta**
	- [ ] `id` (uuid), `createdAt`, `updatedAt`
	- [ ] `version` (versão do schema/ficha) para migrações.
	- [ ] `ownerId` / `playerName`.
	- [ ] `provenance` (importado, criado, duplicado).        
- [ ] **Características primárias**
	- [ ] Valor base persistido (ex.: STR_base).
	- [ ] Flags de modificação: `temporaryModifier`, `permanentModifier`.
	- [ ] Histórico de modificações (quando/por quem/razão) ou ao menos `lastModifiedCharacteristic`.
	- [ ] campo `source` nos modificadores (magia, ferimento, envelhecimento), apenas para rastreabilidade mais fina
- [ ] **Estatísticas derivadas**
	- [ ] Hit Points (HP): `current`, `max`, `temp`, `isMajorWound`, `permanentReduction`.
	- [ ] Magic Points / Spell Points (MP): `current`, `max`.
	- [ ] Sanidade (SAN): `current`, `max`, `temp`, `dailyLoss`, `permanentLoss`, `isIndefinitelyInsane`.
	- [ ] Luck: `current`, `max`, método de recuperação/uso.
	- [ ] Dodge, Damage Bonus, Build: campos derivados calculáveis e **também** cacheáveis com `calculatedAt`.
	- [ ] MOV (Movement): valor derivado, mas armazenado após criação; flag `derivedFrom` que registra fórmula usada.
- [ ] **Perícias (ISkill)**
	- [ ] `name`, `subName` (especialização), `category` (combat/social/academic), `baseValue`, `value`, `occupationPoints`, `interestPoints`.
	- [ ] `isChecked`/`checkedAt` (para evolução), `successCount` (meta).
	- [ ] `baseFormula?` para perícias dinâmicas (ex.: `DEX_HALF`, `EDU_BASE`, `CALCULATED_FROM`).
        
    - Validação de domínio: `value` sempre 0–100 (ou registrar overflow se house-rule).
        
    - `rollHistory[]` opcional (timestamp, roll result, successLevel) para auditoria/evolução.
        
    - `trainingSource` enum (occupation, interest, innate, default).
        
    - `specializations[]` caso múltiplas especializações.
        
5. **Combate / Armas (IWeapon)**
    
    - `name`, `skillUsed` (ligação), `damage` (string e estrutura separada), `reach`, `attacksPerRound`.
        
    - `ammo`: `currentAmmo`, `capacity`, `malfunctionRange` (ex.: 98–100).
        
    - `traits[]` (automatic, semi, conceal, twoHanded, reloadTime).
        
    - `condition` / `durability`, `isJammed`.
        
    - `equipped` flag, `wieldSlot` (main/secondary/back).
        
    - `damageType` (piercing, blunt, incendiary) e `AP` se usar rules que contenham penetração.
        
6. **Inventário / Items**
    
    - `IGear` com `id`, `name`, `quantity`, `weight?`, `isEquipped`, `slot`.
        
    - Encumbrance: `carryingWeight`, `carryingCapacity`, cálculo consistente com `Build` e `SIZ`.
        
    - `container`/`location` (mochila, bolso, mão).
        
    - Itens com propriedades dinâmicas (ex.: bateria com carga).
        
7. **Moeda / Crédito**
    
    - `cash` / `currencies[]` (moeda local, conversão opcional).
        
    - `creditRating` ou `reputation` se aplicável (valor e notas).
        
8. **Backstory / Metadados do personagem**
    
    - `personalInfo`: `name`, `age`, `occupation`, `residence`.
        
    - `backstory`: `ideology`, `importantPeople[]`, `places[]`, `valuedPossessions[]`, `traits[]`.
        
    - `portrait?` (url or blob) + `portraitMeta` (size, format, privacyFlag).
        
9. **Flags de estado**
    
    - `isDead`, `isUnconscious`, `isStabilized`, `isProne`.
        
    - `conditions[]` (bleeding, stunned, poisoned) com `expiresAt` ou `stacks`.
        
    - `restrictions[]` (unableToAct, restrained).
        
10. **Validação e integridade**
    
    - `isValid` (boolean), `validationErrors[]` (lista de campos/falhas).
        
    - Campos obrigatórios bem definidos para criação mínima da ficha.
        

# Recomendados (fortemente recomendados)

11. **Histórico / Audit**
    
    - `changeLog[]` (campo, oldValue, newValue, at, by).
        
    - `rollHistory[]` para testes, evolução e replay.
        
12. **Customização / Homebrew**
    
    - `houseRules[]` ou `customFlags` para marcar divergências do livro.
        
    - `customSkills[]` com definição completa (para permitir adicionar perícias que não estão no enum).
        
13. **Salvamento / Serialização**
    
    - `exportMetadata` (hash, exportAt, shortened snapshot) para backups e diffs.
        
    - Estratégia para imagens grandes (storeReference vs embed).
        
14. **Permissões / Compartilhamento**
    
    - `sharedWith[]` (userId, permission).
        
    - `isPublic` flag (para compartilhar fichas).
        
15. **Localização / Nomes**
    
    - Permitir `displayName` e `localeNames` / i18n para skills/traits.
        
    - Store `languageProficiencies[]` (línguas e níveis) se o jogo usar.
        
16. **Teste e consistência**
    
    - Fixtures de personagens com:
        
        - valores extremos (0, 1, 100+),
            
        - ferimentos/major wound ativo,
            
        - perícias com base dinâmica (DEX/2) e especializações múltiplas.
            

# Casos de borda e regras críticas a capturar no tipo (evitar perda de regra na camada de lógica)

17. **Ferimento grave / cura**
    
    - `isMajorWound` + `majorWoundDate` + `preventsNaturalHealing` (boolean).
        
    - `permanentHPReduction` para ferimentos que não regridem.
        
18. **Sanidade**
    
    - Registro de `temporarySanLossEvents[]` (valor, source, date).
        
    - `dailyLoss` acumulável; trigger para `isIndefinitelyInsane` com regra de transição (data + threshold).
        
19. **Perícias baseadas em atributo**
    
    - Sempre guardar **qual fórmula** foi usada para cálculo (para permitir recálculo automático se atributo mudar).
        
20. **Skill evolution / XP**
    
    - Campos para `xpSpent`, `improvementHistory[]`, `checkedAt` para resgatar regras de evolução.
        
21. **Rounding / truncation rules**
    
    - Registrar regra de arredondamento (floor/round) usada ao calcular percentuais derivados para manter consistência.
        
22. **Unidades**
    
    - Peso (g/kg/lbs) e distância (m/ft): meta `unitSystem` no personagem ou app-wide.
        

# Operacionais / Arquitetura de tipos

23. **Separação de responsabilidade**
    
    - Os tipos devem ser estritamente **dados** — fórmulas e regras ficam em `src/lib/coc-rules.ts` (funções puras). Porém:
        
        - Tipos devem incluir **metadados** que essas funções exijam (ex.: `baseFormula`, `derivedFrom`, `lastCalculatedAt`).
            
24. **Compatibilidade e migração**
    
    - `schemaVersion` em `IInvestigator` + `migrationNotes[]`.
        
25. **Performance / cache**
    
    - Campos cacheáveis: `cachedDerivedValues` com `calculatedAt` para evitar recalcular em cada render sem necessidade.
        

# Segurança e privacidade

26. **Imagem / portrait**
    
    - `privacy` flag (private/public).
        
    - Aviso sobre não incluir imagens sensíveis em export padrão; suportar opção `includeImagesInExport`.
        
27. **Export/Import**
    
    - Permitir export com/sem mídia.
        
    - Checksums/hashes em export para verificar integridade.
        

# Checklist final — itens para confirmar antes de fechar a tipagem

-  Todos os atributos primários têm `base`, `temporaryModifier`, `permanentModifier`.
    
-  Todos os campos derivados importantes têm `value` e `derivedFrom` (fórmula referenciada).
    
-  Perícias permitem `subName`, `category`, `baseFormula` e `rollHistory`.
    
-  Armas têm `skillUsed`, `ammo` e `traits`.
    
-  HP e SAN possuem `current`, `max`, `temp`, e flags de condição (`isMajorWound`, `isIndefinitelyInsane`).
    
-  Inventário contém `weight`/`quantity`/`equipped` e conexão com cálculo de encumbrance.
    
-  Flags de estado (morte/inconsciente) e lista genérica `conditions[]` com duração.
    
-  Metadados de versão/migração e `isValid` para validação.
    
-  Export/import contemplam privacy e imagens.
    
-  Campos para homebrew/custom skills e `houseRules`.
## Inclusões Finais — Pontos Cegos de Regra (Obrigatórios)

### 27. Envelhecimento e Aplicação Única de Modificadores

**Problema resolvido:** dupla aplicação ou omissão de penalidades/benefícios ao alterar idade ou importar ficha.

**Requisitos de Tipagem**

- Flag explícita indicando se as regras de envelhecimento já foram aplicadas.
    
- Registro auditável do impacto do envelhecimento.
    

**Checklist**

- Campo `agingApplied` ou equivalente no Investigador ou IPersonalInfo.
    
- Alternativamente (mais robusto):
    
    - Estrutura que registre:
        
        - atributos afetados,
            
        - valores antes/depois,
            
        - idade-base da aplicação.
            
- Garantir que:
    
    - Importação de ficha preserve esse estado.
        
    - Alteração de idade dispare verificação, não reaplicação automática.
        

---

### 28. Ocupação como Snapshot de Regra (OccupationSnapshot)

**Problema resolvido:** validação legal da ficha e prevenção de alocação inválida de pontos.

**Requisitos de Tipagem**

- Ocupação não deve ser apenas string descritiva.
    
- Deve carregar consigo as **regras vigentes no momento da criação**.
    

**Checklist**

- Estrutura de ocupação contendo:
    
    - nome da ocupação,
        
    - lista de perícias elegíveis para pontos de ocupação,
        
    - intervalo mínimo e máximo de Credit Rating.
        
- Snapshot imutável após criação:
    
    - mudanças futuras no catálogo de ocupações não afetam fichas existentes.
        
- Possibilidade de validação posterior:
    
    - detectar fichas “fora da regra” sem quebrar o carregamento.
        

---

### 29. Modo de Jogo / Conjunto de Regras (RulesetMode)

**Problema resolvido:** incompatibilidade estrutural entre fichas Clássicas, Pulp e variantes.

**Requisitos de Tipagem**

- Toda ficha deve declarar explicitamente **qual conjunto de regras governa seus dados**.
    

**Checklist**

- Campo `ruleset` no Investigador com valores previstos:
    
    - clássico,
        
    - pulp,
        
    - outros (ex.: Delta Green).
        
- Comportamento derivado:
    
    - Pulp habilita HP ampliado, talentos, arquétipos.
        
    - Clássico ignora esses campos sem erro.
        
- Tipos devem:
    
    - permitir campos condicionais por ruleset,
        
    - evitar inferência implícita baseada em valores (ex.: HP alto ≠ Pulp).
        

---

## Checklist Final Consolidado — Encerramento da Fase 1 / Passo 3

Antes de considerar a tipagem “fechada”, confirmar:

-  Envelhecimento aplicado exatamente uma vez e rastreável.
    
-  Ocupação modelada como entidade de regra, não texto livre.
    
-  Ruleset explícito e obrigatório no Investigador.
    
-  Tipos suportam coexistência de fichas Clássicas e Pulp sem ambiguidade.
    
-  Importação/exportação preserva aging, occupation snapshot e ruleset.
    
-  Nenhuma regra crítica depende de inferência implícita.
    

---

## Conclusão Técnica

Com esses três acréscimos:

- **A tipagem passa de “correta” para “canônica”** em relação ao livro do Guardião.
    
- O sistema fica:
    
    - resiliente a importações,
        
    - preparado para Pulp e expansões,
        
    - auditável sem acoplamento à UI.
        
- Refatorações futuras ficam **locais**, não estruturais.
    

Neste ponto, a Fase 1 — Passo 3 pode ser considerada **100% fechada**.

Concordo integralmente com a análise. Ela é tecnicamente precisa, coerente com a 7ª edição e identifica **falhas estruturais reais**, não meros refinamentos estéticos. A tipagem descrita **não fecha o ciclo de integridade de regras** sem os acréscimos apontados.

Abaixo está a **consolidação canônica** da Fase 1 — Passo 3, já incorporando suas correções, com foco em **garantia de estado**, **imutabilidade de regras de criação** e **segurança semântica**.

---

## Encerramento Técnico da Fase 1 — Passo 3

Status atual: **Incompleta sem os acréscimos abaixo**

### 1. Envelhecimento — Estrutura Obrigatória de Aplicação Única

Classificação: **Crítico / Bloqueador**

Você está correto: idade isolada é apenas dado descritivo.  
A regra de envelhecimento é **processual e irreversível**, portanto exige rastreamento explícito.

#### Requisito estrutural mínimo

- Estrutura dedicada (ex.: `IAgingApplication`), **imutável após aplicação**.
    
- Deve registrar:
    
    - se a regra já foi aplicada,
        
    - quando foi aplicada,
        
    - com qual idade-base,
        
    - quais ajustes foram realizados, por atributo.
        

#### Garantias que isso fornece

- Prevenção absoluta de dupla aplicação.
    
- Importação segura de fichas externas.
    
- Edição de idade sem efeitos colaterais silenciosos.
    
- Auditoria clara em caso de inconsistência.
    

Sem isso, qualquer engine de regras é **inerentemente instável**.

---

### 2. Ocupação como Snapshot de Regra

Classificação: **Crítico / Bloqueador**

A ocupação **não é um rótulo**, é um **contrato de criação**.

#### Problema confirmado

- String simples inviabiliza:
    
    - validação posterior,
        
    - evolução do catálogo,
        
    - verificação de legalidade da ficha.
        

#### Requisito estrutural mínimo

- Snapshot imutável contendo:
    
    - nome da ocupação,
        
    - perícias elegíveis,
        
    - intervalo de crédito,
        
    - pontos de perícia concedidos,
        
    - origem da regra (core/homebrew),
        
    - data de criação.
        

#### Garantias que isso fornece

- Fichas permanecem válidas mesmo com mudanças futuras no sistema.
    
- Validação retroativa possível sem “reprocessar” a criação.
    
- Base sólida para warnings de ficha ilegal sem quebrar carregamento.
    

Sem isso, o sistema **não consegue provar que uma ficha é válida**.

---

### 3. Ruleset como Discriminador de União

Classificação: **Crítico / Arquitetural**

A ausência de `ruleset` explícito torna a ficha **semanticamente ambígua**.

#### Correção necessária

- Campo raiz obrigatório `ruleset`.
    
- Uso como discriminador de união:
    
    - Clássico
        
    - Pulp
        
    - (Outros futuros)
        

#### Garantias que isso fornece

- TypeScript passa a **impedir estados inválidos** em tempo de compilação.
    
- Campos Pulp tornam-se obrigatórios apenas quando aplicáveis.
    
- Evita inferência heurística baseada em valores (ex.: HP alto).
    

Sem isso, o sistema aceita fichas **internamente incoerentes**.

---

## Problemas de Modelagem Secundários (Mas Reais)

### 4. Fórmulas Derivadas

- `derivedFrom: string` é frágil.
    
- Deve ser:
    
    - enum fechado **ou**
        
    - estrutura parseável.
        
- Necessário para:
    
    - recálculo seguro,
        
    - migrações,
        
    - testes automatizados.
        

---

### 5. Validação de Domínio

- Tipagem descritiva não impede valores inválidos.
    
- Pontos críticos (SAN, HP, MP, Luck) exigem:
    
    - tipos opacos **ou**
        
    - validação runtime obrigatória e centralizada.
        

Sem isso, bugs passam silenciosamente.

---

### 6. Auditoria de Modificações

- `lastModified` é insuficiente.
    
- Regras como SAN, envelhecimento e ferimentos exigem:
    
    - histórico estruturado de modificações,
        
    - com causa, valor anterior e novo.
        

Isso não é “nice to have”; é **instrumentação mínima**.

---

### 7. Cache de Valores Derivados

A observação é correta: cache sem invalidação definida é dívida técnica.

Antes de codificar, deve estar claro:

- Quais eventos invalidam quais caches.
    
- Onde isso será decidido (motor de regras, não UI).
    
- Como evitar inconsistência silenciosa.
    

---

## Checklist Final Obrigatório (Revisado)

A Fase 1 — Passo 3 **só pode ser considerada fechada** quando todos os itens abaixo existirem na especificação:

-  Estrutura dedicada para aplicação única de envelhecimento.
    
-  Snapshot imutável de ocupação com regras congeladas.
    
-  Campo raiz `ruleset` obrigatório.
    
-  União discriminada de Investigador por ruleset.
    
-  Tipagem segura para fórmulas derivadas.
    
-  Estratégia explícita de validação de domínio.
    
-  Log estruturado de modificações de atributos.
    
-  Definição clara de invalidação de caches derivados.
    

---

## Conclusão

Sua crítica está correta em essência e em detalhe:  
a tipagem anterior **descrevia dados**, mas ainda **não assegurava regras**.

Com os três pontos cegos formalizados como **estruturas obrigatórias**, a Fase 1 deixa de ser apenas sólida e passa a ser:

- canônica em relação ao livro,
    
- resiliente a importações e evolução do sistema,
    
- preparada para múltiplos modos de jogo,
    
- à prova de estados inválidos silenciosos.
    

Somente após isso a implementação deve começar.

Se desejar, o próximo passo lógico é:

- um **diagrama conceitual final do IInvestigator**, já considerando as uniões por ruleset, **ou**
    
- um **mapa de invalidação de regras derivadas** (quem invalida o quê).
    

Ambos fecham definitivamente a base antes do código.