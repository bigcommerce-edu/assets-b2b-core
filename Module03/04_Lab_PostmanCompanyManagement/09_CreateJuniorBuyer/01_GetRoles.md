# Get Roles

Request method:
GET

URL:
```
https://api-b2b.bigcommerce.com/api/v3/io/companies/roles
```

Headers:

| Header    | Value            |
|-----------|------------------|
| Accept    | application/json |
| authToken | {{b2b_v3_token}} |

Post-response Script:
```javascript
pm.test('Response is not an error', () => {
    pm.response.to.not.be.error;
    pm.response.to.not.have.jsonBody("errors");
});
pm.test('Response is JSON with data', () => {
    pm.response.to.have.jsonBody("data");
});

const roles = pm.response.json().data;
pm.test('Response includes array of roles', () => {
    pm.expect(
        roles
    ).to.be.a('array');
    pm.expect(
        roles?.length
    ).to.be.greaterThan(0);
});

pm.collectionVariables.unset('junior_role_id');
if (Array.isArray(roles)) {
    const juniorRole = roles.find(role => role?.name === 'Junior Buyer');
    pm.test('Junior role found', () => {
        pm.expect(
            juniorRole?.id
        ).to.be.a('number');
    });
    
    pm.collectionVariables.set('junior_role_id', parseInt(juniorRole?.id));
}
```

[Next](./02_CreateJuniorBuyerUser.md)