# Authentication

## Using the API to Create Tokens

**Example request:**

```
POST https://api-b2b.bigcommerce.com/api/io/auth/backend

{
  "storeHash": "{Your store hash}",
  "email": "{Your email address}",
  "password": "{Your password}",
  "name": "{Token name}"
}
```

## Get a List of Available Tokens

**Example request:**

```
GET https://api-b2b.bigcommerce.com/api/io/backend/tokens
Accept: application/json
authToken: [insert your auth token here]
```

## Delete a Token

**Example request:**

```
DELETE https://api-b2b.bigcommerce.com/api/io/auth/backend

{
  "email": "{Your email address}",
  "name": "{Token name}",
  "id": [insert token ID here]
}
```

[Next](../02_Lab_APISetup/02_PostmanEnvironment.md)