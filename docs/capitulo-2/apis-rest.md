---
hide:
  - toc
---

# Capítulo 2: Aplicação OCI PIZZA

# 2.3 APIs REST

Uma API define um contrato entre um cliente e um servidor. A API especifica os tipos de requisições que são possíveis.

O estilo predominante são as APIs HTTP classificadas como RESTful.

HTTP CRUD APIs aplicam verbos HTTP em recursos identificados por URIs.

Payloads são formatados através de JSON ou XML.

Verbos
  - PATCH: atualiza propriedades individuais de um recurso.
  - PUT: substituí o recurso por completo com novos valores.

**Pizza**

| Método | Endpoint               | Descrição                                 | Requer Autenticação |
|--------|------------------------|-------------------------------------------|---------------------|
| GET    | /api/pizzas            | Lista todas as pizzas                     | Não                 |
| GET    | /api/pizzas/{pizza_id} | Obtém os detalhes de uma pizza específica | Não                 |
| POST   | /api/pizzas            | Adiciona uma nova pizza                   | Admin               |
| PUT    | /api/pizzas/{pizza_id} | Atualiza informações de uma pizza         | Admin               |
| DELETE | /api/pizzas/{pizza_id} | Remove uma pizza                          | Admin               |

**Order**

| Método | Endpoint                               | Descrição                                                        | Requer Autenticação |
|--------|----------------------------------------|------------------------------------------------------------------|---------------------|
| GET    | /api/orders                            | Lista todos os pedidos                                           | Admin               |
| GET    | /api/orders/users/{user_id}            | Lista todos os pedidos associado a um usuário específico         | Sim                 |
| GET    | /api/orders/{order_id}/users/{user_id} | Obtém os detalhes de um pedido associado a um usuário específico | Sim                 |
| GET    | /api/orders/{order_id}                 | Obtém os detalhes de um pedido específico                        | Sim                 |
| POST   | /api/orders/users/{user_id}            | Criar um novo pedido associado a um usuário específico           | Sim                 |
| PUT    | /api/orders/users/{user_id}            | Atualiza as informações de um pedido de um usuário específico    | Sim                 |
| DELETE | /api/orders/{order_id}                 | Remove um pedido                                                 | Admin               |

**User**

| Método | Endpoint                               | Descrição                                        | Requer Autenticação |
|--------|----------------------------------------|--------------------------------------------------|---------------------|
| GET    | /api/users                             | Lista todos os usuários                          | Admin               |
| GET    | /api/users/{user_id}                   | Obtém os detalhes de um usuário específico       | Sim                 |
| POST   | /api/users                             | Criar um novo usuário                            | Não                 |
| PUT    | /api/users/{user_id}                   | Atualiza as informações de um usuário específico | Sim                 |
| DELETE | /api/users/{user_id}                   | Remove um usuário                                | Admin               |

**Authentication**

| Método | Endpoint          | Descrição                               | Requer Autenticação | 
|--------|-------------------|-----------------------------------------|---------------------|
| POST   | /api/users/login  | Autentica um usuário e faz login        | Não                 |
| POST   | /api/users/logout | Faz logout do usuário autenticado       | Não                 |

**Location**

| Método | Endpoint                     | Descrição                                          | Requer Autenticação | 
|--------|------------------------------|----------------------------------------------------|---------------------|
| GET    | /api/locations               | Lista todos os Estados e Cidades                   | Admin               |
| GET    | /api/locations/{zipcode}     | Obtém o Estado e a Cidade através do código postal | Sim                 |
| POST   | /api/locations               | Cria um Estado e Cidade                            | Admin               |
| PUT    | /api/locations/{location_id} | Atualiza as informações de um Estado e Cidade      | Admin               |
| DELETE | /api/locations/{location_id} | Remove um Estado e Cidade                          | Admin               |

