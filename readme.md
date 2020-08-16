# TypeORM Relations

<p align="center">
    <a href="readme_en.md">English</a>&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;
    <a href="readme.md">Português</a>&nbsp;&nbsp;&nbsp;
</p>

## Sobre

Aplicação que utiliza banco de dados com o TypeORM com relacionamentos entre entidades. Permite a criação de clientes, produtos e pedidos, onde o cliente pode gerar novos pedidos de compra de certos produtos, como um pequeno e-commerce. Este é o nono desafio proposto no bootcamp GoStack da [Rocketseat](https://github.com/Rocketseat).

## Tecnologias utilizadas

- [Node.js](https://nodejs.org/en/)
- Banco de dados [PostgreSQL](https://www.postgresql.org/)
- Mapedor de objetos relacionais [TypeORM](https://typeorm.io/#/)

## Requisitos

Para executar o projeto é necessário ter os seguintes requisitos instalados no sistema:

- [Node.js](https://nodejs.org/en/) 12.x ou superior
- [Yarn](https://yarnpkg.com/) 1.21 ou superior
- Banco de dados [PostgreSQL](https://www.postgresql.org/) 11.x ou superior

## Executando o projeto

### Clonando o projeto

```bash
$ git clone https://github.com/felipedmsantos95/typeorm-relations
$ cd typeorm-relations
```

### Scripts para execução do projeto

Dentro do diretório do projeto pela primeira vez, você deve se certificar que o serviço PostgreSQL está sendo executado e deve criar um banco de dados chamado `gostack_desafio09`. No arquivo `./ormconfig.json` é possivel alterar as configurações de porta, usuario e senha do PostgreSQL de acordo com o seu contexto.

```json
{
  "type": "postgres",
  "host": "address_of_your_host",
  "port": number_of_postgres_port,
  "username": "your_postgres_user",
  "password": "your_password",
  "database": "gostack_desafio09",
  "entities": ["./src/models/*.ts"],
  "migrations": ["./src/database/migrations/*.ts"],
  "cli": {
    "migrationsDir": "./src/database/migrations"
  }
}
```

Com as configurações feitas de forma correnta, pode-se utilizar o comando `yarn` para instalar as dependências, então os seguintes scripts podem ser executados:

#### `yarn typeorm migration:run`

Configura os relacionamentos criados no TypeORM no PostgreSQL.<br />
Você poderá visualizar quaisquer erros no console.

#### `yarn dev:server`

Executa o backend em modo de desenvolvimento.<br />
Você poderá visualizar quaisquer erros no console.

#### `yarn test`

Executa os scripts de testes realizados.<br />
PS: Para este comando é necessário ter criado o banco de dados `gostack_desafio09_tests`. Você poderá visualizar quaisquer erros no console.


<h3 align="center">
  Enunciado do desafio proposto
</h3>


## Sobre o desafio

Nesse desafio, foi criada uma nova aplicação para treinar o que foi aprendido no Node.js junto ao TypeScript, incluindo o uso de banco de dados com o TypeORM, e relacionamentos ManyToMany!

A aplicação deve permitir a criação de clientes, produtos e pedidos, onde o cliente pode gerar novos pedidos de compra de certos produtos, como um pequeno e-commerce.



### Funcionalidades da aplicação


- **`POST /customers`**: A rota deve receber `name` e `email` dentro do corpo da requisição, sendo o `name` o nome do cliente a ser cadastrado. Ao cadastrar um novo cliente, ele deve ser armazenado dentro do seu banco de dados e deve ser retornado o cliente criado. Ao cadastrar no banco de dados, na tabela `customers` deverá possuir os campos `name`, `email`, `created_at`, `updated_at`.

- **`POST /products`**: Essa rota deve receber `name`, `price` e `quantity` dentro do corpo da requisição, sendo o `name` o nome do produto a ser cadastrado, `price` o valor unitário e `quantity` a quantidade existente em estoque do produto. Com esses dados devem ser criados no banco de dados um novo produto com os seguintes campos: `name`, `price`, `quantity`, `created_at`, `updated_at`.

- **`POST /orders/`**: Nessa rota você deve receber no corpo da requisição o `customer_id` e um array de products, contendo o `id` e a `quantity` que você deseja adicionar a um novo pedido. Aqui você deve cadastrar na tabela `order` um novo pedido, que estará relacionado ao `customer_id` informado, `created_at` e `updated_at` . Já na tabela `orders_products`, você deve armazenar o `product_id`, `order_id`, `price` e `quantity`, `created_at` e `updated_at`.

- **`GET /orders/:id`**: Essa rota deve retornar as informações de um pedido específico, com todas as informações que podem ser recuperadas através dos relacionamentos entre a tabela `orders`, `customers` e `orders_products`.


### Específicação dos testes

Para esse desafio temos os seguintes testes:

- **`should be able to create a new customer`**: Para que esse teste passe, sua aplicação deve permitir que um cliente seja criado, e retorne um json com o cliente criado.

- **`should not be able to create a customer with one e-mail thats already registered`**: Para que esse teste passe, sua aplicação deve retornar um erro quando você tentar cadastrar um cliente com um e-mail que já esteja cadastrado no banco de dados.

- **`should be able to create a new product`**: Para que esse teste passe, sua aplicação deve permitir que um produto seja criado, e retorne um json com o produto criado.

- **`should not be able to create a duplicated product`**: Para que esse teste passe, sua aplicação deve retornar um erro quando você tentar cadastrar um produto com um nome que já esteja cadastrado no banco de dados.

- **`should be able to create a new order`**: Para que esse teste passe, sua aplicação deve permitir que um pedido seja criado, e retorne um json com o todos os dados do pedido criado.

- **`should not be able to create an order with a invalid customer`**: Para que esse teste passe, sua aplicação não deve permitir a criação de um novo pedido com um cliente que não existe no banco de dados, retornando um erro.

- **`should not be able to create an order with invalid products`**: Para que esse teste passe, sua aplicação não deve permitir a criação de um novo pedido com um produtos que não existem no banco de dados, retornando um erro caso um ou mais dos produtos enviados não exista no banco de dados.

- **`should not be able to create an order with products with insufficient quantities`**: Para que esse teste passe, sua aplicação não deve permitir a criação de um novo pedido com um produtos que não possuem quantidade disponível, retornando um erro caso um ou mais dos produtos enviados não possua a quantidade necessária.

- **`should be able to subtract an product total quantity when it is ordered`**: Para que esse teste passe, sua aplicação deve permitir que, quando um novo pedido for criado, seja alterada a quantidade total dos produtos baseado na quantidade pedida.

- **`should be able to list one specific order`**: Para que esse teste passe, você deve permitir que a rota `orders/:id` retorne um pedido, contendo todas as informações do pedido com o relacionamento de `customer` e `order_products`.
