# Delete a Company

Request method:
DELETE

URL:
```
https://api-b2b.bigcommerce.com/api/v3/io/companies/:company_id
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

pm.collectionVariables.unset('company_id');
```

[Next](../05_ApproveCompany/01_GetUnapprovedCompanies.md)