# Requisitos Técnicos - BCB

Este documento detalha os requisitos técnicos e orientações para entrega do projeto BCB.

## Tecnologias

### Backend
- Linguagens: **Java**, **Node.js** ou **Go**
- Frameworks sugeridos:
  - Java: Spring Boot, Spring Data
  - Node.js: NestJS, Express, TypeScript
  - Go: Gin, Echo, Fiber
- Banco de dados: PostgreSQL (preferência), MySQL, MongoDB ou outro à sua escolha

### Frontend
- Framework: React ou Angular
- Design responsivo para web e mobile
- Para candidatos frontend: Você pode usar dados mockados (não precisa implementar backend real)

## O Que Entregar (Mínimo Necessário)

### Para todos os perfis:
- Repositório Git com a solução
- Docker-compose para executar o projeto
- README com instruções de execução

### Backend (mínimo):
- API de CRUD para clientes
- Endpoint para envio de mensagens com validação
- Identificação do cliente via parâmetro ou header
- Implementação de pelo menos um tipo de plano
- Processamento síncrono de mensagens (sem fila assíncrona)

### Frontend (mínimo):
- Tela para identificação do cliente (CPF/CNPJ)
- Interface para envio de mensagens
- Visualização de saldo/histórico
- Design responsivo básico

### Fullstack (mínimo):
- Implementação básica de backend e frontend
- Fluxo completo de seleção de cliente e envio de mensagem
- Comunicação eficiente entre as camadas

## Instruções para Entrega

### 1. Documentação:
   - README.md com:
     - Descrição do projeto
     - Premissas assumidas
     - Tecnologias utilizadas
     - Passo a passo para execução

### 2. Docker:
   - Inclua docker-compose.yml para orquestrar todos os serviços
   - Garanta que possamos executar com:
   ```
   git clone seu-repositorio
   cd seu-repositorio
   docker-compose up
   ```

### 3. Organização:
   - Estrutura clara de pastas
   - Separação de responsabilidades
   - Código limpo e comentado onde necessário

## Diferenciais (Bônus)

Escolha um ou mais itens para se destacar:

- **Técnicos**: Testes, Swagger, CI/CD
- **Funcionais**: Implementação completa do desafio principal, dashboard avançado, notificações
- **Arquiteturais**: Cache, estratégias de retry, logs/monitoramento

## Critérios de Avaliação

Avaliaremos principalmente:

1. **Qualidade e organização do código**
2. **Implementação correta das regras de negócio**
3. **Execução do desafio principal do seu perfil**
4. **Decisões técnicas e arquiteturais**

Na entrevista de live-coding, você explicará sua solução e faremos pequenas alterações para avaliar seu raciocínio em tempo real.

**Importante**: Priorizamos qualidade sobre quantidade. Uma solução parcial bem estruturada é melhor que uma solução completa desorganizada.