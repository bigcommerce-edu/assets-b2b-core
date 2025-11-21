# REST API - Specialized Users

## Sales Staff

### Get Sales Staff

```
GET https://api-b2b.bigcommerce.com/api/v3/io/sales-staffs
```

### Get a Sales Staff

```
GET https://api-b2b.bigcommerce.com/api/v3/io/sales-staffs/{salesStaffId}
```

### Update a Sales Staff

```
PUT https://api-b2b.bigcommerce.com/api/v3/io/sales-staffs/{salesStaffId}

[
  {
    "companyId": 0,
    "assignStatus": true
  }
]
```

## Super Admin

### Get a Company's Super Admins

```
GET https://api-b2b.bigcommerce.com/api/v3/io/companies/{companyId}/super-admins
```

### Update a Company's Super Admins

```
PUT https://api-b2b.bigcommerce.com/api/v3/io/companies/{companyId}/super-admins

{
  "superAdmins": [
    {
      "superAdminId": 1,
      "isAssigned": true
    },
    {
      "superAdminId": 2,
      "isAssigned": true
    }
  ]
}
```

### Create a Super Admin User

```
POST https://api-b2b.bigcommerce.com/api/v3/io/super-admins

{
  "firstName": "Tom",
  "lastName": "Cat",
  "phone": "0000000000",
  "email": "Tom@gmail.com",
  "uuid": ""
}
```

### Update a Super Admin

```
PUT https://api-b2b.bigcommerce.com/api/v3/io/super-admins/info/{superAdminId}

{
  "firstName": "string",
  "lastName": "string",
  "uuid": "string",
  "phone": "string",
  "channelIds": [
    0
  ]
}
```

### Get Super Admin Information with Company Count

```
GET https://api-b2b.bigcommerce.com/api/v3/io/companies/super-admins
```

### Get Companies of a Super Admin

```
GET https://api-b2b.bigcommerce.com/api/v3/io/super-admins/{superAdminId}/companies
```
