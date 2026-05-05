# ADR: Arquitetura inicial do ReUseTech

## 1. Titulo

Definicao da arquitetura inicial para o marketplace ReUseTech.

## 2. Contexto

O ReUseTech sera um marketplace simplificado para compra e venda de eletronicos usados, inspirado em experiencias enxutas como OLX e Mercado Livre. Nesta primeira etapa, o objetivo principal e construir um MVP funcional, de facil manutencao e com baixa complexidade operacional.

O sistema deve atender aos seguintes fluxos principais:

- Cadastro e autenticacao de usuarios.
- Cadastro, listagem e visualizacao de produtos usados.
- Carrinho de compras simples.
- Fluxo basico de checkout.

Como o projeto ainda esta em fase inicial, a arquitetura deve favorecer velocidade de desenvolvimento, clareza de organizacao e facilidade para evoluir sem exigir infraestrutura distribuida ou custos operacionais altos.

## 3. Decisao arquitetural

A arquitetura recomendada para o MVP sera um monolito modular.

O backend ficara concentrado em uma unica aplicacao Node.js com Express, organizada por modulos de dominio, como usuarios, produtos, carrinho e checkout. Cada modulo devera concentrar suas rotas, regras de negocio e acesso a dados relacionados.

O frontend inicial sera simples, utilizando HTML, Tailwind CSS e JavaScript leve quando necessario. A renderizacao pode comecar de forma estatica ou com templates simples servidos pelo proprio backend, evitando a introducao precoce de frameworks SPA.

O banco de dados recomendado para desenvolvimento inicial e SQLite, pela simplicidade de configuracao. Para uma evolucao proxima de producao, PostgreSQL deve ser adotado como banco principal, mantendo a modelagem relacional.

## 4. Stack tecnologica recomendada

- Runtime: Node.js.
- Framework backend: Express.
- Banco de dados inicial: SQLite.
- Banco recomendado para producao: PostgreSQL.
- ORM ou query builder: Prisma ou Knex.
- Frontend inicial: HTML, Tailwind CSS e JavaScript.
- Autenticacao: sessoes com cookies HTTP-only ou JWT simples, conforme a necessidade do MVP.
- Validacao de dados: Zod ou Joi.
- Testes: Jest ou Vitest para testes unitarios e de integracao.
- Controle de versao: Git.
- Documentacao: Markdown dentro da pasta `docs`.

## 5. Justificativa

O monolito modular e adequado para o ReUseTech porque o escopo inicial e pequeno e os fluxos principais ainda estao sendo descobertos. Separar o sistema em microsservicos neste momento aumentaria a complexidade sem trazer ganhos proporcionais.

Com Node.js e Express, a equipe consegue desenvolver rapidamente APIs, telas simples e integracoes futuras. A organizacao modular permite manter separacao conceitual entre os dominios sem distribuir fisicamente o sistema.

SQLite reduz atrito no desenvolvimento local e facilita prototipacao. PostgreSQL e uma evolucao natural quando o projeto precisar de maior robustez, concorrencia, integridade e deploy em ambiente produtivo.

Tailwind CSS permite criar uma interface visual inicial com rapidez, consistencia e baixo custo de manutencao, sem exigir a criacao imediata de um design system completo.

## 6. Alternativas consideradas

- Microsservicos: descartado para o MVP por adicionar complexidade de deploy, comunicacao entre servicos, observabilidade e consistencia de dados.
- Frontend SPA com React, Vue ou Angular: adiado para uma etapa futura, pois o MVP pode ser validado com HTML, Tailwind e JavaScript simples.
- Backend serverless: nao escolhido inicialmente porque pode dificultar o entendimento da arquitetura por iniciantes e fragmentar a regra de negocio.
- Banco NoSQL: nao priorizado porque o dominio possui relacionamentos claros entre usuarios, produtos, carrinhos, pedidos e itens.
- Monolito sem modularizacao: descartado porque tende a misturar responsabilidades rapidamente conforme o projeto cresce.

## 7. Consequencias positivas

- Desenvolvimento inicial mais rapido.
- Menor complexidade de infraestrutura.
- Organizacao simples de entender e ensinar.
- Facilidade para executar o projeto localmente.
- Boa separacao de responsabilidades por modulos.
- Caminho evolutivo claro para PostgreSQL e APIs mais maduras.
- Menor custo para validar o produto com usuarios reais.

## 8. Consequencias negativas

- O monolito pode crescer demais se os limites dos modulos nao forem respeitados.
- Mudancas em uma parte do sistema podem exigir redeploy da aplicacao inteira.
- SQLite possui limitacoes para cenarios com alta concorrencia.
- Frontend simples pode se tornar limitado caso a experiencia de usuario fique mais interativa.
- A arquitetura exigira disciplina para evitar acoplamento excessivo entre modulos.

## 9. Estrutura inicial de pastas sugerida

```text
reusetech-marketplace/
|-- docs/
|   `-- adr.md
|-- public/
|   |-- css/
|   |-- js/
|   `-- images/
|-- src/
|   |-- config/
|   |   `-- database.js
|   |-- modules/
|   |   |-- users/
|   |   |   |-- users.routes.js
|   |   |   |-- users.controller.js
|   |   |   |-- users.service.js
|   |   |   `-- users.repository.js
|   |   |-- products/
|   |   |   |-- products.routes.js
|   |   |   |-- products.controller.js
|   |   |   |-- products.service.js
|   |   |   `-- products.repository.js
|   |   |-- cart/
|   |   |   |-- cart.routes.js
|   |   |   |-- cart.controller.js
|   |   |   |-- cart.service.js
|   |   |   `-- cart.repository.js
|   |   `-- checkout/
|   |       |-- checkout.routes.js
|   |       |-- checkout.controller.js
|   |       |-- checkout.service.js
|   |       `-- checkout.repository.js
|   |-- shared/
|   |   |-- middlewares/
|   |   |-- validators/
|   |   `-- utils/
|   |-- views/
|   |   |-- layouts/
|   |   |-- products/
|   |   |-- cart/
|   |   `-- checkout/
|   |-- app.js
|   `-- server.js
|-- prisma/
|   |-- schema.prisma
|   `-- migrations/
|-- tests/
|   |-- users.test.js
|   |-- products.test.js
|   |-- cart.test.js
|   `-- checkout.test.js
|-- .env.example
|-- package.json
`-- README.md
```

Essa estrutura permite iniciar pequeno, com uma unica aplicacao, mas mantendo os principais dominios separados. Caso o projeto cresca, os modulos poderao ser extraidos ou reorganizados com menor impacto.
