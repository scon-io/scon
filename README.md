# Scon.io

A hosting service for public Git repositories. I mean __seriously public__.

> 🚧 I'm keep working in progress. All data is volatile temporarily.  
> 🚧 No front-end application yet.

## Usage

1. Register by using [`createUser`](#createuser-register) mutation.
2. Create new project by using [`createProject`](#createproject) mutation.
3. Clone the project you just created.
4. Commit and push!

## Rule

- A Scon.io user can commit, revert and push any project as one like.
- One project has only one branch, `master`.

## API

Scon.io is using [GraphQL](http://graphql.org/).
There is a single endpoint:
```
POST https://scon.io/api
```

#### `projects`
List all project.

```graphql
query {
  projects {
    name
    url
  }
}
```

#### `createUser` (Register)
Create new user.

```graphql
mutation createUser($email: String!, $username: String!, $password: String!) {
  createUser(email: $email, username: $username, password: $password) {
    id
    username
    email
  }
}
```

#### `createToken` (Sign in)
Create a access token.

Use HTTP Basic authentication with username and password. A request header has to contain `Authorization: Basic [BASE64_ENCODED]`.

```graphql
mutation {
  createToken
}
```

#### `createProject`
Create new project.

Use a token created by `createToken` mutation. A request header has to contain `Authorization: Bearer [TOKEN]`

```graphql
mutation createProject($name: String!){
  createProject(name: $name) {
    id
    name
    url
  }
}
```
