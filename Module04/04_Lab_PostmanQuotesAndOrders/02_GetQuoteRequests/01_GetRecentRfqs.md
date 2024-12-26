# Get Recent RFQs

Request method:
GET

URL:
```
https://api-b2b.bigcommerce.co`m/api/v3/io/rfq?minCreated={{quote_min_created_at}}&status=0
```

Headers:

| Header    | Value            |
|-----------|------------------|
| Accept    | application/json |
| authToken | {{b2b_v3_token}} |

Pre-request Script:
```javascript
const days = 7;

const d = new Date();
d.setSeconds(d.getSeconds() - (days * 24 * 60 * 60));

pm.collectionVariables.unset('quote_min_created_at');
pm.collectionVariables.set('quote_min_created_at', Math.round(d.valueOf() / 1000));
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

const quotes = pm.response.json().data;
pm.test('Response contains at least one quote', () => {
    pm.expect(
        quotes
    ).to.be.a('array');

    pm.expect(
        quotes?.length
    ).to.be.greaterThan(0);
});

pm.collectionVariables.unset('quote_id');
if (Array.isArray(quotes) && quotes.length > 0) {
    pm.collectionVariables.set('quote_id', quotes[0].quoteId);
}
```

[Next](./02_GetQuoteDetails.md)