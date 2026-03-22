<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>VeloRush — Premium Bikes</title>
<link href="https://fonts.googleapis.com/css2?family=Bebas+Neue&family=DM+Sans:wght@300;400;500;600&family=Space+Mono:wght@400;700&display=swap" rel="stylesheet">
<style>
  :root {
    --black: #0a0a0a;
    --white: #f5f0e8;
    --orange: #ff4d00;
    --orange-dim: #cc3d00;
    --gray: #1a1a1a;
    --gray2: #2a2a2a;
    --gray3: #444;
    --text-muted: #888;
    --card-bg: #141414;
    --border: #2a2a2a;
    --success: #00c97a;
  }

  * { margin:0; padding:0; box-sizing:border-box; }

  body {
    background: var(--black);
    color: var(--white);
    font-family: 'DM Sans', sans-serif;
    min-height: 100vh;
    overflow-x: hidden;
  }

  /* ---- NAV ---- */
  nav {
    position: fixed; top:0; left:0; right:0; z-index:100;
    display:flex; align-items:center; justify-content:space-between;
    padding: 18px 48px;
    background: rgba(10,10,10,0.92);
    backdrop-filter: blur(12px);
    border-bottom: 1px solid var(--border);
  }
  .logo {
    font-family: 'Bebas Neue', sans-serif;
    font-size: 2rem;
    color: var(--orange);
    letter-spacing: 3px;
    text-decoration: none;
    cursor: pointer;
  }
  .logo span { color: var(--white); }
  .nav-links { display:flex; gap:32px; align-items:center; }
  .nav-links a {
    color: var(--text-muted);
    text-decoration:none;
    font-size:.9rem;
    font-weight:500;
    letter-spacing:.5px;
    transition: color .2s;
    cursor:pointer;
  }
  .nav-links a:hover { color: var(--white); }
  .nav-links a.active { color: var(--orange); }
  .cart-btn {
    background: var(--orange);
    color: #fff;
    border: none;
    padding: 10px 22px;
    font-family: 'DM Sans', sans-serif;
    font-weight:600;
    font-size:.88rem;
    letter-spacing:.5px;
    cursor:pointer;
    transition: background .2s, transform .1s;
    position:relative;
  }
  .cart-btn:hover { background: var(--orange-dim); transform:translateY(-1px); }
  .cart-count {
    position:absolute; top:-8px; right:-8px;
    background:#fff; color:var(--orange);
    border-radius:50%; width:20px; height:20px;
    font-size:.7rem; font-weight:700;
    display:flex; align-items:center; justify-content:center;
    display:none;
  }
  #userBadge {
    font-size:.85rem; color:var(--success); font-weight:600;
    display:none;
    align-items:center; gap:8px;
  }
  #logoutBtn {
    background:none; border:1px solid var(--gray3);
    color:var(--text-muted); padding:6px 14px;
    font-family:'DM Sans',sans-serif; font-size:.8rem;
    cursor:pointer; transition:.2s;
  }
  #logoutBtn:hover { border-color:var(--orange); color:var(--orange); }

  /* ---- PAGES ---- */
  .page { display:none; }
  .page.active { display:block; }

  /* ---- HERO ---- */
  #heroPage {
    padding-top: 80px;
  }
  .hero {
    min-height: 100vh;
    display:flex; flex-direction:column; align-items:center; justify-content:center;
    text-align:center;
    position:relative;
    overflow:hidden;
    padding: 40px 20px;
    background:
      radial-gradient(ellipse 80% 60% at 50% 0%, rgba(255,77,0,0.12) 0%, transparent 70%),
      repeating-linear-gradient(90deg, transparent, transparent 80px, rgba(255,255,255,0.015) 80px, rgba(255,255,255,0.015) 81px),
      repeating-linear-gradient(0deg, transparent, transparent 80px, rgba(255,255,255,0.015) 80px, rgba(255,255,255,0.015) 81px);
  }
  .hero-eyebrow {
    font-family: 'Space Mono', monospace;
    font-size:.75rem; letter-spacing:4px;
    color: var(--orange); text-transform:uppercase;
    margin-bottom:20px;
    animation: fadeUp .8s both;
  }
  .hero h1 {
    font-family:'Bebas Neue', sans-serif;
    font-size: clamp(5rem, 14vw, 11rem);
    line-height:.9;
    letter-spacing:2px;
    animation: fadeUp .8s .15s both;
  }
  .hero h1 em {
    color: var(--orange); font-style:normal;
    display:block;
  }
  .hero-sub {
    font-size:1.1rem; color:var(--text-muted); max-width:500px;
    margin: 28px auto 40px;
    line-height:1.7;
    animation: fadeUp .8s .3s both;
  }
  .hero-actions {
    display:flex; gap:16px; animation: fadeUp .8s .45s both;
    flex-wrap:wrap; justify-content:center;
  }
  .btn-primary {
    background: var(--orange);
    color:#fff; border:none;
    padding: 16px 40px;
    font-family:'DM Sans',sans-serif;
    font-weight:600; font-size:1rem;
    letter-spacing:.5px;
    cursor:pointer;
    transition: background .2s, transform .15s, box-shadow .2s;
    clip-path: polygon(0 0, calc(100% - 12px) 0, 100% 12px, 100% 100%, 12px 100%, 0 calc(100% - 12px));
  }
  .btn-primary:hover { background: var(--orange-dim); transform:translateY(-2px); box-shadow:0 8px 30px rgba(255,77,0,0.35); }
  .btn-secondary {
    background:transparent; color:var(--white);
    border:1px solid var(--gray3);
    padding:16px 40px;
    font-family:'DM Sans',sans-serif;
    font-weight:500; font-size:1rem;
    cursor:pointer; transition:.2s;
    clip-path: polygon(0 0, calc(100% - 12px) 0, 100% 12px, 100% 100%, 12px 100%, 0 calc(100% - 12px));
  }
  .btn-secondary:hover { border-color:var(--orange); color:var(--orange); }

  .hero-strip {
    width:100%; background:var(--orange);
    padding:14px 0; overflow:hidden;
    margin-top:60px;
  }
  .marquee-track {
    display:flex; gap:60px; white-space:nowrap;
    animation: marquee 20s linear infinite;
  }
  .marquee-track span {
    font-family:'Bebas Neue',sans-serif;
    font-size:1.1rem; letter-spacing:3px;
    color:var(--black);
    flex-shrink:0;
  }
  @keyframes marquee { from{transform:translateX(0)} to{transform:translateX(-50%)} }
  @keyframes fadeUp { from{opacity:0;transform:translateY(30px)} to{opacity:1;transform:translateY(0)} }

  /* ---- SHOP PAGE ---- */
  #shopPage { padding: 120px 40px 80px; max-width:1400px; margin:0 auto; }
  .section-header {
    display:flex; align-items:baseline; justify-content:space-between;
    margin-bottom:48px;
    border-bottom:1px solid var(--border); padding-bottom:20px;
  }
  .section-header h2 {
    font-family:'Bebas Neue',sans-serif;
    font-size:3rem; letter-spacing:2px;
  }
  .section-header h2 span { color:var(--orange); }
  .bike-grid {
    display:grid;
    grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
    gap:24px;
  }
  .bike-card {
    background:var(--card-bg);
    border:1px solid var(--border);
    overflow:hidden;
    transition: border-color .2s, transform .2s, box-shadow .2s;
    cursor:pointer;
    animation: fadeUp .6s both;
  }
  .bike-card:hover {
    border-color: var(--orange);
    transform:translateY(-4px);
    box-shadow:0 12px 40px rgba(255,77,0,0.15);
  }
  .bike-img {
    width:100%; height:200px;
    display:flex; align-items:center; justify-content:center;
    font-size:5rem;
    position:relative; overflow:hidden;
  }
  .bike-badge {
    position:absolute; top:12px; right:12px;
    background:var(--orange); color:#fff;
    font-family:'Space Mono',monospace;
    font-size:.65rem; letter-spacing:1px;
    padding:4px 10px;
    text-transform:uppercase;
  }
  .bike-info { padding:20px 22px 22px; }
  .bike-brand {
    font-family:'Space Mono',monospace;
    font-size:.7rem; letter-spacing:2px;
    color:var(--orange); text-transform:uppercase;
    margin-bottom:6px;
  }
  .bike-name {
    font-family:'Bebas Neue',sans-serif;
    font-size:1.6rem; letter-spacing:1px;
    margin-bottom:8px;
  }
  .bike-desc {
    font-size:.82rem; color:var(--text-muted);
    line-height:1.6; margin-bottom:16px;
  }
  .bike-specs {
    display:flex; gap:16px; margin-bottom:18px;
    flex-wrap:wrap;
  }
  .spec {
    font-family:'Space Mono',monospace;
    font-size:.68rem; color:var(--text-muted);
    letter-spacing:.5px;
  }
  .spec strong { color:var(--white); display:block; font-size:.75rem; }
  .bike-footer {
    display:flex; align-items:center; justify-content:space-between;
  }
  .bike-price {
    font-family:'Bebas Neue',sans-serif;
    font-size:1.8rem; color:var(--orange);
    letter-spacing:1px;
  }
  .bike-price sub { font-size:.9rem; color:var(--text-muted); }
  .add-cart-btn {
    background:var(--orange); color:#fff;
    border:none; padding:10px 20px;
    font-family:'DM Sans',sans-serif;
    font-weight:600; font-size:.85rem;
    cursor:pointer; transition:.2s;
    letter-spacing:.5px;
  }
  .add-cart-btn:hover { background:var(--orange-dim); transform:scale(1.03); }
  .add-cart-btn.added { background:var(--success); color:#fff; }

  /* ---- LOGIN PAGE ---- */
  #loginPage {
    min-height:100vh;
    display:flex; align-items:center; justify-content:center;
    background:
      radial-gradient(ellipse 60% 70% at 80% 50%, rgba(255,77,0,0.08) 0%, transparent 70%),
      var(--black);
    padding:100px 20px 40px;
  }
  .login-container {
    width:100%; max-width:440px;
  }
  .login-eyebrow {
    font-family:'Space Mono',monospace;
    font-size:.7rem; letter-spacing:3px;
    color:var(--orange); text-transform:uppercase;
    margin-bottom:12px;
  }
  .login-container h2 {
    font-family:'Bebas Neue',sans-serif;
    font-size:3.5rem; letter-spacing:2px;
    margin-bottom:8px;
    line-height:1;
  }
  .login-container p {
    color:var(--text-muted); font-size:.9rem;
    margin-bottom:36px;
  }
  .login-box {
    background:var(--card-bg);
    border:1px solid var(--border);
    padding:36px;
  }
  .form-group { margin-bottom:22px; }
  .form-group label {
    display:block;
    font-family:'Space Mono',monospace;
    font-size:.7rem; letter-spacing:1.5px;
    color:var(--text-muted); text-transform:uppercase;
    margin-bottom:8px;
  }
  .form-group input, .form-group select, .form-group textarea {
    width:100%; background:var(--gray2);
    border:1px solid var(--border);
    color:var(--white); padding:13px 16px;
    font-family:'DM Sans',sans-serif;
    font-size:.95rem;
    outline:none;
    transition: border-color .2s;
  }
  .form-group input:focus, .form-group select:focus, .form-group textarea:focus {
    border-color:var(--orange);
    background:var(--gray);
  }
  .form-group textarea { resize:vertical; min-height:90px; }
  .form-row { display:grid; grid-template-columns:1fr 1fr; gap:16px; }
  .form-submit {
    width:100%; background:var(--orange); color:#fff;
    border:none; padding:16px;
    font-family:'DM Sans',sans-serif;
    font-weight:700; font-size:1rem; letter-spacing:.5px;
    cursor:pointer; transition:.2s;
    clip-path: polygon(0 0, calc(100% - 10px) 0, 100% 10px, 100% 100%, 10px 100%, 0 calc(100% - 10px));
  }
  .form-submit:hover { background:var(--orange-dim); }
  .login-switch {
    text-align:center; margin-top:20px;
    font-size:.85rem; color:var(--text-muted);
  }
  .login-switch a { color:var(--orange); cursor:pointer; text-decoration:none; font-weight:600; }
  .login-switch a:hover { text-decoration:underline; }
  .input-error { border-color:#ff4444 !important; }
  .error-msg { color:#ff4444; font-size:.78rem; margin-top:5px; font-family:'Space Mono',monospace; }
  .success-msg { color:var(--success); font-size:.82rem; text-align:center; margin-top:12px; font-weight:600; }

  /* ---- CART / ORDER PAGE ---- */
  #cartPage { padding:120px 40px 80px; max-width:1100px; margin:0 auto; }
  .cart-header {
    font-family:'Bebas Neue',sans-serif;
    font-size:3rem; letter-spacing:2px; margin-bottom:40px;
    border-bottom:1px solid var(--border); padding-bottom:16px;
  }
  .cart-header span { color:var(--orange); }
  .cart-empty {
    text-align:center; padding:80px 20px;
    color:var(--text-muted);
  }
  .cart-empty .empty-icon { font-size:4rem; margin-bottom:16px; }
  .cart-empty p { font-size:1.1rem; margin-bottom:24px; }
  .cart-layout {
    display:grid; grid-template-columns:1fr 380px; gap:40px;
    align-items:start;
  }
  .cart-items { display:flex; flex-direction:column; gap:16px; }
  .cart-item {
    background:var(--card-bg); border:1px solid var(--border);
    display:flex; align-items:center; gap:20px;
    padding:20px 24px;
    transition: border-color .2s;
  }
  .cart-item:hover { border-color:var(--gray3); }
  .item-emoji { font-size:2.8rem; flex-shrink:0; width:60px; text-align:center; }
  .item-details { flex:1; }
  .item-brand-name {
    font-family:'Space Mono',monospace;
    font-size:.7rem; letter-spacing:1px;
    color:var(--orange); text-transform:uppercase;
    margin-bottom:4px;
  }
  .item-name {
    font-family:'Bebas Neue',sans-serif;
    font-size:1.4rem; letter-spacing:1px; margin-bottom:4px;
  }
  .item-price-unit { font-size:.85rem; color:var(--text-muted); }
  .item-qty {
    display:flex; align-items:center; gap:10px;
    flex-shrink:0;
  }
  .qty-btn {
    width:30px; height:30px; background:var(--gray2);
    border:1px solid var(--border); color:var(--white);
    font-size:1.1rem; cursor:pointer; transition:.2s;
    display:flex; align-items:center; justify-content:center;
  }
  .qty-btn:hover { background:var(--orange); border-color:var(--orange); }
  .qty-num {
    font-family:'Space Mono',monospace; font-size:.95rem;
    min-width:20px; text-align:center;
  }
  .item-total {
    font-family:'Bebas Neue',sans-serif;
    font-size:1.5rem; color:var(--orange);
    flex-shrink:0; min-width:90px; text-align:right;
  }
  .remove-btn {
    background:none; border:none; color:var(--text-muted);
    cursor:pointer; font-size:1.2rem; padding:4px;
    transition:.2s; flex-shrink:0;
  }
  .remove-btn:hover { color:#ff4444; }

  .order-summary {
    background:var(--card-bg); border:1px solid var(--border);
    padding:28px; position:sticky; top:100px;
  }
  .summary-title {
    font-family:'Bebas Neue',sans-serif;
    font-size:1.6rem; letter-spacing:1px;
    margin-bottom:24px; padding-bottom:12px;
    border-bottom:1px solid var(--border);
  }
  .summary-row {
    display:flex; justify-content:space-between;
    font-size:.9rem; margin-bottom:12px; color:var(--text-muted);
  }
  .summary-row.total {
    font-family:'Bebas Neue',sans-serif;
    font-size:1.4rem; color:var(--white);
    margin-top:16px; padding-top:16px;
    border-top:1px solid var(--border);
  }
  .summary-row.total span:last-child { color:var(--orange); }
  .checkout-btn {
    width:100%; background:var(--orange); color:#fff;
    border:none; padding:16px;
    font-family:'DM Sans',sans-serif;
    font-weight:700; font-size:1rem; letter-spacing:.5px;
    cursor:pointer; transition:.2s; margin-top:20px;
    clip-path: polygon(0 0, calc(100% - 10px) 0, 100% 10px, 100% 100%, 10px 100%, 0 calc(100% - 10px));
  }
  .checkout-btn:hover { background:var(--orange-dim); box-shadow:0 8px 24px rgba(255,77,0,0.3); }
  .checkout-btn:disabled { background:var(--gray3); cursor:not-allowed; box-shadow:none; }

  /* ---- ORDER FORM ---- */
  #orderFormPage { padding:120px 40px 80px; max-width:800px; margin:0 auto; }
  .order-form-header {
    font-family:'Bebas Neue',sans-serif;
    font-size:3rem; letter-spacing:2px; margin-bottom:8px;
  }
  .order-form-header span { color:var(--orange); }
  .order-form-sub { color:var(--text-muted); margin-bottom:40px; font-size:.9rem; }
  .form-section-title {
    font-family:'Space Mono',monospace;
    font-size:.75rem; letter-spacing:3px; color:var(--orange);
    text-transform:uppercase; margin-bottom:20px; margin-top:32px;
    padding-bottom:8px; border-bottom:1px solid var(--border);
  }
  .form-box {
    background:var(--card-bg); border:1px solid var(--border);
    padding:32px;
  }

  /* ---- ORDER CONFIRMATION ---- */
  #confirmPage { padding:120px 40px 80px; max-width:700px; margin:0 auto; text-align:center; }
  .confirm-icon { font-size:5rem; margin-bottom:20px; animation: pop .5s both; }
  @keyframes pop { from{transform:scale(0)} to{transform:scale(1)} }
  .confirm-title {
    font-family:'Bebas Neue',sans-serif;
    font-size:3.5rem; letter-spacing:2px; margin-bottom:16px;
  }
  .confirm-title span { color:var(--orange); }
  .confirm-sub { color:var(--text-muted); font-size:1rem; margin-bottom:32px; line-height:1.7; }
  .order-id-box {
    background:var(--card-bg); border:1px solid var(--border);
    padding:20px 32px; display:inline-block; margin-bottom:32px;
  }
  .order-id-label {
    font-family:'Space Mono',monospace;
    font-size:.7rem; letter-spacing:2px; color:var(--text-muted);
    text-transform:uppercase; margin-bottom:6px;
  }
  .order-id-val {
    font-family:'Bebas Neue',sans-serif;
    font-size:2rem; color:var(--orange); letter-spacing:3px;
  }
  .order-details-table {
    width:100%; border-collapse:collapse;
    margin-bottom:32px; text-align:left;
  }
  .order-details-table th {
    font-family:'Space Mono',monospace;
    font-size:.68rem; letter-spacing:1.5px; text-transform:uppercase;
    color:var(--text-muted); padding:10px 16px;
    border-bottom:1px solid var(--border);
  }
  .order-details-table td {
    padding:12px 16px; border-bottom:1px solid rgba(255,255,255,0.04);
    font-size:.9rem;
  }
  .order-details-table tr:last-child td { border-bottom:none; }
  .td-name { font-weight:600; }
  .td-price { font-family:'Space Mono',monospace; color:var(--orange); font-size:.85rem; }

  /* ---- TOAST ---- */
  #toast {
    position:fixed; bottom:32px; right:32px;
    background:var(--gray2); border:1px solid var(--success);
    color:var(--white); padding:14px 24px;
    font-weight:600; font-size:.9rem;
    z-index:9999; display:none;
    animation: slideIn .3s;
    border-left:3px solid var(--success);
  }
  @keyframes slideIn { from{transform:translateX(100px);opacity:0} to{transform:translateX(0);opacity:1} }

  /* ---- FOOTER ---- */
  footer {
    border-top:1px solid var(--border);
    padding:32px 48px;
    display:flex; align-items:center; justify-content:space-between;
    flex-wrap:wrap; gap:16px;
  }
  footer .logo { font-size:1.5rem; }
  footer p { font-size:.82rem; color:var(--text-muted); }
  .footer-links { display:flex; gap:24px; }
  .footer-links a { font-size:.82rem; color:var(--text-muted); text-decoration:none; cursor:pointer; }
  .footer-links a:hover { color:var(--orange); }

  @media(max-width:768px) {
    nav { padding:14px 20px; }
    .nav-links { display:none; }
    #shopPage, #cartPage, #orderFormPage, #confirmPage { padding:100px 20px 60px; }
    .cart-layout { grid-template-columns:1fr; }
    .hero h1 { font-size:5rem; }
    .form-row { grid-template-columns:1fr; }
  }
</style>
</head>
<body>

<!-- NAV -->
<nav>
  <div class="logo" onclick="showPage('heroPage')">VELO<span>RUSH</span></div>
  <div class="nav-links">
    <a onclick="showPage('heroPage')">Home</a>
    <a onclick="showPage('shopPage')">Shop</a>
    <a onclick="showPage('cartPage')">My Cart</a>
    <a onclick="showPage('loginPage')" id="loginNavLink">Login</a>
  </div>
  <div style="display:flex;gap:12px;align-items:center;">
    <div id="userBadge">
      <span id="userGreet"></span>
      <button id="logoutBtn" onclick="logout()">Logout</button>
    </div>
    <button class="cart-btn" onclick="showPage('cartPage')">
      🛒 Cart
      <span class="cart-count" id="cartCount">0</span>
    </button>
  </div>
</nav>

<!-- ===== HERO PAGE ===== -->
<div id="heroPage" class="page active">
  <div class="hero">
    <div class="hero-eyebrow">★ Premium Bikes Since 2010 ★</div>
    <h1>RIDE<em>BEYOND</em>LIMITS</h1>
    <p class="hero-sub">Handpicked performance bikes for every terrain. From mountain trails to city streets — find your perfect ride.</p>
    <div class="hero-actions">
      <button class="btn-primary" onclick="showPage('shopPage')">SHOP NOW</button>
      <button class="btn-secondary" onclick="showPage('loginPage')">CREATE ACCOUNT</button>
    </div>
  </div>
  <div class="hero-strip">
    <div class="marquee-track" id="marqueeTrack"></div>
  </div>
  <div style="padding:80px 40px;max-width:1200px;margin:0 auto;">
    <div style="display:grid;grid-template-columns:repeat(auto-fit,minmax(200px,1fr));gap:32px;">
      <div style="text-align:center;">
        <div style="font-size:2.5rem;margin-bottom:12px;">🏆</div>
        <div style="font-family:'Bebas Neue',sans-serif;font-size:1.3rem;letter-spacing:1px;margin-bottom:6px;">Top Brands</div>
        <div style="color:var(--text-muted);font-size:.85rem;">Trek, Giant, Specialized & more</div>
      </div>
      <div style="text-align:center;">
        <div style="font-size:2.5rem;margin-bottom:12px;">🚚</div>
        <div style="font-family:'Bebas Neue',sans-serif;font-size:1.3rem;letter-spacing:1px;margin-bottom:6px;">Free Shipping</div>
        <div style="color:var(--text-muted);font-size:.85rem;">On orders above ₹50,000</div>
      </div>
      <div style="text-align:center;">
        <div style="font-size:2.5rem;margin-bottom:12px;">🔧</div>
        <div style="font-family:'Bebas Neue',sans-serif;font-size:1.3rem;letter-spacing:1px;margin-bottom:6px;">Free Assembly</div>
        <div style="color:var(--text-muted);font-size:.85rem;">Expert setup at your doorstep</div>
      </div>
      <div style="text-align:center;">
        <div style="font-size:2.5rem;margin-bottom:12px;">🛡️</div>
        <div style="font-family:'Bebas Neue',sans-serif;font-size:1.3rem;letter-spacing:1px;margin-bottom:6px;">2-Year Warranty</div>
        <div style="color:var(--text-muted);font-size:.85rem;">All frames & components</div>
      </div>
    </div>
  </div>
  <footer>
    <div class="logo">VELO<span>RUSH</span></div>
    <p>© 2026 VeloRush. All rights reserved.</p>
    <div class="footer-links">
      <a onclick="showPage('shopPage')">Shop</a>
      <a onclick="showPage('loginPage')">Account</a>
      <a onclick="showPage('cartPage')">Cart</a>
    </div>
  </footer>
</div>

<!-- ===== LOGIN PAGE ===== -->
<div id="loginPage" class="page">
  <div id="loginPage" style="min-height:100vh;display:flex;align-items:center;justify-content:center;padding:100px 20px 40px;background:radial-gradient(ellipse 60% 70% at 80% 50%,rgba(255,77,0,.08) 0%,transparent 70%),var(--black);">
    <div class="login-container">
      <div class="login-eyebrow">Member Access</div>
      <h2 id="loginTitle">SIGN IN</h2>
      <p id="loginSubtitle">Welcome back, rider. Sign in to your account.</p>
      <div class="login-box">
        <!-- Login Form -->
        <div id="signinForm">
          <div class="form-group">
            <label>Email Address</label>
            <input type="email" id="loginEmail" placeholder="you@example.com">
          </div>
          <div class="form-group">
            <label>Password</label>
            <input type="password" id="loginPassword" placeholder="••••••••">
          </div>
          <div id="loginError" class="error-msg" style="margin-bottom:12px;display:none;"></div>
          <button class="form-submit" onclick="doLogin()">SIGN IN →</button>
          <div class="login-switch">Don't have an account? <a onclick="toggleAuthForm(true)">Create one</a></div>
        </div>
        <!-- Register Form -->
        <div id="registerForm" style="display:none;">
          <div class="form-row">
            <div class="form-group">
              <label>First Name</label>
              <input type="text" id="regFirst" placeholder="John">
            </div>
            <div class="form-group">
              <label>Last Name</label>
              <input type="text" id="regLast" placeholder="Doe">
            </div>
          </div>
          <div class="form-group">
            <label>Email Address</label>
            <input type="email" id="regEmail" placeholder="you@example.com">
          </div>
          <div class="form-group">
            <label>Password</label>
            <input type="password" id="regPassword" placeholder="Min 6 characters">
          </div>
          <div class="form-group">
            <label>Phone Number</label>
            <input type="tel" id="regPhone" placeholder="+91 98765 43210">
          </div>
          <div id="regError" class="error-msg" style="margin-bottom:12px;display:none;"></div>
          <div id="regSuccess" class="success-msg" style="display:none;">✔ Account created! Signing you in...</div>
          <button class="form-submit" onclick="doRegister()">CREATE ACCOUNT →</button>
          <div class="login-switch">Already have an account? <a onclick="toggleAuthForm(false)">Sign in</a></div>
        </div>
      </div>
    </div>
  </div>
</div>

<!-- ===== SHOP PAGE ===== -->
<div id="shopPage" class="page">
  <div style="padding:120px 40px 80px;max-width:1400px;margin:0 auto;">
    <div class="section-header">
      <h2>OUR <span>BIKES</span></h2>
      <div style="font-family:'Space Mono',monospace;font-size:.75rem;color:var(--text-muted);letter-spacing:1px;">10 MODELS AVAILABLE</div>
    </div>
    <div class="bike-grid" id="bikeGrid"></div>
  </div>
</div>

<!-- ===== CART PAGE ===== -->
<div id="cartPage" class="page">
  <div style="padding:120px 40px 80px;max-width:1100px;margin:0 auto;">
    <div class="cart-header">YOUR <span>CART</span></div>
    <div id="cartContent"></div>
  </div>
</div>

<!-- ===== ORDER FORM PAGE ===== -->
<div id="orderFormPage" class="page">
  <div style="padding:120px 40px 80px;max-width:800px;margin:0 auto;">
    <div class="order-form-header">PLACE YOUR <span>ORDER</span></div>
    <p class="order-form-sub">Fill in your delivery details and complete your purchase.</p>
    <div class="form-box">
      <div class="form-section-title">Shipping Information</div>
      <div class="form-row">
        <div class="form-group">
          <label>First Name</label>
          <input type="text" id="oFirst" placeholder="John">
        </div>
        <div class="form-group">
          <label>Last Name</label>
          <input type="text" id="oLast" placeholder="Doe">
        </div>
      </div>
      <div class="form-group">
        <label>Email Address</label>
        <input type="email" id="oEmail" placeholder="you@example.com">
      </div>
      <div class="form-group">
        <label>Phone Number</label>
        <input type="tel" id="oPhone" placeholder="+91 98765 43210">
      </div>
      <div class="form-group">
        <label>Street Address</label>
        <input type="text" id="oAddress" placeholder="123 Main Street, Apartment 4B">
      </div>
      <div class="form-row">
        <div class="form-group">
          <label>City</label>
          <input type="text" id="oCity" placeholder="Chennai">
        </div>
        <div class="form-group">
          <label>PIN Code</label>
          <input type="text" id="oPin" placeholder="600001">
        </div>
      </div>
      <div class="form-group">
        <label>State</label>
        <select id="oState">
          <option value="">Select State</option>
          <option>Tamil Nadu</option><option>Maharashtra</option><option>Karnataka</option>
          <option>Delhi</option><option>Uttar Pradesh</option><option>Gujarat</option>
          <option>West Bengal</option><option>Rajasthan</option><option>Kerala</option>
          <option>Telangana</option>
        </select>
      </div>

      <div class="form-section-title">Order Notes</div>
      <div class="form-group">
        <label>Special Instructions (Optional)</label>
        <textarea id="oNotes" placeholder="Any special assembly requests or delivery instructions..."></textarea>
      </div>

      <div class="form-section-title">Payment Method</div>
      <div style="display:flex;flex-direction:column;gap:12px;margin-bottom:28px;">
        <label style="display:flex;align-items:center;gap:12px;cursor:pointer;padding:14px;border:1px solid var(--border);transition:.2s;" onmouseover="this.style.borderColor='var(--orange)'" onmouseout="this.style.borderColor='var(--border)'">
          <input type="radio" name="payment" value="cod" checked style="accent-color:var(--orange)">
          <span>💵 Cash on Delivery</span>
        </label>
        <label style="display:flex;align-items:center;gap:12px;cursor:pointer;padding:14px;border:1px solid var(--border);transition:.2s;" onmouseover="this.style.borderColor='var(--orange)'" onmouseout="this.style.borderColor='var(--border)'">
          <input type="radio" name="payment" value="upi" style="accent-color:var(--orange)">
          <span>📱 UPI / Net Banking</span>
        </label>
        <label style="display:flex;align-items:center;gap:12px;cursor:pointer;padding:14px;border:1px solid var(--border);transition:.2s;" onmouseover="this.style.borderColor='var(--orange)'" onmouseout="this.style.borderColor='var(--border)'">
          <input type="radio" name="payment" value="card" style="accent-color:var(--orange)">
          <span>💳 Credit / Debit Card</span>
        </label>
      </div>

      <div id="orderFormError" class="error-msg" style="margin-bottom:14px;display:none;"></div>
      <button class="form-submit" onclick="placeOrder()" style="font-size:1.1rem;">CONFIRM ORDER →</button>
    </div>
  </div>
</div>

<!-- ===== CONFIRMATION PAGE ===== -->
<div id="confirmPage" class="page">
  <div style="padding:120px 40px 80px;max-width:700px;margin:0 auto;text-align:center;">
    <div class="confirm-icon">🎉</div>
    <div class="confirm-title">ORDER <span>CONFIRMED!</span></div>
    <p class="confirm-sub">Your ride is on its way! Our team will contact you within 24 hours to schedule delivery and assembly.</p>
    <div class="order-id-box">
      <div class="order-id-label">Order Reference</div>
      <div class="order-id-val" id="confirmOrderId">VR-000000</div>
    </div>
    <div id="confirmItemsTable"></div>
    <div style="display:flex;gap:16px;justify-content:center;flex-wrap:wrap;">
      <button class="btn-primary" onclick="showPage('shopPage')">CONTINUE SHOPPING</button>
      <button class="btn-secondary" onclick="showPage('heroPage')">BACK TO HOME</button>
    </div>
  </div>
</div>

<!-- TOAST -->
<div id="toast"></div>

<script>
// ==============================
//  DATA
// ==============================
const bikes = [
  {
    id:1, brand:"Trek", name:"Marlin 7", emoji:"🚵",
    price:85000, category:"Mountain",
    desc:"Trail-ready hardtail with Shimano Deore drivetrain and RockShox fork.",
    specs:{frame:"Alpha Silver Alum.",gear:"1×10 Shimano",wheel:'29"',weight:"13.1 kg"},
    badge:"BESTSELLER", color:"#1a3a5c"
  },
  {
    id:2, brand:"Giant", name:"Talon 1", emoji:"⛰️",
    price:62000, category:"Mountain",
    desc:"Cross-country speed with lightweight ALUXX aluminum and 2×8 gearing.",
    specs:{frame:"ALUXX Aluminium",gear:"2×8 Shimano",wheel:'27.5"',weight:"12.5 kg"},
    badge:"NEW", color:"#1c3d2a"
  },
  {
    id:3, brand:"Specialized", name:"Allez E5", emoji:"🚴",
    price:75000, category:"Road",
    desc:"E5 premium aluminum frame designed for speed and long-distance comfort.",
    specs:{frame:"E5 Premium Alum.",gear:"2×8 Claris",wheel:'700c',weight:"9.2 kg"},
    badge:"POPULAR", color:"#3d1c1c"
  },
  {
    id:4, brand:"Cannondale", name:"Quick CX 4", emoji:"🏙️",
    price:58000, category:"Hybrid",
    desc:"Urban commuter meets trail explorer. Fast, nimble, and versatile.",
    specs:{frame:"SmartForm C3",gear:"3×7 Shimano",wheel:'700c',weight:"11.8 kg"},
    badge:null, color:"#1c1c3d"
  },
  {
    id:5, brand:"Scott", name:"Aspect 950", emoji:"🌲",
    price:49000, category:"Mountain",
    desc:"Entry-level mountain with a Syncros spec and reliable hydraulic brakes.",
    specs:{frame:"6061 Aluminium",gear:"1×9 Shimano",wheel:'29"',weight:"14.0 kg"},
    badge:null, color:"#2a1c0a"
  },
  {
    id:6, brand:"Merida", name:"Scultura 100", emoji:"🏁",
    price:92000, category:"Road",
    desc:"Race-bred geometry, Shimano Tiagra drivetrain, and Merida's CF2 carbon fork.",
    specs:{frame:"7005 Double Butted",gear:"2×10 Tiagra",wheel:'700c',weight:"8.9 kg"},
    badge:"RACE", color:"#3d1c2a"
  },
  {
    id:7, brand:"Trek", name:"FX 3 Disc", emoji:"🛞",
    price:68000, category:"Hybrid",
    desc:"Flat-bar performance hybrid with disc brakes for all-weather confidence.",
    specs:{frame:"Alpha Platinum Alum",gear:"1×10 Deore",wheel:'700c',weight:"10.5 kg"},
    badge:null, color:"#1a2d3d"
  },
  {
    id:8, brand:"Polygon", name:"Premier 5", emoji:"🌀",
    price:38000, category:"Mountain",
    desc:"Budget-friendly trail machine with SR Suntour fork and Shimano Acera.",
    specs:{frame:"6061 Aluminium",gear:"2×8 Acera",wheel:'27.5"',weight:"13.8 kg"},
    badge:"VALUE", color:"#2a2a1c"
  },
  {
    id:9, brand:"Fuji", name:"Nevada 29 1.9", emoji:"🌵",
    price:44000, category:"Mountain",
    desc:"29er hardtail with smooth-rolling Kenda tires and SR Suntour suspension.",
    specs:{frame:"6061 T6 Butted",gear:"2×8 Altus",wheel:'29"',weight:"13.6 kg"},
    badge:null, color:"#1c2a1c"
  },
  {
    id:10, brand:"Bianchi", name:"C-Sport 2", emoji:"🇮🇹",
    price:110000, category:"Road",
    desc:"Italian heritage with a stiff alloy frame and Shimano 105 11-speed groupset.",
    specs:{frame:"Alloy 7005 Series",gear:"2×11 Shimano 105",wheel:'700c',weight:"8.4 kg"},
    badge:"PREMIUM", color:"#0a2a1c"
  }
];

// ==============================
//  STATE
// ==============================
let cart = [];
let currentUser = null;
const users = []; // in-memory user store

// ==============================
//  NAVIGATION
// ==============================
function showPage(id) {
  document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
  const page = document.getElementById(id);
  if(page) { page.classList.add('active'); window.scrollTo(0,0); }
  if(id === 'cartPage') renderCart();
  if(id === 'shopPage') renderShop();
}

// ==============================
//  MARQUEE
// ==============================
function buildMarquee() {
  const track = document.getElementById('marqueeTrack');
  const items = ['FREE ASSEMBLY', 'TOP BRANDS', '10 MODELS', 'BEST PRICES', '2-YEAR WARRANTY', 'FREE SHIPPING OVER ₹50K', 'EXPERT SUPPORT'];
  let html = '';
  for(let i=0;i<4;i++) items.forEach(t => html += `<span>★ ${t}</span>`);
  track.innerHTML = html;
}

// ==============================
//  SHOP RENDER
// ==============================
function renderShop() {
  const grid = document.getElementById('bikeGrid');
  grid.innerHTML = bikes.map((b,i) => `
    <div class="bike-card" style="animation-delay:${i*0.07}s;background:linear-gradient(160deg,${b.color}33 0%,var(--card-bg) 60%)">
      <div class="bike-img" style="background:linear-gradient(135deg,${b.color}55,${b.color}22)">
        <span>${b.emoji}</span>
        ${b.badge ? `<span class="bike-badge">${b.badge}</span>` : ''}
      </div>
      <div class="bike-info">
        <div class="bike-brand">${b.brand} · ${b.category}</div>
        <div class="bike-name">${b.name}</div>
        <div class="bike-desc">${b.desc}</div>
        <div class="bike-specs">
          <div class="spec"><span>Frame</span><strong>${b.specs.frame}</strong></div>
          <div class="spec"><span>Gear</span><strong>${b.specs.gear}</strong></div>
          <div class="spec"><span>Wheel</span><strong>${b.specs.wheel}</strong></div>
          <div class="spec"><span>Weight</span><strong>${b.specs.weight}</strong></div>
        </div>
        <div class="bike-footer">
          <div class="bike-price">₹${b.price.toLocaleString('en-IN')}</div>
          <button class="add-cart-btn" id="cartBtn_${b.id}" onclick="addToCart(${b.id})">ADD TO CART</button>
        </div>
      </div>
    </div>
  `).join('');
  // Mark already-in-cart buttons
  cart.forEach(item => {
    const btn = document.getElementById(`cartBtn_${item.id}`);
    if(btn) { btn.textContent='IN CART ✓'; btn.classList.add('added'); }
  });
}

// ==============================
//  CART
// ==============================
function addToCart(id) {
  if(!currentUser) { showToast('Please sign in to add items!'); showPage('loginPage'); return; }
  const bike = bikes.find(b=>b.id===id);
  if(!bike) return;
  const existing = cart.find(c=>c.id===id);
  if(existing) { existing.qty++; }
  else { cart.push({...bike, qty:1}); }
  updateCartCount();
  showToast(`${bike.name} added to cart!`);
  // Update button in shop
  const btn = document.getElementById(`cartBtn_${id}`);
  if(btn) { btn.textContent='IN CART ✓'; btn.classList.add('added'); }
}

function updateCartCount() {
  const total = cart.reduce((s,c)=>s+c.qty,0);
  const el = document.getElementById('cartCount');
  el.textContent = total;
  el.style.display = total > 0 ? 'flex' : 'none';
}

function renderCart() {
  const cont = document.getElementById('cartContent');
  if(cart.length === 0) {
    cont.innerHTML = `
      <div class="cart-empty">
        <div class="empty-icon">🛒</div>
        <p>Your cart is empty. Time to find your ride!</p>
        <button class="btn-primary" onclick="showPage('shopPage')">BROWSE BIKES</button>
      </div>`;
    return;
  }
  const subtotal = cart.reduce((s,c)=>s+c.price*c.qty,0);
  const shipping = subtotal >= 50000 ? 0 : 999;
  const total = subtotal + shipping;

  cont.innerHTML = `
    <div class="cart-layout">
      <div class="cart-items">
        ${cart.map(item => `
          <div class="cart-item" id="cartItem_${item.id}">
            <div class="item-emoji">${item.emoji}</div>
            <div class="item-details">
              <div class="item-brand-name">${item.brand} · ${item.category}</div>
              <div class="item-name">${item.name}</div>
              <div class="item-price-unit">₹${item.price.toLocaleString('en-IN')} each</div>
            </div>
            <div class="item-qty">
              <button class="qty-btn" onclick="changeQty(${item.id},-1)">−</button>
              <span class="qty-num">${item.qty}</span>
              <button class="qty-btn" onclick="changeQty(${item.id},1)">+</button>
            </div>
            <div class="item-total">₹${(item.price*item.qty).toLocaleString('en-IN')}</div>
            <button class="remove-btn" onclick="removeItem(${item.id})" title="Remove">✕</button>
          </div>
        `).join('')}
      </div>
      <div class="order-summary">
        <div class="summary-title">Order Summary</div>
        <div class="summary-row"><span>Subtotal (${cart.reduce((s,c)=>s+c.qty,0)} items)</span><span>₹${subtotal.toLocaleString('en-IN')}</span></div>
        <div class="summary-row"><span>Shipping</span><span>${shipping===0?'<span style="color:var(--success)">FREE</span>':'₹'+shipping}</span></div>
        <div class="summary-row"><span>Assembly</span><span style="color:var(--success)">FREE</span></div>
        <div class="summary-row total"><span>Total</span><span>₹${total.toLocaleString('en-IN')}</span></div>
        ${subtotal < 50000 ? `<div style="font-size:.75rem;color:var(--text-muted);margin-top:8px;font-family:'Space Mono',monospace;">Add ₹${(50000-subtotal).toLocaleString('en-IN')} more for free shipping</div>` : ''}
        <button class="checkout-btn" onclick="goToOrderForm()">PLACE ORDER →</button>
        <div style="margin-top:12px;font-size:.75rem;color:var(--text-muted);text-align:center;font-family:'Space Mono',monospace;">🔒 SECURE CHECKOUT · FREE RETURNS</div>
      </div>
    </div>`;
}

function changeQty(id, delta) {
  const item = cart.find(c=>c.id===id);
  if(!item) return;
  item.qty += delta;
  if(item.qty <= 0) removeItem(id);
  else { updateCartCount(); renderCart(); }
}

function removeItem(id) {
  cart = cart.filter(c=>c.id!==id);
  updateCartCount();
  renderCart();
  showToast('Item removed from cart');
}

function goToOrderForm() {
  if(!currentUser) { showToast('Please sign in first!'); showPage('loginPage'); return; }
  // Pre-fill form
  document.getElementById('oFirst').value = currentUser.first || '';
  document.getElementById('oLast').value = currentUser.last || '';
  document.getElementById('oEmail').value = currentUser.email || '';
  document.getElementById('oPhone').value = currentUser.phone || '';
  showPage('orderFormPage');
}

// ==============================
//  ORDER
// ==============================
function placeOrder() {
  const fields = ['oFirst','oLast','oEmail','oPhone','oAddress','oCity','oPin','oState'];
  const labels = ['First Name','Last Name','Email','Phone','Address','City','PIN Code','State'];
  const err = document.getElementById('orderFormError');
  for(let i=0;i<fields.length;i++) {
    const val = document.getElementById(fields[i]).value.trim();
    if(!val) { err.textContent=`Please fill in: ${labels[i]}`; err.style.display='block'; return; }
  }
  err.style.display='none';
  const orderId = 'VR-' + Math.floor(100000+Math.random()*900000);
  const payment = document.querySelector('input[name="payment"]:checked').value;
  // Show confirm
  document.getElementById('confirmOrderId').textContent = orderId;
  const subtotal = cart.reduce((s,c)=>s+c.price*c.qty,0);
  const shipping = subtotal>=50000?0:999;
  document.getElementById('confirmItemsTable').innerHTML = `
    <table class="order-details-table" style="margin-bottom:24px;">
      <thead><tr>
        <th>Bike</th><th>Qty</th><th>Price</th>
      </tr></thead>
      <tbody>
        ${cart.map(c=>`<tr>
          <td class="td-name">${c.emoji} ${c.brand} ${c.name}</td>
          <td>${c.qty}</td>
          <td class="td-price">₹${(c.price*c.qty).toLocaleString('en-IN')}</td>
        </tr>`).join('')}
        <tr><td colspan="2" style="text-align:right;color:var(--text-muted);font-size:.85rem;">Shipping</td><td class="td-price">${shipping===0?'FREE':'₹'+shipping}</td></tr>
        <tr><td colspan="2" style="text-align:right;font-weight:700;">Total</td><td style="font-family:'Bebas Neue',sans-serif;font-size:1.3rem;color:var(--orange);">₹${(subtotal+shipping).toLocaleString('en-IN')}</td></tr>
      </tbody>
    </table>
    <div style="margin-bottom:28px;padding:16px;background:var(--card-bg);border:1px solid var(--border);text-align:left;">
      <div style="font-family:'Space Mono',monospace;font-size:.7rem;letter-spacing:1.5px;color:var(--text-muted);text-transform:uppercase;margin-bottom:8px;">Delivery Details</div>
      <div style="font-size:.9rem;line-height:1.8;">
        <strong>${document.getElementById('oFirst').value} ${document.getElementById('oLast').value}</strong><br>
        ${document.getElementById('oAddress').value}, ${document.getElementById('oCity').value}<br>
        ${document.getElementById('oState').value} - ${document.getElementById('oPin').value}<br>
        📞 ${document.getElementById('oPhone').value}<br>
        💳 Payment: ${payment.toUpperCase()}
      </div>
    </div>`;
  cart = [];
  updateCartCount();
  showPage('confirmPage');
  showToast('🎉 Order placed successfully!');
}

// ==============================
//  AUTH
// ==============================
function toggleAuthForm(showReg) {
  document.getElementById('signinForm').style.display = showReg ? 'none' : 'block';
  document.getElementById('registerForm').style.display = showReg ? 'block' : 'none';
  document.getElementById('loginTitle').textContent = showReg ? 'REGISTER' : 'SIGN IN';
  document.getElementById('loginSubtitle').textContent = showReg ? 'Create your VeloRush account.' : 'Welcome back, rider. Sign in to your account.';
}

function doLogin() {
  const email = document.getElementById('loginEmail').value.trim();
  const pass = document.getElementById('loginPassword').value;
  const err = document.getElementById('loginError');
  if(!email || !pass) { err.textContent='Please fill in all fields.'; err.style.display='block'; return; }
  const user = users.find(u=>u.email===email && u.password===pass);
  if(!user) {
    // Demo: allow any login with "demo@velOrush.com" / "demo123"
    if(email==='demo@velorush.com' && pass==='demo123') {
      setUser({first:'Demo',last:'Rider',email,phone:'+91 99999 99999'});
    } else {
      err.textContent='Invalid credentials. Try demo@velorush.com / demo123'; err.style.display='block'; return;
    }
  } else { setUser(user); }
  err.style.display='none';
  showPage('shopPage');
  showToast(`Welcome back, ${currentUser.first}!`);
}

function doRegister() {
  const first = document.getElementById('regFirst').value.trim();
  const last = document.getElementById('regLast').value.trim();
  const email = document.getElementById('regEmail').value.trim();
  const pass = document.getElementById('regPassword').value;
  const phone = document.getElementById('regPhone').value.trim();
  const err = document.getElementById('regError');
  const suc = document.getElementById('regSuccess');
  if(!first||!last||!email||!pass||!phone) { err.textContent='Please fill all fields.'; err.style.display='block'; return; }
  if(pass.length<6) { err.textContent='Password must be at least 6 characters.'; err.style.display='block'; return; }
  if(users.find(u=>u.email===email)) { err.textContent='Email already registered.'; err.style.display='block'; return; }
  err.style.display='none';
  const user = {first,last,email,password:pass,phone};
  users.push(user);
  suc.style.display='block';
  setTimeout(()=>{ suc.style.display='none'; setUser(user); showPage('shopPage'); showToast(`Welcome to VeloRush, ${first}!`); }, 1200);
}

function setUser(user) {
  currentUser = user;
  document.getElementById('userBadge').style.display='flex';
  document.getElementById('userGreet').textContent = `Hi, ${user.first}`;
  document.getElementById('loginNavLink').style.display = 'none';
}

function logout() {
  currentUser = null;
  cart = [];
  updateCartCount();
  document.getElementById('userBadge').style.display='none';
  document.getElementById('loginNavLink').style.display='block';
  showPage('heroPage');
  showToast('Logged out successfully');
}

// ==============================
//  TOAST
// ==============================
let toastTimer;
function showToast(msg) {
  const t = document.getElementById('toast');
  t.textContent = msg;
  t.style.display='block';
  clearTimeout(toastTimer);
  toastTimer = setTimeout(()=>{ t.style.display='none'; }, 2800);
}

// ==============================
//  INIT
// ==============================
buildMarquee();
renderShop();
</script>
</body>
</html>
