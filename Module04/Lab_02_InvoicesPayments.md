# Lab - Postman Invoices and Payments Workflow

### Prerequisites

* A BigCommerce [sandbox store](https://developer.bigcommerce.com/docs/start/about/sandboxes) or [trial store](https://www.bigcommerce.com/essentials/), or a full production store
* B2B Edition enabled in your store
* [Postman](https://www.postman.com/) or a similar API client
* An existing Postman environment and collectionas configured in previous labs
* An existing company and Admin or Senior Buyer user login
* Minimal invoice settings as described below

### Required Invoice Settings

The lab will involve logging into your storefront as a company user and placing an order to pay an invoice. The following minimal settings are required in the B2B Edition section of your control panel:

* In Settings > General, "Invoices" must be checked under "Feature management."
* In Settings > Invoice, at least one valid option must be enabled under "Payment methods for paying invoices."


If you don't have a valid payment method option available in the invoice settings, make sure you have enabled a method other than Check/Purchase Order in the main Settings > Payments section of the BigCommerce control panel.

## Invoice Exercises

Try the following requests in the "Invoices" folder.

For each request, verify that all tests succeed.

### Create Invoice from Order

This request will generate an invoice using only an order ID, populating the invoice details from the order.

* **Enter** a valid B2B order ID for the `:order_id` path variable.
* **Verify** in the B2B Edition control panel that an accurate invoice has been created.
* **Record** the `invoiceId` from the API response data.

**AUTOMATION:** The automated version of the request should have `:order_id` populated from your previous "Get Recent Orders" request, and it should save `invoice_id` to the collection variables.

### Get Invoices / Get Old Open Invoices

* **Try out** filtering with the various query params, such as `customerId` with the ID of a valid company.
* **Observe** the invoice response data.

**AUTOMATION:** The automated version of the request is already filtered on status 0 and an `endDateAt` value automatically calculated to reflect invoices opened over 30 days ago.

### Get Invoice

* **Enter** the previously captured invoice ID for the `:invoice_id` path variable.
* **Observe** the invoice response data.

**AUTOMATION:** The automated version of the request should have `:invoice_id` populated from your previously created invoice.

### Export Invoice PDF

* **Enter** an invoice ID for the `:invoice_id` path variable.
* **Follow** the URL from the response and **verify** that this results in downloading a PDF with the details of the invoice.

**AUTOMATION:** The automated version of the request should have `:invoice_id` automatically populated.

## Payment Exercises

Try the following requests in the "Payments" folder.

For each request, verify that all tests succeed.

### Create Offline Payment

This request will _record_ a payment against an invoice, not capture funds.

* **Enter** an `invoiceId` in the Body, and enter an `amount` to pay. **Try** a partial or full amount for the invoice.
* **Enter** a valid company ID as `customerId` in the Body.
* **Verify** in the B2B Edition control panel or via the "Get Invoice" request that the payment was applied to the invoice.
* **Record** the `paymentId` from the API response.
* **Try out** making multiple partial payments for the same invoice.

**AUTOMATION:** The automated version of the request should have `invoiceId` and `customerId` automatically populated and will save `payment_id` in the collection variables.

### Get Payments / Get Invoice Payments

* **Try out** filtering on the various query params, such as `invoiceId` to retrieve payments for a specific invoice.
* **Observe** the payment response data.

**AUTOMATION:** The automated version of the request is already filtered on the ID of the previously created invoice.

### Update Payment Status

* **Enter** the previously captured payment ID for the `:payment_id` path variable.
* **Verify** in the B2B Edition control panel or via the "Get Invoice" request that the invoice reflects the settled payment.

**AUTOMATION:** The automated version of the request should have `:payment_id` automatically populated.

## Apply Payment as a User

If you used a payment amount less than the invoice's total open balance, the invoice still has a balance remaining.

Instead of applying an offline payment for the remaining amount, let's perform a BigCommerce checkout to pay it "online" as a company user.

1. **Log in** to your storefront as an Admin user for the company the invoice is associated with.
2. **Find** the invoice in the Invoice tab and **select**"Pay" from the invoice's action menu.
3. **Complete** the BigCommerce checkout to finish paying the open invoice balance.
4. **Re-run** the "Get Invoice Payments" request.

    You should now observe the multiple existing payments for the current invoice, with the most recent reflecting the details of an online transaction.

5. **Re-run** the "Get Invoice" request to observe the new _status_ and open balance.


