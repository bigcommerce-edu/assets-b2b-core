# Get User

Request method:
GET

URL:
```
https://api-b2b.bigcommerce.com/api/v3/io/users/:user_id
```

Params:

| Key     | Value       |
|---------|-------------|
| user_id | {{user_id}} |

Headers:

| Header       | Value            |
|--------------|------------------|
| Accept       | application/json |
| Content-Type | application/json |
| authToken    | {{b2b_v3_token}} |

Post-response Script:
```javascript
pm.test('Response is not an error', () => {
    pm.response.to.not.be.error;
    pm.response.to.not.have.jsonBody("errors");
});
pm.test('Response is JSON with data', () => {
    pm.response.to.have.jsonBody("data");
});

const user = pm.response.json().data;
pm.test('Response includes user with ID', () => {
    pm.expect(
        user?.id
    ).to.be.a('number');
});
```

[Next](../../../Module04/02_RESTListsAndQuotes/02_RESTListsAndQuotes.md)