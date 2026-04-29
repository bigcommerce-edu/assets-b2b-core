# Lab - Postman Quote and Order Workflow

### Prerequisites

* A BigCommerce [sandbox store](https://docs.bigcommerce.com/developer/docs/start/about/sandboxes) or [trial store](https://www.bigcommerce.com/essentials/), or a full production store
* B2B Edition enabled in your store
* [Postman](https://www.postman.com/) or a similar API client
* An existing Postman environment and collection as configured in previous labs
* An existing company and Admin or Senior Buyer user login
* Minimal quote/payment/shipping settings as described below

### Configure Shipping and Payments

In order to complete checkout, you'll need to make sure you have the appropriate minimal store configuration in place for shipping and payments.

If you've previously configured shipping and payment options for your store, you won't need to do any additional setup.

We won't walk through the details of configuring your store settings, but make sure you have:

* A [Shipping Zone](https://support.bigcommerce.com/s/article/Shipping-Zones) that applies to any billing address you will use at checkout
* An enabled [Shipping Method](https://support.bigcommerce.com/s/article/Shipping-Methods) on the Shipping Zone
* An enabled test/sandbox Payment Method. (Check the "Enable test credit card payments" option in your Payments Methods settings for the simplest option.) This will be necessary once we get to paying invoices.
* The "Check" payment method enabled

### Required B2B Quote/Payment Settings

The lab will involve logging in as a company user, creating, and submitting a quote-based order. The following minimal settings are required in the B2B Edition section of your control panel:

* In Settings > General, "Quotes" must be checked under "Feature Management."
* In Settings > Quotes, "Allow Quote Request for" should have "Company user" checked, and "Enable add to quote button" should be checked.
* In Settings > Checkout, the "Purchase Order Payment Method" should be enabled.
* The Payments settings for the company you will use for the storefront must not have been customized to exclude "PO" as an available payment option.

## Submit a Quote Request

For the steps ahead, you'll need the ability to log into your storefront with the credentials for an Admin user associated with a company.

If the only company users you have in your store so far are those you created via the API in previous labs, then these customers do not yet have a password set. (Typically, a password would be set by the customer after receiving a welcome email.) If this is the case, set a password in the control panel:

1. In the BigCommerce control panel, **navigate** to Customers and then to the customer associated with the email address of your company's Admin user.
2. **Set** a password for the customer and **save**.

   You'll also need to have quote requests submitted within the past 7 days. If your store doesn't contain any such quote requests, submit a request now from your storefront:

3. **Browse** to your storefront URL and **log in** with the credentials of a company user.
4. **Navigate** to a product page and use the "Add to quote" button to add the product to your request.
5. **Use** the "Open Quote" link in the success message, or **browse**to Account > Quotes and **select** the draft quote.
6. **Submit** the quote.

## Quote Exercises

Try the following requests in the "Quotes" folder.

For each request, verify that all tests succeed.

### Get RFQs / Get Recent RFQs

* **Try out** filtering on the various query params.
* **Observe** the quote response data.
* **Record** the `quoteId` of a quote in the results.

**AUTOMATION:** The automated version of the request should be filtered on status 0 and a `minCreated` value automatically calculated for the last 7 days, and `quote_id` should automatically be saved to the collection variables based on the first returned result.

### Get Quote Detail

* **Enter** the previously captured quote ID for the `:quote_id` path variable.
* **Observe** the quote response data.

**AUTOMATION:** The automated version of the request should have `:quote_id` automatically populated.

### Export Quote PDF

* **Enter** the previously captured quote ID for the `:quote_id` path variable.
* **Follow** the URL from the response and **verify** that this results in downloading a PDF with the details of the quote.

**AUTOMATION:** The automated version of the request should have `:quote_id` automatically populated.

### Get Quote Checkout

This request will generate a URL that can be used to check out with the quote.

* **Enter** the previously captured quote ID for the `:quote_id` path variable.
* **Follow** the URL from the response and **verify** that this results in initiating a checkout reflecting the quote details.
* **Complete** the checkout and **place** an order from the quote, using the Purchase Order payment method.

**AUTOMATION:** The automated version of the request should have `:quote_id` automatically populated.

## Order Exericses

Try the following requests in the "Orders" folder.

For each request, verify that all tests succeed.

### Get Orders / Get Recent Orders

* **Try out** filtering on the various query params, such as `companyId` to retrieve a single company's orders.
* **Observe** the order response data.
* **Record** the `id` and `bcOrderId` for one of the orders in the results.

**AUTOMATION:** The automated version of the request should be filtered on a `minCreated` value automatically calculated for the last 7 days, and `order_id` and `bc_order_id` should automatically be saved to the collection variables based on the first returned result.

### Get Order

* **Enter** the previously captured `bcOrderId` for the `:bc_order_id` path variable.
* **Observe** the order response data.

**AUTOMATION:** The automated version of the request should have `:bc_order_id` automatically populated.
