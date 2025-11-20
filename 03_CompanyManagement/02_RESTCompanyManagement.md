# REST API - Company Management

## Get a List of Company Accounts

```
GET https://api-b2b.bigcommerce.com/api/v3/io/companies
```

## Update a Company Status

```
PUT https://api-b2b.bigcommerce.com/api/v3/io/companies/{companyId}/status

{
    "companyStatus": 1
}
```

## Creating Company Accounts

```
POST https://api-b2b.bigcommerce.com/api/v3/io/companies

{
    "companyName": "V2 Test Company",
    "companyPhone": "111-222-3333",
    "companyEmail": "email@company.com",
    "addressLine1": "987 Park Place",
    "city": "Austin",
    "state": "Texas",
    "country": "United States",
    "zipCode": "78726",
    "adminFirstName": "John",
    "adminLastName": "Foo",
    "adminEmail": "email@company.com",
    "adminPhoneNumber": "222-333-4444",
    "customerGroupId": 4,
    "channelIds": [1]
}
```

## Updating Company Information

```
PUT https://api-b2b.bigcommerce.com/api/v3/io/companies/{companyId}

{
    "companyName": "{Your company name}",
    "companyEmail": "{Your email address}",
    "companyPhone": "{Company phone number}",
    "addressLine1": "{Company address}",
    "city": "{Your city}",
    "state": "{Your state}",
    "country": "{Your country}",
    "zipCode": "{Your zip code}"
}
```

## Get a List of Addresses

```
GET https://api-b2b.bigcommerce.com/api/v3/io/addresses
```

**Example filtered request:**

```
GET https://api-b2b.bigcommerce.com/api/v3/io/addresses?companyId={{company_id}}&isShipping=true
```

## Create a Company Address

```
POST  https://api-b2b.bigcommerce.com/api/v3/io/companies

{
    "addressLine1": "321 Park Place",
    "addressLine2": "Ste 3",
    "city": "Austin",
    "stateCode": "TX",
    "countryCode": "US",
    "zipCode": "78726",
    "firstName": "Jane",
    "lastName": "Foo",
    "isBilling": true,
    "isDefaultBilling": true,
    "isShipping": true,
    "isDefaultShipping": true,
    "phoneNumber": "888-777-6666",
    "companyId": {{company_id}},
    "label": "Main Address"
}
```

## Get a List of Users

```
GET https://api-b2b.bigcommerce.com/api/v3/io/users
```

**Example filtered request:**

```
GET https://api-b2b.bigcommerce.com/api/v3/io/users?companyId={{company_id}}
```

## Create a User

**Example using static role:**

```
POST https://api-b2b.bigcommerce.com/api/v3/io/users

{
    "companyId": {{company_id}},
    "channelIds": [1],
    "email": "email@company.com",
    "firstName": "Jack",
    "lastName": "Foo",
    "phoneNumber": "444-777-9999",
    "role": 2
}
```

**Example using companyRoleId:**

```
POST https://api-b2b.bigcommerce.com/api/v3/io/users

{
    "companyId": {{company_id}},
    "channelIds": [1],
    "email": "email@company.com",
    "firstName": "Jack",
    "lastName": "Foo",
    "phoneNumber": "444-777-9999",
    "companyRoleId": 11223
}
```
