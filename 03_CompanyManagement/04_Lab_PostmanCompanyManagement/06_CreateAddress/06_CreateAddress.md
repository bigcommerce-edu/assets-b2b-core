# Create an Address

Request method:
POST

URL:
```
https://api-b2b.bigcommerce.com/api/v3/io/addresses
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
    "addressLine1": "321 Park Place",
    "addressLine2": "Ste 3",
    "city": "Austin",
    "stateCode": "TX",
    "countryCode": "US",
    "zipCode": "78726",
    "firstName": "Jane",
    "lastName": "Doe",
    "isBilling": true,
    "isDefaultBilling": true,
    "isShipping": true,
    "isDefaultShipping": true,
    "phoneNumber": "888-777-6666",
    "companyId": {{company_id}},
    "label": "Main Address"
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

const address = pm.response.json().data;
pm.test('Response included address with ID', () => {
    pm.expect(
        address?.addressId
    ).to.be.a('number');
});

pm.collectionVariables.unset('address_id');
pm.collectionVariables.set('address_id', address?.addressId);
```