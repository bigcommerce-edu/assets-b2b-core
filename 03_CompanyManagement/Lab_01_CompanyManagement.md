# Lab - Postman Company Management Workflow

### Prerequisites

* A BigCommerce [sandbox store](https://developer.bigcommerce.com/docs/start/about/sandboxes) or [trial store](https://www.bigcommerce.com/essentials/), or a full production store
* B2B Edition enabled in your store
* [Postman](https://www.postman.com/) or a similar API client
* An existing Postman environment, collection, and headers preset as configured in previous labs

## Company Exercises

Try the following requests in the "Companies" folder.

For each request, verify that all tests succeed.

### Create Company

* **Verify** the new company exists in the B2B Edition control panel, in the "Approved" status.
* **Record** the `companyId` value from the API response for use in the next requests.

#### Automated Request

The automated version of the request should save `company_id` in the collection variables.

### Get Companies

* **Observe** the company response data.
* **Try out** the `companyStatus` query param to filter on status "0" (Unapproved).

#### Automated Request

The automated version of the request should already be filtered on "Unapproved" status and save a `pending_company_id` collection variable for the approval step.

### Get Company

* **Enter** the previously captured company ID for the `:company_id` path variable.
* **Observe** the company response data.

#### Automated Request

The automated version of the request should have `:company_id` automatically populated.

### Update Company

* **Enter** a company ID for the `:company_id` path variable.
* **Edit** the Body details as you please.
* **Verify** company data is updated accordingly.

#### Automated Request

The automated version of the request should have `:company_id` automatically populated.
