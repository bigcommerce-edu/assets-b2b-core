# Apply an Invoice Payment

Request method:
POST

URL:
```
https://api-b2b.bigcommerce.com/api/v3/io/ip/payments/offline
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
    "lineItems": [
        {
            "invoiceId": {{invoice_id}},
            "amount": <Amount>
        }
    ],
    "currency": "USD",
    "details": {
        "memo": "Paid by check"
    },
    "customerId": "{{company_id}}",
    "payerName": "John Doe",
    "processingStatus": 2
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

const paymentId = pm.response.json().data?.paymentId;
pm.test('Response included payment ID', () => {
    pm.expect(
        paymentId
    ).to.be.a('number');
});

pm.collectionVariables.unset('payment_id');
pm.collectionVariables.set('payment_id', paymentId);
```

[Next](../05_GetInvoicePayments/05_GetInvoicePayments.md)