Paylot Integration
==================

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

Paylot Inline offers a simple, secure and convenient payment flow for
web and mobile. It can be integrated with a line of code thereby making
it the easiest way to start accepting payments. It also makes it
possible to start and end the payment flow on the same page, thus
combating redirect fatigue.

Here is a sample code that calls Paylot and also handles outcome.

**NB:** Please, note that the key used is your merchant key. To get this
key, go to your merchant profile by clicking one of your businesses on
your dashboard @ https://beta.paylot.co/dashboard and then clicking
profile on the sidebar.

.. figure:: https://paper.dropbox.com/ep/redirect/image?url=https%3A%2F%2Fd2mxuefqeaa7sj.cloudfront.net%2Fs_35814BAC5F7624142CDDFC983969C815F29CF37B2336DA8B86FD0AF1CAB80DB6_1531410955555_image.png&hmac=%2F4nRKSQKHKOD81K9wVYMXQxkF8LA%2BOIFZDum%2FNPqi8A%3D
   :alt: Image One

   Image One

.. figure:: https://paper.dropbox.com/ep/redirect/image?url=https%3A%2F%2Fd2mxuefqeaa7sj.cloudfront.net%2Fs_35814BAC5F7624142CDDFC983969C815F29CF37B2336DA8B86FD0AF1CAB80DB6_1531410653540_image.png&hmac=h2jGhD8grjEFqwKE45T6JVYm5QMvTvB9ED%2BENDgEohQ%3D
   :alt: Image Two

   Image Two

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
           secret: '498eac70-6fde-11e8-a9f9-1f1f6cb61ea8',
           merchant: '5b227a029674d8001475a19b',
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
       }, (tx, error) => {
           console.log(tx);
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
| merchant\*                        | The merchant Id (string)          |
+-----------------------------------+-----------------------------------+
| currency\*                        | The base currency (NGN, BTC, ETH, |
|                                   | LTC & BCH allowed) (string)       |
+-----------------------------------+-----------------------------------+
| secret\*                          | The merchant integration key      |
|                                   | (string)                          |
+-----------------------------------+-----------------------------------+
| payload.email                     | The email of the customer         |
|                                   | (string)                          |
+-----------------------------------+-----------------------------------+
| payload.type                      | The type of payment (string)      |
+-----------------------------------+-----------------------------------+
| p                                 |                                   |
+-----------------------------------+-----------------------------------+