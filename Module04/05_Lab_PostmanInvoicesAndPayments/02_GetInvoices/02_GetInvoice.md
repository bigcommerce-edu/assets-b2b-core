# Get Invoice

Request method:
GET

URL:
```
https://api-b2b.bigcommerce.com/api/v3/io/ip/invoices/:invoice_id
```

Params:

| Key        | Value          |
|------------|----------------|
| invoice_id | {{invoice_id}} |

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

const invoice = pm.response.json().data;
pm.test('Response contained an invoice with ID', () => {
    pm.expect(
        invoice?.id
    ).to.be.a('number');
});
```

[Next](../03_ExportInvoicePdf/03_ExportInvoicePdf.md)