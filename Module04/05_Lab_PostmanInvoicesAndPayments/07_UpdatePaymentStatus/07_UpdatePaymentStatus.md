# Update a Payment Status

Request method:
PUT

URL:
```
https://api-b2b.bigcommerce.com/api/v3/io/ip/payments/:payment_id/processing-status
```

Params:

| Key        | Value          |
|------------|----------------|
| payment_id | {{payment_id}} |

Headers:

| Header    | Value            |
|-----------|------------------|
| Accept    | application/json |
| authToken | {{b2b_v3_token}} |

Body:
```json
{
    "processingStatus": 3
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
```

[Next](../../../Module05/02_RESTSpecializedUsers.md)