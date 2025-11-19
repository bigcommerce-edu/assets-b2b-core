# Generate a Quote Checkout URL

Request method:
POST

URL:
```
https://api-b2b.bigcommerce.com/api/v3/io/rfq/:quote_id/checkout
```

Params:

| Key      | Value        |
|----------|--------------|
| quote_id | {{quote_id}} |

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

const checkoutUrl = pm.response.json().data?.checkoutUrl;
pm.test('Response includes checkout URL', () => {
    pm.expect(
        checkoutUrl
    ).to.be.a('string');
});
```
