```html
<!DOCTYPE html>
<html lang="bn">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Hamid Store - হামিদ স্টোর</title>
    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- FontAwesome Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <!-- Google Font: Hind Siliguri for Bengali -->
    <link href="https://fonts.googleapis.com/css2?family=Hind+Siliguri:wght@400;500;600;700&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Hind Siliguri', sans-serif;
            background-color: #f3f4f6;
        }
        .ad-placeholder {
            background: linear-gradient(135deg, #fef3c7 0%, #fde68a 100%);
            border: 2px dashed #d97706;
        }
    </style>
</head>
<body class="bg-gray-100 text-gray-800 min-h-screen flex flex-col">

    <!-- Header Section -->
    <header class="bg-emerald-700 text-white shadow-lg sticky top-0 z-40">
        <div class="container mx-auto px-4 py-3">
            <div class="flex flex-col md:flex-row justify-between items-center gap-3">
                <!-- Store Name & Location -->
                <div class="text-center md:text-left">
                    <h1 class="text-3xl font-extrabold tracking-wide text-amber-300 drop-shadow">Hamid Store</h1>
                    <p class="text-xs md:text-sm text-emerald-100 flex items-center justify-center md:justify-start gap-1">
                        <i class="fa-solid fa-location-dot text-amber-300"></i>
                        Kumulli Namder Karatia Post Office
                    </p>
                </div>

                <!-- Search Bar & Cart / Admin Buttons -->
                <div class="flex items-center gap-3 w-full md:w-auto">
                    <div class="relative flex-1 md:w-64">
                        <input type="text" id="searchInput" onkeyup="filterProducts()" placeholder="পণ্য খুঁজুন..." class="w-full pl-9 pr-3 py-1.5 rounded-full text-gray-800 text-sm focus:outline-none focus:ring-2 focus:ring-amber-400">
                        <i class="fa-solid fa-magnifying-glass absolute left-3 top-2.5 text-gray-400 text-xs"></i>
                    </div>

                    <!-- Cart Button -->
                    <button onclick="toggleCartModal()" class="relative bg-amber-400 hover:bg-amber-500 text-emerald-950 font-bold px-3 py-1.5 rounded-full flex items-center gap-1.5 text-sm transition">
                        <i class="fa-solid fa-cart-shopping"></i>
                        <span>কার্ট</span>
                        <span id="cartCount" class="bg-red-600 text-white text-xs w-5 h-5 rounded-full flex items-center justify-center">0</span>
                    </button>

                    <!-- Admin Panel Toggle -->
                    <button onclick="openAdminAuth()" class="bg-emerald-900 hover:bg-emerald-950 text-white text-xs px-2.5 py-1.5 rounded-full transition border border-emerald-500 flex items-center gap-1">
                        <i class="fa-solid fa-user-gear"></i>
                        <span class="hidden sm:inline">এডমিন</span>
                    </button>
                </div>
            </div>
        </div>
    </header>

    <!-- Navigation / Categories Bar -->
    <nav class="bg-emerald-800 text-white shadow-inner sticky top-[68px] z-30">
        <div class="container mx-auto px-2 overflow-x-auto">
            <div class="flex whitespace-nowrap py-2 gap-2 text-sm" id="categoryTabs">
                <button onclick="selectCategory('all')" class="category-btn active bg-amber-400 text-emerald-950 px-3 py-1 rounded-full font-medium transition">সব পণ্য</button>
                <button onclick="selectCategory('সাবান')" class="category-btn bg-emerald-700 hover:bg-emerald-600 px-3 py-1 rounded-full font-medium transition">সাবান</button>
                <button onclick="selectCategory('তেল')" class="category-btn bg-emerald-700 hover:bg-emerald-600 px-3 py-1 rounded-full font-medium transition">তেল</button>
                <button onclick="selectCategory('নুডুলস/চিপস/চকলেট')" class="category-btn bg-emerald-700 hover:bg-emerald-600 px-3 py-1 rounded-full font-medium transition">নুডুলস / চিপস / চকলেট</button>
                <button onclick="selectCategory('লুডু/খেলনা')" class="category-btn bg-emerald-700 hover:bg-emerald-600 px-3 py-1 rounded-full font-medium transition">লুডু / খেলনা</button>
            </div>
        </div>
    </nav>

    <!-- Main Content Area Grid (Sketch Layout) -->
    <main class="container mx-auto px-4 py-6 flex-1">
        
        <div class="grid grid-cols-1 lg:grid-cols-4 gap-6">
            
            <!-- Left Side / Top Banner: Adsterra Ads Container (Based on Sketch 'Ads' Box) -->
            <aside class="lg:col-span-1 flex flex-col gap-4">
                <!-- Adsterra Placeholders -->
                <div class="ad-placeholder p-4 rounded-xl text-center shadow-sm flex flex-col items-center justify-center min-h-[250px]">
                    <span class="bg-amber-600 text-white text-xs font-bold px-2 py-0.5 rounded mb-2">বিজ্ঞাপন (Ads)</span>
                    <p class="text-xs text-amber-900 mb-2 font-semibold">Adsterra Banner Code Here</p>
                    <div class="w-full text-gray-500 text-xs border border-amber-300 p-3 rounded bg-white/60">
                        <!-- PASTE YOUR ADSTERRA BANNER CODE BELOW THIS COMMENT -->
                        <i class="fa-regular fa-rectangle-ad text-3xl text-amber-600 mb-1"></i>
                        <p class="text-[11px]">এখানে Adsterra এর ৩২০x২৫০ বা অন্যান্য ব্যানার অ্যাড কোড বসান</p>
                    </div>
                </div>

                <!-- Info Box -->
                <div class="bg-white p-4 rounded-xl shadow-sm border border-gray-200">
                    <h3 class="font-bold text-emerald-800 text-sm mb-2 border-b pb-1 flex items-center gap-1">
                        <i class="fa-solid fa-truck-fast text-emerald-600"></i> হোম ডেলিভারি তথ্য
                    </h3>
                    <p class="text-xs text-gray-600 leading-relaxed">
                        কুমুল্লী নাম্বারের করটিয়া এলাকায় ক্যাশ অন ডেলিভারিতে দ্রুত পণ্য পৌঁছে দেওয়া হয়। যেকোনো প্রয়োজনে যোগাযোগ করুন।
                    </p>
                </div>
            </aside>

            <!-- Right Side Grid: Products Display (Based on Sketch Product Boxes) -->
            <section class="lg:col-span-3">
                <div class="flex justify-between items-center mb-4">
                    <h2 id="currentCategoryTitle" class="text-xl font-bold text-gray-800 border-l-4 border-emerald-600 pl-2">সব পণ্য</h2>
                    <span id="productCount" class="text-xs text-gray-500">০টি পণ্য পাওয়া গেছে</span>
                </div>

                <!-- Products Grid -->
                <div id="productsGrid" class="grid grid-cols-2 sm:grid-cols-3 md:grid-cols-3 lg:grid-cols-4 gap-3 sm:gap-4">
                    <!-- Products will render dynamically here -->
                </div>
            </section>
        </div>

        <!-- Horizontal Native Adsterra Banner Slot -->
        <div class="mt-8 ad-placeholder p-4 rounded-xl text-center shadow-sm">
            <span class="bg-amber-600 text-white text-xs font-bold px-2 py-0.5 rounded mb-1 inline-block">বিজ্ঞাপন (Adsterra Native / Banner)</span>
            <div class="text-xs text-gray-500 border border-amber-300 p-2 rounded bg-white/60 min-h-[60px] flex items-center justify-center">
                <!-- PASTE YOUR ADSTERRA HORIZONTAL AD CODE HERE -->
                <p>Adsterra 728x90 or Native Banner Ad Code</p>
            </div>
        </div>
    </main>

    <!-- Footer -->
    <footer class="bg-gray-800 text-gray-300 py-6 mt-6 border-t border-gray-700 text-center text-xs">
        <div class="container mx-auto px-4">
            <p class="font-bold text-amber-400 text-sm mb-1">Hamid Store (হামিদ স্টোর)</p>
            <p class="text-gray-400 mb-3">কুমুল্লী নাম্বারের করটিয়া, পোস্ট অফিস</p>
            <p class="text-gray-500">© 2026 Hamid Store. All rights reserved.</p>
        </div>
    </footer>

    <!-- Shopping Cart Modal -->
    <div id="cartModal" class="fixed inset-0 bg-black/60 z-50 flex justify-end hidden">
        <div class="bg-white w-full max-w-md h-full shadow-2xl flex flex-col justify-between p-4 overflow-y-auto">
            <div>
                <div class="flex justify-between items-center border-b pb-3">
                    <h3 class="text-lg font-bold text-emerald-800 flex items-center gap-2">
                        <i class="fa-solid fa-cart-shopping"></i> আপনার শপিং কার্ট
                    </h3>
                    <button onclick="toggleCartModal()" class="text-gray-500 hover:text-red-500 text-xl font-bold">&times;</button>
                </div>

                <!-- Cart Items List -->
                <div id="cartItems" class="divide-y divide-gray-100 my-4 max-h-[50vh] overflow-y-auto">
                    <!-- Dynamic Cart Items -->
                </div>
            </div>

            <!-- Customer Details Form & Checkout -->
            <div class="border-t pt-3 bg-gray-50 -mx-4 -mb-4 p-4">
                <div class="flex justify-between font-bold text-base mb-3">
                    <span>মোট মূল্য:</span>
                    <span id="cartTotal" class="text-emerald-700">৳ 0</span>
                </div>

                <div class="space-y-2 mb-3">
                    <input type="text" id="custName" placeholder="আপনার নাম *" class="w-full text-xs p-2 border rounded focus:outline-none focus:border-emerald-600">
                    <input type="tel" id="custPhone" placeholder="মোবাইল নম্বর *" class="w-full text-xs p-2 border rounded focus:outline-none focus:border-emerald-600">
                    <textarea id="custAddress" placeholder="ঠিকানা / বাসা নং *" rows="2" class="w-full text-xs p-2 border rounded focus:outline-none focus:border-emerald-600"></textarea>
                </div>

                <button onclick="submitOrder()" class="w-full bg-emerald-600 hover:bg-emerald-700 text-white font-bold py-2.5 rounded-lg shadow transition text-sm flex items-center justify-center gap-2">
                    <i class="fa-brands fa-whatsapp text-lg"></i> হোয়াটসঅ্যাপে অর্ডার পাঠান
                </button>
            </div>
        </div>
    </div>

    <!-- Admin Panel Modal -->
    <div id="adminModal" class="fixed inset-0 bg-black/70 z-50 flex items-center justify-center p-3 hidden">
        <div class="bg-white rounded-xl shadow-2xl w-full max-w-2xl max-h-[90vh] flex flex-col overflow-hidden">
            <!-- Admin Header -->
            <div class="bg-emerald-800 text-white p-4 flex justify-between items-center">
                <h3 class="font-bold text-lg flex items-center gap-2">
                    <i class="fa-solid fa-user-shield"></i> হামিদ স্টোর - এডমিন প্যানেল
                </h3>
                <button onclick="closeAdminPanel()" class="text-white hover:text-red-300 text-2xl font-bold">&times;</button>
            </div>

            <!-- Admin Content -->
            <div class="p-4 overflow-y-auto flex-1 space-y-6">
                <!-- Add New Product Form -->
                <div class="bg-emerald-50 p-4 rounded-lg border border-emerald-200">
                    <h4 class="font-bold text-emerald-900 mb-3 text-sm flex items-center gap-1">
                        <i class="fa-solid fa-plus-circle"></i> নতুন পণ্য যোগ করুন
                    </h4>
                    <form id="addProductForm" onsubmit="handleAddProduct(event)" class="grid grid-cols-1 sm:grid-cols-2 gap-3">
                        <input type="text" id="pName" placeholder="পণ্যের নাম (যেমন: মেরিল সাবান)" required class="text-xs p-2 border rounded">
                        <select id="pCategory" required class="text-xs p-2 border rounded">
                            <option value="">ক্যাটাগরি নির্বাচন করুন</option>
                            <option value="সাবান">সাবান</option>
                            <option value="তেল">তেল</option>
                            <option value="নুডুলস/চিপস/চকলেট">নুডুলস / চিপস / চকলেট</option>
                            <option value="লুডু/খেলনা">লুডু / খেলনা</option>
                        </select>
                        <input type="number" id="pPrice" placeholder="মূল্য (টাকা)" required class="text-xs p-2 border rounded">
                        <input type="url" id="pImg" placeholder="ছবি URL (অপশনাল)" class="text-xs p-2 border rounded">
                        <button type="submit" class="sm:col-span-2 bg-emerald-700 hover:bg-emerald-800 text-white font-bold py-2 rounded text-xs transition">
                            পণ্য সেভ করুন
                        </button>
                    </form>
                </div>

                <!-- Product List Management -->
                <div>
                    <h4 class="font-bold text-gray-800 mb-2 text-sm">বর্তমান পণ্যসমূহ</h4>
                    <div class="overflow-x-auto">
                        <table class="w-full text-left text-xs border-collapse">
                            <thead>
                                <tr class="bg-gray-100 border-b">
                                    <th class="p-2">নাম</th>
                                    <th class="p-2">ক্যাটাগরি</th>
                                    <th class="p-2">মূল্য</th>
                                    <th class="p-2 text-right">অ্যাকশন</th>
                                </tr>
                            </thead>
                            <tbody id="adminProductTable">
                                <!-- Dynamic Rows -->
                            </tbody>
                        </table>
                    </div>
                </div>

                <!-- Received Orders -->
                <div class="border-t pt-4">
                    <h4 class="font-bold text-gray-800 mb-2 text-sm">সম্প্রতি প্রাপ্ত অর্ডারসমূহ</h4>
                    <div id="adminOrdersList" class="space-y-2 text-xs max-h-40 overflow-y-auto">
                        <p class="text-gray-400 italic">কোনো নতুন অর্ডার নেই</p>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <!-- JavaScript Application Logic -->
    <script>
        // Sample Initial Products (Default fallback)
        const defaultProducts = [
            { id: 1, name: "মেরিল বিউটি সাবান", category: "সাবান", price: 45, image: "https://placehold.co/200x200/e2e8f0/1e293b?text=Soap" },
            { id: 2, name: "লাইফবয় সাবান", category: "সাবান", price: 40, image: "https://placehold.co/200x200/e2e8f0/1e293b?text=Lifebuoy" },
            { id: 3, name: "রূপচাঁদা সোয়াবিন তেল ১ লিটার", category: "তেল", price: 165, image: "https://placehold.co/200x200/e2e8f0/1e293b?text=Oil" },
            { id: 4, name: "ম্যাগি নুডুলস ৮ প্যাক", category: "নুডুলস/চিপস/চকলেট", price: 160, image: "https://placehold.co/200x200/e2e8f0/1e293b?text=Noodles" },
            { id: 5, name: "লেজ চিপস (আালু)", category: "নুডুলস/চিপস/চকলেট", price: 20, image: "https://placehold.co/200x200/e2e8f0/1e293b?text=Chips" },
            { id: 6, name: "ডেয়ারি মিল্ক চকলেট", category: "নুডুলস/চিপস/চকলেট", price: 50, image: "https://placehold.co/200x200/e2e8f0/1e293b?text=Chocolate" },
            { id: 7, name: "লুডু বোর্ড সেট", category: "লুডু/খেলনা", price: 120, image: "https://placehold.co/200x200/e2e8f0/1e293b?text=Ludo" },
            { id: 8, name: "প্লাস্টিক খেলনা গাড়ি", category: "লুডু/খেলনা", price: 80, image: "https://placehold.co/200x200/e2e8f0/1e293b?text=Toy" }
        ];

        // State Management
        let products = JSON.parse(localStorage.getItem('hamid_products')) || defaultProducts;
        let cart = [];
        let orders = JSON.parse(localStorage.getItem('hamid_orders')) || [];
        let currentCategory = 'all';

        // Save default products if first time
        if(!localStorage.getItem('hamid_products')) {
            localStorage.setItem('hamid_products', JSON.stringify(defaultProducts));
        }

        // Initialize Page
        window.onload = function() {
            renderProducts();
            renderAdminProducts();
            renderOrders();
        };

        // Render Products Grid
        function renderProducts(itemsToRender = null) {
            const grid = document.getElementById('productsGrid');
            const items = itemsToRender || (currentCategory === 'all' ? products : products.filter(p => p.category === currentCategory));
            
            document.getElementById('productCount').innerText = `${items.length}টি পণ্য পাওয়া গেছে`;
            grid.innerHTML = '';

            if (items.length === 0) {
                grid.innerHTML = `<div class="col-span-full text-center py-8 text-gray-400">কোনো পণ্য পাওয়া যায়নি</div>`;
                return;
            }

            items.forEach(product => {
                const card = document.createElement('div');
                card.className = "bg-white rounded-xl shadow-sm hover:shadow-md transition p-3 flex flex-col justify-between border border-gray-100";
                card.innerHTML = `
                    <div>
                        <img src="${product.image}" alt="${product.name}" onerror="this.src='https://placehold.co/200x200/e2e8f0/1e293b?text=Hamid+Store'" class="w-full h-28 object-cover rounded-lg mb-2">
                        <span class="text-[10px] bg-emerald-50 text-emerald-700 px-1.5 py-0.5 rounded font-medium">${product.category}</span>
                        <h3 class="font-bold text-gray-800 text-xs sm:text-sm mt-1 line-clamp-2">${product.name}</h3>
                    </div>
                    <div class="mt-3 pt-2 border-t flex items-center justify-between">
                        <span class="font-bold text-emerald-700 text-sm">৳ ${product.price}</span>
                        <button onclick="addToCart(${product.id})" class="bg-amber-400 hover:bg-amber-500 text-emerald-950 p-1.5 rounded-lg text-xs font-bold transition flex items-center gap-1">
                            <i class="fa-solid fa-plus"></i> যোগ করুন
                        </button>
                    </div>
                `;
                grid.appendChild(card);
            });
        }

        // Category Filter
        function selectCategory(category) {
            currentCategory = category;
            const buttons = document.querySelectorAll('.category-btn');
            buttons.forEach(btn => {
                btn.classList.remove('bg-amber-400', 'text-emerald-950');
                btn.classList.add('bg-emerald-700', 'text-white');
            });

            event.target.classList.remove('bg-emerald-700', 'text-white');
            event.target.classList.add('bg-amber-400', 'text-emerald-950');

            document.getElementById('currentCategoryTitle').innerText = category === 'all' ? 'সব পণ্য' : category;
            renderProducts();
        }

        // Search Filter
        function filterProducts() {
            const query = document.getElementById('searchInput').value.toLowerCase();
            const filtered = products.filter(p => p.name.toLowerCase().includes(query) || p.category.toLowerCase().includes(query));
            renderProducts(filtered);
        }

        // Shopping Cart Functions
        function addToCart(productId) {
            const product = products.find(p => p.id === productId);
            const existing = cart.find(item => item.id === productId);

            if (existing) {
                existing.qty += 1;
            } else {
                cart.push({ ...product, qty: 1 });
            }

            updateCartUI();
        }

        function updateCartUI() {
            const cartCount = document.getElementById('cartCount');
            const cartItems = document.getElementById('cartItems');
            const cartTotal = document.getElementById('cartTotal');
