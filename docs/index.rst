Introduction
============

This is the documentation for integration of Paylot inline javascript
client.

**NB:** Before you can start integrating Paylot, you will need a Paylot
account. Create a free account now if you haven’t already done so:
https://beta.paylot.co/signup.

After that, you can proceed to add a merchant/business at
https://beta.paylot.co/businesses/create

Once you have added your business details, you would be required to add
at least one payment processor to accept payments. This involves adding
a currency you would be collecting (**BTC, ETH, LTC, BCH**) and what you
prefer to store it as (For now, Naira).

Once you are done. You are good to go.

Paylot inline javascript client offers a simple, secure and convenient
payment flow for web and mobile. It can be integrated with a line of
code thereby making it the easiest way to start accepting payments. It
also makes it possible to start and end the payment flow on the same
page, thus combating redirect fatigue.

Here is a sample code that calls Paylot and also handles outcome.

**NB:** Please, note that the key used is your merchant key. To get this
key, go to your merchant profile by clicking one of your businesses on
your dashboard @ https://beta.paylot.co/dashboard and then clicking
profile on the sidebar.

+-------------------+------------------+
| Clicking Business | Clicking profile |
+===================+==================+
| |Image One|       | |Image Two|      |
+-------------------+------------------+

Integration Code
----------------

This HTML code shows a simple way to integrate Paylot into your webpage.

.. code:: html

   <form >
       <script src="https://paylot-payment-widget.herokuapp.com/js/client.js"></script>
       <button type="button" onclick="pay()"> Pay </button> 
   </form>

   <script>
     function pay(){
       paylot({
           amount: 10000,
           key: 'pyt_pk-6efec0d34c8147eba4de783714c6eae7',
           reference: Date.now(),
           currency: 'NGN',
           payload: {
               type: 'payment',
               subject: 'Test payment',
               email: 'john.doe@gmail.com',
               sendMail: true
           },
           onClose: function(){
               console.log('I just closed the payment modal');
           }
       }, (err, tx) => {
           if(err){
               console.log('An error has occured');
           }else{
               //Transaction was successful
               console.log(tx);
           }
       });
     }
   </script>

Configuration options
---------------------

(\* indicates required)

+-----------------------------------+-----------------------------------+
| Parameter                         | Description                       |
+===================================+===================================+
| amount \*                         | The amount to be paid (number)    |
+-----------------------------------+-----------------------------------+
| key \*                            | The merchant public key (string)  |
+-----------------------------------+-----------------------------------+
| reference \*                      | A unique reference that           |
|                                   | identifies your transaction. If   |
|                                   | not found, a random reference     |
|                                   | would be generated (string)       |
+-----------------------------------+-----------------------------------+
| currency\*                        | The base currency (NGN, BTC, ETH, |
|                                   | LTC & BCH allowed) (string)       |
+-----------------------------------+-----------------------------------+
| payload.email                     | The email of the customer         |
|                                   | (string)                          |
+-----------------------------------+-----------------------------------+
| payload.type                      | The type of payment (string)      |
+-----------------------------------+-----------------------------------+
| payload.sendMail                  | Determines whether an email       |
|                                   | should be sent to the user or not |
|                                   | (boolean)                         |
+-----------------------------------+-----------------------------------+
| onClose                           | Function called when popup is     |
|                                   | closed                            |
+-----------------------------------+-----------------------------------+

Callback Parameters
-------------------

The paylot function has the following signature.

.. code:: javascript

   function paylot(options, callback);

Options specifies the Configuration options as highlighted above while
callback takes the form of normal javascript callbacks i.e. accepts a
function with the following signature.

.. code:: javascript

   function callback(error, data);

Here, in the absence of errors, the data parameter will contain the
transaction details and is an object with the following properties
stated below.

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

**NB:** These are the same parameters posted to the call back url which
can be set in the business profile.

.. toctree:: 
   :caption: Table of Contents 
   :maxdepth: 2

   index
   verification

.. |Image One| image:: https://res.cloudinary.com/dozie/image/upload/v1536582441/paylot_instructions_01.png
.. |Image Two| image:: https://res.cloudinary.com/dozie/image/upload/v1536582444/paylot_instructions_02.png

