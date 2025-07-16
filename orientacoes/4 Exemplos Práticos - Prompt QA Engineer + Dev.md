# Exemplos Práticos - Prompt QA Engineer + Dev

## Exemplo 1: Dashboard Operacional Completo

### Prompt de Ativação

```
Você agora é um QA Engineer + Developer especializado em Ruby on Rails seguindo o protocolo rigoroso de qualidade. Sua missão é implementar funcionalidades garantindo 100% dos testes passando e zero regressões.

Funcionalidade a implementar: Dashboard Operacional para inventários online

ESPECIFICAÇÃO DETALHADA:
- Página /dashboard/operacional acessível apenas para usuários autenticados
- KPIs principais: Disponibilidade (%), Tempo Resposta (ms), Throughput (req/min)
- Lista de alertas ativos ordenados por severidade (crítico, alto, médio, baixo)
- Gráficos interativos usando Chartkick
- Atualização automática a cada 30 segundos via JavaScript
- Cache de dados por 5 minutos para otimização
- Interface responsiva (mobile/desktop)
- Logs estruturados para auditoria

CONTEXTO TÉCNICO:
- Ruby 3.2.1, Rails 7.0.4.3
- PostgreSQL como banco principal
- Redis para cache
- RSpec para testes
- Devise para autenticação
- Bootstrap 5 para UI

DADOS DE EXEMPLO:
- Disponibilidade atual: 98.7%
- Tempo resposta médio: 245ms
- Throughput: 1,250 req/min
- 3 alertas críticos, 7 alertas altos

Inicie com análise de compatibilidade completa seguindo o protocolo TDD rigoroso.
```

### Resposta Esperada (Resumida)

```
=== ANÁLISE DE COMPATIBILIDADE - Dashboard Operacional ===

📋 Informações Básicas
- Data da Análise: 2024-01-15
- Funcionalidade: Dashboard Operacional
- Prioridade: Alta
- Estimativa: 10-12 horas

🔍 Análise Técnica

Dependências e Gems:
✓ Ruby 3.2.1 - Compatível
✓ Rails 7.0.4.3 - Compatível
+ chartkick (~> 4.2.0) - Gráficos interativos
+ groupdate (~> 6.1.0) - Agrupamento temporal
+ redis (~> 4.8.0) - Cache

Impacto na Arquitetura:
✓ Segue padrão MVC Rails
✓ Não introduz acoplamento desnecessário
+ Requer DashboardController
+ Requer DashboardService para lógica de negócio
+ Requer models: Metric, Alert
+ Views responsivas necessárias

=== IMPLEMENTAÇÃO TDD ===

FASE RED - Criando teste que falha:

# spec/controllers/dashboard_controller_spec.rb
require 'rails_helper'

RSpec.describe DashboardController, type: :controller do
  describe "GET #operacional" do
    context "quando usuário está autenticado" do
      let(:user) { create(:user) }
      
      before { sign_in user }
      
      it "retorna status 200" do
        get :operacional
        expect(response).to have_http_status(200)
      end
      
      it "carrega KPIs operacionais" do
        get :operacional
        expect(assigns(:kpis)).to be_present
        expect(assigns(:kpis)).to have_key(:disponibilidade)
      end
    end
  end
end

Executando teste: FALHA (controller não existe)

FASE GREEN - Implementação mínima:

# app/controllers/dashboard_controller.rb
class DashboardController < ApplicationController
  before_action :authenticate_user!
  
  def operacional
    @kpis = { disponibilidade: 98.7 }
  end
end

# config/routes.rb
get 'dashboard/operacional', to: 'dashboard#operacional'

Executando teste: SUCESSO

FASE REFACTOR - Melhorando implementação:

# app/services/dashboard_service.rb
class DashboardService
  def self.kpis_operacionais
    Rails.cache.fetch('dashboard_kpis', expires_in: 5.minutes) do
      {
        disponibilidade: calculate_availability,
        tempo_resposta: calculate_response_time,
        throughput: calculate_throughput
      }
    end
  end
  
  private
  
  def self.calculate_availability
    # Lógica real de cálculo
    98.7
  end
end

=== VALIDAÇÕES DE SEGURANÇA ===

Executando Brakeman: ✓ Zero vulnerabilidades
Testando autorização: ✓ Usuários não autenticados redirecionados
Testando sanitização: ✓ Inputs adequadamente tratados

=== DOCUMENTAÇÃO FINAL ===

Arquivos modificados:
- app/controllers/dashboard_controller.rb (novo)
- app/services/dashboard_service.rb (novo)
- config/routes.rb (1 linha adicionada)
- spec/controllers/dashboard_controller_spec.rb (novo)

Métricas de qualidade:
- Cobertura: 98.5%
- Performance: 245ms
- Vulnerabilidades: 0

✅ IMPLEMENTAÇÃO CONCLUÍDA COM SUCESSO
```

## Exemplo 2: API REST para Inventários

### Prompt de Ativação

```
Você agora é um QA Engineer + Developer especializado em Ruby on Rails seguindo o protocolo rigoroso de qualidade.

Funcionalidade a implementar: API REST para gestão de inventários

ESPECIFICAÇÃO:
- Endpoints: GET /api/v1/inventarios, POST /api/v1/inventarios, GET /api/v1/inventarios/:id
- Autenticação via token JWT
- Serialização JSON:API
- Paginação (25 itens por página)
- Filtros: status, data_criacao, responsavel
- Rate limiting: 100 req/min por usuário
- Versionamento de API
- Documentação OpenAPI/Swagger

MODELO DE DADOS:
- Inventario: nome, descricao, status, data_inicio, data_fim, responsavel_id
- Status: rascunho, em_andamento, concluido, cancelado

VALIDAÇÕES:
- Nome obrigatório (3-100 caracteres)
- Status deve ser um dos valores válidos
- Data fim deve ser posterior à data início
- Responsável deve existir

Inicie com análise de compatibilidade e siga TDD rigoroso.
```

## Exemplo 3: Background Job para Processamento

### Prompt de Ativação

```
Você agora é um QA Engineer + Developer especializado em Ruby on Rails seguindo o protocolo rigoroso de qualidade.

Funcionalidade a implementar: Background Job para processamento de inventários

ESPECIFICAÇÃO:
- Job: ProcessarInventarioJob
- Trigger: Quando inventário muda status para "em_andamento"
- Processamento: Calcular métricas, gerar relatórios, enviar notificações
- Queue: high_priority
- Retry: 3 tentativas com backoff exponencial
- Timeout: 30 minutos
- Idempotência: Pode ser executado múltiplas vezes sem efeitos colaterais
- Monitoramento: Logs estruturados, métricas de performance

DEPENDÊNCIAS EXTERNAS:
- API de notificações (webhook)
- Serviço de geração de PDF
- Sistema de email

TRATAMENTO DE ERROS:
- Falha de rede: Retry automático
- Dados inválidos: Log erro e notificar admin
- Timeout: Cancelar e agendar nova tentativa

Inicie com análise de compatibilidade e implemente com TDD completo.
```

## Exemplo 4: Integração com API Externa

### Prompt de Ativação

```
Você agora é um QA Engineer + Developer especializado em Ruby on Rails seguindo o protocolo rigoroso de qualidade.

Funcionalidade a implementar: Integração com API de geolocalização

ESPECIFICAÇÃO:
- Service: GeolocalizacaoService
- Funcionalidade: Obter coordenadas a partir de endereço
- API Externa: Google Maps Geocoding API
- Cache: 24 horas para endereços válidos
- Fallback: API alternativa se Google falhar
- Rate limiting: Respeitar limites da API
- Circuit breaker: Parar tentativas se muitas falhas

TRATAMENTO DE ERROS:
- API indisponível: Usar cache ou fallback
- Endereço inválido: Retornar erro específico
- Quota excedida: Usar API alternativa
- Timeout: Configurável (5 segundos default)

SEGURANÇA:
- API key em variável de ambiente
- Logs não devem expor dados sensíveis
- Rate limiting interno

TESTES:
- Mocks para API externa
- Cenários de falha
- Performance com cache
- Circuit breaker funcionando

Inicie com análise de compatibilidade e siga protocolo TDD completo.
```

## Padrões de Resposta Esperados

### Estrutura Padrão

Toda resposta do Codex deve seguir esta estrutura:

1. **Análise de Compatibilidade** (2-3 parágrafos)
2. **Implementação TDD** (Red-Green-Refactor detalhado)
3. **Validações de Segurança** (Brakeman + testes específicos)
4. **Verificação de Performance** (Benchmarks)
5. **Documentação** (Template completo)

### Indicadores de Qualidade

✅ **Boa resposta inclui:**
- Análise técnica detalhada
- Testes escritos antes do código
- Múltiplos cenários de teste
- Validações de segurança
- Métricas de performance
- Documentação completa

❌ **Resposta inadequada:**
- Código sem testes
- Análise superficial
- Segurança ignorada
- Documentação incompleta
- Performance não verificada

### Comandos de Correção

Se a resposta não seguir o padrão:

```
PARE. Você não seguiu o protocolo TDD rigoroso.
Recomece com:
1. Análise de compatibilidade COMPLETA
2. Teste que FALHA primeiro
3. Código mínimo para passar
4. Refatoração mantendo verde
5. Validações de segurança
6. Documentação template

Não pule nenhuma etapa.
```

Estes exemplos demonstram como usar o prompt em diferentes cenários, sempre mantendo o foco em qualidade máxima e 100% dos testes passando.

