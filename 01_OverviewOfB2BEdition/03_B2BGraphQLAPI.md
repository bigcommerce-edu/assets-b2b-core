# B2B GraphQL API

**GraphQL endpoint:**

```
https://api-b2b.bigcommerce.com/graphql
```

## GraphQL Authentication

**Example request:**

```
mutation {
    login(
        loginData: {
            storeHash: "pki...",
            email: "user@example.com",
            password: "MyPassword123..."
        }
    ) {
        result {
            token
        }
    }
}
```

**Using the token:**

```
Authorization: "Bearer {token}"
```

**loginWithCustomerLoginJwt request:**

```
mutation Login($jwt: String!) {
 loginWithCustomerLoginJwt(jwt: $jwt) {
   customer {
     entityId
     email
   }
   customerAccessToken {
     value
     expiresAt
   }
 }
}
```
