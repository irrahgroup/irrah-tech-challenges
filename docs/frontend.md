# Desafio Frontend - BCB

Como desenvolvedor frontend, seu desafio principal será implementar um **dashboard interativo com visualizações de dados**. Abaixo estão os detalhes do que deve ser implementado, dividido em partes progressivas.

## Desafio: Dashboard Interativo

### Parte 1: Funcionalidades Essenciais
- **Interfaces básicas**:
  - Tela simples para identificação do cliente (CPF/CNPJ)
  - Formulário para envio de mensagens
  - Listagem simples de mensagens enviadas
  - Exibição básica de saldo

- **Mocks simples**:
  - Dados estáticos (JSON)
  - Simulação básica de respostas da API

### Parte 2: Aprimoramentos
- **Autenticação simplificada**:
  - Armazenamento do identificador do cliente (CPF/CNPJ) em localStorage/sessionStorage
  - Inclusão automática deste identificador nas requisições à API
  - Feedback visual do cliente logado

- **Visualização de dados**:
  - Dashboard com pelo menos um gráfico (ex: mensagens por status)
  - Lista paginada de mensagens com filtros simples
  - Design responsivo (desktop/mobile)

### Parte 3: Recursos Adicionais
- **Dashboard completo**:
  - Múltiplos gráficos e KPIs
  - Filtros avançados e ordenação
  - Funcionalidades para cancelar/promover mensagens

- **Tempo real**:
  - Atualização automática dos dados (simule com setInterval)
  - Indicadores de loading durante operações
  - Notificações para eventos importantes

> **Nota sobre mocks**: Para o perfil frontend, você pode usar dados simulados em vez de um backend real. Use ferramentas como JSON Server, ou simplesmente funções que simulem chamadas de API.

> **Nota sobre pagamento**: Implemente apenas uma versão simplificada do sistema de pagamento - exibir saldo atual e registrar transações básicas é suficiente.

> **Dica**: Comece pela Parte 1 e avance conforme o tempo. É melhor ter funcionalidades essenciais bem implementadas do que muitas funcionalidades incompletas.

## Entregas Mínimas

Como desenvolvedor frontend, você deve entregar no mínimo:
- Tela para identificação do cliente (CPF/CNPJ)
- Interface para envio de mensagens
- Visualização de saldo/histórico
- Design responsivo básico

## Tecnologias Recomendadas

Para o desenvolvimento frontend, sugerimos:
- Framework: React ou Angular
- Design responsivo para web e mobile
- Bibliotecas de gráficos (ex: Chart.js, D3.js, Recharts)
- JSON Server ou similar para mocks (opcional)

## Diferenciais

Para se destacar, considere implementar:
- Testes unitários e de componentes
- Animações e transições fluidas
- Design system/componentes reutilizáveis
- PWA (Progressive Web App)
- Acessibilidade

Lembre-se de consultar também:
- [Regras de negócio](./regras-negocio.md)
- [Requisitos técnicos](./requisitos-tecnicos.md)
- [Dicas gerais](./dicas.md)