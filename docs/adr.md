# ADR: Arquitetura inicial do ReUseTech

## 1. Título

Definição da arquitetura inicial para o marketplace ReUseTech.

## 2. Contexto

O ReUseTech será um marketplace simplificado para compra e venda de eletrônicos usados, inspirado em experiências enxutas como OLX e Mercado Livre. Nesta primeira etapa, o objetivo principal é construir um MVP funcional, de fácil manutenção e com baixa complexidade operacional.

O sistema deve atender aos seguintes fluxos principais:

- Cadastro e autenticação de usuários.
- Cadastro, listagem e visualização de produtos usados.
- Carrinho de compras simples.
- Fluxo básico de checkout.

Como o projeto ainda está em fase inicial, a arquitetura deve favorecer velocidade de desenvolvimento, clareza de organização e facilidade para evoluir sem exigir infraestrutura distribuída ou custos operacionais altos.

## 3. Decisão arquitetural

A arquitetura recomendada para o MVP será um monolito modular.

O backend ficará concentrado em uma única aplicação Node.js com Express, organizada por módulos de domínio, como usuários, produtos, carrinho e checkout. Cada módulo deverá concentrar suas rotas, regras de negócio e acesso a dados relacionados.

O frontend inicial será simples, utilizando HTML, Tailwind CSS e JavaScript leve quando necessário. A renderização pode começar de forma estática ou com templates simples servidos pelo próprio backend, evitando a introdução precoce de frameworks SPA.

O banco de dados recomendado para desenvolvimento inicial é SQLite, pela simplicidade de configuração. Para uma evolução próxima de produção, PostgreSQL deve ser adotado como banco principal, mantendo a modelagem relacional.

## 4. Stack tecnológica recomendada

- Runtime: Node.js.
- Framework backend: Express.
- Banco de dados inicial: SQLite.
- Banco recomendado para produção: PostgreSQL.
- ORM ou query builder: Prisma ou Knex.
- Frontend inicial: HTML, Tailwind CSS e JavaScript.
- Autenticação: sessões com cookies HTTP-only ou JWT simples, conforme a necessidade do MVP.
- Validação de dados: Zod ou Joi.
- Testes: Jest ou Vitest para testes unitários e de integração.
- Controle de versão: Git.
- Documentação: Markdown dentro da pasta `docs`.

## 5. Justificativa

O monolito modular é adequado para o ReUseTech porque o escopo inicial é pequeno e os fluxos principais ainda estão sendo descobertos. Separar o sistema em microsserviços neste momento aumentaria a complexidade sem trazer ganhos proporcionais.

Com Node.js e Express, a equipe consegue desenvolver rapidamente APIs, telas simples e integrações futuras. A organização modular permite manter separação conceitual entre os domínios sem distribuir fisicamente o sistema.

SQLite reduz atrito no desenvolvimento local e facilita prototipação. PostgreSQL é uma evolução natural quando o projeto precisar de maior robustez, concorrência, integridade e deploy em ambiente produtivo.

Tailwind CSS permite criar uma interface visual inicial com rapidez, consistência e baixo custo de manutenção, sem exigir a criação imediata de um design system completo.

## 6. Alternativas consideradas

- Microsserviços: descartado para o MVP por adicionar complexidade de deploy, comunicação entre serviços, observabilidade e consistência de dados.
- Frontend SPA com React, Vue ou Angular: adiado para uma etapa futura, pois o MVP pode ser validado com HTML, Tailwind e JavaScript simples.
- Backend serverless: não escolhido inicialmente porque pode dificultar o entendimento da arquitetura por iniciantes e fragmentar a regra de negócio.
- Banco NoSQL: não priorizado porque o domínio possui relacionamentos claros entre usuários, produtos, carrinhos, pedidos e itens.
- Monolito sem modularização: descartado porque tende a misturar responsabilidades rapidamente conforme o projeto cresce.

## 7. Consequencias positivas

- Desenvolvimento inicial mais rápido.
- Menor complexidade de infraestrutura.
- Organização simples de entender e ensinar.
- Facilidade para executar o projeto localmente.
- Boa separação de responsabilidades por módulos.
- Caminho evolutivo claro para PostgreSQL e APIs mais maduras.
- Menor custo para validar o produto com usuários reais.

## 8. Consequencias negativas

- O monolito pode crescer demais se os limites dos módulos não forem respeitados.
- Mudanças em uma parte do sistema podem exigir redeploy da aplicação inteira.
- SQLite possui limitações para cenários com alta concorrência.
- Frontend simples pode se tornar limitado caso a experiência de usuário fique mais interativa.
- A arquitetura exigirá disciplina para evitar acoplamento excessivo entre módulos.

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

Essa estrutura permite iniciar pequeno, com uma única aplicação, mas mantendo os principais domínios separados. Caso o projeto cresça, os módulos poderão ser extraídos ou reorganizados com menor impacto.
