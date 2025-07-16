# Análise do Contexto - Prompt QA Engineer + Dev

## Componentes-Chave Identificados

### 1. Pré-requisitos Obrigatórios
- Ambiente local Ruby/Rails configurado
- Permissões para instalar dependências
- Banco de dados de desenvolvimento com dados de teste
- Suite de testes funcional (RSpec/Minitest)

### 2. Objetivo Principal
Integrar Dashboard Operacional ao projeto Pedrookas07/inventarios-online com:
- 100% dos testes passando
- Compatibilidade com versões existentes
- Zero regressões funcionais
- Documentação replicável

### 3. Fluxo de Trabalho Iterativo
O documento menciona um diagrama de fluxo que deve incluir:
- Análise → Implementação → Teste → Validação → Documentação

### 4. Ações Específicas Requeridas

#### Análise de Compatibilidade
- Verificação de vulnerabilidades (bundle audit)
- Métodos depreciados
- Vazamento de dados sensíveis
- Conformidade com convenções Rails (MVC)
- Padrão de internacionalização
- Validação de rotas dinâmicas

#### Simulação de Dados
- Factory objects para testes
- Datasets para cenários extremos
- Alta carga de alertas
- Dados temporais inconsistentes

#### Testes Automáticos
- Ordem de execução: unitários → controle → sistema
- Monitoramento de cobertura (simplecov)
- Performance (tempo de execução)

#### Tratamento de Erros
- Screenshot do erro
- Contexto de execução
- Stacktrace completo
- Classificação de severidade

#### Refatoração
- Princípios SOLID
- Redução de complexidade ciclomática
- Eliminação de antipadrões

#### Validação Visual
- Renderização responsiva
- Consistência visual
- Acessibilidade (WCAG 2.1)
- Console limpo

### 5. Critérios de Sucesso
- Cobertura de testes (%)
- Tempo de carregamento (ms)
- Alertas pendentes zerados
- Documentação completa

## Requisitos Técnicos Específicos

### Stack Tecnológico
- Ruby 3.2.1
- Rails 7.0.4.3
- RSpec/Minitest para testes
- FactoryBot para dados de teste
- Chartkick para gráficos
- Brakeman para segurança
- SimpleCov para cobertura

### Arquivos Típicos Modificados
- Controllers (dashboard_controller.rb)
- Views (operacional.html.erb)
- Routes
- Models
- Factories
- Specs/Tests

### Comandos Essenciais
- bundle install
- rails assets:precompile
- rails db:migrate
- bin/webpack
- bundle audit
- rspec
- rails test

