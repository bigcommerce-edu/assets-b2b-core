# Get Quote Details

Request method:
GET

URL:
```
https://api-b2b.bigcommerce.com/api/v3/io/rfq/:quote_id
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

const quote = pm.response.json().data;
pm.test('Response includes quote with number', () => {
    pm.expect(
        quote?.quoteNumber
    ).to.be.a('string');
});
```

[Next](../03_ExportQuotePdf/03_ExportQuotePdf.md)