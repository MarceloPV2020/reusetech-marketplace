# Prompts do Projeto ReUseTech

Registro resumido dos prompts usados na construção inicial do projeto.

## ADR da Arquitetura

Criar `docs/adr.md` com uma ADR para o marketplace ReUseTech, incluindo:

- contexto do projeto;
- decisão arquitetural;
- stack recomendada;
- justificativa;
- alternativas consideradas;
- consequências positivas e negativas;
- estrutura inicial de pastas.

Arquitetura sugerida: monólito modular para MVP, com Node.js, Express, SQLite/PostgreSQL e frontend simples com HTML e Tailwind CSS.

## Diagramas Conceituais

Criar `docs/Diagramas.md` com dois diagramas em Mermaid:

- diagrama ER conceitual com `Usuario`, `Produto`, `Pedido` e `ItemPedido`;
- fluxo do usuário da home até a criação do pedido.

Relacionamentos principais:

- um usuário cadastra vários produtos;
- um usuário realiza vários pedidos;
- um pedido possui vários itens;
- cada item aponta para um produto.

## Mockup da Home Page

Criar `index.html` para a home page do ReUseTech usando apenas HTML e Tailwind via CDN.

A página deve conter:

- header com logo e links;
- seção hero;
- barra de busca;
- botões para buscar produtos e anunciar eletrônico;
- cards de produtos usados;
- seção "Como funciona";
- rodapé.

Produtos de exemplo:

- iPhone 12 usado;
- Notebook Dell i5;
- PlayStation 4;
- Samsung Galaxy S21.

## Commits Iniciais

Criar commits semânticos para:

- ADR da arquitetura inicial;
- diagramas conceituais;
- mockup inicial da home page;
- README inicial.

## PRD do Checkout

Criar `docs/PRD_CHECKOUT.md` com um PRD enxuto para o módulo Checkout, incluindo:

- objetivo;
- personas;
- regras básicas de pagamento;
- aceite exclusivo de PIX;
- fluxo principal;
- critérios de aceite.
