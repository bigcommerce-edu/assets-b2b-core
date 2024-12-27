# Get an Invoice's Payments

Request method:
GET

URL:
```
https://api-b2b.bigcommerce.com/api/v3/io/ip/payments?invoiceId={{invoice_id}}
```

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

const payments = pm.response.json().data;
pm.test('Response contains at least one payment', () => {
    pm.expect(
        payments
    ).to.be.a('array');

    pm.expect(
        payments?.length
    ).to.be.greaterThan(0);
});
```

[Next](../07_UpdatePaymentStatus/07_UpdatePaymentStatus.md)