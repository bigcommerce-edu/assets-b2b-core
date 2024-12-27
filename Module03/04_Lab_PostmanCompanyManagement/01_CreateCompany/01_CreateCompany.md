# Create a Company

Request method:
POST

URL:
```
https://api-b2b.bigcommerce.com/api/v3/io/companies
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
    "companyName": "Jane's Widgets",
    "companyPhone": "111-222-3333",
    "companyEmail": "janedoe@example.com",
    "addressLine1": "987 Park Place",
    "city": "Austin",
    "state": "Texas",
    "country": "United States",
    "zipCode": "78726",
    "adminFirstName": "Jane",
    "adminLastName": "Doe",
    "adminEmail": "janedoe@example.com",
    "adminPhoneNumber": "222-333-4444"
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

const company = pm.response.json().data;
pm.test('Response includes a company with ID', () => {
    pm.expect(
        company?.companyId
    ).to.be.a('number');
});

pm.collectionVariables.unset('company_id');
pm.collectionVariables.set('company_id', company?.companyId);
```

[Next](../02_GetCompanies/01_GetCompanies.md)