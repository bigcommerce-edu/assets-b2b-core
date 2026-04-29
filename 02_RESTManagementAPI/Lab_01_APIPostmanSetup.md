# Lab - API Account and Postman Setup

## Introduction

To facilitate the API workflows, you will need to create a B2B Edition API account and do initial setup in the REST client.

### Prerequisites

* A BigCommerce [sandbox store](https://docs.bigcommerce.com/developer/docs/overview/sandboxes) or [trial store](https://www.bigcommerce.com/essentials/), or a full production store
* B2B Edition enabled in your store
* [Postman](https://www.postman.com/) or a similar API client


### In this lab, you will:

* Generate a store-level API account token
* Create a Postman environment, collection, and headers preset
* Run a test API request


## Step 1: Create an API Account

1. **Log in** to your BigCommerce control panel and **navigate**to Settings &gt; API &gt; Store-level API accounts.
2. **Create** an API account.
3. **Select** "V2/V3 API token" as the token type and **enter** a name.
4. Under "OAuth scopes," **select** "modify" for "B2B Edition".
5. **Save** the API account.


   After saving your API account, you will be presented with a dialog containing info including an access token. Be sure to copy this value before closing the modal, as it will not be retrievable afterward.

6. **Copy** the access token and **store** it securely where you will be able to access it in the next step.
7. **Copy** your store's unique store hash, which can be found in your control panel URL. For example, in the control panel URL `https://store-abcd1234.mybigcommerce.com`, the store hash is **abcd1234**.


## Step 2: Configure a Postman Environment

All subsequent steps will take place in the Postman API client.

1. **Create** a new Postman environment with the following variables.


   | Variable Name | Value |
   | --- | --- |
   | v3_token | The access token of your API account |
   | store_hash | Your store hash |
   | storefront_channel_id | 1 |

<blockquote>
Note that the value set for `storefront_ channel_id` is 1, which assumes the default channel for a given store.  If your store has multiple storefront channels and you intend to utilize a different channel, use the appropriate channel ID.
A channel's ID can be obtained by inspecting channel information via the REST Management API, or from the control panel URL when viewing the channel's settings in Channels.
</blockquote>

2. **Create** a new collection and give it an appropriate name, such as "B2B Core REST."
3. **Select** your new environment from the environment drop-down at the top of the Postman interface.

The correct value must be selected from the environment drop-down whenever you send a request, in order to ensure the appropriate token is used.

## Step 3: Create Your First Request

1. **Create** a new HTTP request called "Get Company Roles."
2. In the Headers tab, use the Presets drop-down to **Manage Presets**, then **add** a header preset with the following values, saving it with a name like "B2B REST."


   | Field | Value |
   |---|---|
   | Accept | application/json |
   | Content-Type | application/json |
   | X-Auth-Token | `{{v3_token}}` |
   | X-Store-Hash | `{{store_hash}}` |

<Callout>
Make sure to enter e.g., `{{v3_token}}` exactly as it appears. This is a reference to the environment variable you created and will inject its value.
</Callout>

This headers Preset will allow you to apply the same headers to all subsequent requests without needing to re-enter them individually.

3. **Select** your newly created header preset to populate headers.
4. **Configure** the remaining details of your request as follows.


   | Field | Value |
   |---|---|
   | Method | GET |
   | URL | `https://api-b2b.bigcommerce.com/api/v3/io/companies/roles` |

5. **Send** the request.

If your configuration is correct, you should see a list of your store's company roles in the response. At minimum, this should include the built-in Admin, Senior Buyer, and Junior Buyer roles.

## Step 4: Import Collection

Import the [B2B Core Labs collection](../B2B%20Core%20Labs.postman_collection.json).
