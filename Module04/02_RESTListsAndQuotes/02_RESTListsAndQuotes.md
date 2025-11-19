# REST API - Shopping Lists and Quotes

## Shopping Lists

### Get Shopping Lists

**Get lists filtered by user:**

```
GET https://api-b2b.bigcommerce.com/api/v3/io/shopping-list?userId={userId}
```

**Get list:**

```
GET https://api-b2b.bigcommerce.com/api/v3/io/shopping-list/{shoppingListId}
```

### Create a Shopping List

```
POST https://api-b2b.bigcommerce.com/api/v3/io/shopping-list

{
  "name": "my first shopping list",
  "userId": 0,
  "status": 0,
  "items": [
    {
      "productId": 123,
      "variantId": 321,
      "quantity": 5
    },
        {
      "productId": 123,
      "variantId": 321,
      "quantity": 5
    },
        {
      "productId": 123,
      "variantId": 321,
      "quantity": 5
    }
  ]
}
```

### Update a Shopping List

```
PUT https://api-b2b.bigcommerce.com/api/v3/io/shopping-list/{shoppingListId}

{
  "name": "test",
  "description": "my first shopping list",
  "status": 40,
  "items": [
    {
      "id": 75693,
      "productId": 123,
      "variantId": 321,
      "quantity": 0
    },
    {
      "id": 85416,
      "productId": 123,
      "variantId": 321,
      "quantity": 5
    },
    {
      "id": 76533,
      "productId": 123,
      "variantId": 321,
      "quantity": 1
    }
  ]
}
```

## Quotes

### Get a List of Requests for Quotes

```
GET https://api.bundleb2b.net/api/v3/io/rfq
```

### Create a RFQ

```
POST  https://api.bundleb2b.net/api/v3/io/rfq

{
  "grandTotal": 0,
  "discount": 0,
  "totalAmount": 0,
  "subtotal": 0,
  "userEmail": "string",
  "quoteTitle": "string",
  "expiredAt": "string",
  "shippingAddress": {
    "country": "string",
    "state": "string",
    "city": "string",
    "zipCode": "string",
    "address": "string",
    "apartment": "string"
  },
  "contactInfo": {
    "name": "string",
    "email": "string"
  },
  "productList": [
    {
      "sku": "string",
      "basePrice": 0,
      "discount": 0,
      "offeredPrice": 0,
      "quantity": 0,
      "productId": 0,
      "variantId": 0,
      "imageUrl": "string",
      "orderQuantityMaximum": 0,
      "orderQuantityMinimum": 0,
      "productName": "string",
      "options": [
        {
          "optionId": 0,
          "optionValue": 0,
          "optionLabel": "string",
          "optionName": "string"
        }
      ]
    }
  ]
}
```

### Update a Quote

```
PUT  https://api.bundleb2b.net/api/v3/io/rfq/{quote_id}
```

### Create Checkout Quote Form

```
POST   https://api-b2b.bigcommerce.com/api/v3/io/rfq/{quote_id}/checkout
```

### Send a Quote Email

```
POST   https://api-b2b.bigcommerce.com/api/v3/io/rfq/emails

{
  "quoteId": "string",
  "email": "string",
  "withAttach": 0,
  "emailTemplate": "Simple",
  "ccTo": [
    "string"
  ],
  "emailLang": "en"
}
```

### Export a Quote as a PDF

```
POST  https://api-b2b.bigcommerce.com/api/v3/io/rfq/{quote_id}/pdf-export
```
