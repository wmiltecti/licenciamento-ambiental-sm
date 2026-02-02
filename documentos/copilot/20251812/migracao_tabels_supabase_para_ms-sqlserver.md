list o nome das tabelas que estãocom acesso direto no banco de dados

Com base na análise completa do código, aqui está a lista de tabelas com acesso direto ao banco de dados através do Supabase:

📊 Lista de Tabelas com Acesso Direto ao Supabase
1. Tabelas de Administração/Parametrização (Admin Dashboard)
property_types - Tipos de Imóvel
process_types - Tipos de Processo ⭐
enterprise_sizes - Porte do Empreendimento
pollution_potentials - Potencial Poluidor
reference_units - Unidades de Referência
license_types - Tipos de Licença
study_types - Tipos de Estudo
billing_configurations - Configuração de Cobrança
activities - Atividades
documents - Documentos (template)
2. Tabelas de Processos e Licenciamento
license_processes - Processos de Licenciamento (legacy)
processes - Processos (nova estrutura)
process_documents - Documentos do Processo
process_comments - Comentários do Processo
process_collaborators - Colaboradores do Processo
process_participants - Participantes do Processo
3. Tabelas de Pessoas e Propriedades
people - Pessoas (físicas/jurídicas)
profiles - Perfis de usuário
user_profiles - Perfis de usuário (variante)
properties - Propriedades/Imóveis
property_titles - Títulos de Propriedade
addresses - Endereços
4. Tabelas de Relacionamentos/Vínculos
activity_license_types - Atividades x Tipos de Licença
activity_documents - Documentos por Atividade
activity_license_type_documents - Documentos por Atividade+Licença
activity_enterprise_ranges - Faixas de Porte por Atividade
license_type_documents - Documentos por Tipo de Licença
5. Tabelas de Sistema e Controle
system_configurations - Configurações do Sistema
form_wizard_steps - Etapas do Wizard
collaboration_invites - Convites de Colaboração
activity_logs - Logs de Atividades
processos_pendentes_sync - Fila de Sincronização
6. Storage (Supabase Storage)
docs (bucket) - Armazenamento de documentos
7. Tabelas de Empresas
companies - Empresas

📋 Priorização para Refatoração
🔴 Alta Prioridade (uso frequente em CRUD):
✅ process_types - Tipos de Processo
property_types - Tipos de Imóvel
license_types - Tipos de Licença
activities - Atividades
pollution_potentials - Potencial Poluidor
enterprise_sizes - Porte do Empreendimento
reference_units - Unidades de Referência
study_types - Tipos de Estudo
billing_configurations - Configuração de Cobrança
documents - Documentos

🟡 Média Prioridade (uso em processos principais):
processes / license_processes - Processos
people - Pessoas
properties - Propriedades
process_participants - Participantes
process_documents - Documentos do Processo
property_titles - Títulos

🟢 Baixa Prioridade (uso secundário/interno):
activity_license_types - Relacionamentos
activity_documents - Relacionamentos
process_collaborators - Colaboração
collaboration_invites - Convites
process_comments - Comentários
system_configurations - Configurações
Demais tabelas auxiliares

🎯 Recomendação de Ordem de Implementação
Fase 1 - Parametrização Básica (todas usam GenericCRUD):

process_types
property_types
enterprise_sizes
pollution_potentials
reference_units
study_types
Fase 2 - Parametrização Complexa:

license_types (tem form customizado)
activities (tem form complexo)
billing_configurations (tem form muito complexo)
Fase 3 - Core do Sistema:

processes
people
properties
Fase 4 - Relacionamentos e Auxiliares:

Todas as tabelas de junção/relacionamento
Tabelas de log e controle
Todas essas tabelas precisam de endpoints REST na API FastAPI para substituir o acesso direto ao Supabase!
