# PRD - Modulo Checkout

## Objetivo

Criar um modulo de checkout simples e seguro para finalizar compras no marketplace ReuseTech, permitindo que o usuario revise os itens selecionados, confirme seus dados e realize o pagamento exclusivamente via PIX.

## Escopo

O modulo deve permitir:

- Visualizar resumo do pedido.
- Confirmar dados do comprador.
- Confirmar endereco de entrega, quando aplicavel.
- Gerar pagamento via PIX.
- Exibir status basico do pagamento.
- Confirmar pedido apos pagamento aprovado.

Fora do escopo inicial:

- Cartao de credito.
- Boleto.
- Parcelamento.
- Cupons de desconto.
- Multiplos enderecos por usuario.
- Reembolso automatizado.

## Personas

### Comprador

Usuario que deseja adquirir produtos usados ou recondicionados de tecnologia com uma experiencia simples, objetiva e confiavel.

Necessidades principais:

- Entender claramente o valor total da compra.
- Finalizar o pedido com poucos passos.
- Pagar via PIX sem confusao.
- Receber confirmacao do pedido.

### Administrador

Pessoa responsavel por acompanhar pedidos e validar se o fluxo de compra esta funcionando corretamente.

Necessidades principais:

- Consultar pedidos criados.
- Verificar status de pagamento.
- Identificar falhas no processo de checkout.

## Regras Basicas de Pagamento

- O checkout deve aceitar apenas pagamento via PIX.
- Nao devem ser exibidas opcoes de cartao, boleto ou parcelamento.
- O pedido so deve ser confirmado apos identificacao de pagamento aprovado.
- O valor do PIX deve ser igual ao total do pedido.
- O usuario deve conseguir copiar o codigo PIX copia e cola.
- Quando disponivel, o checkout deve exibir QR Code PIX.
- O pagamento deve possuir tempo limite de validade.
- Caso o pagamento expire, o pedido deve ficar com status de pagamento expirado.
- Caso o pagamento seja aprovado, o pedido deve ficar com status de pagamento aprovado.
- Caso haja falha na geracao do PIX, o usuario deve receber uma mensagem clara e poder tentar novamente.

## Fluxo Principal

1. Usuario acessa o carrinho.
2. Usuario revisa produtos, quantidades e valor total.
3. Usuario avanca para checkout.
4. Usuario confirma seus dados.
5. Sistema gera pagamento PIX.
6. Usuario realiza pagamento.
7. Sistema identifica pagamento aprovado.
8. Sistema confirma o pedido.
9. Usuario visualiza confirmacao da compra.

## Status do Pedido

- `aguardando_pagamento`: pedido criado e PIX gerado.
- `pagamento_aprovado`: pagamento PIX confirmado.
- `pagamento_expirado`: PIX expirado sem pagamento.
- `cancelado`: pedido cancelado manualmente ou por falha de processo.

## Criterios de Aceite

- O usuario consegue finalizar uma compra usando somente PIX.
- O checkout nao mostra outros meios de pagamento.
- O usuario consegue copiar o codigo PIX.
- O pedido nao e confirmado antes do pagamento aprovado.
- O sistema atualiza o status do pedido conforme o retorno do pagamento.
- Mensagens de erro sao claras em caso de falha na geracao ou confirmacao do PIX.
