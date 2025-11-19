# Create an Invoice

Request method:
POST

URL:
```
https://api-b2b.bigcommerce.com/api/v3/io/ip/orders/:order_id/invoices
```

Params:

| Key      | Value        |
|----------|--------------|
| order_id | {{order_id}} |

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

const invoice = pm.response.json().data;
pm.test('Response includes invoice with ID', () => {
    pm.expect(
        invoice?.invoiceId
    ).to.be.a('number');
});

pm.collectionVariables.unset('invoice_id');
pm.collectionVariables.set('invoice_id', invoice?.invoiceId);
```
