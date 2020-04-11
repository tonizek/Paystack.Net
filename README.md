# Paystack.Net
Integrating Paystack for Asp.net C# is made simple or simplified 

to connect your .net web application to paystack should not be that deficult, I have search through all the reposatory provided by even paystack itself, that was like play with a giant lip.

follow below:

to connect to their site through you site, is simple
copy and paste this 
<form id="paymentForm">
            <script src="https://js.paystack.co/v1/inline.js"></script>
            <div class="form-group">
                <label for="email">Email Address</label>
                <input type="email" id="email-address" required />
                <br>
            </div>
            <div class="form-group">
                <label for="amount">Amount</label>
                <input type="tel" id="amount" required />
                <br>
            </div>
            <div class="form-group">
                <label for="first-name">First Name</label>
                <input type="text" id="first-name" />
                <br>
            </div>
            <div class="form-group">
                <label for="last-name">Last Name</label>
                <input type="text" id="last-name" />
                <br>
            </div>
            <div class="form-submit">
                <button type="submit"> Pay </button>
            </div>
        </form>
       <script src="https://code.jquery.com/jquery-3.4.1.slim.min.js"></script>
       <script src="/Scripts/paystackJS.js"></script>

  ---------------------------------------------------------------------------------------------------------------------
  create a javascript file and name it paystackJs.js
  and then copy this below into it
  ----------------------------------------------------------------------------------------------------------------------
  function payWithPaystack() {
    var handler = PaystackPop.setup({
        key: 'pk_test_1dd48db3358dc78a60417dff17d03d1fc69874ad', // Replace with your public key
        email: document.getElementById("email-address").value,
        amount: document.getElementById("amount").value * 100,
        firstname: document.getElementById("first-name").value,
        lastname: document.getElementById("first-name").value,
        ref: '' + Math.floor((Math.random() * 1000000000) + 1), // generates a pseudo-unique reference. Please replace with a reference you generated. Or remove the line entirely so our API will generate one for you
        // label: "Optional string that replaces customer email"
        onClose: function () {
            alert('Window closed.');
        },
        // On the  callback function, you can redirect to another page, passing the transaction reference 
        callback: function (response) {
            //var message = 'Payment complete! Reference: ' + response.reference;
            //alert(message);
            window.location = "https://localhost:44340/Home/RequestPayment?reference=" + response.reference;
        }
    });
    handler.openIframe();
}
$('#paymentForm').on('submit', function (event) {
    event.preventDefault();
    payWithPaystack();
    return false;
});
-------------------------------------------------------------------------------------------------------
Make sure you have a jquery version jquery-3.4.1 running on you progrram https://code.jquery.com/jquery-3.4.1.slim.min.js
