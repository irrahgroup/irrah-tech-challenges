# Desafio Fullstack - BCB

Como desenvolvedor fullstack, seu desafio principal será implementar a **integração completa entre backend e frontend**. Abaixo estão os detalhes do que deve ser implementado, dividido em partes progressivas.

## Desafio: Integração Completa

### Parte 1: Funcionalidades Essenciais
- **Backend básico**:
  - API REST para clientes (pelo menos listar e criar)
  - Endpoint simples para envio de mensagens
  - Armazenamento básico em banco de dados

- **Frontend básico**:
  - Interface de login conectada ao backend
  - Formulário de envio de mensagens funcional
  - Listagem básica de mensagens do usuário

- **Integração**:
  - Comunicação básica entre frontend e backend
  - Fluxo completo: login → enviar mensagem → listar mensagens

### Parte 2: Aprimoramentos
- **Ampliando funcionalidades**:
  - Backend: Implementação de pré/pós-pago e validações
  - Frontend: Dashboard simples com pelo menos um gráfico
  - Tratamento de erros e estados de loading

- **Escolha um foco**:
  - Implementar o sistema de fila simples no backend, OU
  - Desenvolver visualizações mais completas no frontend

### Parte 3: Recursos Adicionais
- **Recursos avançados**:
  - Implementação completa de um dos desafios principais
  - Tratamento avançado de estados e erros
  - Docker configurado corretamente para o ambiente completo

> **Importante para Fullstack**: Diferente do perfil Frontend (onde você pode mockar o backend), aqui você deve implementar um backend real que se integre ao frontend. O foco principal da avaliação será esta integração.

> **Dica**: Priorize ter um fluxo completo funcionando (mesmo que simples) antes de adicionar recursos avançados. É melhor ter um sistema básico totalmente integrado do que partes complexas desconectadas.

## Entregas Mínimas

Como desenvolvedor fullstack, você deve entregar no mínimo:
- Implementação básica de backend e frontend
- Fluxo completo de seleção de cliente e envio de mensagem
- Comunicação eficiente entre as camadas

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

## Diferenciais

Para se destacar, considere implementar:
- Testes em ambas as camadas
- CI/CD para integração contínua
- Documentação da API
- Monitoramento e logging
- Deployment automatizado

Lembre-se de consultar também:
- [Regras de negócio](./regras-negocio.md)
- [Requisitos técnicos](./requisitos-tecnicos.md)
- [Dicas gerais](./dicas.md)