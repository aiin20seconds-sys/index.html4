<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Ubaid Shaikh Restaurant - Digital Menu</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }

        body {
            background-color: #f9f9f9;
            color: #333;
            padding-bottom: 90px;
        }

        /* Welcome Overlay Modal for Audio Interaction */
        .welcome-overlay {
            position: fixed;
            top: 0; left: 0; right: 0; bottom: 0;
            background: rgba(0, 0, 0, 0.85);
            z-index: 1000;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 20px;
            text-align: center;
        }

        .welcome-box {
            background: #fff;
            padding: 35px 25px;
            border-radius: 20px;
            max-width: 350px;
            width: 100%;
            box-shadow: 0 10px 30px rgba(0,0,0,0.3);
        }

        .welcome-box h2 {
            color: #1a1a1a;
            margin-bottom: 10px;
            font-size: 1.4rem;
        }

        .welcome-box p {
            color: #666;
            font-size: 0.9rem;
            margin-bottom: 20px;
        }

        .enter-btn {
            background: #ffb703;
            color: #1a1a1a;
            border: none;
            padding: 12px 25px;
            border-radius: 10px;
            font-weight: 700;
            font-size: 1rem;
            cursor: pointer;
            width: 100%;
            transition: 0.2s;
        }

        .enter-btn:active {
            transform: scale(0.96);
        }

        /* Header */
        header {
            background: #1a1a1a;
            color: #fff;
            padding: 20px;
            text-align: center;
            position: sticky;
            top: 0;
            z-index: 100;
            box-shadow: 0 2px 10px rgba(0,0,0,0.1);
        }

        header h1 {
            font-size: 1.5rem;
            letter-spacing: 1px;
            color: #ffb703;
        }

        header p {
            font-size: 0.85rem;
            color: #ccc;
            margin-top: 4px;
        }

        /* Categories Navigation */
        .categories {
            display: flex;
            gap: 10px;
            overflow-x: auto;
            padding: 15px 20px;
            background: #fff;
            white-space: nowrap;
            border-bottom: 1px solid #eee;
        }

        .categories::-webkit-scrollbar {
            display: none;
        }

        .cat-btn {
            background: #f1f1f1;
            border: none;
            padding: 8px 16px;
            border-radius: 20px;
            font-size: 0.9rem;
            cursor: pointer;
            transition: 0.3s;
            font-weight: 500;
        }

        .cat-btn.active {
            background: #ffb703;
            color: #1a1a1a;
        }

        /* Menu Section */
        .menu-container {
            padding: 20px;
            max-width: 600px;
            margin: 0 auto;
        }

        .section-title {
            font-size: 1.2rem;
            margin-bottom: 15px;
            color: #1a1a1a;
            border-left: 4px solid #ffb703;
            padding-left: 8px;
        }

        .food-card {
            background: #fff;
            border-radius: 12px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 15px;
            margin-bottom: 15px;
            box-shadow: 0 4px 15px rgba(0,0,0,0.03);
            transition: transform 0.2s;
        }

        .food-card:hover {
            transform: translateY(-2px);
        }

        .food-info {
            flex-grow: 1;
            padding-right: 15px;
        }

        .food-name {
            font-size: 1rem;
            font-weight: 600;
            color: #222;
        }

        .food-desc {
            font-size: 0.8rem;
            color: #777;
            margin: 4px 0 8px 0;
        }

        .food-price {
            font-size: 0.95rem;
            font-weight: 700;
            color: #1a1a1a;
        }

        .add-btn {
            background: #1a1a1a;
            color: #ffb703;
            border: none;
            padding: 8px 18px;
            border-radius: 8px;
            cursor: pointer;
            font-weight: 600;
            font-size: 0.85rem;
            transition: 0.2s;
        }

        .add-btn:active {
            transform: scale(0.95);
        }

        /* Bottom Floating Cart Bar */
        .cart-bar {
            position: fixed;
            bottom: 0;
            left: 0;
            right: 0;
            background: #1a1a1a;
            color: #fff;
            padding: 15px 25px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            box-shadow: 0 -4px 20px rgba(0,0,0,0.15);
            max-width: 600px;
            margin: 0 auto;
            border-top-left-radius: 16px;
            border-top-right-radius: 16px;
            display: none; /* Hidden initially */
        }

        .cart-info h4 {
            font-size: 0.95rem;
            color: #ffb703;
        }

        .cart-info p {
            font-size: 0.8rem;
            color: #bbb;
        }

        .pay-btn {
            background: #ffb703;
            color: #1a1a1a;
            border: none;
            padding: 10px 20px;
            border-radius: 8px;
            font-weight: 700;
            cursor: pointer;
            font-size: 0.95rem;
        }

        /* Success / Order Placed Popup Modal */
        .modal {
            display: none;
            position: fixed;
            top: 0; left: 0; right: 0; bottom: 0;
            background: rgba(0,0,0,0.6);
            z-index: 200;
            justify-content: center;
            align-items: center;
            padding: 20px;
        }

        .modal-content {
            background: #fff;
            padding: 30px;
            border-radius: 16px;
            text-align: center;
            max-width: 400px;
            width: 100%;
            animation: popUp 0.3s ease-in-out;
        }

        @keyframes popUp {
            0% { transform: scale(0.8); opacity: 0; }
            100% { transform: scale(1); opacity: 1; }
        }

        .modal-content h2 {
            color: #2e7d32;
            margin-bottom: 10px;
        }

        .modal-content p {
            color: #666;
            font-size: 0.9rem;
            margin-bottom: 20px;
        }

        .close-modal-btn {
            background: #1a1a1a;
            color: #fff;
            border: none;
            padding: 10px 25px;
            border-radius: 8px;
            cursor: pointer;
            font-weight: 650;
        }
    </style>
</head>
<body>

    <!-- Welcome Pop-up for User Interaction & Voice Trigger -->
    <div class="welcome-overlay" id="welcomeOverlay">
        <div class="welcome-box">
            <h2>Ubaid Shaikh Restaurant</h2>
            <p>Tap below to view menu & start ordering</p>
            <button class="enter-btn" onclick="startAppWithVoice()">Enter Menu 🍽️</button>
        </div>
    </div>

    <!-- Header / Table Info -->
    <header>
        <h1>UBAID SHAIKH RESTAURANT</h1>
        <p>🪑 Table No: <strong>04</strong> | Scan → Order → Pay</p>
    </header>

    <!-- Categories Navigation -->
    <div class="categories">
        <button class="cat-btn active">🔥 Recommended</button>
        <button class="cat-btn">☕ Coffee & Beverages</button>
        <button class="cat-btn">🍔 Fast Food</button>
        <button class="cat-btn">🍰 Desserts</button>
    </div>

    <!-- Menu List -->
    <div class="menu-container">
        <h3 class="section-title">Today's Special</h3>

        <div class="food-card">
            <div class="food-info">
                <div class="food-name">Cold Brew Classic</div>
                <div class="food-desc">Slow-steeped cold coffee with rich aromatic notes.</div>
                <div class="food-price">₹220</div>
            </div>
            <button class="add-btn" onclick="addToCart('Cold Brew Classic', 220)">ADD</button>
        </div>

        <div class="food-card">
            <div class="food-info">
                <div class="food-name">Truffle Mushroom Burger</div>
                <div class="food-desc">Crispy patty, creamy truffle mayo, wild mushrooms.</div>
                <div class="food-price">₹340</div>
            </div>
            <button class="add-btn" onclick="addToCart('Truffle Mushroom Burger', 340)">ADD</button>
        </div>

        <div class="food-card">
            <div class="food-info">
                <div class="food-name">Belgian Waffle</div>
                <div class="food-desc">Served with warm dark chocolate ganache and berries.</div>
                <div class="food-price">₹280</div>
            </div>
            <button class="add-btn" onclick="addToCart('Belgian Waffle', 280)">ADD</button>
        </div>
    </div>

    <!-- Floating Checkout Bar -->
    <div class="cart-bar" id="cartBar">
        <div class="cart-info">
            <h4 id="itemCount">0 Items Added</h4>
            <p>Total: ₹<span id="totalPrice">0</span></p>
        </div>
        <button class="pay-btn" onclick="checkout()">Pay & Order 🚀</button>
    </div>

    <!-- Success Modal -->
    <div class="modal" id="successModal">
        <div class="modal-content">
            <h2>Order Placed Successfully! 🎉</h2>
            <p>Aapka order kitchen mein bhej diya gaya hai. Thodi der mein table par serve kiya jayega.</p>
            <button class="close-modal-btn" onclick="resetApp()">New Order / Reset</button>
        </div>
    </div>

    <!-- JavaScript Logic -->
    <script>
        let cartCount = 0;
        let cartTotal = 0;

        function startAppWithVoice() {
            // Hide the welcome overlay
            document.getElementById('welcomeOverlay').style.display = 'none';

            // Play the Voice Greeting
            if ('speechSynthesis' in window) {
                const text = "Ubaid Shaikh Restaurant mein aapka swagat hai";
                const utterance = new SpeechSynthesisUtterance(text);
                utterance.lang = 'hi-IN'; // Indian accent
                utterance.rate = 1.0; 
                utterance.pitch = 1.0; 
                window.speechSynthesis.speak(utterance);
            }
        }

        function addToCart(itemName, itemPrice) {
            cartCount += 1;
            cartTotal += itemPrice;

            document.getElementById('itemCount').innerText = `${cartCount} Item(s) Added`;
            document.getElementById('totalPrice').innerText = cartTotal;
            document.getElementById('cartBar').style.display = 'flex';
        }

        function checkout() {
            document.getElementById('successModal').style.display = 'flex';
        }

        function resetApp() {
            cartCount = 0;
            cartTotal = 0;
            document.getElementById('cartBar').style.display = 'none';
            document.getElementById('successModal').style.display = 'none';
            document.getElementById('welcomeOverlay').style.display = 'flex';
        }
    </script>

</body>
</html>
