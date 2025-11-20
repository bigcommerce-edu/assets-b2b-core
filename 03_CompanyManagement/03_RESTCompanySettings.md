# REST API - Company Settings

## Roles and Permissions

### Get Roles

```
GET https://api-b2b.bigcommerce.com/api/v3/io/companies/roles
```

### Create Custom Role

```
POST https://api-b2b.bigcommerce.com/api/v3/io/companies/roles

{
  "name": "Custom test 2",
  "permissions": [
    {
      "code": "get_addresses",
      "permissionLevel": 2
    },
    {
        "code": "get_orders",
        "permissionLevel": 1
    },
    {
        "code": "get_quotes",
        "permissionLevel": 2
    }
  ]
}
```

### Get Company Role Details

```
GET https://api-b2b.bigcommerce.com/api/v3/io/companies/roles/{roleId}
```

### Get All Permissions

```
GET https://api-b2b.bigcommerce.com/api/v3/io/companies/permissions
```

## Company Credit and Payment Terms

### Get Company Credit

```
GET https://api-b2b.bigcommerce.com/api/v3/io/companies/{company_id}/credit
```

### Update Company Credit

```
PUT https://api-b2b.bigcommerce.com/api/v3/io/companies/{company_id}/credit

{
        "creditEnabled": true,
        "creditCurrency": "USD",
        "availableCredit": 1000.0,
        "limitPurchases": false,
        "creditHold": false
}
```

### Get Company Payment Terms

```
GET https://api-b2b.bigcommerce.com/api/v3/io/companies/{companyId}/payment-terms
```

### Update Company Payment Terms

```
PUT https://api-b2b.bigcommerce.com/api/v3/io/companies/{companyId}/payment-terms

{
  "isEnabled": true,
  "paymentTerms": 30
}
```
