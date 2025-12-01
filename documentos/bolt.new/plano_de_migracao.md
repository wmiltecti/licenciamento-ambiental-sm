# 📋 Plano de Migração - Sistema de Licenciamento Ambiental

## 🎯 Resumo Executivo

### 📊 Distribuição de Tabelas

| Destino | Quantidade | Percentual |
|---------|------------|------------|
| **PostgreSQL** | 23-26 tabelas | 79-90% |
| **Bolt Database** | 3-6 tabelas | 10-21% |

---

## 🔄 MIGRAR para PostgreSQL (23-26 tabelas)

### 🔴 Críticas (11 tabelas)
**Tabelas de referência e configuração essenciais**

- `property_types` - Tipos de propriedade (Rural, Urbano, Linear)
- `process_types` - Tipos de processo de licenciamento
- `enterprise_sizes` - Portes de empreendimento
- `pollution_potentials` - Potenciais poluidores
- `reference_units` - Unidades de medida de referência
- `license_types` - Tipos de licença (LP, LI, LO, etc)
- `study_types` - Tipos de estudos ambientais
- `documentation_templates` - Templates de documentação
- `activities` - Atividades econômicas
- `system_configurations` - Configurações do sistema
- `billing_configurations` - Configurações de cobrança

### 🟠 Alta Prioridade (8 tabelas)
**Relacionamentos e processos de negócio**

- `activity_license_types` - Relação atividade ↔ tipo de licença
- `activity_documents` - Documentos por atividade
- `activity_license_type_documents` - Documentos por atividade/licença
- `activity_enterprise_ranges` - Faixas de porte por atividade
- `license_type_documents` - Documentos por tipo de licença
- `processes` - Processos de licenciamento
- `license_processes` - Licenças de processos
- `process_movements` - Movimentações de processo
- `form_wizard_steps` - Etapas do wizard

### 🟡 Média Prioridade (7 tabelas)
**Dados cadastrais e imóveis**

- `companies` - Empresas
- `people` - Pessoas físicas
- `addresses` - Endereços
- `properties` - Imóveis (Rural, Urbano, Linear)
- `property_titles` - Títulos de propriedade
- `process_collaborators` - Colaboradores do processo
- `process_comments` - Comentários
- `activity_logs` - Logs de auditoria

### 📄 Metadata de Documentos (1 tabela)

- `process_documents` - **Apenas metadados** (não os arquivos físicos)

---

## 💾 MANTER no Bolt Database (3-6 tabelas)

### 🔐 Autenticação (2 tabelas)
- `user_profiles` - Perfis de usuário
- `profiles` - Perfis de acesso

### 📦 Storage (2 tabelas)
- `documents` - Bucket de armazenamento
- Arquivos físicos referenciados por `process_documents`

### ❓ Opcional (2 tabelas)
*Avaliar caso a caso*
- `collaboration_invites` - Pode ser migrado
- `docs` - Verificar se é metadata ou storage

---

## 🗺️ Ordem de Migração Recomendada

### **FASE 1** 🏗️ Tabelas de Referência
*Não possuem dependências*

1. `property_types`
2. `process_types`
3. `enterprise_sizes`
4. `pollution_potentials`
5. `reference_units`
6. `study_types`
7. `documentation_templates`
8. `system_configurations`

---

### **FASE 2** 🔗 Dependência Simples

- `license_types`
- `activities` *(depende de `pollution_potentials`)*

---

### **FASE 3** 🔀 Relacionamentos

- `activity_license_types` *(activities + license_types)*
- `activity_documents` *(activities + documentation_templates)*
- `activity_license_type_documents` *(múltiplas dependências)*
- `activity_enterprise_ranges` *(activities + enterprise_sizes)*
- `license_type_documents` *(license_types + documentation_templates)*

---

### **FASE 4** 💰 Billing
*Depende de todas as tabelas anteriores*

- `billing_configurations` *(activities, license_types, reference_units, etc)*

---

### **FASE 5** 👥 Cadastros de Entidades

- `people`
- `addresses`
- `companies`

---

### **FASE 6** 🏡 Imóveis

- `properties` *(depende de `addresses`)*
- `property_titles` *(depende de `properties`)*

---

### **FASE 7** 📋 Processos

- `processes` *(people, companies, properties)*
- `license_processes` *(processes)*
- `process_movements` *(license_processes)*
- `form_wizard_steps` *(processes)*

---

### **FASE 8** 🤝 Colaboração e Auditoria

- `process_collaborators`
- `process_comments`
- `activity_logs`
- `process_documents` *(metadata)*

---

## ✨ Benefícios da Separação

### 🐘 PostgreSQL - Regras de Negócio

| Benefício | Descrição |
|-----------|-----------|
| ⚡ **Transações ACID** | Garantias de consistência e integridade |
| 🔧 **Procedures/Triggers** | Validações complexas no banco |
| 🚀 **Performance** | Otimizada para cálculos e consultas complexas |
| 💾 **Backup/Recovery** | Corporativo e confiável |
| 📊 **Integração BI** | Ferramentas de análise e relatórios |

### 🔥 Bolt Database - Auth + Storage

| Benefício | Descrição |
|-----------|-----------|
| 🔐 **Autenticação** | Gerenciada e segura out-of-the-box |
| ⚡ **Real-time** | Subscriptions para atualizações em tempo real |
| 📦 **Storage** | Otimizado para arquivos e documentos |
| 🌐 **CDN Global** | Distribuição mundial de assets |
| 👤 **Gestão Usuários** | Simplificada e escalável |

---

## 📈 Resumo Final

- ✅ **23-26 tabelas** migradas para PostgreSQL (79-90%)
- ✅ **3-6 tabelas** mantidas no Bolt Database (10-21%)
- ✅ **8 fases** de migração organizadas por dependência
- ✅ **Separação clara** entre regras de negócio e autenticação/storage