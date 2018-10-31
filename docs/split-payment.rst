Split Payments
==============

Split payments are necessary in cases where the merchant wants to split
payments with another entity or bank account. To enable split payments,
we use the concept of subaccounts. Sub accounts are bank accounts with
the split percentage specified. The following describe how to manage
subccounts on paylot.

**NB:** To manage your subaccounts, it’s required that you have your API
Secret key which can be accessed from your merchant profile on the
dashboard.

Requirements
------------

**API Url:** ``https://api.paylot.co``

All requests accept and return **JSON**.

For all stated requests, it’s required that you specify your **secret
key** in the authorization header i.e

``Authorizaion: Bearer SECRET_KEY``

This authenticates the specific merchant and ensures everything is done
in the confines of the 1 merchant.

**NB:** \*\* specifies required properties while \* specifies properties
required for fiat only.

Create Sub Accounts
-------------------

**URL:** ``POST /subAccounts``

This creates a new sub account.

Request
~~~~~~~

The expected request is a JSON object of the format stated below.

.. code:: json

   {
     "currency": "NGN",
     "accountName": "JOHN & SONS Ltd.",
     "accountNumber": "0050505022",
     "bankName": "ACCESS BANK",
     "schedule": "auto",
     "percentage": 70
   }

+--------------------------------------+--------------------------------+
| Property                             | Description                    |
+======================================+================================+
| currency \*\*                        | This specifies the currency of |
|                                      | the account. (Possible         |
|                                      | options: NGN)                  |
+--------------------------------------+--------------------------------+
| accountNumber \*\*                   | This specifies the bank        |
|                                      | account number or for digital  |
|                                      | currencies, the wallet address |
+--------------------------------------+--------------------------------+
| bankName \*                          | This specifies the bank name   |
|                                      | or for digital currencies, the |
|                                      | wallet name (optional for      |
|                                      | digital currencies)            |
+--------------------------------------+--------------------------------+
| accountName \*                       | This specifies the name of the |
|                                      | bank account or optional for   |
|                                      | digital currencies             |
+--------------------------------------+--------------------------------+
| schedule                             | This specifies how often the   |
|                                      | subaccount should receive      |
|                                      | payouts. The dafault is auto   |
|                                      | (24 hours interval). Other     |
|                                      | options are coming soon.       |
+--------------------------------------+--------------------------------+
| percentage \*\*                      | This specifies the the         |
|                                      | percentage of payment they are |
|                                      | expected to receive            |
+--------------------------------------+--------------------------------+

Response
~~~~~~~~

The expected response is a JSON object of the format stated below.

.. code:: json

   {
     "accountName": "JOHN & SONS Ltd.",
     "accountNumber": "0050505022",
     "bankName": "ACCESS BANK",
     "schedule": "auto",
     "percentage": 70,
     "reference": "1876187618761876"
   }

The *reference* is a uniquely generated code for each subaccount and
it’s required for initializing split payments.

Update Sub Accounts
-------------------

**URL:** ``PUT /subAccounts/{id}``

This updates a specified subaccount by it’s id.

.. _request-1:

Request
~~~~~~~

The expected request is a JSON object of the format stated below.

.. code:: json

   {
     "currency": "NGN",
     "accountName": "JOHN & SONS Ltd.",
     "accountNumber": "0050505022",
     "bankName": "ACCESS BANK",
     "schedule": "auto",
     "percentage": 70
   }

**NB:** Same as in Create sub accounts above

.. _response-1:

Response
~~~~~~~~

The expected response is a JSON object of the format stated below.

.. code:: json

   {
     "accountName": "JOHN & SONS Ltd.",
     "accountNumber": "0050505022",
     "bankName": "ACCESS BANK",
     "schedule": "auto",
     "percentage": 70,
     "reference": "1876187618761876"
   }

Get All Sub Accounts
--------------------

**URL:** ``GET /subAccounts``

This gets all the subaccounts of a specific merchant.

.. _response-2:

Response
~~~~~~~~

The expected response is a JSON object of the format stated below.

.. code:: json

   [{
     "id": "1",
     "currency": {
         symbol: "NGN",
         name: "Naira"
     },
     "accountName": "JOHN & SONS Ltd.",
     "accountNumber": "0050505022",
     "bankName": "ACCESS BANK",
     "schedule": "auto",
     "percentage": 70,
     "reference": "1876187618761876"
   },{
     "id": "2",
     "currency": {
         symbol: "NGN",
         name: "Naira"
     },
     "accountName": "JOHN & SONS Ltd.",
     "accountNumber": "0050505022",
     "bankName": "ACCESS BANK",
     "schedule": "auto",
     "percentage": 70,
     "reference": "1876187618761876"
   }]

Get Sub Account
---------------

**URL:** ``GET /subAccounts/{id}``

This fetches a subaccount by it’s id.

.. _response-3:

Response
~~~~~~~~

The expected response is a JSON object of the format stated below.

.. code:: json

   {
     "id": "1",
     "currency": {
         symbol: "NGN",
         name: "Naira"
     },
     "accountName": "JOHN & SONS Ltd.",
     "accountNumber": "0050505022",
     "bankName": "ACCESS BANK",
     "schedule": "auto",
     "percentage": 70,
     "reference": "1876187618761876"
   }

**URL:** ``GET /subAccounts/ref/{reference}``

This fetches a subaccount by it’s reference.

.. _response-4:

Response
~~~~~~~~

The expected response is a JSON object of the format stated below.

.. code:: json

   {
     "currency": {
         symbol: "NGN",
         name: "Naira"
     },
     "accountName": "JOHN & SONS Ltd.",
     "accountNumber": "0050505022",
     "bankName": "ACCESS BANK",
     "schedule": "auto",
     "percentage": 70,
     "reference": "1876187618761876"
   }

Usage
-----

To split payments with a subaccount, it is required that you specify the
reference of the subaccount while initializing a transaction. Check the
integration section for more.
