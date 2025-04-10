# Regras de Negócio - BCB (Big Chat Brasil)

Este documento detalha as principais regras de negócio da plataforma BCB.

## Visão Geral do Sistema

O **BCB** é uma plataforma de chat para comunicação entre empresas e seus clientes finais, similar a aplicativos populares de mensagens, com:
- Cadastro de empresas clientes (PF/PJ)
- Conversas individuais com clientes finais
- Dois tipos de plano de pagamento: pré-pago e pós-pago
- Dois níveis de prioridade de mensagens: normal (R$0,25) e urgente (R$0,50)
- Interface interativa de chat com histórico de conversas

## Principais Regras de Negócio

### 1. Clientes e Planos
- Clientes podem ser pessoa física (CPF) ou jurídica (CNPJ)
- Cada cliente tem um plano (pré ou pós-pago) e status (ativo/inativo)

### 2. Envio de Mensagens
- Mensagens contêm: destinatário, texto e tipo (SMS/WhatsApp)
- Cada mensagem tem custo fixo (normal: R$0,25, urgente: R$0,50)
- Ciclo de vida: enfileirada → processando → enviada (ou falha)
- Sistema registra data/hora, status e cliente que solicitou

### 3. Sistema de Pagamento

#### Pré-pago
- Cliente precisa ter saldo suficiente antes do envio
- **Validação**: Sistema verifica saldo → debita valor → registra transação → enfileira mensagem
- *Exemplo*: Cliente com R$10 de saldo envia 5 mensagens normais (R$1,25) → Saldo final: R$8,75
  
#### Pós-pago
- Cliente tem limite mensal de consumo (zerado no início de cada mês)
- **Validação**: Sistema verifica limite → registra consumo → atualiza limite → enfileira mensagem
- *Exemplo*: Cliente com limite R$50/mês já usou R$40 → Envia 10 mensagens (R$2,50) → Limite restante: R$7,50

### 4. Administração
- Adicionar créditos (pré-pago) ou ajustar limites (pós-pago)
- Consultar saldo/consumo dos clientes
- Converter entre planos (com tratamento de saldo residual ou consumo pendente)
- Manter histórico de transações financeiras

## Priorização de Mensagens

Em um contexto mais avançado, o sistema deve suportar diferentes níveis de prioridade:

- **Mensagens normais**: Custo de R$0,25, processadas em ordem FIFO
- **Mensagens urgentes**: Custo de R$0,50, processadas prioritariamente

A implementação da priorização varia conforme o perfil (backend/frontend/fullstack) e está detalhada nos documentos específicos.