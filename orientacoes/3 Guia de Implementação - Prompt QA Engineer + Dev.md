# Guia de Implementação - Prompt QA Engineer + Dev

## Como Usar Este Prompt

### Pré-Requisitos

Antes de usar o prompt, certifique-se de que você tem:

1. **Ambiente Ruby on Rails configurado**
   - Ruby 3.x instalado
   - Rails 7.x instalado
   - Bundler atualizado

2. **Ferramentas de Qualidade**
   - RSpec ou Minitest configurado
   - Brakeman para análise de segurança
   - SimpleCov para cobertura de testes

3. **Projeto Base**
   - Repositório Git inicializado
   - Banco de dados configurado
   - Suite de testes básica funcionando

### Ativação do Prompt

Para ativar o prompt no Codex, use esta instrução exata:

```
Você agora é um QA Engineer + Developer especializado em Ruby on Rails seguindo o protocolo rigoroso de qualidade. Sua missão é implementar funcionalidades garantindo 100% dos testes passando e zero regressões.

PROCESSO OBRIGATÓRIO:
1. Análise de compatibilidade completa
2. Implementação TDD (Red-Green-Refactor)
3. Validações de segurança (Brakeman + testes específicos)
4. Verificação de performance
5. Documentação completa

CRITÉRIOS DE SUCESSO:
- 100% dos testes passando
- Cobertura ≥ 95%
- Zero vulnerabilidades
- Performance < 500ms
- Documentação completa

Funcionalidade a implementar: [DESCREVER AQUI A FUNCIONALIDADE ESPECÍFICA]
```

### Exemplo Prático: Dashboard Operacional

Vamos implementar o Dashboard Operacional como exemplo:

#### 1. Ativação com Contexto Específico

```
Você agora é um QA Engineer + Developer especializado em Ruby on Rails seguindo o protocolo rigoroso de qualidade. Sua missão é implementar funcionalidades garantindo 100% dos testes passando e zero regressões.

Funcionalidade a implementar: Dashboard Operacional para o projeto inventarios-online

REQUISITOS ESPECÍFICOS:
- Exibir KPIs de disponibilidade, tempo de resposta e throughput
- Mostrar alertas ativos ordenados por severidade
- Interface responsiva com gráficos interativos
- Cache de 5 minutos para otimização
- Autenticação obrigatória
- Logs estruturados para auditoria

CONTEXTO DO PROJETO:
- Ruby 3.2.1, Rails 7.0.4.3
- Banco PostgreSQL
- RSpec para testes
- Chartkick para gráficos
- Devise para autenticação

Inicie com a análise de compatibilidade completa.
```

#### 2. Resposta Esperada do Codex

O Codex deve responder seguindo o protocolo:

```
Iniciando análise de compatibilidade para Dashboard Operacional...

=== ANÁLISE DE COMPATIBILIDADE ===

📋 Informações Básicas
- Funcionalidade: Dashboard Operacional
- Prioridade: Alta
- Estimativa: 8-12 horas

🔍 Análise Técnica

Dependências e Gems:
✓ Ruby 3.2.1 - Compatível
✓ Rails 7.0.4.3 - Compatível
+ Chartkick ~> 4.2.0 - Para gráficos interativos
+ Groupdate ~> 6.1.0 - Para agrupamento temporal

Impacto na Arquitetura:
✓ Segue padrão MVC
✓ Não introduz acoplamento
+ Requer DashboardController
+ Requer DashboardService para lógica de negócio
+ Views responsivas necessárias

Análise de Performance:
+ Cache Redis recomendado (TTL 5min)
+ Queries otimizadas com includes
+ Índices necessários em metrics.created_at

Segurança:
✓ Autenticação via Devise
✓ Autorização por roles
✓ Sanitização de inputs
✓ CSRF protection

Iniciando implementação TDD...

=== FASE RED (Teste Falhando) ===

Criando spec/controllers/dashboard_controller_spec.rb...
```

#### 3. Acompanhamento do Processo

Durante a implementação, o Codex deve:

1. **Mostrar cada teste antes da implementação**
2. **Implementar código mínimo para passar**
3. **Refatorar mantendo testes verdes**
4. **Executar validações de segurança**
5. **Documentar cada decisão**

### Comandos de Monitoramento

Use estes comandos para acompanhar o progresso:

```bash
# Verificar status dos testes
watch -n 5 'bundle exec rspec --format progress'

# Monitorar cobertura
open coverage/index.html

# Verificar segurança
bundle exec brakeman --no-pager

# Análise de performance
bundle exec rspec --profile 10
```

### Sinais de Sucesso

O prompt está funcionando corretamente quando você vê:

✅ **Análise sistemática antes de qualquer código**
✅ **Testes escritos antes da implementação**
✅ **Validações de segurança automáticas**
✅ **Documentação detalhada de cada etapa**
✅ **Métricas de qualidade reportadas**

### Sinais de Problema

Intervenha se observar:

❌ **Código implementado sem testes**
❌ **Testes pulados ou ignorados**
❌ **Validações de segurança omitidas**
❌ **Documentação incompleta**
❌ **Performance não verificada**

### Troubleshooting Comum

#### Problema: Codex pula etapas do processo

**Solução**: Reforce o prompt com:
```
PARE. Você deve seguir RIGOROSAMENTE o processo TDD. 
Primeiro escreva o teste que falha, depois implemente o código mínimo.
Não pule nenhuma etapa de validação.
```

#### Problema: Testes muito simples

**Solução**: Especifique cenários:
```
Os testes devem cobrir:
- Casos de sucesso
- Casos de falha
- Edge cases (dados nulos, strings vazias)
- Cenários de segurança
- Performance com grandes volumes
```

#### Problema: Documentação insuficiente

**Solução**: Exija templates:
```
Use o template de documentação fornecido.
Inclua: arquivos modificados, dependências, instruções de deploy,
troubleshooting, e métricas de qualidade.
```

### Customização para Projetos Específicos

Adapte o prompt para seu contexto:

#### Para APIs REST
```
Funcionalidade: API REST para [recurso]
Requisitos adicionais:
- Serializers JSON:API
- Versionamento de API
- Rate limiting
- Documentação OpenAPI
```

#### Para Background Jobs
```
Funcionalidade: Job para [processamento]
Requisitos adicionais:
- Sidekiq/Resque
- Retry logic
- Monitoramento de falhas
- Idempotência
```

#### Para Integrações Externas
```
Funcionalidade: Integração com [serviço]
Requisitos adicionais:
- Circuit breaker
- Timeout configurável
- Fallback strategies
- Logs estruturados
```

### Métricas de Sucesso

Acompanhe estas métricas para validar a eficácia:

| Métrica | Meta | Como Medir |
|---------|------|------------|
| Cobertura de Testes | ≥ 95% | SimpleCov |
| Tempo de Resposta | ≤ 500ms | Benchmark |
| Vulnerabilidades | 0 | Brakeman |
| Complexidade | ≤ 10 | Flog |
| Duplicação | 0% | Flay |

### Evolução do Prompt

Mantenha o prompt atualizado:

1. **Adicione novos padrões** conforme aprende
2. **Refine critérios** baseado em experiência
3. **Atualize ferramentas** para versões mais recentes
4. **Documente lições aprendidas** para referência futura

Este guia garante que você extraia o máximo valor do prompt QA Engineer + Dev, mantendo sempre os mais altos padrões de qualidade.

