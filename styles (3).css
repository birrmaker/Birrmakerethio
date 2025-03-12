<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Investment Platform Demo</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background: #f2f2f2;
      margin: 0;
      padding: 0;
    }
    h1, h2, h3 {
      color: #2a2a72;
    }
    button {
      background: #ff4d4d;
      border: none;
      color: white;
      padding: 10px 20px;
      margin: 5px;
      cursor: pointer;
      font-size: 16px;
      border-radius: 4px;
    }
    button:hover {
      background: #e60000;
    }
    nav {
      background: #2a2a72;
      padding: 10px;
      display: flex;
      justify-content: space-around;
      align-items: center;
    }
    nav button {
      background: #ff4d4d;
      flex: 1;
      margin: 0 5px;
    }
    .section {
      padding: 20px;
      background: white;
      margin: 20px;
      border-radius: 8px;
      box-shadow: 0 2px 5px rgba(0,0,0,0.1);
    }
    .product {
      border-bottom: 1px solid #ddd;
      padding: 10px 0;
    }
    /* Modal Styles */
    .modalOverlay {
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background: rgba(0,0,0,0.5);
      display: none;
      justify-content: center;
      align-items: center;
      z-index: 1000;
    }
    .modalContent {
      background: white;
      padding: 20px;
      border-radius: 8px;
      width: 300px;
      text-align: center;
    }
  </style>
</head>
<body>

  <!-- Sign Up Section -->
  <div id="signupSection" class="section">
    <h1>Welcome to the Investment Platform</h1>
    <button id="signupBtn">Sign Up</button>
  </div>

  <!-- Welcome Intro Section (5 seconds) -->
  <div id="welcomeSection" class="section" style="display:none;">
    <h2>Welcome Intro</h2>
    <p>Get ready to explore our platform!</p>
  </div>

  <!-- Main Platform Section -->
  <div id="mainSection" style="display:none;">
    <nav>
      <button data-section="home">Home</button>
      <button data-section="products">Products</button>
      <button data-section="myProducts">My Products</button>
      <button data-section="myPage">My Page</button>
    </nav>

    <!-- Home Section -->
    <div id="homeSection" class="section">
      <h2>Home</h2>
      <p>This platform allows you to invest in various products with daily income. Choose a product, pay using your preferred bank method, and track your investments!</p>
    </div>

    <!-- Products Section -->
    <div id="productsSection" class="section" style="display:none;">
      <h2>Products</h2>
      <div id="productList"></div>
    </div>

    <!-- My Products Section -->
    <div id="myProductsSection" class="section" style="display:none;">
      <h2>My Products</h2>
      <p>Purchased products will appear here.</p>
      <ul id="purchasedList"></ul>
    </div>

    <!-- My Page Section -->
    <div id="myPageSection" class="section" style="display:none;">
      <h2>My Page</h2>
      <p>Balance: <span id="balance">80</span> birr</p>
      <p>
        Referral Link: 
        <input type="text" value="https://yourplatform.com/referral?code=XYZ" readonly style="width:80%;">
      </p>
      <button id="withdrawBtn">Withdraw</button>
      <div id="withdrawSection" style="display:none;">
        <h3>Withdraw Funds</h3>
        <select id="withdrawBank">
          <option value="cbe">CBE</option>
          <option value="mpessa">Mpessa</option>
          <option value="telebirr">Telebirr</option>
        </select>
        <input type="number" id="withdrawAmount" placeholder="Amount" style="padding:5px; margin:5px;">
        <button id="confirmWithdraw">Confirm Withdraw</button>
        <p id="withdrawStatus"></p>
      </div>
    </div>
  </div>

  <!-- Payment Modal -->
  <div id="paymentModal" class="modalOverlay">
    <div class="modalContent">
      <h3>Choose Bank Method</h3>
      <button class="bankOption" data-bank="cbe">CBE</button>
      <button class="bankOption" data-bank="telebirr">Telebirr</button>
      <button class="bankOption" data-bank="mpessa">Mpessa</button>
      <div id="bankInfo" style="display:none; margin-top:10px;">
        <p>Account Number: <span id="accountNumber"></span></p>
        <p>
          Transaction ID: 
          <input type="text" id="tnxId" placeholder="Enter Tnx ID">
        </p>
        <p>Upload Screenshot:</p>
        <input type="file" id="screenshotInput" accept="image/*">
        <button id="submitPayment">Submit Payment</button>
        <button id="closeModal">Close</button>
      </div>
    </div>
  </div>

  <!-- Telegram Modal -->
  <div id="telegramModal" class="modalOverlay">
    <div class="modalContent">
      <h3>Payment Submitted!</h3>
      <p>Your payment details have been sent to Telegram <br>
         <a href="https://t.me/birrmaker25" target="_blank" style="color:#ff4d4d; text-decoration:none;">@birrmaker25</a>
      </p>
      <button id="closeTelegramModal">Close</button>
    </div>
  </div>

  <script>
    var selectedBank = "";
    
    // Sign up button click: show welcome intro for 5 seconds then main interface
    document.getElementById('signupBtn').addEventListener('click', function() {
      document.getElementById('signupSection').style.display = 'none';
      document.getElementById('welcomeSection').style.display = 'block';
      setTimeout(function(){
          document.getElementById('welcomeSection').style.display = 'none';
          document.getElementById('mainSection').style.display = 'block';
          showSection('home');
      }, 5000);
    });

    // Navigation: show the requested section and hide others
    function showSection(section) {
      // Hide all main sections first
      document.getElementById('homeSection').style.display = 'none';
      document.getElementById('productsSection').style.display = 'none';
      document.getElementById('myProductsSection').style.display = 'none';
      document.getElementById('myPageSection').style.display = 'none';

      if(section === 'home'){
        document.getElementById('homeSection').style.display = 'block';
      } else if(section === 'products'){
        document.getElementById('productsSection').style.display = 'block';
        loadProducts();
      } else if(section === 'myProducts'){
        document.getElementById('myProductsSection').style.display = 'block';
      } else if(section === 'myPage'){
        document.getElementById('myPageSection').style.display = 'block';
      }
    }

    document.querySelectorAll('nav button').forEach(function(btn){
      btn.addEventListener('click', function(){
         var section = btn.getAttribute('data-section');
         showSection(section);
      });
    });

    // Create sample data for 20 products with requested pattern:
    // Product 1: price=500, dailyIncome=150, time=30 days
    // Product 2: price=1000, dailyIncome=300, time=30 days, etc.
    var products = [];
    for(var i = 1; i <= 20; i++){
      products.push({
          name: 'Product ' + i,
          price: i * 500,
          dailyIncome: i * 150,
          timeSet: "30 days"
      });
    }

    // Populate products into the products section
    function loadProducts(){
      var productList = document.getElementById('productList');
      productList.innerHTML = '';
      products.forEach(function(product, index){
         var productDiv = document.createElement('div');
         productDiv.className = 'product';
         productDiv.innerHTML = '<h4>' + product.name + '</h4>' +
                                '<p>Price: ' + product.price + ' birr</p>' +
                                '<p>Daily Income: ' + product.dailyIncome + ' birr</p>' +
                                '<p>Time: ' + product.timeSet + '</p>' +
                                '<button class="payBtn" data-index="' + index + '">Pay</button>';
         productList.appendChild(productDiv);
      });
    }

    // Handle clicks on any pay button using event delegation
    document.getElementById('productList').addEventListener('click', function(e){
      if(e.target && e.target.className === 'payBtn'){
         // Optionally, store the product index for later use
         document.getElementById('paymentModal').style.display = 'flex';
      }
    });

    // Map bank details
    var bankDetails = {
      cbe: '1000579029009',
      telebirr: '0910228603',
      mpessa: '0716062746'
    };

    // When a bank option is clicked, store the selected bank and show its info
    document.querySelectorAll('.bankOption').forEach(function(btn){
      btn.addEventListener('click', function(){
         selectedBank = btn.getAttribute('data-bank');
         document.getElementById('bankInfo').style.display = 'block';
         document.getElementById('accountNumber').innerText = bankDetails[selectedBank];
      });
    });

    // Submit Payment: validate Tnx ID and screenshot, then simulate sending to Telegram
    document.getElementById('submitPayment').addEventListener('click', function(){
       var tnxId = document.getElementById('tnxId').value.trim();
       var screenshotInput = document.getElementById('screenshotInput');
       if(tnxId === ""){
         alert("Please enter Transaction ID");
         return;
       }
       if(screenshotInput.files.length === 0){
         alert("Please upload a screenshot");
         return;
       }
       // In a real implementation, use a server-side script to handle file upload
       // and integrate with the Telegram Bot API to send the data to @birrmaker25.
       
       // Simulate sending by closing the payment modal and showing the Telegram modal
       document.getElementById('tnxId').value = "";
       screenshotInput.value = "";
       document.getElementById('bankInfo').style.display = 'none';
       document.getElementById('paymentModal').style.display = 'none';
       document.getElementById('telegramModal').style.display = 'flex';
    });

    // Close the payment modal
    document.getElementById('closeModal').addEventListener('click', function(){
       document.getElementById('paymentModal').style.display = 'none';
       document.getElementById('bankInfo').style.display = 'none';
    });

    // Close Telegram modal
    document.getElementById('closeTelegramModal').addEventListener('click', function(){
       document.getElementById('telegramModal').style.display = 'none';
    });

    // Withdraw functionality: toggle withdraw section
    document.getElementById('withdrawBtn').addEventListener('click', function(){
       var withdrawSection = document.getElementById('withdrawSection');
       withdrawSection.style.display = (withdrawSection.style.display === 'none' || withdrawSection.style.display === '') ? 'block' : 'none';
    });

    // Process withdrawal (simulated with a timer; for demo, 10 seconds instead of 10 minutes)
    document.getElementById('confirmWithdraw').addEventListener('click', function(){
        var bank = document.getElementById('withdrawBank').value;
        var amount = document.getElementById('withdrawAmount').value;
        if(amount <= 0){
           alert('Please enter a valid amount');
           return;
        }
        document.getElementById('withdrawStatus').innerText = 'Processing withdrawal...';
        // Simulated process time (use 600000 for 10 minutes in production)
        setTimeout(function(){
           document.getElementById('withdrawStatus').innerText = 'Withdrawal complete. Please contact support on Telegram @birrmaker25';
        }, 10000);
    });
  </script>
</body>
</html>