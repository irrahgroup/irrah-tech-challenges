# Desafio Frontend - BCB

Como desenvolvedor frontend, seu desafio principal será implementar uma **interface de chat interativa** para a plataforma BCB. Abaixo estão os detalhes do que deve ser implementado, dividido em partes progressivas.

## Desafio: Interface de Chat

### Parte 1: Funcionalidades Essenciais
- **Interface de chat básica**:
  - Tela de identificação do cliente (CPF/CNPJ)
  - Lista de conversas recentes
  - Tela de chat com histórico de mensagens (estilo bolhas)
  - Campo para digitação e envio de novas mensagens
  - Exibição de saldo disponível

- **Mocks simples**:
  - Dados estáticos (JSON)
  - Simulação básica de respostas da API

### Parte 2: Aprimoramentos
- **Autenticação simplificada**:
  - Armazenamento básico do identificador do cliente
  - Exibição de informações do perfil
  - Feedback visual após envio de mensagens

- **Recursos de chat**:
  - Diferenciação visual entre mensagens normais e urgentes
  - Indicadores de status (enviada, lida, erro)
  - Design responsivo (desktop/mobile)
  - Busca simples nas conversas

### Parte 3: Recursos Adicionais
- **Funcionalidades extra**:
  - Lista de contatos com últimas mensagens e status
  - Notificações para novas mensagens
  - Indicador de digitação ("escrevendo...")
  - Visualização de histórico de consumo/saldo

- **Experiência aprimorada**:
  - Atualizações automáticas (simulação de tempo real)
  - Animações suaves de transição
  - Opções básicas de formatação de texto

> **Nota sobre mocks**: Para o perfil frontend, você pode usar dados simulados em vez de um backend real. Use ferramentas como JSON Server, ou simplesmente funções que simulem chamadas de API.

> **Nota sobre pagamento**: Implemente apenas uma versão simplificada do sistema de pagamento - exibir saldo atual e registrar transações básicas é suficiente.

> **Dica**: Comece pela Parte 1 e avance conforme o tempo. É melhor ter funcionalidades essenciais bem implementadas do que muitas funcionalidades incompletas.

## Entregas Mínimas

Como desenvolvedor frontend, você deve entregar no mínimo:
- Tela para identificação do cliente (CPF/CNPJ)
- Lista de conversas recentes
- Interface de chat com histórico e campo de envio
- Indicador de saldo disponível
- Design responsivo básico

## Especificações Técnicas

### Wireframes das Telas Principais

**1. Tela de Login**
```
┌─────────────────────────────┐
│        Big Chat Brasil      │
│                             │
│   ┌─────────────────────┐   │
│   │ CPF/CNPJ            │   │
│   └─────────────────────┘   │
│                             │
│   ┌─────────────────────┐   │
│   │ Tipo: ○ PF  ● PJ    │   │
│   └─────────────────────┘   │
│                             │
│   ┌─────────────────────┐   │
│   │       Entrar        │   │
│   └─────────────────────┘   │
│                             │
└─────────────────────────────┘
```

**2. Lista de Conversas**
```
┌─────────────────────────────┐
│ Empresa ABC    [Saldo: R$50]│
├─────────────────────────────┤
│ 🔍 Buscar...                │
├─────────────────────────────┤
│ Maria Oliveira         9:30 │
│ Olá, como vai?              │
├─────────────────────────────┤
│ Carlos Pereira      ●  Ontem│
│ Poderia me ajudar com...    │
├─────────────────────────────┤
│ Ana Costa             14/07 │
│ Boa tarde, gostaria de...   │
├─────────────────────────────┤
│ Pedro Santos           14/07│
│ Obrigado pelo atendim...    │
├─────────────────────────────┤
│                             │
│     [+ Nova Conversa]       │
└─────────────────────────────┘
```

**3. Interface de Chat**
```
┌─────────────────────────────┐
│ ← Maria Oliveira     ⋮      │
├─────────────────────────────┤
│                             │
│  ┌───────────────────────┐  │
│  │ Olá, como vai?        │  │
│  │ 9:30               ✓✓ │  │
│  └───────────────────────┘  │
│                             │
│         ┌──────────────┐    │
│         │ Tudo bem!    │    │
│         │ 9:32         │    │
│         └──────────────┘    │
│                             │
│  ┌───────────────────────┐  │
│  │ Estou com dúvidas     │  │
│  │ sobre o produto X.    │  │
│  │ 9:33               ✓  │  │
│  └───────────────────────┘  │
│                             │
│                             │
│                             │
├─────────────────────────────┤
│ ┌───┐  Mensagem...      ⚡ ▶ │
└─────────────────────────────┘
```

### Estados e Componentes

```typescript
// Modelo de dados para o frontend alinhado com o backend

// Cliente (empresa que usa o sistema)
interface Client {
  id: string;
  name: string;
  documentId: string;      // CPF ou CNPJ
  documentType: 'CPF' | 'CNPJ';
  planType: 'prepaid' | 'postpaid';
  balance?: number;        // saldo (para pré-pago)
  limit?: number;          // limite (para pós-pago)
  active: boolean;
}

// Conversa entre empresa e usuário
interface Conversation {
  id: string;
  recipientId: string;     // ID do destinatário
  recipientName: string;   // Nome do destinatário (ex: Maria Silva)
  lastMessageContent: string;
  lastMessageTime: Date;
  unreadCount: number;
}

// Mensagem individual
interface Message {
  id: string;
  conversationId: string;  // ID da conversa à qual pertence
  content: string;
  sentBy: {               // Dados de quem enviou
    id: string,           // ID do remetente (cliente ou usuário)
    type: 'client' | 'user' // Tipo de remetente
  };
  timestamp: Date;
  priority: 'normal' | 'urgent';
  status: 'queued' | 'processing' | 'sent' | 'delivered' | 'read' | 'failed';
  cost?: number;           // custo da mensagem
}

// Observação: Você deve implementar os componentes necessários para exibir mensagens, 
// como bolhas de chat que mostram o conteúdo da mensagem, horário, status e prioridade.
// Fique livre para usar qualquer abordagem que preferir para implementar a interface
// desde que atenda aos requisitos funcionais.

// Observação: Para obter conversas e mensagens, use as interfaces definidas acima
// para implementar sua lógica de comunicação com o backend ou mock de dados.
```

### Fluxo de Interação
```
┌────────┐     ┌─────────────────┐     ┌───────────────┐     ┌─────────────┐
│ Login  │────>│ Lista Conversas │────>│ Conversa Chat │────>│ Enviar Msg  │
└────┬───┘     └─────┬───────┬───┘     └───────┬───────┘     └─────┬───────┘
     │               │       │                 │                   │
     │               │       v                 │                   v
     │               │   ┌─────────┐           │             ┌───────────┐
     │               │   │ Filtros │           │             │ Validação │
     v               v   └─────────┘           v             └───────────┘
┌────────┐     ┌─────────────┐         ┌───────────────┐          │
│ Logout │<────┤ Preferências│<────────┤ Detalhes Msg  │<─────────┘
└────────┘     └─────────────┘         └───────────────┘
                                             ^
                                             │
                                        ┌────┴────────┐
                                        │ Notificações│
                                        │ (Status Msg)│
                                        └─────────────┘
```

## Tecnologias Recomendadas

Para o desenvolvimento frontend, sugerimos:
- Framework: React ou Angular
- Design responsivo para web e mobile
- Bibliotecas de gestão de estado (Redux, MobX, Context API)
- JSON Server ou similar para mocks (opcional)

## Critérios de Avaliação Detalhados

Sua implementação frontend será avaliada nos seguintes aspectos:

| Critério | Peso | O que será avaliado | 
|----------|------|---------------------|
| **Interface de usuário** | 30% | Design visual, usabilidade, responsividade, consistência com o wireframe |
| **Estrutura e componentes** | 25% | Componentização, reutilização, organização do código, padrões de projeto |
| **Gerenciamento de estado** | 20% | Fluxo de dados, gestão do estado da aplicação, comunicação com API |
| **Experiência do usuário** | 15% | Feedback visual, tratamento de erros, estados de carregamento, transições |
| **Código e performance** | 10% | Legibilidade, boas práticas, otimizações, tempo de carregamento |

### Exemplos por nível de complexidade:

**Implementação básica (Parte 1)**:
- Interface funcional seguindo o wireframe básico
- Componentes simples mas funcionais
- Gerenciamento de estado básico (useState/props)
- Indicadores simples de carregamento e erro
- Código limpo e organizado

**Implementação intermediária (Parte 2)**:
- Interface com design responsivo completo e elementos visuais consistentes
- Componentes reutilizáveis com props bem definidas
- Gerenciamento de estado mais sofisticado (Context API, Redux)
- Tratamento completo de estados de UI (loading, error, empty, success)
- Organização de código em módulos/features

**Implementação avançada (Parte 3)**:
- Interface polida com detalhes de UX avançados (micro-interações, transições)
- Sistema de componentes modular com estilização temática
- Arquitetura de estado otimizada, com cache e controle fino de renderizações
- Tratamento avançado de experiência, incluindo otimizações de performance
- Padrões arquiteturais avançados e hooks customizados

## Diferenciais

Para se destacar, considere implementar:
- Testes unitários e de componentes com boa cobertura
- Animações e transições fluidas que enriqueçam a experiência
- Design system completo com componentes reutilizáveis
- Recursos de acessibilidade (ARIA, contraste, navegação por teclado)
- Performance otimizada (lazy loading, memoização, code splitting)

Lembre-se de consultar também:
- [Regras de negócio](./regras-negocio.md)
- [Requisitos técnicos](./requisitos-tecnicos.md)
- [Dicas gerais](./dicas.md)