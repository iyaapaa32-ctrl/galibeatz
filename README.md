<!DOCTYPE html>
<html lang="id">
<head>
  <meta charset="UTF-8">
  <title>GalibEatz</title>
  <style>
    body {
      font-family: 'Segoe UI', Arial, sans-serif;
      background: #f5f6fa;
      margin: 0;
      padding: 0;
    }
    header {
      background: linear-gradient(135deg, #ff4d4d, #ff9966);
      color: white;
      text-align: center;
      padding: 20px;
      font-size: 28px;
      font-weight: bold;
      position: sticky;
      top: 0;
      z-index: 1000;
    }
    header a {
      display: block;
      color: #fff;
      font-size: 14px;
      margin-top: 5px;
      text-decoration: none;
    }
    #searchBar {
      margin: 10px auto;
      display: block;
      width: 80%;
      max-width: 400px;
      padding: 10px;
      border-radius: 8px;
      border: 1px solid #ccc;
      font-size: 16px;
    }
    .category {
      padding: 20px;
    }
    .category h2 {
      margin-bottom: 15px;
      color: #333;
      border-left: 5px solid #ff4d4d;
      padding-left: 10px;
    }
    .menu-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
      gap: 20px;
    }
    .card {
      background: white;
      border-radius: 12px;
      box-shadow: 0 4px 10px rgba(0,0,0,0.1);
      padding: 15px;
      text-align: center;
      transition: transform 0.2s;
    }
    .card:hover {
      transform: translateY(-5px);
    }
    .card img {
      width: 100%;
      height: 150px;
      object-fit: cover; /* ini bikin tetap rapi */
      border-radius: 8px;
      margin-bottom: 10px;
    }
    .card h3 {
      margin: 10px 0 5px;
      font-size: 18px;
      color: #444;
    }
    .price {
      font-size: 16px;
      font-weight: bold;
      color: #e74c3c;
      margin-bottom: 8px;
    }
    .desc {
      font-size: 14px;
      color: #666;
      margin-bottom: 10px;
      min-height: 40px;
    }
    .btn {
      display: inline-block;
      padding: 8px 14px;
      border-radius: 8px;
      color: #fff;
      font-weight: bold;
      text-decoration: none;
      transition: 0.3s;
      margin: 2px;
      cursor: pointer;
    }
    .btn:hover { opacity: 0.8; }
    .red { background: #e74c3c; }
    .blue { background: #3498db; }
    .green { background: #2ecc71; }
    .orange { background: #e67e22; }

    #cart {
      position: fixed;
      bottom: 20px;
      right: 20px;
      background: #2ecc71;
      color: white;
      padding: 12px 18px;
      border-radius: 50px;
      font-weight: bold;
      cursor: pointer;
      box-shadow: 0 4px 10px rgba(0,0,0,0.2);
    }
    #cartItems {
      position: fixed;
      bottom: 80px;
      right: 20px;
      background: white;
      border-radius: 12px;
      box-shadow: 0 4px 10px rgba(0,0,0,0.2);
      padding: 15px;
      display: none;
      width: 250px;
    }
    #cartItems h3 { margin-top: 0; }
    #cartItems ul {
      list-style: none;
      padding: 0;
      margin: 0;
    }
    #cartItems li {
      font-size: 14px;
      margin-bottom: 6px;
    }
    footer {
      background: #2c3e50;
      color: white;
      text-align: center;
      padding: 15px;
      margin-top: 30px;
    }
    footer a {
      color: #f39c12;
      text-decoration: none;
    }
  </style>
</head>
<body>
  <header>
    🍽️ GalibEatz
    <input type="text" id="searchBar" placeholder="Cari menu...">
    <p>Follow us on IG:
      <a href="https://www.instagram.com/sgalibb" target="_blank">@sgalibb</a>
    </p>
  </header>

  <div class="category">
    <h2>🍝 Main Course</h2>
    <div class="menu-grid" id="menuList">
      <div class="card" data-name="Spaghetti Carbonara">
        <img src="https://drive.google.com/uc?export=view&id=1fVRhyvj6NHGLVEuWbm9fobxJ6Ecxhw41" alt="Spaghetti Carbonara">
        <h3>Spaghetti Carbonara</h3>
        <div class="price">Rp 65.000</div>
        <div class="desc">Pasta creamy dengan bacon, telur, dan parmesan.</div>
        <button class="btn orange addCart">+ Keranjang</button>
      </div>
      <div class="card" data-name="Pizza Margherita">
        <img src="https://drive.google.com/uc?export=view&id=1jKImTFl1FLYCqnCWHH-l4UeHlNMsENty" alt="Pizza Margherita">
        <h3>Pizza Margherita</h3>
        <div class="price">Rp 80.000</div>
        <div class="desc">Pizza klasik dengan mozzarella, tomat, basil segar.</div>
        <button class="btn green addCart">+ Keranjang</button>
      </div>
      <div class="card" data-name="Tiramisu">
        <img src="https://drive.google.com/uc?export=view&id=13Dq3P2sPAxHGUL0YYGRHsrHdpTZjCwTI" alt="Tiramisu">
        <h3>Tiramisu</h3>
        <div class="price">Rp 45.000</div>
        <div class="desc">Dessert Italia dengan kopi, mascarpone, cocoa.</div>
        <button class="btn red addCart">+ Keranjang</button>
      </div>
    </div>
  </div>

  <div id="cart">🛒 Keranjang (0)</div>
  <div id="cartItems">
    <h3>Pesanan Kamu</h3>
    <ul id="cartList"></ul>
    <a id="checkoutBtn" href="#" class="btn blue">Checkout via WA</a>
  </div>

  <footer>
    © 2025 GalibEatz | Follow us on
    <a href="https://www.instagram.com/sgalibb" target="_blank">Instagram</a>
  </footer>

  <script>
    const searchBar = document.getElementById('searchBar');
    const menuCards = document.querySelectorAll('.card');
    searchBar.addEventListener('input', () => {
      const q = searchBar.value.toLowerCase();
      menuCards.forEach(card => {
        card.style.display = card.dataset.name.toLowerCase().includes(q) ? 'block' : 'none';
      });
    });

    let cart = [];
    const cartBtn = document.getElementById('cart');
    const cartBox = document.getElementById('cartItems');
    const cartList = document.getElementById('cartList');
    const checkoutBtn = document.getElementById('checkoutBtn');

    document.querySelectorAll('.addCart').forEach(btn => {
      btn.addEventListener('click', e => {
        const name = e.target.closest('.card').dataset.name;
        cart.push(name);
        updateCart();
      });
    });

    function updateCart() {
      cartBtn.textContent = `🛒 Keranjang (${cart.length})`;
      cartList.innerHTML = "";
      cart.forEach((item) => {
        let li = document.createElement('li');
        li.textContent = item;
        cartList.appendChild(li);
      });
      checkoutBtn.href = `https://wa.me/6285135383485?text=Halo%20saya%20mau%20pesan:%20${cart.join(', ')}`;
    }

    cartBtn.addEventListener('click', () => {
      cartBox.style.display = cartBox.style.display === 'block' ? 'none' : 'block';
    });
  </script>
</body>
</html>
``
