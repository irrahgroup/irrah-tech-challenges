# Desafio Backend - BCB

Como desenvolvedor backend, seu desafio principal será implementar um **sistema de filas para processamento de mensagens de chat** com priorização. O foco está na estrutura de dados e algoritmos para gerenciar e processar mensagens em ordem correta. Abaixo estão os detalhes do que deve ser implementado, dividido em partes progressivas.

## Desafio: Sistema de Filas para Chat

### Parte 1: Funcionalidades Essenciais
- **API básica**:
  - Endpoints para autenticação e gerenciamento de clientes
  - Endpoints para envio e recebimento de mensagens
  - Validação de saldo/limite conforme tipo de plano
  - Identificação do cliente via parâmetro na requisição (ex: clientId)

- **Fila de mensagens (síncrona)**:
  - Implementação de uma fila em memória (array/lista)
  - Processamento síncrono de mensagens na mesma requisição
  - Ordenação básica (FIFO - primeiro a entrar, primeiro a sair)
  - Registro de status das mensagens processadas

### Parte 2: Aprimoramentos
- **Autenticação simplificada**:
  - Identificação do cliente via CPF/CNPJ no header
  - Associação básica de requisições ao cliente correspondente

- **Fila com priorização**:
  - Implementação de fila com dois níveis de prioridade (Normal/Urgente)
  - Estrutura de dados que garanta que mensagens urgentes sejam processadas primeiro
  - Lógica para balancear prioridade vs. ordem de chegada (evitar starvation)
  - Status detalhado de mensagens (enviada, entregue, lida)
  - Processamento mantido síncrono, mas com estrutura de fila completa

### Parte 3: Recursos Adicionais
- **Fila assíncrona com worker**:
  - Thread/processo separado para processar a fila em background
  - Execução contínua e assíncrona (independente da requisição HTTP)
  - Sistema completo de status (enfileirada, processando, enviada, entregue)
  - Tratamento de falhas e reprocessamento automático

- **Recursos avançados**:
  - Simulação de comunicação em tempo real
  - Endpoints para estatísticas da fila (tamanho, mensagens processadas/pendentes)
  - API para monitoramento de desempenho da fila
  - Cache para otimização de performance

> **Dica**: Comece pela Parte 1 e avance conforme o tempo disponível. Uma boa implementação da Parte 1 já é suficiente para a avaliação.

## Entregas Mínimas

Como desenvolvedor backend, você deve entregar no mínimo:
- API para autenticação e gerenciamento de clientes
- Implementação de fila em memória para processamento de mensagens
- Validação financeira de plano (pré ou pós-pago)
- Endpoints para listagem de histórico de conversas
- Estrutura básica para envio e processamento de mensagens

O desafio principal é implementar uma estrutura de fila que permita o processamento ordenado das mensagens, não apenas um CRUD básico.

## Especificações Técnicas

### Estrutura de Dados

#### Cliente
```json
{
  "id": "client123",
  "name": "Empresa ABC Ltda",
  "documentId": "12345678000199",  // CPF ou CNPJ
  "documentType": "CNPJ",          // "CPF" ou "CNPJ"
  "planType": "prepaid",           // "prepaid" ou "postpaid"
  "balance": 100.00,               // saldo (para pré-pago)
  "limit": 0,                      // limite (para pós-pago)
  "active": true                   // status do cliente
}
```

#### Mensagem
```json
{
  "id": "msg123",
  "conversationId": "conv456",     // ID da conversa
  "senderId": "client123",         // ID do cliente que enviou
  "recipientId": "user789",        // ID do destinatário 
  "content": "Olá, como vai?",     // conteúdo da mensagem
  "timestamp": "2023-07-15T10:30:00Z",
  "priority": "normal",            // "normal" ou "urgent"
  "status": "queued",              // "queued", "processing", "sent", "delivered", "read", "failed"
  "cost": 0.25                     // custo da mensagem (0.25 normal, 0.50 urgente)
}
```

#### Conversa
```json
{
  "id": "conv456",
  "clientId": "client123",         // ID do cliente
  "recipientId": "user789",        // ID do usuário/destinatário
  "recipientName": "Maria Silva",  // Nome do destinatário
  "lastMessageContent": "Olá, como vai?",
  "lastMessageTime": "2023-07-15T10:30:00Z",
  "unreadCount": 0                 // contador de mensagens não lidas
}
```

### APIs Esperadas

#### Autenticação e Clientes
```
POST   /auth                - Autenticação simples do cliente (CPF/CNPJ)
GET    /clients             - Lista clientes (admin)
POST   /clients             - Cria novo cliente
GET    /clients/:id         - Obtém detalhes de um cliente
PUT    /clients/:id         - Atualiza um cliente
GET    /clients/:id/balance - Consulta saldo/limite do cliente
```

#### Conversas
```
GET    /conversations             - Lista conversas do cliente autenticado
GET    /conversations/:id         - Obtém detalhes de uma conversa
GET    /conversations/:id/messages - Obtém mensagens de uma conversa
```

#### Mensagens
```
POST   /messages            - Envia nova mensagem
GET    /messages            - Lista mensagens com filtros
GET    /messages/:id        - Obtém detalhes de uma mensagem
GET    /messages/:id/status - Verifica status de uma mensagem
```

#### Sistema de Fila
```
GET    /queue/status        - Estatísticas da fila (tamanho, processadas, etc)
```

### Exemplos de Requisições e Respostas

#### Envio de Mensagem (Request)
```json
// POST /messages
{
  "conversationId": "conv456",
  "recipientId": "user789",
  "content": "Olá, como vai?",
  "priority": "normal"
}
```

#### Envio de Mensagem (Response)
```json
// Status: 201 Created
{
  "id": "msg123",
  "status": "queued",
  "estimatedDelivery": "2023-07-15T10:30:05Z",
  "cost": 0.25,
  "currentBalance": 99.75  // apenas para pré-pago
}
```

### Diagrama de Fluxo
```
           ┌─ Normal Queue ─┐
Cliente --> Validação  ──┬──>  Enfileiramento  ──> Processamento --> Atualização
            Financeira   │     priorizado         (worker)         de Status
   (saldo/limite)        └─ Urgent Queue ─┘   (sync/async)     (enviada/entregue)
```

## Tecnologias Recomendadas

Para o desenvolvimento backend, sugerimos:
- Linguagens: **Java** (Spring Boot), **Node.js** (NestJS/Express) ou **Go** (Gin/Echo/Fiber)
- Banco de dados: PostgreSQL (preferência), MySQL, MongoDB ou outro à sua escolha
- Docker para containerização

## Critérios de Avaliação Detalhados

Sua implementação será avaliada nos seguintes aspectos:

| Critério | Peso | O que será avaliado | 
|----------|------|---------------------|
| **Estrutura de dados** | 30% | Eficiência da implementação da fila, estratégia de priorização, tratamento de edge cases (fila vazia, starvation) |
| **APIs e validações** | 25% | Design dos endpoints, validações de entrada, respostas adequadas, tratamento de erros |
| **Regras de negócio** | 20% | Implementação das regras de validação financeira, estados das mensagens, fluxo de processamento |
| **Organização do código** | 15% | Separação de responsabilidades, padrões de projeto, legibilidade, documentação |
| **Performance** | 10% | Eficiência do processamento, uso adequado de recursos, técnicas de otimização |

### Exemplos por nível de complexidade:

**Implementação básica (Parte 1)**:
- Fila simples usando arrays
- Priorização básica (if-else)
- Validação simples de saldo
- Estrutura organizada e funcional

**Implementação intermediária (Parte 2)**:
- Fila com estruturas de dados apropriadas
- Priorização com balanceamento básico
- Validações de regras de negócio completas
- Arquitetura em camadas, com separação de responsabilidades

**Implementação avançada (Parte 3)**:
- Estruturas de dados otimizadas para o caso de uso
- Algoritmo sofisticado para priorização com anti-starvation
- Sistema completo de validação, com tratamentos de casos especiais
- Arquitetura limpa, testes automatizados, tratamento de concorrência

## Diferenciais

Para se destacar, considere implementar:
- Testes unitários e de integração (cobertura >80%)
- Documentação da API (Swagger/OpenAPI)
- Tratamento avançado de erros com feedback detalhado
- Monitoramento e logging estruturado
- CI/CD com validações automatizadas

Lembre-se de consultar também:
- [Regras de negócio](./regras-negocio.md)
- [Requisitos técnicos](./requisitos-tecnicos.md)
- [Dicas gerais](./dicas.md)