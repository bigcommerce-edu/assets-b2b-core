# Create Junior Buyer User

Request method:
POST

URL:
```
https://api-b2b.bigcommerce.com/api/v3/io/users
```

Headers:

| Header       | Value            |
|--------------|------------------|
| Accept       | application/json |
| Content-Type | application/json |
| authToken    | {{b2b_v3_token}} |

Body:
```json
{
    "companyId": {{company_id}},
    "email": "jilldoe@example.com",
    "firstName": "Jill",
    "lastName": "Doe",
    "phoneNumber": "444-777-9999",
    "companyRoleId": {{junior_role_id}}
}
```

Post-response Script:
```javascript
pm.test('Response is not an error', () => {
    pm.response.to.not.be.error;
    pm.response.to.not.have.jsonBody("errors");
});
pm.test('Response is JSON with data', () => {
    pm.response.to.have.jsonBody("data");
});

const message = pm.response.json().meta?.message;
pm.test('Operation was successful', () => {
    pm.expect(
        message
    ).to.be.eq('Success');
});

const user = pm.response.json().data;
pm.test('Response contains user with ID', () => {
    pm.expect(
        user?.userId
    ).to.be.a('number');
});

pm.collectionVariables.unset('user_id');
pm.collectionVariables.set('user_id', user?.userId);
```

[Next](../10_GetUser/10_GetUser.md)