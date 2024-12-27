# Get Old Open Invoices

Request method:
GET

URL:
```
https://api-b2b.bigcommerce.com/api/v3/io/ip/invoices?status=0&endDateAt={{invoice_max_created_at}}
```

Headers:

| Header       | Value            |
|--------------|------------------|
| Accept       | application/json |
| Content-Type | application/json |
| authToken    | {{b2b_v3_token}} |

Pre-request Script:
```javascript
const days = 30;

const d = new Date();
d.setSeconds(d.getSeconds() - (days * 24 * 60 * 60));

pm.collectionVariables.unset('invoice_max_created_at');
pm.collectionVariables.set('invoice_max_created_at', Math.round(d.valueOf() / 1000));
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

const invoices = pm.response.json().data;
pm.test('Response includes at least one invoice', () => {
    pm.expect(
        invoices
    ).to.be.a('array');

    pm.expect(
        invoices?.length
    ).to.be.greaterThan(0);
});
```

[Next](./02_GetInvoice.md)