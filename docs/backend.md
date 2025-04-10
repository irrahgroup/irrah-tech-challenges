# Desafio Backend - BCB

Como desenvolvedor backend, seu desafio principal será implementar um **sistema de fila com priorização de mensagens**. Abaixo estão os detalhes do que deve ser implementado, dividido em partes progressivas.

## Desafio: Sistema de Priorização de Mensagens

### Parte 1: Funcionalidades Essenciais
- **API básica**:
  - Endpoints CRUD simples para clientes
  - Endpoint para envio de mensagem
  - Validação básica de saldo
  - Identificação do cliente via parâmetro na requisição (ex: clientId)

- **Processamento de mensagens (síncrono)**:
  - Armazenamento de mensagens em uma lista/tabela
  - Endpoint para visualizar mensagens enviadas
  - Processamento síncrono (mesmo request/response)
  - Simulação de envio: log das mensagens processadas

### Parte 2: Aprimoramentos
- **Autenticação simplificada**:
  - Identificação do cliente via token/header (ex: CPF/CNPJ em base64 no header "X-Client-Id")
  - Middleware para validar e associar requisições ao cliente correto

- **Processamento de mensagens (com fila)**:
  - Implementação de fila com dois níveis (Normal/Urgente)
  - Lógica para processar mensagens urgentes primeiro
  - Processamento ainda síncrono, mas com estrutura de fila
  - Simulação com delay e atualização de status

### Parte 3: Recursos Adicionais
- **Worker em background**:
  - Thread/processo separado para processar a fila
  - Execução contínua em background
  - Sistema de status (enfileirada, processando, enviada)

- **Monitoramento**:
  - Endpoints para estatísticas da fila
  - Tratamento de falhas e recuperação
  - Serviço mock com simulação de sucessos/falhas

> **Dica**: Comece pela Parte 1 e avance conforme o tempo disponível. Uma boa implementação da Parte 1 já é suficiente para a avaliação.

## Entregas Mínimas

Como desenvolvedor backend, você deve entregar no mínimo:
- API de CRUD para clientes
- Endpoint para envio de mensagens com validação
- Identificação do cliente via parâmetro ou header
- Implementação de pelo menos um tipo de plano
- Processamento síncrono de mensagens (sem fila assíncrona)

## Tecnologias Recomendadas

Para o desenvolvimento backend, sugerimos:
- Linguagens: **Java** (Spring Boot), **Node.js** (NestJS/Express) ou **Go** (Gin/Echo/Fiber)
- Banco de dados: PostgreSQL (preferência), MySQL, MongoDB ou outro à sua escolha
- Docker para containerização

## Diferenciais

Para se destacar, considere implementar:
- Testes unitários e de integração
- Documentação da API (Swagger/OpenAPI)
- Tratamento avançado de erros
- Monitoramento e logging
- CI/CD

Lembre-se de consultar também:
- [Regras de negócio](./regras-negocio.md)
- [Requisitos técnicos](./requisitos-tecnicos.md)
- [Dicas gerais](./dicas.md)