# Export Invoice PDF

Request method:
GET

URL:
```
https://api-b2b.bigcommerce.com/api/v3/io/ip/invoices/:invoice_id/download-pdf
```

Params:

| Key        | Value          |
|------------|----------------|
| invoice_id | {{invoice_id}} |

Headers:

| Header    | Value            |
|-----------|------------------|
| Accept    | application/json |
| authToken | {{b2b_v3_token}} |

Post-response Script:
```javascript
pm.test('Response is not an error', () => {
    pm.response.to.not.be.error;
    pm.response.to.not.have.jsonBody("errors");
});
pm.test('Response is JSON with data', () => {
    pm.response.to.have.jsonBody("data");
});

const url = pm.response.json().data?.url;
pm.test('Response contained a download URL', () => {
    pm.expect(
        url
    ).to.be.a('string');
});
```

[Next](../04_ApplyInvoicePayment/04_ApplyInvoicePayment.md)