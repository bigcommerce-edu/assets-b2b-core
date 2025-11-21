# REST API - Orders, Invoices, and Payments

## Orders

### Get Orders

```
GET https://api-b2b.bigcommerce.com/api/v3/io/orders?companyId={company_id}
```

### Get an Order

```
GET https://api-b2b.bigcommerce.com/api/v3/io/orders/{bcOrderId}
```

### Get Order Products

```
GET https://api-b2b.bigcommerce.com/api/v3/io/orders/{bcOrderId}/products
```

### Update an Order

```
PUT https://api-b2b.bigcommerce.com/api/v3/io/orders/{bcOrderId}

{
    "poNumber": "ah21",
    "status": "Complete"
}
```

### Update a Customer's BigCommerce Orders

```
PUT https://api-b2b.bigcommerce.com/api/v3/io/customers/{customerId}/orders/b2b
```

### Create an Order

```
POST https://api-b2b.bigcommerce.com/api/v3/io/orders

{
  "bcOrderId": 0,
  "customerId": 0,
  "poNumber": "bc156"
}
```

## Invoices

### Create an Invoice from an Order

```
POST https://api-b2b.bigcommerce.com/api/v3/io/ip/orders/{orderId}/invoices
```

### Create an Invoice

```
POST https://api-b2b.bigcommerce.com/api/v3/io/ip/invoices

{
  "invoiceNumber": "0000003",
  "originalBalance": {
    "code": "USD",
    "value": 500
  },
  "openBalance": {
    "code": "USD",
    "value": 100
  },
  "customerId": "{customer_Id}",
  "channelId": 1
}
```

### Get Invoices

```
GET https://api-b2b.bigcommerce.com/api/v3/io/ip/invoices
```

### Update an Invoice

```
PUT https://api-b2b.bigcommerce.com/api/v3/io/ip/invoices/{invoiceId}
```

### Export an Invoice as a PDF

```
GET  https://api-b2b.bigcommerce.com/api/v3/io/ip/invoices/{invoiceId}/download-pdf
```

### Delete an Invoice

```
DELETE https://api-b2b.bigcommerce.com/api/v3/io/ip/invoices/{invoiceId}
```

## Payments

### Get a List of Payments

```
GET https://api-b2b.bigcommerce.com/api/v3/io/ip/payments
```

### Update Payment Processing Status

```
PUT https://api-b2b.bigcommerce.com/api/v3/io/ip/payments/{paymentId}/processing-status

{
  "processingStatus": 3
}
```

## Payment Methods

### Get Payment Methods

```
GET  https://api-b2b.bigcommerce.com/api/v3/io/company-payment-methods
```

### Get Company Payments

```
GET https://api-b2b.bigcommerce.com/api/v3/io/companies/{companyId}/payments
```

### Update Company Payments

```
PUT https://api-b2b.bigcommerce.com/api/v3/io/companies/{companyId}/payments

{
  "payments": [
    {
      "code": "cheque",
      "isEnabled": true
    },
    {
      "code": "braintree",
      "isEnabled": true
    },
    {
      "code": "authorizenet",
      "isEnabled": false
    }
  ]
}
```
