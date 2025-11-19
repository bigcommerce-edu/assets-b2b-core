# Get Recent Orders

Request method:
GET

URL:
```
https://api-b2b.bigcommerce.com/api/v3/io/orders?minCreated={{order_min_created_at}}
```

Headers:

| Header       | Value            |
|--------------|------------------|
| Accept       | application/json |
| Content-Type | application/json |
| authToken    | {{b2b_v3_token}} |

Pre-request Script:
```javascript
const days = 7;

const d = new Date();
d.setSeconds(d.getSeconds() - (days * 24 * 60 * 60));

pm.collectionVariables.unset('order_min_created_at');
pm.collectionVariables.set('order_min_created_at', Math.round(d.valueOf() / 1000));
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

const orders = pm.response.json().data;
pm.test('Response contains at least one order', () => {
    pm.expect(
        orders
    ).to.be.a('array');

    pm.expect(
        orders?.length
    ).to.be.greaterThan(0);
});

pm.collectionVariables.unset('order_id');
pm.collectionVariables.unset('bc_order_id');
if (Array.isArray(orders) && orders.length > 0) {
    pm.collectionVariables.set('order_id', orders[0].id);
    pm.collectionVariables.set('bc_order_id', orders[0].bcOrderId);
}
```
