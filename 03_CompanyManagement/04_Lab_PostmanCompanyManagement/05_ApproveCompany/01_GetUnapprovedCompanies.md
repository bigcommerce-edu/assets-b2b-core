# Get Unapproved Companies

Request method:
GET

URL:
```
https://api-b2b.bigcommerce.com/api/v3/io/companies?companyStatus=0
```

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

const companies = pm.response.json().data;
pm.test('Response includes at least one company', () => {
    pm.expect(
        companies
    ).to.be.a('array');

    pm.expect(
        companies?.length
    ).to.be.greaterThan(0);
});

pm.collectionVariables.unset('pending_company_id');
if (Array.isArray(companies)) {
    const pendingCompanies = companies.filter(company => company.companyStatus === 0);
    if (pendingCompanies.length > 0) {
        pm.collectionVariables.set('pending_company_id', pendingCompanies[0]?.companyId);
    }
}
```