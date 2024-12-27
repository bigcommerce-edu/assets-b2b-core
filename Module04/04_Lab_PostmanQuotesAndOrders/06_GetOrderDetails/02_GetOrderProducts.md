# Get Order Products

Request method:
GET

URL:
```
https://api-b2b.bigcommerce.com/api/v3/io/orders/:bc_order_id/products
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

const items = pm.response.json().data;
pm.test('Response contains at least one item with ID', () => {
    pm.expect(
        items
    ).to.be.a('array');
    pm.expect(
        items?.length
    ).to.be.greaterThan(0);

    const firstItem = Array.isArray(items) ? items[0] : null;
    pm.expect(
        firstItem?.id
    ).to.be.a('number');
});
```

[Next](../../05_Lab_PostmanInvoicesAndPayments/01_CreateInvoice/01_CreateInvoice.md)