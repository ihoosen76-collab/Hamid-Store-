<!DOCTYPE html>
<html lang="bn">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Hamid Store | Online Grocery & Daily Needs</title>
  <meta name="description" content="Hamid Store - আপনার ঘর, খাবার, দৈনন্দিন প্রয়োজনের একটি বিশ্বস্ত অনলাইন স্টোর।" />
  <script src="https://cdn.tailwindcss.com"></script>
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css" />
  <link href="https://fonts.googleapis.com/css2?family=Hind+Siliguri:wght@400;500;600;700;800&display=swap" rel="stylesheet" />
  <style>
    :root {
      --primary: #0f766e;
      --primary-dark: #115e59;
      --accent: #f59e0b;
      --accent-soft: #fef3c7;
      --bg: #f8fafc;
      --muted: #64748b;
      --success: #16a34a;
      --card: #ffffff;
      --shadow: 0 10px 30px rgba(15, 23, 42, 0.08);
    }

    html { scroll-behavior: smooth; }

    body {
      font-family: 'Hind Siliguri', sans-serif;
      background: linear-gradient(180deg, #f8fafc 0%, #f1f5f9 100%);
      color: #1f2937;
    }

    .section-title {
      position: relative;
      display: inline-block;
      font-weight: 800;
      color: #0f172a;
      margin-bottom: 1rem;
    }

    .section-title::after {
      content: '';
      position: absolute;
      left: 0;
      bottom: -8px;
      width: 60%;
      height: 4px;
      background: linear-gradient(90deg, #f59e0b, #10b981);
      border-radius: 999px;
    }

    .ad-slot {
      background: linear-gradient(135deg, #fef3c7 0%, #fde68a 100%);
      border: 2px dashed #d97706;
      border-radius: 1rem;
      color: #7c2d12;
    }

    .product-card {
      transition: transform 0.2s ease, box-shadow 0.2s ease;
    }

    .product-card:hover {
      transform: translateY(-4px);
      box-shadow: var(--shadow);
    }

    .btn-primary {
      background: linear-gradient(135deg, #0f766e, #0f766e);
      color: white;
    }

    .btn-primary:hover {
      background: linear-gradient(135deg, #115e59, #0f766e);
    }

    .btn-accent {
      background: linear-gradient(135deg, #fbbf24, #f59e0b);
      color: #1f2937;
    }

    .btn-accent:hover {
      background: linear-gradient(135deg, #f59e0b, #d97706);
    }

    .glass {
      background: rgba(255,255,255,0.78);
      backdrop-filter: blur(10px);
      -webkit-backdrop-filter: blur(10px);
    }
  </style>
</head>
<body>
  <header class="bg-gradient-to-r from-emerald-800 via-emerald-700 to-teal-700 text-white shadow-lg sticky top-0 z-40">
    <div class="container mx-auto px-4 py-3">
      <div class="flex flex-col lg:flex-row justify-between items-center gap-4">
        <div class="flex items-center gap-4">
          <div class="w-12 h-12 rounded-full bg-white/10 border border-white/20 flex items-center justify-center shadow-md">
            <i class="fa-solid fa-store text-xl text-amber-300"></i>
          </div>
          <div>
            <h1 class="text-2xl md:text-3xl font-extrabold tracking-wide text-amber-300">Hamid Store</h1>
            <p class="text-xs md:text-sm text-emerald-100 flex items-center gap-1 justify-center lg:justify-start">
              <i class="fa-solid fa-location-dot text-amber-300"></i>
              Kumulli Namder Karatia Post Office
            </p>
          </div>
        </div>

        <div class="flex items-center gap-3 w-full lg:w-auto">
          <div class="relative flex-1 lg:w-80">
            <input id="searchInput" type="text" onkeyup="filterProducts()" placeholder="পণ্য খুঁজুন..." class="w-full pl-10 pr-4 py-2.5 rounded-full text-gray-800 focus:outline-none focus:ring-2 focus:ring-amber-400 shadow-sm" />
            <i class="fa-solid fa-magnifying-glass absolute left-3 top-3.5 text-gray-400"></i>
          </div>

          <button onclick="toggleCartModal()" class="relative btn-accent hover:shadow-md font-bold px-4 py-2.5 rounded-full flex items-center gap-2 text-sm">
            <i class="fa-solid fa-cart-shopping"></i>
            <span>কার্ট</span>
            <span id="cartCount" class="bg-red-600 text-white text-xs w-5 h-5 rounded-full flex items-center justify-center">0</span>
          </button>

          <button onclick="openAdminAuth()" class="bg-emerald-900/80 hover:bg-emerald-950 text-white text-xs px-3 py-2.5 rounded-full transition border border-emerald-500 flex items-center gap-2">
            <i class="fa-solid fa-user-gear"></i>
            <span class="hidden sm:inline">এডমিন</span>
          </button>
        </div>
      </div>
    </div>
  </header>

  <nav class="bg-emerald-900 text-white shadow-inner sticky top-[82px] z-30">
    <div class="container mx-auto px-2 overflow-x-auto">
      <div class="flex whitespace-nowrap py-3 gap-2 text-sm" id="categoryTabs">
        <button data-category="all" class="category-btn active bg-amber-400 text-emerald-950 px-4 py-1.5 rounded-full font-bold transition">সব পণ্য</button>
        <button data-category="সাবান" class="category-btn bg-emerald-700 hover:bg-emerald-600 px-4 py-1.5 rounded-full font-medium transition">সাবান</button>
        <button data-category="তেল" class="category-btn bg-emerald-700 hover:bg-emerald-600 px-4 py-1.5 rounded-full font-medium transition">তেল</button>
        <button data-category="নুডুলস/চিপস/চকলেট" class="category-btn bg-emerald-700 hover:bg-emerald-600 px-4 py-1.5 rounded-full font-medium transition">নুডুলস / চিপস / চকলেট</button>
        <button data-category="লুডু/খেলনা" class="category-btn bg-emerald-700 hover:bg-emerald-600 px-4 py-1.5 rounded-full font-medium transition">লুডু / খেলনা</button>
      </div>
    </div>
  </nav>

  <main class="container mx-auto px-4 py-6 md:py-8">
    <section class="mb-8">
      <div class="grid grid-cols-1 lg:grid-cols-[1.2fr_2.5fr] gap-6 items-center">
        <div class="ad-slot p-4 md:p-6 min-h-[180px] flex flex-col justify-center shadow-sm">
          <span class="inline-block bg-amber-600 text-white text-[10px] font-bold px-2 py-1 rounded-full uppercase tracking-wide mb-3 w-fit">Ad space</span>
          <h3 class="text-lg md:text-xl font-extrabold">আপনার ব্র্যান্ড বা বিজ্ঞাপন</h3>
          <p class="text-sm mt-2 leading-relaxed">এখানে Adsterra, Google AdSense বা কাস্টম বিজ্ঞাপন বসাতে পারবেন।</p>
          <div class="mt-4 border border-amber-300 bg-white/60 rounded-lg p-3 text-xs text-amber-900">
            <i class="fa-regular fa-rectangle-ad text-2xl mb-2 block"></i>
            320x250 / 728x90 / Native Ad Code Here
          </div>
        </div>

        <div class="rounded-3xl overflow-hidden bg-gradient-to-r from-emerald-700 via-teal-700 to-emerald-800 p-6 md:p-8 text-white shadow-xl relative">
          <div class="absolute inset-0 bg-[radial-gradient(circle_at_top_right,_rgba(255,255,255,0.18),_transparent_30%)]"></div>
          <div class="relative z-10">
            <span class="inline-block text-xs font-bold uppercase tracking-[0.2em] bg-white/15 px-3 py-1 rounded-full">Fresh Daily</span>
            <h2 class="text-2xl md:text-4xl font-extrabold mt-4 leading-tight">এক ক্লিকে আপনার প্রয়োজনের সবকিছু</h2>
            <p class="mt-3 max-w-xl text-sm md:text-base text-emerald-50">সাবান, তেল, নুডলস, চকলেট, খেলনা ও দৈনন্দিন জীবনের জিনিসপত্র — Hamid Store-এ অর্ডার করুন, ঘরে বসে নিন দ্রুত ডেলিভারি।</p>
            <div class="mt-6 flex flex-wrap gap-3">
              <a href="#products" class="btn-accent font-bold px-5 py-2.5 rounded-full shadow-sm">শপ করুন</a>
              <a href="https://wa.me/8801700000000" target="_blank" class="bg-white/10 hover:bg-white/20 border border-white/20 font-bold px-5 py-2.5 rounded-full">হোয়াটসঅ্যাপ</a>
            </div>
          </div>
        </div>
      </div>
    </section>

    <section class="mb-10">
      <div class="grid grid-cols-1 md:grid-cols-3 gap-4">
        <div class="bg-white rounded-2xl shadow-sm border border-slate-200 p-4 flex items-center gap-4">
          <div class="w-12 h-12 rounded-full bg-emerald-100 text-emerald-700 flex items-center justify-center text-xl"><i class="fa-solid fa-truck-fast"></i></div>
          <div>
            <h3 class="font-bold text-slate-800">দ্রুত ডেলিভারি</h3>
            <p class="text-sm text-slate-500">সারা এলাকার জন্য দ্রুত সার্ভিস</p>
          </div>
        </div>

        <div class="bg-white rounded-2xl shadow-sm border border-slate-200 p-4 flex items-center gap-4">
          <div class="w-12 h-12 rounded-full bg-amber-100 text-amber-700 flex items-center justify-center text-xl"><i class="fa-solid fa-shield-heart"></i></div>
          <div>
            <h3 class="font-bold text-slate-800">বিশ্বস্ত পণ্য</h3>
            <p class="text-sm text-slate-500">নির্ভরযোগ্য ও মানসম্পন্ন পণ্য</p>
          </div>
        </div>

        <div class="bg-white rounded-2xl shadow-sm border border-slate-200 p-4 flex items-center gap-4">
          <div class="w-12 h-12 rounded-full bg-cyan-100 text-cyan-700 flex items-center justify-center text-xl"><i class="fa-solid fa-wallet"></i></div>
          <div>
            <h3 class="font-bold text-slate-800">ক্যাশ অন ডেলিভারি</h3>
            <p class="text-sm text-slate-500">যাচাই করে পণ্য নিন</p>
          </div>
        </div>
      </div>
    </section>

    <div class="grid grid-cols-1 lg:grid-cols-4 gap-6">
      <aside class="lg:col-span-1 flex flex-col gap-5">
        <div class="ad-slot p-4 shadow-sm min-h-[260px] flex flex-col justify-center">
          <span class="bg-amber-600 text-white text-[10px] font-bold px-2 py-1 rounded-full uppercase tracking-wide w-fit mb-2">বিজ্ঞাপন</span>
          <p class="text-sm font-semibold mb-3">Adsterra Banner / Sidebar Ad</p>
          <div class="w-full border border-amber-300 bg-white/60 rounded-lg p-3 text-xs text-gray-600 min-h-[150px] flex flex-col items-center justify-center text-center">
            <i class="fa-regular fa-rectangle-ad text-4xl text-amber-600 mb-2"></i>
            300x250 / 160x600 Ad Code Here
          </div>
        </div>

        <div class="bg-white rounded-2xl border border-slate-200 shadow-sm p-4">
          <h3 class="font-extrabold text-emerald-800 text-base mb-3 border-b border-slate-200 pb-2 flex items-center gap-2">
            <i class="fa-solid fa-truck-fast text-emerald-600"></i> হোম ডেলিভারি
          </h3>
          <ul class="space-y-2 text-sm text-slate-600 leading-relaxed">
            <li><i class="fa-solid fa-check text-emerald-500 mr-2"></i> কুমুল্লী ও আশেপাশের এলাকার জন্য ডেলিভারি</li>
            <li><i class="fa-solid fa-check text-emerald-500 mr-2"></i> ক্যাশ অন ডেলিভারি সিস্টেম</li>
            <li><i class="fa-solid fa-check text-emerald-500 mr-2"></i> দ্রুত রেসপন্স ও সঠিক পণ্য</li>
            <li><i class="fa-solid fa-check text-emerald-500 mr-2"></i> অর্ডার পেতে কল/হোয়াটসঅ্যাপ</li>
          </ul>
        </div>
      </aside>

      <section id="products" class="lg:col-span-3">
        <div class="flex flex-col sm:flex-row sm:justify-between sm:items-center gap-3 mb-5">
          <h2 id="currentCategoryTitle" class="section-title text-2xl">সব পণ্য</h2>
          <span id="productCount" class="text-sm text-slate-500 bg-white px-3 py-1.5 rounded-full border border-slate-200">০টি পণ্য পাওয়া গেছে</span>
        </div>

        <div id="productsGrid" class="grid grid-cols-2 md:grid-cols-3 xl:grid-cols-4 gap-4 md:gap-5"></div>
      </section>
    </div>

    <div class="mt-10 ad-slot p-4 md:p-5 shadow-sm">
      <div class="flex items-center justify-between gap-4 flex-wrap">
        <span class="bg-amber-600 text-white text-[10px] font-bold px-2 py-1 rounded-full uppercase tracking-wide">Promotional Banner</span>
        <span class="text-xs font-semibold text-amber-900">Adsterra / Native Banner Section</span>
      </div>
      <div class="mt-3 min-h-[80px] border border-amber-300 bg-white/60 rounded-xl flex items-center justify-center text-sm text-slate-600">
        728x90 / 970x250 Native Banner Ad Code Here
      </div>
    </div>
  </main>

  <footer class="bg-slate-900 text-slate-300 py-8 mt-10 border-t border-slate-700">
    <div class="container mx-auto px-4">
      <div class="flex flex-col md:flex-row md:justify-between md:items-center gap-4">
        <div>
          <p class="font-extrabold text-amber-400 text-lg mb-1">Hamid Store</p>
          <p class="text-sm text-slate-400">কুমুল্লী নাম্বারের করটিয়া, পোস্ট অফিস</p>
        </div>
        <div class="flex items-center gap-4 text-sm">
          <a href="https://wa.me/8801700000000" target="_blank" class="hover:text-white transition"><i class="fa-brands fa-whatsapp mr-1"></i> WhatsApp</a>
          <a href="tel:+8801700000000" class="hover:text-white transition"><i class="fa-solid fa-phone mr-1"></i> Call</a>
        </div>
      </div>
      <div class="mt-4 pt-4 border-t border-slate-700 text-xs text-slate-500 text-center md:text-left">
        © 2026 Hamid Store. All rights reserved.
      </div>
    </div>
  </footer>

  <div id="cartModal" class="fixed inset-0 bg-black/60 z-50 hidden">
    <div class="absolute inset-0" onclick="toggleCartModal()"></div>
    <div class="relative ml-auto h-full w-full max-w-md bg-white shadow-2xl flex flex-col">
      <div class="flex justify-between items-center border-b border-slate-200 px-4 py-4">
        <h3 class="text-xl font-extrabold text-emerald-800 flex items-center gap-2">
          <i class="fa-solid fa-cart-shopping"></i> আপনার শপিং কার্ট
        </h3>
        <button onclick="toggleCartModal()" class="text-2xl text-slate-500 hover:text-red-500">&times;</button>
      </div>

      <div class="flex-1 overflow-y-auto px-4 py-3">
        <div id="cartItems" class="space-y-3"></div>
      </div>

      <div class="border-t border-slate-200 bg-slate-50 px-4 py-4">
        <div class="flex justify-between items-center font-bold text-lg mb-4">
          <span>মোট মূল্য:</span>
          <span id="cartTotal" class="text-emerald-700">৳ 0</span>
        </div>

        <div class="space-y-2 mb-4">
          <input id="custName" type="text" placeholder="আপনার নাম *" class="w-full text-sm p-2.5 border border-slate-300 rounded-lg focus:outline-none focus:border-emerald-600" />
          <input id="custPhone" type="tel" placeholder="মোবাইল নম্বর *" class="w-full text-sm p-2.5 border border-slate-300 rounded-lg focus:outline-none focus:border-emerald-600" />
          <textarea id="custAddress" rows="2" placeholder="ঠিকানা / বাসা নং *" class="w-full text-sm p-2.5 border border-slate-300 rounded-lg focus:outline-none focus:border-emerald-600"></textarea>
        </div>

        <button onclick="submitOrder()" class="w-full btn-primary font-bold py-3 rounded-xl shadow-md flex items-center justify-center gap-2 text-sm">
          <i class="fa-brands fa-whatsapp text-lg"></i> হোয়াটসঅ্যাপে অর্ডার পাঠান
        </button>
      </div>
    </div>
  </div>

  <div id="adminModal" class="fixed inset-0 bg-black/70 z-50 flex items-center justify-center p-3 hidden">
    <div class="bg-white rounded-2xl shadow-2xl w-full max-w-3xl max-h-[90vh] overflow-hidden">
      <div class="bg-gradient-to-r from-emerald-800 to-teal-700 text-white p-4 flex justify-between items-center">
        <h3 class="font-extrabold text-lg flex items-center gap-2">
          <i class="fa-solid fa-user-shield"></i> Hamid Store - এডমিন প্যানেল
        </h3>
        <button onclick="closeAdminPanel()" class="text-white hover:text-red-300 text-3xl leading-none">&times;</button>
      </div>

      <div class="p-4 overflow-y-auto max-h-[80vh] space-y-6">
        <div class="bg-emerald-50 border border-emerald-200 rounded-2xl p-4">
          <h4 class="font-extrabold text-emerald-900 mb-3 flex items-center gap-2">
            <i class="fa-solid fa-plus-circle"></i> নতুন পণ্য যোগ করুন
          </h4>
          <form id="addProductForm" onsubmit="handleAddProduct(event)" class="grid grid-cols-1 sm:grid-cols-2 gap-3">
            <input id="pName" type="text" placeholder="পণ্যের নাম" required class="text-sm p-2.5 border border-slate-300 rounded-lg focus:outline-none focus:border-emerald-600" />
            <select id="pCategory" required class="text-sm p-2.5 border border-slate-300 rounded-lg focus:outline-none focus:border-emerald-600">
              <option value="">ক্যাটাগরি নির্বাচন করুন</option>
              <option value="সাবান">সাবান</option>
              <option value="তেল">তেল</option>
              <option value="নুডুলস/চিপস/চকলেট">নুডুলস / চিপস / চকলেট</option>
              <option value="লুডু/খেলনা">লুডু / খেলনা</option>
            </select>
            <input id="pPrice" type="number" min="1" placeholder="মূল্য (টাকা)" required class="text-sm p-2.5 border border-slate-300 rounded-lg focus:outline-none focus:border-emerald-600" />
            <input id="pImg" type="url" placeholder="ছবি URL (অপশনাল)" class="text-sm p-2.5 border border-slate-300 rounded-lg focus:outline-none focus:border-emerald-600" />
            <button type="submit" class="sm:col-span-2 btn-primary font-bold py-2.5 rounded-lg text-sm">পণ্য সেভ করুন</button>
          </form>
        </div>

        <div>
          <h4 class="font-extrabold text-slate-800 mb-3">বর্তমান পণ্যসমূহ</h4>
          <div class="overflow-x-auto border border-slate-200 rounded-xl">
            <table class="w-full text-left text-sm">
              <thead class="bg-slate-100 text-slate-700">
                <tr>
                  <th class="p-3 font-bold">নাম</th>
                  <th class="p-3 font-bold">ক্যাটাগরি</th>
                  <th class="p-3 font-bold">মূল্য</th>
                  <th class="p-3 font-bold text-right">অ্যাকশন</th>
                </tr>
              </thead>
              <tbody id="adminProductTable"></tbody>
            </table>
          </div>
        </div>

        <div class="border-t border-slate-200 pt-4">
          <h4 class="font-extrabold text-slate-800 mb-3">সম্প্রতি প্রাপ্ত অর্ডার</h4>
          <div id="adminOrdersList" class="space-y-2 text-sm max-h-52 overflow-y-auto"></div>
        </div>
      </div>
    </div>
  </div>

  <script>
    const defaultProducts = [
      { id: 1, name: 'মেরিল বিউটি সাবান', category: 'সাবান', price: 45, image: 'https://placehold.co/400x400/edf7f2/0f766e?text=Soap' },
      { id: 2, name: 'লাইফবয় সাবান', category: 'সাবান', price: 40, image: 'https://placehold.co/400x400/f8fafc/0f172a?text=Lifebuoy' },
      { id: 3, name: 'রূপচাঁদা সয়াবিন তেল ১ লিটার', category: 'তেল', price: 165, image: 'https://placehold.co/400x400/fef3c7/d97706?text=Oil' },
      { id: 4, name: 'ম্যাগি নুডুলস ৮ প্যাক', category: 'নুডুলস/চিপস/চকলেট', price: 160, image: 'https://placehold.co/400x400/f0fdf4/166534?text=Noodles' },
      { id: 5, name: 'লেজ চিপস (আলু)', category: 'নুডুলস/চিপস/চকলেট', price: 20, image: 'https://placehold.co/400x400/faf5ff/7c3aed?text=Chips' },
      { id: 6, name: 'ডেয়ারি মিল্ক চকলেট', category: 'নুডুলস/চিপস/চকলেট', price: 50, image: 'https://placehold.co/400x400/fff7ed/c2410c?text=Chocolate' },
      { id: 7, name: 'লুডু বোর্ড সেট', category: 'লুডু/খেলনা', price: 120, image: 'https://placehold.co/400x400/e0f2fe/0369a1?text=Ludo' },
      { id: 8, name: 'প্লাস্টিক খেলনা গাড়ি', category: 'লুডু/খেলনা', price: 80, image: 'https://placehold.co/400x400/eff6ff/1d4ed8?text=Toy' }
    ];

    const storageKeys = {
      products: 'hamid_products',
      orders: 'hamid_orders'
    };

    let products = JSON.parse(localStorage.getItem(storageKeys.products)) || defaultProducts;
    let cart = [];
    let orders = JSON.parse(localStorage.getItem(storageKeys.orders)) || [];
    let currentCategory = 'all';

    if (!localStorage.getItem(storageKeys.products)) {
      localStorage.setItem(storageKeys.products, JSON.stringify(defaultProducts));
    }

    function formatCurrency(amount) {
      return `৳ ${Number(amount).toLocaleString('en-BD')}`;
    }

    function getProductImage(product) {
      return product.image || 'https://placehold.co/400x400/e2e8f0/1e293b?text=Hamid+Store';
    }

    function renderProducts(itemsToRender = null) {
      const grid = document.getElementById('productsGrid');
      const items = itemsToRender || (currentCategory === 'all' ? products : products.filter(p => p.category === currentCategory));
      const productCount = document.getElementById('productCount');
      productCount.textContent = `${items.length}টি পণ্য পাওয়া গেছে`;
      grid.innerHTML = '';

      if (items.length === 0) {
        grid.innerHTML = '<div class="col-span-full text-center py-10 text-slate-400 text-sm">কোনো পণ্য পাওয়া যায়নি</div>';
        return;
      }

      items.forEach(product => {
        const card = document.createElement('div');
        card.className = 'product-card bg-white rounded-2xl border border-slate-200 shadow-sm overflow-hidden';
        card.innerHTML = `
          <div class="relative">
            <img src="${getProductImage(product)}" alt="${product.name}" onerror="this.src='https://placehold.co/400x400/e2e8f0/1e293b?text=Hamid+Store'" class="w-full h-40 object-cover" />
            <span class="absolute top-2 left-2 text-[10px] bg-white/90 text-emerald-700 font-bold px-2 py-1 rounded-full border border-emerald-200">${product.category}</span>
          </div>
          <div class="p-3">
            <h3 class="font-extrabold text-slate-800 text-sm min-h-[48px]">${product.name}</h3>
            <div class="mt-3 flex items-center justify-between">
              <span class="font-bold text-lg text-emerald-700">${formatCurrency(product.price)}</span>
              <button onclick="addToCart(${product.id})" class="btn-accent px-3 py-2 rounded-lg text-xs font-bold flex items-center gap-1">
                <i class="fa-solid fa-plus"></i> যোগ করুন
              </button>
            </div>
          </div>
        `;
        grid.appendChild(card);
      });
    }

    function renderAdminProducts() {
      const tbody = document.getElementById('adminProductTable');
      tbody.innerHTML = '';

      products.forEach(product => {
        const tr = document.createElement('tr');
        tr.className = 'border-b border-slate-200';
        tr.innerHTML = `
          <td class="p-3 font-medium text-slate-700">${product.name}</td>
          <td class="p-3 text-slate-600">${product.category}</td>
          <td class="p-3 font-bold text-emerald-700">${formatCurrency(product.price)}</td>
          <td class="p-3 text-right">
            <button onclick="deleteProduct(${product.id})" class="text-red-600 hover:text-red-700 font-bold text-xs">মুছে দিন</button>
          </td>
        `;
        tbody.appendChild(tr);
      });
    }

    function renderOrders() {
      const container = document.getElementById('adminOrdersList');
      container.innerHTML = '';

      if (!orders.length) {
        container.innerHTML = '<p class="text-slate-400 italic">কোনো নতুন অর্ডার নেই</p>';
        return;
      }

      orders.slice().reverse().forEach(order => {
        const item = document.createElement('div');
        item.className = 'bg-slate-50 border border-slate-200 rounded-lg p-3';
        item.innerHTML = `
          <div class="flex justify-between items-center mb-1">
            <strong class="text-slate-800">${order.name}</strong>
            <span class="text-xs text-emerald-700 font-bold">${order.time}</span>
          </div>
          <p class="text-slate-600 text-xs">${order.phone}</p>
          <p class="text-slate-600 text-xs mt-1">${order.address}</p>
          <p class="text-slate-800 font-bold mt-2">${order.items}</p>
        `;
        container.appendChild(item);
      });
    }

    function selectCategory(category) {
      currentCategory = category;
      const buttons = document.querySelectorAll('.category-btn');
      buttons.forEach(btn => {
        const isActive = btn.dataset.category === category;
        btn.classList.toggle('bg-amber-400', isActive);
        btn.classList.toggle('text-emerald-950', isActive);
        btn.classList.toggle('font-bold', isActive);
        btn.classList.toggle('bg-emerald-700', !isActive);
        btn.classList.toggle('text-white', !isActive);
      });

      const title = category === 'all' ? 'সব পণ্য' : category;
      document.getElementById('currentCategoryTitle').textContent = title;
      renderProducts();
    }

    document.querySelectorAll('.category-btn').forEach(button => {
      button.addEventListener('click', () => selectCategory(button.dataset.category));
    });

    function filterProducts() {
      const query = document.getElementById('searchInput').value.trim().toLowerCase();
      const filtered = products.filter(product => {
        return product.name.toLowerCase().includes(query) || product.category.toLowerCase().includes(query);
      });
      renderProducts(filtered);
    }

    function addToCart(productId) {
      const product = products.find(item => item.id === productId);
      if (!product) return;

      const existing = cart.find(item => item.id === productId);
      if (existing) {
        existing.qty += 1;
      } else {
        cart.push({ ...product, qty: 1 });
      }

      updateCartUI();
      toggleCartModal(true);
    }

    function updateCartUI() {
      const totalCount = cart.reduce((sum, item) => sum + item.qty, 0);
      document.getElementById('cartCount').textContent = totalCount;

      const cartItems = document.getElementById('cartItems');
      const cartTotal = document.getElementById('cartTotal');

      if (!cart.length) {
        cartItems.innerHTML = '<div class="text-center py-8 text-slate-400 text-sm">কার্ট খালি</div>';
        cartTotal.textContent = '৳ 0';
        return;
      }

      let total = 0;
      cartItems.innerHTML = cart.map(item => {
        total += item.price * item.qty;
        return `
          <div class="flex items-center gap-3 border border-slate-200 rounded-xl p-2 bg-white shadow-sm">
            <img src="${getProductImage(item)}" alt="${item.name}" class="w-16 h-16 rounded-lg object-cover" />
            <div class="flex-1 min-w-0">
              <div class="font-bold text-slate-800 text-sm">${item.name}</div>
              <div class="text-xs text-slate-500">${formatCurrency(item.price)} x ${item.qty}</div>
            </div>
            <div class="text-right">
              <div class="font-bold text-emerald-700 text-sm">${formatCurrency(item.price * item.qty)}</div>
              <button onclick="removeFromCart(${item.id})" class="mt-1 text-xs text-red-600 hover:text-red-700 font-bold">মুছে দিন</button>
            </div>
          </div>
        `;
      }).join('');

      cartTotal.textContent = formatCurrency(total);
    }

    function removeFromCart(productId) {
      cart = cart.filter(item => item.id !== productId);
      updateCartUI();
    }

    function toggleCartModal(forceOpen = null) {
      const modal = document.getElementById('cartModal');
      const shouldOpen = forceOpen === null ? modal.classList.contains('hidden') : forceOpen;
      modal.classList.toggle('hidden', !shouldOpen);
      if (shouldOpen) updateCartUI();
    }

    function openAdminAuth() {
      const password = prompt('এডমিন পাসওয়ার্ড লিখুন');
      if (password === 'hamid123') {
        document.getElementById('adminModal').classList.remove('hidden');
      } else if (password !== null) {
        alert('পাসওয়ার্ড ভুল হয়েছে');
      }
    }

    function closeAdminPanel() {
      document.getElementById('adminModal').classList.add('hidden');
    }

    function handleAddProduct(event) {
      event.preventDefault();
      const name = document.getElementById('pName').value.trim();
      const category = document.getElementById('pCategory').value;
      const price = Number(document.getElementById('pPrice').value);
      const image = document.getElementById('pImg').value.trim();

      if (!name || !category || !price) {
        alert('সব ফিল্ড পূরণ করুন');
        return;
      }

      const newProduct = {
        id: Date.now(),
        name,
        category,
        price,
        image: image || `https://placehold.co/400x400/e2e8f0/1e293b?text=${encodeURIComponent(name)}`
      };

      products.unshift(newProduct);
      localStorage.setItem(storageKeys.products, JSON.stringify(products));
      renderProducts();
      renderAdminProducts();
      document.getElementById('addProductForm').reset();
    }

    function deleteProduct(productId) {
      const confirmDelete = confirm('এই পণ্যটি মুছে ফেলবেন?');
      if (!confirmDelete) return;

      products = products.filter(product => product.id !== productId);
      localStorage.setItem(storageKeys.products, JSON.stringify(products));
      renderProducts();
      renderAdminProducts();
    }

    function submitOrder() {
      const name = document.getElementById('custName').value.trim();
      const phone = document.getElementById('custPhone').value.trim();
      const address = document.getElementById('custAddress').value.trim();

      if (!cart.length) {
        alert('কার্টে কোনো পণ্য নেই');
        return;
      }

      if (!name || !phone || !address) {
        alert('আপনার নাম, মোবাইল ও ঠিকানা পূরণ করুন');
        return;
      }

      const orderSummary = cart.map(item => `${item.name} (${item.qty}টি)`).join(', ');
      const total = cart.reduce((sum, item) => sum + item.price * item.qty, 0);
      const timestamp = new Date().toLocaleString('bn-BD');

      orders.push({
        name,
        phone,
        address,
        items: orderSummary,
        total,
        time: timestamp
      });

      localStorage.setItem(storageKeys.orders, JSON.stringify(orders));
      renderOrders();

      const message = `Hamid Store অর্ডার\n\nনাম: ${name}\nমোবাইল: ${phone}\nঠিকানা: ${address}\n\nপণ্যসমূহ:\n${orderSummary}\n\nমোট: ${formatCurrency(total)}`;
      const waLink = `https://wa.me/8801700000000?text=${encodeURIComponent(message)}`;
      window.open(waLink, '_blank');

      cart = [];
      updateCartUI();
      document.getElementById('custName').value = '';
      document.getElementById('custPhone').value = '';
      document.getElementById('custAddress').value = '';
      toggleCartModal(false);
      alert('অর্ডারটি WhatsApp-এ পাঠানো হয়েছে');
    }

    window.onload = function () {
      renderProducts();
      renderAdminProducts();
      renderOrders();
      updateCartUI();
    };
  </script>
</body>
</html>
