Transaction Verification
========================

In a situation where the call back url is not suitable, the developer
might require a way to query transactions to know the status of
transactions.

We have an API endpoint for checking transaction status with url as
stated below:

https://api.paylot.co/transactions/verify/{reference}

**reference:** This is the reference used while creating a transaction
or the reference returned in the callback.

To access this endpoint, the business secret key is required and this
secret key can be obtained at the business profile page.

This key should never be exposed to the public and is of the format:

*pyt_sk-123455****

To send a request, use bearer authentication with your secret key as
token i.e. add this to your request header.

*Authorization: Bearer pyt_sk-123455****

The API returns an object with the parameters described below.

+-----------------------------------+-----------------------------------+
| Parameter                         | Description                       |
+===================================+===================================+
| reference                         | The transaction reference. Pay    |
|                                   | attention to this if you didn’t   |
|                                   | create a reference manually.      |
|                                   | (string)                          |
+-----------------------------------+-----------------------------------+
| sent                              | Specifies if payment was made     |
|                                   | successfully (boolean)            |
+-----------------------------------+-----------------------------------+
| confirmed                         | Specifies if the payment has been |
|                                   | confirmed on the blockchain       |
|                                   | (boolean)                         |
+-----------------------------------+-----------------------------------+
| amount                            | Specifies the intended amount in  |
|                                   | the currency selected during      |
|                                   | payment (number)                  |
+-----------------------------------+-----------------------------------+
| amountSent                        | Specifies the actual amount that  |
|                                   | was sent to the blockchain        |
|                                   | (number)                          |
+-----------------------------------+-----------------------------------+
