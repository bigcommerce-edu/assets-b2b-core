# Get Order

Request method:
GET

URL:
```
https://api-b2b.bigcommerce.com/api/v3/io/orders/:bc_order_id
```

Params:

| Key         | Value           |
|-------------|-----------------|
| bc_order_id | {{bc_order_id}} |

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

const order = pm.response.json().data;
pm.test('Response contained an order with ID', () => {
    pm.expect(
        order?.id
    ).to.be.a('number');
});
```

[Next](./02_GetOrderProducts.md)