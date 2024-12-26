# JavaScript API Methods

## Opening a Buyer Portal Page

```javascript
window.b2b.utils.openPage('INVOICE');
```

**Closing Buyer Portal interface:**

```javascript
window.b2b.utils.openPage('CLOSE');
```

## User Profile and Token

**Example fetch for logged-in user:**

```javascript
console.log(window.b2b.utils.user.getProfile());
```

**Example result:**

```json
{
  b2bId: 123456,
  companyRoleName: "Admin",
  customerGroupId: 2,
  emailAddress: "johndoe@example.com",
  firstName: "John",
  id: 20,
  lastName: "Doe"
  phoneNumber: "111-222-3333",
  role: 0
}
```

**Example fetch for B2B GraphQL token:**

```javascript
const token = window.b2b.utils.user.getB2BToken();
```

**Example using GraphQL token:**

```javascript
const user = window.b2b.utils.user.getProfile();
const b2bUserId = user.b2;
const token = window.b2b.utils.user.getB2BToken();

const result = await fetch('https://api-b2b.bigcommerce.com/graphql', {
    method: 'POST',
    headers: {
        Authorization: `Bearer ${token}`,
        Accept: 'application/json',
        'Content-Type': 'application/json',
    },
    body: JSON.stringify({
        query: `
        query GetUserCompany(
            $userId: Int!
        ) {
            userCompany(
                userId: $userId
            ) {
                id
                companyName
                companyStatus
            }
        }
        `,
        variables: {userId: b2bUserId},
    }),
}).then(res => res.json());
```

## Working with Quotes

**Adding products to quote:**

```javascript
window.b2b.utils.quote.addProducts([
    {
        quantity: 10,
        productEntityId: 1,
        sku: 'PRODUCT1',
    },
    {
        quantity: 10,
        productEntityId: 2,
        sku: 'PRODUCT2',
    }
]).then(
    () => { 
        // Success 
    },
    () => {
        // Failure
    }
);
```

**Example with variant ID:**

```javascript
window.b2b.utils.quote.addProducts([
    {
        quantity: 10,
        productEntityId: 1,
        variantEntityId: 10,
    },
    {
        quantity: 10,
        productEntityId: 2,
        variantEntityId: 20,
    }
]).then(
    // ...
);
```

**Example with addProductFromPage:**

```javascript
window.b2b.utils.quote.addProductFromPage(
    {
        quantity: 10,
        productEntityId: 1,
        sku: 'PRODUCT1',
    }
).then(
    // ...
);
```

**Example from cart:**

```javascript
window.b2b.utils.quote.addProductsFromCart()
    .then(
        () => {
            // Success
        },
        () => {
            // Failure
        }
    );
```

**Getting quote details:**

```javascript
console.log(window.b2b.utils.quote.getCurrent());
```

**Example quote details result:**

```json
{
  productList: [
    {
      basePrice: 50,
      id: "abc123...",
      optionSelections: [
        {
          optionId: 100,
          optionValue: 4,
        }
      ],
      primaryImage: "https://cdn11.bigcomerce.com/...",
      productId: 2,
      productName: "Example Product",
      quantity: 10,
      taxPrice: 3.24,
      variantId: 13,
      variantSku: "PRODUCT1-LG"
    }
  ]
}
```

## Working with Shopping Lists

**Create new shopping list example:**

```javascript
window.b2b.utils.shoppingList.createNewShoppingList(
    'Quarterly Re-stock', 
    'Standard re-stock list for per-quarter order'
).then(
    (list) => {
        console.log(list);
    },
    () => {
        // Failure
    }
);
```

**Example result:**

```json
{
  id: '67890',
  name: "Quarterly Re-stock",
  description: "Standard re-stock list for per-quarter order",
  customerInfo: {
    firstName: "John",
    lastName: "Doe",
    userId: 123456,
    email: "johndoe@example.com",
  },
  grandTotal: "0",
  totalDiscount: "0",
  totalTax: "0",
}
```

**Example adding products:**

```javascript
window.b2b.utils.shoppingList.addProductFromPage(
    {
        quantity: 10,
        productEntityId: 1,
        sku: 'PRODUCT1'
    }
).then(
    () => {
        // Success
    },
    () => {
        // Failure
    }
);
```

## Super Admins and Masquerade

**Start masquerade example:**

```javascript
window.b2b.utils.user.setMasqueradeCompany(123456);
```

**End masquerade example:**

```javascript
window.b2b.utils.user.endMasquerade();
```

[Next](./04_CustomizingBuyerPortal.md)
