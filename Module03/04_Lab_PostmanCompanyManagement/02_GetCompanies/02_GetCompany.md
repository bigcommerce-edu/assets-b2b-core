# Get Company

Request method:
GET

URL:
```
https://api-b2b.bigcommerce.com/api/v3/io/companies/:company_id
```

Params:

| Key        | Value          |
|------------|----------------|
| company_id | {{company_id}} |

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

const company = pm.response.json().data;
pm.test('Response includes a company with ID', () => {
    pm.expect(
        company?.companyId
    ).to.be.a('number');
});
```

[Next](../04_UpdateAndDeleteCompany/01_UpdateCompany.md)