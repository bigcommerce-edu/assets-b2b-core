# Get Company Users

Request method:
GET

URL:
```
https://api-b2b.bigcommerce.com/api/v3/io/users?companyId={{company_id}}
```

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

const users = pm.response.json().data;
pm.test('Response contains at least one user', () => {
    pm.expect(
        users
    ).to.be.a('array');

    pm.expect(
        users?.length
    ).to.be.greaterThan(0);
});
```
