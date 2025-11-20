# Approve a Company

Request method:
PUT

URL:
```
https://api-b2b.bigcommerce.com/api/v3/io/companies/:company_id/status
```

Params:

| Key        | Value          |
|------------|----------------|
| company_id | {{company_id}} |

Headers:

| Header       | Value            |
|--------------|------------------|
| Accept       | application/json |
| Content-Type | application/json |
| authToken    | {{b2b_v3_token}} |

Body:
```json
{
    "companyStatus": 1
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
    ).to.be.eq('SUCCESS');
});
```