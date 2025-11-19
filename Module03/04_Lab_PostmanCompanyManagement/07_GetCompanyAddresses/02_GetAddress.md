# Get Company Address

Request method:
GET

URL:
```
https://api-b2b.bigcommerce.com/api/v3/io/addresses/:address_id
```

Params:

| Key        | Value          |
|------------|----------------|
| address_id | {{address_id}} |

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

const address = pm.response.json().data;
pm.test('Response included address with ID', () => {
    pm.expect(
        address?.addressId
    ).to.be.a('number');
});
```
