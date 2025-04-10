# Desafio Fullstack - BCB

Como desenvolvedor fullstack, seu desafio principal será implementar uma **aplicação equilibrada de chat** combinando frontend e backend de forma integrada. Este desafio foi calibrado para permitir que você demonstre habilidades em ambas as camadas, com foco na integração.

## Desafio: Aplicação Completa de Chat

### Parte 1: Funcionalidades Essenciais
- **Backend core**:
  - API com endpoints essenciais:
    - Autenticação e gerenciamento básico de usuários
    - Sistema de mensagens com fila simples (array ordenado)
    - Armazenamento e recuperação de conversas

- **Frontend core**:
  - Interface de login/identificação
  - Lista de conversas com indicadores visuais básicos
  - Tela de chat com histórico e campo de envio
  - Design responsivo simples (mobile/desktop)

- **Integração fundamental**:
  - Fluxo completo de dados bidirecional
  - Autenticação básica integrada
  - Atualização dos dados após operações

### Parte 2: Melhorias Equilibradas (escolha duas)
- **Backend (escolha uma)**:
  - Implementação de fila com prioridade (normal/urgente)
  - Sistema básico de validação financeira (pré/pós-pago)
  - Persistência de dados em banco (em vez de memória)

- **Frontend (escolha uma)**:
  - Status visuais de mensagens (enviada, entregue, lida)
  - Indicadores de digitação ou presença online
  - Filtros e busca no histórico de conversas

### Parte 3: Infraestrutura e Qualidade (opcional)
- **Escolha apenas uma destas opções**:
  - Docker para execução simplificada do projeto completo
  - Testes básicos em ambas as camadas
  - Documentação da API (Swagger) e componentes

> **Importante para Fullstack**: Diferente do perfil Frontend (onde você pode mockar o backend), aqui você deve implementar um backend real que se integre ao frontend. O foco principal da avaliação será esta integração.

> **Dica**: Priorize ter um fluxo completo funcionando (mesmo que simples) antes de adicionar recursos avançados. É melhor ter um sistema básico totalmente integrado do que partes complexas desconectadas.

## Entregas Mínimas

Como desenvolvedor fullstack, você deve entregar:

**Backend (40% da avaliação)**:
- APIs funcionais para autenticação e mensagens
- Estrutura de dados para armazenamento ordenado de mensagens (fila simples)
- Persistência de dados (memória ou banco)

**Frontend (40% da avaliação)**:
- Interface de chat com troca de mensagens
- Lista de conversas navegável
- Design responsivo básico

**Integração (20% da avaliação)**:
- Fluxo completo: login → listar conversas → enviar/receber mensagens
- Sincronização de dados entre camadas
- Tratamento básico de estados (carregando, erro, sucesso)

**Nota importante**: O desafio foi desenhado para permitir demonstrar habilidades equilibradas entre frontend e backend. A avaliação levará em conta a qualidade da implementação em ambas as camadas, com ênfase especial na integração entre elas.

## Especificações Técnicas

### Arquitetura Sugerida

```
+------------------+          +------------------+
|     FRONTEND     |          |     BACKEND      |
| +---------------+|          | +---------------+|
| |   Interface   ||  REST    | |     APIs      ||
| | +-----------+ ||  API     | | +-----------+ ||
| | |   UI      | ||<-------->| | |Controllers| ||
| | +-----------+ ||          | | +-----------+ ||
| |               ||          | |       |       ||
| | +-----------+ ||          | | +-----------+ ||
| | |   Estado  | ||          | | |  Serviços | ||
| | +-----------+ ||          | | +-----------+ ||
| +---------------+|          | |       |       ||
+------------------+          | | +-----------+ ||
                              | | |   Filas   | ||
                              | | +-----------+ ||
                              | |       |       ||
                              | | +-----------+ ||
                              | | |    BD     | ||
                              | | +-----------+ ||
                              | +---------------+|
                              +------------------+
```

### Fluxo de Integração

```
Frontend                               Backend
   |                                      |
   |-- POST /auth {documentId, type} ---->|
   |<-- {token, client} -----------------|
   |                                      |
   |-- GET /conversations -------------->|
   |    Authorization: Bearer {token}     |
   |<-- [{id, recipientName, ...}] ------|
   |                                      |
   |-- GET /conversations/{id}/messages ->|
   |    Authorization: Bearer {token}     |
   |<-- [{id, content, status, ...}] -----|
   |                                      |
   |-- POST /messages ------------------>|
   |    {conversationId, content, ...}    |
   |<-- {id, status: 'queued', cost} -----|
   |                                      |   +-----------------+
   |                                      |-->| Fila de Mensagens|
   |                                      |   | - Normal        |
   |                                      |   | - Urgente       |
   |                                      |<--| Worker Process  |
   |                                      |   +-----------------+
   |                                      |
   |<-- WebSocket/Polling: status='sent' -|
```

### Interface de Integração

```typescript
// Interfaces de comunicação entre frontend e backend

// 1. Autenticação
interface AuthRequest {
  documentId: string;         // CPF ou CNPJ
  documentType: 'CPF' | 'CNPJ';
}

interface AuthResponse {
  token: string;             // Token de identificação simples
  client: {
    id: string;              // Identificador do cliente
    name: string;            // Nome do cliente
    documentId: string;      // CPF ou CNPJ do cliente
    documentType: 'CPF' | 'CNPJ';
    balance?: number;        // Saldo para pré-pago
    limit?: number;          // Limite para pós-pago
    planType: 'prepaid' | 'postpaid';
    active: boolean;
  };
}

// 2. Conversas
interface ConversationResponse {
  id: string;
  recipientId: string;
  recipientName: string;
  lastMessageContent: string;
  lastMessageTime: string;
  unreadCount: number;
}

// 3. Mensagens
interface SendMessageRequest {
  conversationId: string;     // ID da conversa existente
  recipientId?: string;       // Para novas conversas
  content: string;
  priority: 'normal' | 'urgent';
}

interface SendMessageResponse {
  id: string;
  status: 'queued';
  timestamp: string;
  estimatedDelivery: string;
  cost: number;
  currentBalance?: number;    // apenas para pré-pago
}

interface MessageResponse {
  id: string;
  conversationId: string;
  content: string;
  sentBy: {
    id: string;
    type: 'client' | 'user';
  };
  timestamp: string;
  priority: 'normal' | 'urgent';
  status: 'queued' | 'processing' | 'sent' | 'delivered' | 'read' | 'failed';
  cost: number;
}

// Observação: Você deve implementar um serviço de integração que gerencie a comunicação
// entre o frontend e o backend. As principais funcionalidades a serem implementadas são:
//
// - Autenticação do cliente
// - Obtenção das conversas do cliente autenticado
// - Envio de novas mensagens
// - Obtenção das mensagens de uma conversa específica
//
// Use as interfaces acima como guia para os tipos de dados esperados nas requisições e respostas.
```

## Tecnologias Recomendadas

Para o desenvolvimento fullstack, sugerimos:

**Backend**:
- Linguagens: **Java** (Spring Boot), **Node.js** (NestJS/Express) ou **Go** (Gin/Echo/Fiber)
- Banco de dados: PostgreSQL (preferência), MySQL, MongoDB ou outro à sua escolha

**Frontend**:
- Framework: React ou Angular
- Design responsivo para web e mobile

**Integração**:
- Docker e docker-compose para orquestração
- REST API ou GraphQL para comunicação

## Critérios de Avaliação Detalhados

Sua implementação fullstack será avaliada com base em três dimensões principais:

| Dimensão | Peso | O que será avaliado | 
|----------|------|---------------------|
| **Backend** | 40% | Implementação da API, estrutura de fila, validações, tratamento de dados |
| **Frontend** | 40% | Interface do usuário, componentização, gestão de estado, experiência |
| **Integração** | 20% | Comunicação entre camadas, consistência, fluxo de dados, tratamento de erros |

### Critérios específicos por dimensão:

**Backend (40%)**:
- Qualidade da implementação da fila simples (15%)
- Design e implementação das APIs (10%)
- Implementação das regras de negócio (10%) 
- Organização do código e estrutura do projeto (5%)

**Frontend (40%)**:
- Design e usabilidade da interface (15%)
- Componentização e estrutura do código (10%)
- Gerenciamento de estado e fluxo de dados (10%)
- Tratamento de estados de UI (loading, error, success) (5%)

**Integração (20%)**:
- Comunicação eficiente entre camadas (10%)
- Consistência de dados entre frontend e backend (5%)
- Tratamento de erros na comunicação (5%)

### Exemplos por nível de complexidade:

**Implementação básica (Parte 1)**:
- Backend com APIs funcionais e fila simples
- Frontend seguindo o wireframe e com funcionalidades básicas
- Integração direta com tratamento básico de erros

**Implementação intermediária (Parte 2)**:
- Backend com APIs bem estruturadas e fila com priorização
- Frontend com componentes reutilizáveis e estado bem gerenciado
- Integração robusta com tratamento adequado de todos os estados

**Implementação avançada (Parte 3)**:
- Backend com arquitetura sólida, fila otimizada e tratamento de edge cases
- Frontend com arquitetura escalável, componentização avançada e ótima UX
- Integração perfeita com abstrações elegantes e tratamento completo

## Diferenciais

Para se destacar, considere implementar:
- Testes unitários em ambas as camadas (backend e frontend)
- Docker configurado corretamente para todo o ambiente
- Documentação detalhada da API (Swagger/OpenAPI)
- README bem estruturado com instruções claras
- Código limpo com padrões consistentes em todo o projeto

Lembre-se de consultar também:
- [Regras de negócio](./regras-negocio.md)
- [Requisitos técnicos](./requisitos-tecnicos.md)
- [Dicas gerais](./dicas.md)