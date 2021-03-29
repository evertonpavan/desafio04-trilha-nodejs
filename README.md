<h1 align="center">
  <img alt="" src=".github/cover-node.js.png">
  
  <br>

  Ignite Journey
</h1>

<p align="center">
  <img alt="Node.js Logo" src="https://img.shields.io/badge/Node.js-LTS-339933?logo=node.js">&nbsp;&nbsp;
   <img alt="GitHub" src="https://img.shields.io/github/license/lemuelZara/concepts-nodejs.svg">
</p>

<br>

## Desafio 04 - Introdução ao SOLID

Nesse desafio, você deverá criar uma aplicação para treinar o que aprendeu até agora no Node.js!

Essa será uma aplicação de listagem e cadastro de usuários. Para que a listagem de usuários funcione, o usuário que solicita a listagem deve ser um admin (mais detalhes ao longo da descrição).

<br>

## Especificação dos testes

<br>

### Teste do model

<br>

- **Should be able to create an user with all props**

    Para que esse teste passe, você deve completar o código do model de usuários que está em **src/modules/users/model/User.ts**.
    O usuário deve ter as seguintes propriedades:

```json
{
	id: string;

  name: string;

  admin: boolean;

  email: string;

  created_at: Date;

  updated_at: Date;
}
```

Lembre que a propriedade `admin` deve sempre ser iniciada como `false` e o `id` deve ser um `uuid` gerado automaticamente.

<br>

### Testes do repositório

<br>

- **Should be able to create new users**

    Para que esse teste passe, é necessário que o método `create` do arquivo **src/modules/users/repositories/implementations/UsersRepository** permita receber o `name` e `email` de um usuário, crie um usuário a partir do model (que foi completado no teste anterior).

<br>

- **Should be able to list all users**

    Para que esse teste passe, é necessário que o método `list` do arquivo **src/modules/users/repositories/implementations/UsersRepository** retorne a lista de todos os usuários cadastrados na aplicação.

<br>

- **Should be able to find user by ID**

    Para que esse teste passe, é necessário que o método `findById` do arquivo **src/modules/users/repositories/implementations/UsersRepository** receba o `id` ****de um usuário e ****retorne o usuário que possui o mesmo `id`.

<br>

- **Should be able to find user by e-mail address**

    Para que esse teste passe, é necessário que o método `findByEmail` do arquivo **src/modules/users/repositories/implementations/UsersRepository** receba o `email` ****de um usuário e ****retorne o usuário que possui o mesmo `email`.

<br>

- **Should be able to turn an user as admin**

    Para que esse teste passe, é necessário que o método `turnAdmin` do arquivo **src/modules/users/repositories/implementations/UsersRepository** receba o objeto do usuário completo, mude a propriedade `admin` para `true`, atualize também a propriedade `updated_at`  e retorne o usuário atualizado.

<br>

### Testes de useCases

<br>

- **Should be able to create new users**

    Para que esse teste passe, é necessário que o método `execute` do arquivo **src/modules/users/useCases/createUser/CreateUserUseCase.ts** receba `name` e `email` do usuário a ser criado, crie o usuário através do método `create` do repositório e retorne o usuário criado.

<br>

- **Should not be able to create new users when email is already taken**

    Para que esse teste passe, é necessário que o método `execute` do arquivo **src/modules/users/useCases/createUser/CreateUserUseCase.ts** não permita que um usuário seja criado caso já exista um usuário com o mesmo email e, nesse caso, lance um erro no seguinte formato:

    ```tsx
    throw new Error("Mensagem do erro");
    ```

<br>

- **Should be able to turn an user as admin**

    Para que esse teste passe, é necessário que o método `execute` do arquivo **src/modules/users/useCases/turnUserAdmin/TurnUserAdminUseCase.ts** receba o `id` de um usuário, chame o método do repositório que transforma esse usuário em administrador e retorne o usuário após a alteração.

<br>

- **Should not be able to turn a non existing user as admin**

    Para que esse teste passe, é necessário que o método `execute` do arquivo **src/modules/users/useCases/turnUserAdmin/TurnUserAdminUseCase.ts** não permita que um usuário que não existe seja transformado em admin. Caso o usuário não exista, lance um erro no seguinte formato:

    ```tsx
    throw new Error("Mensagem do erro");
    ```

<br>

- **Should be able to get user profile by ID**

    Para que esse teste passe, é necessário que o método `execute` do arquivo **src/modules/users/useCases/showUserProfile/ShowUserProfileUseCase.ts** receba o `id` de um usuário, chame o método do repositório que busca um usuário pelo `id` e retorne o usuário encontrado.

<br>

- **Should not be able to show profile of a non existing user**

    Para que esse teste passe, é necessário que o método `execute` do arquivo **src/modules/users/useCases/showUserProfile/ShowUserProfileUseCase.ts** não permita que um usuário que não existe seja retornado. Caso o usuário não exista, lance um erro no seguinte formato:

    ```tsx
    throw new Error("Mensagem do erro");
    ```

<br>

- **Should be able to list all users**

    Para que esse teste passe, é necessário que o método `execute` do arquivo **src/modules/users/useCases/listAllUsers/ListAllUsersUseCase.ts** receba o `id` de um usuário, chame o método do repositório que retorna todos os usuários cadastrados e retorne essa informação.

<br>

- **Should not be able to a non admin user get list of all users**

    Para que esse teste passe, é necessário que o método `execute` do arquivo **src/modules/users/useCases/listAllUsers/ListAllUsersUseCase.ts** não permita que um usuário que não seja admin, acesse a listagem de usuários cadastrados na aplicação. Caso o usuário não seja admin, lance um erro no seguinte formato:

    ```tsx
    throw new Error("Mensagem do erro");
    ```

<br>

- **Should not be able to a non existing user get list of all users**

    Para que esse teste passe, é necessário que o método `execute` do arquivo **src/modules/users/useCases/listAllUsers/ListAllUsersUseCase.ts** não permita que um usuário que não exista, acesse a listagem de usuários cadastrados na aplicação. Caso o usuário não exista, lance um erro no seguinte formato:

    ```tsx
    throw new Error("Mensagem do erro");
    ```

<br>

### Testes das rotas

<br>

Para que esses testes passem, você deve fazer alterações em todos os controllers da aplicação. 

Você pode olhar qual controller recebe o conteúdo de qual rota observando o arquivo **src/routes/users.routes.ts**.

<br>


- **Rota - [POST] /users**
	
	<br>

    - **Should be able to create new users**

        Para que esse teste passe, usando o useCase apropriado, você deve permitir que a rota crie um usuário e retorne um status `201` junto ao objeto do usuário criado.

		<br>

    - **Should not be able to create new users when email is already taken**

        Para que esse teste passe, caso algum erro tenha acontecido no useCase, retorne a resposta com status `400` e um json com um objeto `{ error: "mensagem do erro" }`, onde o valor da propriedade `error` deve ser a mensagem lançada pelo erro no useCase.

        Para capturar erros lançados por outros arquivos, você pode envolver o conteúdo do controller em um `try/catch` e acessar a propriedade `message` do erro recebido pelo `catch`

<br>

- **Rota - [PATCH] /users/:user_id/admin**

	<br>

    - **Should be able to turn an user as admin**

        Para que esse teste passe, usando o useCase apropriado, você deve permitir que a rota mude um usuário padrão para um admin e retorne o usuário alterado no corpo da resposta.

		<br>

    - **Should not be able to turn a non existing user as admin**

        Para que esse teste passe, caso algum erro tenha acontecido no useCase, retorne a resposta com status `404` e um json com um objeto `{ error: "mensagem do erro" }`, onde o valor da propriedade `error` deve ser a mensagem lançada pelo erro no useCase.

	<br>
	

- **Rota - [GET] /users/:user_id**

	<br>

    - **Should be able to get user profile by ID**

        Para que esse teste passe, usando o useCase apropriado, você deve permitir que a rota receba o `id` de um usuário pelo parâmetro na rota e retorne, no corpo da resposta, o objeto do usuário encontrado.

		<br>

    - **Should not be able to show profile of a non existing user**

        Para que esse teste passe, caso algum erro tenha acontecido no useCase, retorne a resposta com status `404` e um json com um objeto `{ error: "mensagem do erro" }`, onde o valor da propriedade `error` deve ser a mensagem lançada pelo erro no useCase.

	<br>	

- **Rota - [GET] /users**

	<br>	

    - **Should be able to list all users**

        Para que esse teste passe, usando o useCase apropriado, você deve permitir que a rota receba o `id` de um usuário **admin** pelo header `user_id` da requisição e retorne, no corpo da resposta, a lista dos usuários cadastrados.

		<br>	

    - **Should not be able to a non admin user get list of all users**

        **Should not be able to a non existing user get list of all users**

        Para que **esses dois testes** passem, caso algum erro tenha acontecido no useCase, retorne a resposta com status `400` e um json com um objeto `{ error: "mensagem do erro" }`, onde o valor da propriedade `error` deve ser a mensagem lançada pelo erro no useCase.