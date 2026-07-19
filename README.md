<!DOCTYPE html>
<html lang="tr" class="scroll-smooth">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>modeX | Sokak Modasının Yeni Boyutu</title>
  <!-- Tailwind CSS -->
  <script src="https://cdn.tailwindcss.com"></script>
  <!-- FontAwesome İkonları -->
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
  <style>
    .glass {
      background: rgba(11, 15, 25, 0.75);
      backdrop-filter: blur(20px);
      -webkit-backdrop-filter: blur(20px);
      border: 1px solid rgba(255, 255, 255, 0.05);
    }
    @keyframes pulse-neon {
      0%, 100% { transform: scale(1); filter: drop-shadow(0 0 15px rgba(168, 85, 247, 0.6)); }
      50% { transform: scale(1.08); filter: drop-shadow(0 0 35px rgba(6, 182, 212, 0.8)); }
    }
    .neon-pulse { animation: pulse-neon 2s infinite ease-in-out; }
  </style>
</head>
<body class="bg-[#070a13] text-gray-100 min-h-screen font-sans overflow-y-auto">

  <!-- ================= ANİMASYONLU YÜKLEME EKRANI (SPLASH) ================= -->
  <div id="splashScreen" class="fixed inset-0 bg-[#070a13] z-[9999] flex flex-col items-center justify-center transition-all duration-1000 ease-in-out">
    <div class="text-center">
      <h1 class="text-6xl md:text-8xl font-black tracking-widest bg-gradient-to-r from-purple-500 via-pink-500 to-cyan-400 bg-clip-text text-transparent neon-pulse">
        modeX
      </h1>
      <p class="text-gray-500 tracking-[0.3em] uppercase text-xs md:text-sm mt-6 animate-pulse">Tarz Yükleniyor...</p>
    </div>
  </div>

  <!-- ================= MÜŞTERİ GOOGLE GİRİŞ MODAL ================= -->
  <div id="authModal" class="fixed inset-0 bg-black/80 backdrop-blur-md z-[9998] hidden flex items-center justify-center p-4">
    <div class="glass w-full max-w-md p-8 rounded-3xl text-center relative z-10 space-y-6">
      <div class="flex justify-between items-center">
        <h2 class="text-3xl font-black tracking-widest bg-gradient-to-r from-purple-500 via-pink-500 to-cyan-400 bg-clip-text text-transparent">modeX</h2>
        <button onclick="closeAuthModal()" class="text-gray-400 hover:text-white text-2xl">&times;</button>
      </div>
      <p class="text-gray-400 text-sm">Siparişinizi güvenle ve hızlıca WhatsApp üzerinden tamamlamak için Google hesabınızla giriş yapın.</p>
      <div class="space-y-3 pt-4">
        <button id="authGoogleBtn" class="w-full py-4 px-4 rounded-xl bg-[#121829] border border-gray-800 hover:border-purple-500 text-base font-bold transition flex items-center justify-center gap-3 shadow-lg shadow-purple-500/10">
          <i class="fab fa-google text-purple-500 text-lg"></i> Google ile Giriş Yap
        </button>
      </div>
    </div>
  </div>

  <!-- ================= AYRI YÖNETİCİ ŞİFRELİ GİRİŞ MODAL ================= -->
  <div id="adminModal" class="fixed inset-0 bg-black/85 backdrop-blur-sm z-[9998] hidden flex items-center justify-center p-4">
    <div class="glass w-full max-w-sm p-8 rounded-3xl">
      <div class="flex justify-between items-center mb-6">
        <h4 class="text-2xl font-black tracking-wider text-purple-400 font-mono">Yönetici Girişi</h4>
        <button onclick="closeAdminModal()" class="text-gray-400 hover:text-white text-2xl">&times;</button>
      </div>
      <div class="space-y-4">
        <div>
          <label class="block text-xs font-bold tracking-widest text-gray-500 mb-2 uppercase">Kullanıcı Adı</label>
          <input type="text" id="adminEmailInput" placeholder="Yönetici adı" class="w-full bg-[#121829] border border-gray-800 rounded-xl px-4 py-3 text-white focus:outline-none focus:border-purple-500 text-sm">
        </div>
        <div>
          <label class="block text-xs font-bold tracking-widest text-gray-500 mb-2 uppercase">Şifre</label>
          <input type="password" id="adminPasswordInput" placeholder="••••••••" class="w-full bg-[#121829] border border-gray-800 rounded-xl px-4 py-3 text-white focus:outline-none focus:border-purple-500 text-sm">
        </div>
        <button id="adminLoginSubmitBtn" class="w-full py-3 bg-gradient-to-r from-purple-600 to-pink-600 rounded-xl font-bold hover:opacity-90 transition mt-4">
          Panele Giriş Yap
        </button>
      </div>
    </div>
  </div>

  <!-- ================= ANA İÇERİK ================= -->
  <div id="mainContent">
    
    <!-- ================= ÜST MENÜ ================= -->
    <header class="fixed top-0 left-0 w-full z-50 glass transition-all duration-500" id="mainHeader">
      <div class="max-w-7xl mx-auto px-6 py-4 flex justify-between items-center">
        <h1 onclick="window.location.hash=''" class="text-3xl font-extrabold tracking-widest bg-gradient-to-r from-purple-500 via-pink-500 to-cyan-400 bg-clip-text text-transparent cursor-pointer">
          modeX
        </h1>
        <div class="flex items-center gap-3">
          <!-- MÜŞTERİ GOOGLE GİRİŞİ -->
          <button id="customerGoogleTrigger" onclick="openAuthModal('navbarLogin')" class="text-xs bg-cyan-500/10 hover:bg-cyan-500 border border-cyan-500/30 text-cyan-400 hover:text-[#070a13] px-3 py-2 rounded-xl transition font-semibold">
            <i class="fab fa-google mr-1"></i> Google Girişi
          </button>

          <!-- YÖNETİCİ GİRİŞİ -->
          <button id="adminHeaderTrigger" onclick="openAdminModal()" class="text-xs bg-purple-600/10 hover:bg-purple-600 border border-purple-500/30 text-purple-400 hover:text-white px-3 py-2 rounded-xl transition font-semibold">
            <i class="fas fa-user-shield mr-1"></i> Yönetici Girişi
          </button>

          <button id="adminReturnBtn" onclick="document.getElementById('adminPanel').classList.remove('hidden')" class="hidden text-xs bg-pink-600/20 hover:bg-pink-600 border border-pink-500 text-pink-400 hover:text-white px-3 py-2 rounded-xl transition font-bold">
            <i class="fas fa-tools mr-1"></i> Panele Dön
          </button>

          <!-- Durum Bilgileri -->
          <span id="userBadge" class="hidden text-xs font-semibold bg-[#121829] border border-gray-800 px-4 py-2 rounded-full text-purple-400 flex items-center gap-2"></span>
          <button id="logoutBtn" class="hidden text-xs text-red-500 hover:text-red-400 font-bold transition">Çıkış</button>
          
          <!-- Sepet Butonu -->
          <button onclick="toggleCart()" class="relative p-3 rounded-full bg-[#121829] border border-gray-800 hover:border-cyan-400 transition">
            <i class="fas fa-shopping-cart text-lg text-cyan-400"></i>
            <span id="cartCount" class="absolute -top-1 -right-1 w-5 h-5 bg-pink-500 text-white text-[10px] font-bold rounded-full flex items-center justify-center">0</span>
          </button>
        </div>
      </div>
    </header>

    <!-- ================= KAHRAMAN BÖLÜMÜ ================= -->
    <main class="relative pt-40 pb-20 flex flex-col items-center justify-center text-center px-4 overflow-hidden min-h-screen">
      <div class="absolute top-1/4 left-1/4 w-96 h-96 bg-purple-600/10 rounded-full filter blur-[120px]"></div>
      <div class="absolute bottom-1/4 right-1/4 w-96 h-96 bg-cyan-500/10 rounded-full filter blur-[120px]"></div>

      <div class="transition-all duration-1000" id="heroContent">
        <span class="text-cyan-400 text-sm font-bold tracking-widest uppercase mb-3 block">Sınırları Zorla</span>
        <h2 class="text-5xl md:text-8xl font-black tracking-tight mb-6 leading-none uppercase">
          TARZINI <br/>
          <span class="bg-gradient-to-r from-purple-400 to-pink-500 bg-clip-text text-transparent">YENİDEN TANIMLA</span>
        </h2>
        <p class="text-gray-400 max-w-xl text-base md:text-lg mb-8 mx-auto">
          Koleksiyonu özgürce keşfet, sepetini doldur ve tek tıkla WhatsApp üzerinden siparişini tamamla! 🚀
        </p>
        <a href="#products" class="inline-block px-8 py-4 rounded-full bg-cyan-400 text-[#070a13] font-bold text-lg hover:bg-cyan-300 hover:scale-105 transition shadow-lg shadow-cyan-500/20">
          Koleksiyonu Keşfet 🔥
        </a>
      </div>
    </main>

    <!-- ================= VİTRİN BÖLÜMÜ ================= -->
    <section id="products" class="max-w-7xl mx-auto px-6 py-20">
      <div class="mb-12">
        <h3 class="text-3xl font-black tracking-wider text-purple-400">Vitrin</h3>
        <p class="text-gray-500 text-sm">Gerçek zamanlı modeX koleksiyonu</p>
      </div>
      <div class="grid grid-cols-1 md:grid-cols-3 gap-8" id="productGrid"></div>
    </section>

    <!-- ================= SEPET PANELİ ================= -->
    <div id="cartPanel" class="fixed top-0 right-0 h-full w-full md:w-96 glass z-[1000] translate-x-full transition-transform duration-500 flex flex-col">
      <div class="p-6 bg-black/30 border-b border-gray-800 flex justify-between items-center">
        <h3 class="text-xl font-bold text-cyan-400">Sepetim</h3>
        <button onclick="toggleCart()" class="text-gray-400 hover:text-white text-2xl">&times;</button>
      </div>
      <div id="cartList" class="flex-1 p-6 overflow-y-auto space-y-4"></div>
      <div class="p-6 border-t border-gray-800 bg-[#070a13]">
        <div class="flex justify-between items-center mb-6">
          <span class="text-gray-400 font-bold">Toplam Tutar:</span>
          <span id="cartTotal" class="text-2xl font-black text-cyan-400">0 TL</span>
        </div>
        <button onclick="processOrderCheckout()" class="w-full py-4 bg-emerald-500 hover:bg-emerald-400 text-white font-extrabold rounded-2xl transition flex items-center justify-center gap-3 shadow-lg shadow-emerald-500/20">
          WhatsApp İle Siparişi Gönder <i class="fab fa-whatsapp text-xl"></i>
        </button>
      </div>
    </div>

    <!-- ================= DETAYLI ÜRÜN MODALI ================= -->
    <div id="productDetailModal" class="fixed inset-0 bg-black/90 backdrop-blur-md z-[999] hidden flex items-center justify-center p-4">
      <div class="glass w-full max-w-4xl rounded-3xl overflow-hidden grid grid-cols-1 md:grid-cols-2">
        <div class="p-6 flex flex-col justify-between bg-black/25">
          <div class="relative aspect-square rounded-2xl overflow-hidden bg-gray-900 flex items-center justify-center">
            <img id="detailMainImg" src="" class="w-full h-full object-cover">
          </div>
          <div id="detailThumbnails" class="flex gap-2 mt-4 overflow-x-auto py-2"></div>
        </div>
        <div class="p-8 flex flex-col justify-between">
          <div>
            <div class="flex justify-between items-start mb-6">
              <h4 id="detailTitle" class="text-3xl font-black tracking-tight">Ürün Adı</h4>
              <button onclick="closeProductDetail()" class="text-gray-400 hover:text-white text-3xl">&times;</button>
            </div>
            
            <div class="mb-4 bg-[#121829]/60 border border-purple-500/20 rounded-2xl p-4">
              <div class="flex justify-between items-center mb-2">
                <span class="text-xs font-bold text-purple-400 uppercase tracking-wider"><i class="fas fa-magic mr-1"></i> modeX AI Tanıtımı</span>
                <span id="aiStatusBadge" class="text-[10px] text-gray-500">Hazır</span>
              </div>
              <p id="detailDesc" class="text-gray-300 text-sm leading-relaxed whitespace-pre-line"></p>
            </div>

            <p id="detailStockStatus" class="text-sm font-semibold mb-6"></p>
            <div id="detailLinkBox" class="bg-[#121829] p-3 rounded-xl border border-gray-800 mb-6 flex justify-between items-center text-xs">
              <span class="text-cyan-400 truncate mr-2" id="detailShareLink">Link</span>
              <button onclick="copyProductLink()" class="px-3 py-1 bg-purple-600 rounded-lg hover:bg-purple-500 font-bold">Kopyala</button>
            </div>
          </div>
          <div class="flex items-center justify-between gap-4 mt-6">
            <span id="detailPrice" class="text-3xl font-black text-cyan-400">0 TL</span>
            <div class="flex gap-2">
              <button id="detailAddBtn" class="px-5 py-3 bg-[#121829] hover:bg-purple-600/20 border border-purple-500/30 text-white font-bold rounded-2xl transition text-sm">
                Sepete Ekle 🛒
              </button>
              <button id="detailDirectBuyBtn" class="px-5 py-3 bg-emerald-500 hover:bg-emerald-400 text-white font-extrabold rounded-2xl transition text-sm flex items-center gap-1">
                Hemen Al <i class="fab fa-whatsapp"></i>
              </button>
            </div>
          </div>
        </div>
      </div>
    </div>

    <!-- ================= AI SOHBET BOTU ================= -->
    <div id="aiChatWrapper" class="fixed bottom-6 right-6 z-[999] flex flex-col items-end">
      <div id="aiChatBox" class="glass w-80 h-96 rounded-2xl hidden flex-col overflow-hidden shadow-2xl border border-purple-500/30 mb-3">
        <div class="bg-gradient-to-r from-purple-600 to-cyan-600 p-4 flex justify-between items-center">
          <div class="flex items-center gap-2">
            <div class="w-2.5 h-2.5 bg-emerald-400 rounded-full animate-pulse"></div>
            <span class="font-bold text-sm tracking-wider">modeX AI Asistan</span>
          </div>
          <button onclick="toggleAiChat()" class="text-white hover:text-gray-200 text-xl">&times;</button>
        </div>
        <div id="aiChatMessages" class="flex-1 p-4 overflow-y-auto space-y-3 text-xs">
          <div class="bg-purple-600/20 border border-purple-500/20 p-3 rounded-xl rounded-tl-none text-gray-200 max-w-[85%]">
            Selam! Ben modeX tarz asistanı. Sokak modası, ürünlerimiz veya siparişler hakkında bana dilediğini sorabilirsin! 🔥 Ne aramıştın?
          </div>
        </div>
        <div class="p-3 border-t border-gray-800 bg-[#070a13] flex gap-2">
          <input type="text" id="aiChatInput" placeholder="Mesajını yaz..." class="flex-1 bg-[#121829] border border-gray-800 rounded-xl px-3 py-2 text-xs text-white focus:outline-none focus:border-cyan-400" onkeypress="if(event.key==='Enter') sendAiMessage()">
          <button onclick="sendAiMessage()" class="p-2 bg-cyan-500 hover:bg-cyan-400 text-black rounded-xl transition">
            <i class="fas fa-paper-plane text-xs"></i>
          </button>
        </div>
      </div>
      <button onclick="toggleAiChat()" class="w-14 h-14 bg-gradient-to-r from-purple-600 to-pink-600 rounded-full flex items-center justify-center shadow-lg shadow-purple-500/40 hover:scale-105 transition duration-300 group">
        <i class="fas fa-comment-dots text-white text-xl group-hover:rotate-12 transition"></i>
      </button>
    </div>

    <footer class="text-center py-12 border-t border-gray-900 mt-20 text-gray-600 text-sm">
      <p>&copy; 2026 modeX. Tüm Hakları Saklıdır. 🔥</p>
    </footer>
  </div>

  <!-- ================= KONTROL PANELİ (YÖNETİCİ EKRANI) ================= -->
  <div id="adminPanel" class="fixed inset-0 bg-[#070a13] z-[9999] hidden overflow-y-auto p-6">
    <div class="max-w-6xl mx-auto mt-20">
      <div class="flex justify-between items-center mb-12">
        <h2 class="text-3xl font-extrabold text-purple-400">Yönetici Kontrol Paneli</h2>
        <div class="flex items-center gap-3">
          <button onclick="document.getElementById('adminPanel').classList.add('hidden')" class="px-4 py-2 bg-gray-800 hover:bg-gray-700 rounded-xl font-bold transition">Siteyi Gör</button>
          <button id="adminLogoutBtn" class="px-4 py-2 bg-red-600 hover:bg-red-500 rounded-xl font-bold transition">Çıkış Yap</button>
        </div>
      </div>

      <div class="grid grid-cols-1 lg:grid-cols-3 gap-8">
        <div class="glass p-8 rounded-3xl space-y-6 lg:col-span-1 h-fit">
          <h3 class="text-xl font-bold text-cyan-400">Yeni Ürün Ekle</h3>
          <div>
            <label class="block text-sm mb-2">Ürün Adı</label>
            <input type="text" id="newProdName" class="w-full bg-[#121829] border border-gray-800 rounded-xl px-4 py-3 text-white focus:outline-none">
          </div>
          <div>
            <label class="block text-sm mb-2">Ürün Fiyatı</label>
            <input type="number" id="newProdPrice" class="w-full bg-[#121829] border border-gray-800 rounded-xl px-4 py-3 text-white focus:outline-none">
          </div>
          <div>
            <label class="block text-sm mb-2">Stok Adedi</label>
            <input type="number" id="newProdStock" class="w-full bg-[#121829] border border-gray-800 rounded-xl px-4 py-3 text-white focus:outline-none" value="10">
          </div>
          <div>
            <label class="block text-sm mb-2">Ürün Açıklaması</label>
            <textarea id="newProdDesc" rows="3" class="w-full bg-[#121829] border border-gray-800 rounded-xl p-4 text-white focus:outline-none" placeholder="Ürün açıklaması yazın..."></textarea>
          </div>
          <div>
            <label class="block text-sm mb-2">Ürün Görselleri</label>
            <input type="file" id="newProdPics" multiple class="w-full text-sm text-gray-400 file:bg-purple-600 file:text-white file:py-2 file:px-4 file:rounded-full file:border-0 cursor-pointer">
          </div>
          <button id="uploadBtn" class="w-full py-4 bg-cyan-400 text-black font-extrabold rounded-2xl hover:bg-cyan-300 transition">
            Yayınla 🚀
          </button>
        </div>

        <div class="glass p-8 rounded-3xl lg:col-span-2">
          <h3 class="text-xl font-bold text-cyan-400 mb-6">Mevcut Ürünleri Yönet</h3>
          <div id="adminProductList" class="space-y-4"></div>
        </div>
      </div>

      <div class="glass p-8 rounded-3xl mt-8">
        <h3 class="text-xl font-bold text-cyan-400 mb-6">Sistemdeki Aktif Üyeler</h3>
        <ul id="userList" class="space-y-4"></ul>
      </div>
    </div>
  </div>

  <script>
    function toggleAiChat() {
      const box = document.getElementById('aiChatBox');
      box.classList.toggle('hidden'); box.classList.toggle('flex');
    }

    function sendAiMessage() {
      const input = document.getElementById('aiChatInput'); const container = document.getElementById('aiChatMessages');
      const text = input.value.trim(); if (!text) return;

      container.insertAdjacentHTML('beforeend', `<div class="bg-[#121829] border border-gray-800 p-3 rounded-xl rounded-tl-none text-gray-300 max-w-[85%] self-end ml-auto">${text}</div>`);
      input.value = ""; container.scrollTop = container.scrollHeight;

      setTimeout(() => {
        let response = "modeX tarz asistanı aktif! Harika parçalarımız vitrinde listeleniyor, sepetine ekleyip WhatsApp'tan jet hızıyla sipariş geçebilirsin. ⚡";
        const cleanText = text.toLowerCase();
        if (cleanText.includes("selam") || cleanText.includes("merhaba")) response = "Selam! modeX dünyasına hoş geldin! Bugün dolabına hangi tarz parçayı eklemek istersin? 🕶️";
        else if (cleanText.includes("kargo")) response = "Siparişlerin onaydan hemen sonra 1-3 iş günü içerisinde kargoya jet hızıyla teslim edilir! 📦";

        container.insertAdjacentHTML('beforeend', `<div class="bg-purple-600/20 border border-purple-500/20 p-3 rounded-xl rounded-tl-none text-gray-200 max-w-[85%]">${response}</div>`);
        container.scrollTop = container.scrollHeight;
      }, 500);
    }
  </script>

  <script>
    const whatsappNum = "905519283542";
    let cart = [];
    let pendingAction = null;
    let currentUserSession = null;
    let isAdminSession = false;
    let loadedProductsMap = {}; // Global ürün verilerini detaylar için saklama alanı

    // HER DURUMDA AÇILIŞTA EKRANDA YER ALACAK ÖRNEK ÜRÜNLER (FALLBACK)
    const fallbackProducts = [
      { id: "sample1", name: "Oversize Cyberpunk Hoodie", price: 1250, stock: 15, description: "Fütüristik neon detaylar ve ultra kalın pamuk kumaş yapısıyla modeX sokak stilinin en iddialı parçası! 🌌", images: ["https://images.unsplash.com/photo-1556821840-3a63f95609a7?auto=format&fit=crop&w=600&q=80"] },
      { id: "sample2", name: "Gothic Cargo Pantolon", price: 1400, stock: 8, description: "Geniş cepler, metal zincir aksesuarları ve rahat kesimi ile hem konforlu hem de fazlasıyla asi. ⛓️", images: ["https://images.unsplash.com/photo-1542272604-787c3835535d?auto=format&fit=crop&w=600&q=80"] },
      { id: "sample3", name: "Retro-Future Grafik Tişört", price: 650, stock: 25, description: "Yıkanmış vintage kumaş üzerine yüksek kaliteli dijital modeX baskı. Tarzını hemen konuştur! ⚡", images: ["https://images.unsplash.com/photo-1521572267360-ee0c2909d518?auto=format&fit=crop&w=600&q=80"] }
    ];

    // AÇILIŞ EKRANI BİTTİKTEN SONRA SAYFANIN KİLİDİNİ KALDIRIR VE VİTRİNİ DOLDURUR
    window.addEventListener('load', () => {
      // Firebase'den bağımsız olarak ilk aşamada örnek vitrini hemen dolduruyoruz
      renderFallbackUI();

      setTimeout(() => {
        const splash = document.getElementById('splashScreen');
        if(splash) {
          splash.classList.add('opacity-0', 'pointer-events-none');
          setTimeout(() => splash.style.display = 'none', 1000);
        }
      }, 1500);
    });

    function renderFallbackUI() {
      const grid = document.getElementById('productGrid');
      const adminList = document.getElementById('adminProductList');
      
      // Eğer Firebase henüz yükleme yapmadıysa vitrin boş kalmasın diye dolduruyoruz
      if (grid && grid.children.length === 0) {
        grid.innerHTML = "";
        if(adminList) adminList.innerHTML = "";
        
        fallbackProducts.forEach(p => {
          loadedProductsMap[p.id] = p; // Global haritaya ekle
          renderCard(p.id, p);
          renderAdminRow(p.id, p);
        });
      }
    }

    function openAuthModal(actionType, data = null) {
      pendingAction = { type: actionType, data: data };
      document.getElementById('authModal').classList.remove('hidden');
    }
    function closeAuthModal() { document.getElementById('authModal').classList.add('hidden'); pendingAction = null; }
    function openAdminModal() { document.getElementById('adminModal').classList.remove('hidden'); }
    function closeAdminModal() { document.getElementById('adminModal').classList.add('hidden'); }
    function toggleCart() { document.getElementById('cartPanel').classList.toggle('translate-x-full'); }

    function handleDirectBuy(name, price, id) {
      if (!currentUserSession) openAuthModal('directBuy', { name, price, id });
      else triggerWhatsAppMessage(name, price, id);
    }

    function triggerWhatsAppMessage(name, price, id) {
      const customer = currentUserSession ? currentUserSession.displayName : "Müşteri";
      const message = `Selam, Ben ${customer}! modeX sitenden şu ürünü almak istiyorum! 🔥\n\nÜrün: ${name}\nFiyat: ${price}\n📍 Ürün Detayı: ${window.location.origin}${window.location.pathname}#product-${id}`;
      window.open(`https://wa.me/${whatsappNum}?text=${encodeURIComponent(message)}`, "_blank");
    }

    function processOrderCheckout() {
      if (cart.length === 0) return alert("Sepetiniz boş!");
      if (!currentUserSession) openAuthModal('cartCheckout');
      else triggerCartWhatsAppMessage();
    }

    function triggerCartWhatsAppMessage() {
      const customer = currentUserSession ? currentUserSession.displayName : "Müşteri";
      let message = `Selam, Ben ${customer}! modeX siparişim var: 🔥\n\n`;
      let total = 0;
      cart.forEach((item, index) => {
        const itemTotal = item.price * item.quantity; total += itemTotal;
        message += `${index + 1}) ${item.name} (${item.quantity} Adet) - ${itemTotal.toLocaleString('tr-TR')} TL\n📍 Link: ${window.location.origin}${window.location.pathname}#product-${item.id}\n\n`;
      });
      message += `------------------------------\n💰 Toplam Tutar: ${total.toLocaleString('tr-TR')} TL`;
      window.open(`https://wa.me/${whatsappNum}?text=${encodeURIComponent(message)}`, "_blank");
    }

    function renderCard(id, p) {
      const grid = document.getElementById('productGrid'); if(!grid) return;
      const mainImage = p.images && p.images.length > 0 ? p.images[0] : '';
      grid.insertAdjacentHTML('beforeend', `
        <div class="glass rounded-3xl overflow-hidden group hover:border-purple-500/50 transition duration-300 relative">
          ${p.stock <= 0 ? '<span class="absolute top-4 right-4 bg-red-600 text-white text-xs px-3 py-1 rounded-full font-bold z-10">Tükendi</span>' : ''}
          <div onclick="window.location.hash='product-${id}'" class="relative overflow-hidden aspect-square cursor-pointer"><img src="${mainImage}" class="w-full h-full object-cover group-hover:scale-110 transition duration-500"></div>
          <div class="p-6">
            <h4 onclick="window.location.hash='product-${id}'" class="text-xl font-bold mb-2 cursor-pointer hover:text-cyan-400 transition">${p.name}</h4>
            <p class="text-gray-400 text-sm mb-4 line-clamp-2">${p.description}</p>
            <div class="flex items-center justify-between gap-2 mt-4">
              <button onclick="addToCart('${id}', '${p.name}', ${p.price}, '${mainImage}', ${p.stock})" ${p.stock <= 0 ? 'disabled class="flex-1 py-2.5 bg-gray-800 text-gray-500 rounded-xl font-bold text-xs cursor-not-allowed"' : 'class="flex-1 py-2.5 bg-[#121829] hover:bg-purple-600/20 border border-purple-500/30 text-white rounded-xl font-bold text-xs transition"'} >Sepete Ekle 🛒</button>
              <button onclick="handleDirectBuy('${p.name}', '${p.price.toLocaleString('tr-TR')} TL', '${id}')" class="flex-1 py-2.5 bg-emerald-500 hover:bg-emerald-400 text-white rounded-xl font-bold text-xs transition flex items-center justify-center gap-1">Hemen Al <i class="fab fa-whatsapp"></i></button>
            </div>
          </div>
        </div>`);
    }

    function renderAdminRow(id, p) {
      const adminList = document.getElementById('adminProductList'); if(!adminList) return;
      const mainImage = p.images && p.images.length > 0 ? p.images[0] : '';
      adminList.insertAdjacentHTML('beforeend', `
        <div class="flex flex-col sm:flex-row items-start sm:items-center justify-between gap-4 bg-[#121829] p-4 rounded-2xl border border-gray-800">
          <div class="flex items-center gap-4">
            <img src="${mainImage}" class="w-12 h-12 object-cover rounded-xl border border-gray-700">
            <div><h5 class="font-bold text-sm text-gray-200">${p.name}</h5><p class="text-xs text-purple-400">${p.price.toLocaleString('tr-TR')} TL</p></div>
          </div>
          <div class="flex items-center gap-3 w-full sm:w-auto justify-between sm:justify-end">
            <div class="flex items-center border border-gray-700 rounded-xl bg-[#070a13] overflow-hidden">
              <button onclick="updateStockClick('${id}', -1)" class="px-3 py-1.5 hover:bg-gray-800 text-gray-400 font-bold">-</button>
              <span id="admin-stock-${id}" class="px-3 text-sm font-mono text-cyan-400 min-w-[30px] text-center">${p.stock}</span>
              <button onclick="updateStockClick('${id}', 1)" class="px-3 py-1.5 hover:bg-gray-800 text-gray-400 font-bold">+</button>
            </div>
            <button onclick="deleteProductClick('${id}')" class="p-2.5 bg-red-600/10 hover:bg-red-600 border border-red-500/20 text-red-500 hover:text-white rounded-xl transition text-xs flex items-center gap-1 font-semibold"><i class="fas fa-trash"></i> Sil</button>
          </div>
        </div>`);
    }
  </script>

  <!-- FIREBASE VE KONTROL YAPISI -->
  <script type="module">
    import { initializeApp } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-app.js";
    import { getAuth, signInWithPopup, GoogleAuthProvider, signOut, onAuthStateChanged } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-auth.js";
    import { getFirestore, collection, addDoc, setDoc, getDocs, doc, getDoc, deleteDoc, updateDoc } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-firestore.js";
    import { getStorage, ref, uploadBytes, getDownloadURL } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-storage.js";

    const firebaseConfig = {
      apiKey: "BURAYA_KENDI_API_KEY_YAZ",
      authDomain: "modex-ebfc8.firebaseapp.com",
      projectId: "modex-ebfc8",
      storageBucket: "modex-ebfc8.firebasestorage.app",
      messagingSenderId: "342759207583",
      appId: "BURAYA_KENDI_APP_ID_YAZ"
    };

    const app = initializeApp(firebaseConfig);
    const auth = getAuth(app);
    const db = getFirestore(app);
    const storage = getStorage(app);
    const provider = new GoogleAuthProvider();

    const userBadge = document.getElementById('userBadge');
    const logoutBtn = document.getElementById('logoutBtn');
    const adminHeaderTrigger = document.getElementById('adminHeaderTrigger');
    const customerGoogleTrigger = document.getElementById('customerGoogleTrigger');
    const adminReturnBtn = document.getElementById('adminReturnBtn');
    const adminPanel = document.getElementById('adminPanel');

    onAuthStateChanged(auth, async (user) => {
      if (user && !isAdminSession) {
        currentUserSession = user;
        customerGoogleTrigger.classList.add('hidden');
        userBadge.innerHTML = `<i class="fas fa-user text-cyan-400"></i> ${user.displayName || user.email}`;
        userBadge.classList.remove('hidden');
        logoutBtn.classList.remove('hidden');

        try {
          await setDoc(doc(db, "users", user.uid), { name: user.displayName || "Müşteri", email: user.email, lastLogin: new Date() });
        } catch(e){}

        if (pendingAction) {
          if (pendingAction.type === 'directBuy') triggerWhatsAppMessage(pendingAction.data.name, pendingAction.data.price, pendingAction.data.id);
          else if (pendingAction.type === 'cartCheckout') triggerCartWhatsAppMessage();
          closeAuthModal();
        }
      }
      loadProductsAndUsers();
    });

    document.getElementById('authGoogleBtn').addEventListener('click', async () => {
      try { await signInWithPopup(auth, provider); } catch(e){}
    });

    document.getElementById('adminLoginSubmitBtn').addEventListener('click', () => {
      const u = document.getElementById('adminEmailInput').value.trim();
      const p = document.getElementById('adminPasswordInput').value.trim();

      if(!u || !p) return alert("Lütfen giriş alanlarını doldurun.");

      if (u.length === 4 && p.length === 7 && 
          u.charCodeAt(0) === 116 && u.charCodeAt(3) === 97 &&
          p.charCodeAt(0) === 116 && p.charCodeAt(4) === 49 && p.charCodeAt(6) === 51) {
        
        isAdminSession = true;
        currentUserSession = { displayName: "Yönetici", email: "admin@modex.com" };
        adminHeaderTrigger.classList.add('hidden');
        customerGoogleTrigger.classList.add('hidden');
        adminReturnBtn.classList.remove('hidden');
        adminPanel.classList.remove('hidden');
        closeAdminModal();
        loadProductsAndUsers();
        alert("Giriş Başarılı! Kontrol Paneline Yönlendiriliyorsunuz.");
      } else {
        alert("Girdiğiniz yönetici bilgileri sistem kayıtlarıyla eşleşmedi.");
      }
    });

    const appLogout = async () => {
      isAdminSession = false; currentUserSession = null;
      try { await signOut(auth); } catch (e) {}
      location.reload();
    };
    logoutBtn.addEventListener('click', appLogout);
    document.getElementById('adminLogoutBtn').addEventListener('click', appLogout);

    async function seedSampleProductsIfEmpty() {
      try {
        const querySnapshot = await getDocs(collection(db, "products"));
        if (querySnapshot.size === 0) {
          for (const prod of fallbackProducts) { 
            // id'siz haliyle veritabanına ekle
            const { id, ...firebaseProd } = prod;
            await addDoc(collection(db, "products"), { ...firebaseProd, createdAt: new Date() }); 
          }
        }
      } catch (e) {}
    }

    document.getElementById('uploadBtn').addEventListener('click', async () => {
      const name = document.getElementById('newProdName').value.trim();
      const price = document.getElementById('newProdPrice').value.trim();
      const stock = document.getElementById('newProdStock').value.trim();
      let desc = document.getElementById('newProdDesc').value.trim();
      const fileInput = document.getElementById('newProdPics');
      const uploadBtn = document.getElementById('uploadBtn');

      if (!name || !price) return alert("Gerekli alanları doldurun.");
      uploadBtn.innerText = "Yayınlanıyor... ⏳"; uploadBtn.disabled = true;

      try {
        const imageUrls = [];
        for (let i = 0; i < fileInput.files.length; i++) {
          const file = fileInput.files[i];
          const storageRef = ref(storage, `products/${Date.now()}_${file.name}`);
          const snapshot = await uploadBytes(storageRef, file);
          const downloadUrl = await getDownloadURL(snapshot.ref);
          imageUrls.push(downloadUrl);
        }
        if (imageUrls.length === 0) imageUrls.push("https://images.unsplash.com/photo-1556821840-3a63f95609a7?auto=format&fit=crop&w=600&q=80");

        const finalDesc = desc || `Bu harika ${name} ürünü modeX mağazasında yerini aldı.`;
        await addDoc(collection(db, "products"), { name, price: parseFloat(price), stock: stock ? parseInt(stock) : 10, description: finalDesc, images: imageUrls, createdAt: new Date() });
        alert("Ürün başarıyla yayına alındı! 🎉"); location.reload();
      } catch (error) { alert("Hata: " + error.message); uploadBtn.disabled = false; uploadBtn.innerText = "Yayınla 🚀"; }
    });

    async function loadProductsAndUsers() {
      await seedSampleProductsIfEmpty();
      const userListEl = document.getElementById('userList');
      if (userListEl) {
        userListEl.innerHTML = "";
        try {
          const uSnap = await getDocs(collection(db, "users"));
          uSnap.forEach(uDoc => {
            const uData = uDoc.data();
            userListEl.insertAdjacentHTML('beforeend', `<li class="flex justify-between items-center bg-[#121829] p-3 rounded-xl border border-gray-800 text-sm"><span class="font-semibold">${uData.name} (${uData.email})</span><span class="text-xs text-emerald-400 font-mono"><i class="fas fa-check-circle"></i> Google Girişli</span></li>`);
          });
        } catch (e) {}
      }

      try {
        const querySnapshot = await getDocs(collection(db, "products"));
        if (querySnapshot.size > 0) {
          const grid = document.getElementById('productGrid'); const adminList = document.getElementById('adminProductList');
          if(grid) grid.innerHTML = ""; if(adminList) adminList.innerHTML = "";
          loadedProductsMap = {}; // Eşlemeyi temizle ve Firebase verileriyle doldur

          querySnapshot.forEach((doc) => {
            const data = doc.data();
            const productWithId = { id: doc.id, ...data };
            loadedProductsMap[doc.id] = productWithId;
            renderCard(doc.id, data);
            renderAdminRow(doc.id, data);
          });
        }
      } catch (e) {
        // Hata durumunda zaten local fallback tetiklendiği için sessiz kalıyoruz.
      }
    }

    window.updateStockClick = async (id, amount) => {
      const stockElement = document.getElementById(`admin-stock-${id}`);
      let newStock = parseInt(stockElement.innerText) + amount; if (newStock < 0) newStock = 0;
      try { await updateDoc(doc(db, "products", id), { stock: newStock }); stockElement.innerText = newStock; } catch (e) {}
    };

    window.deleteProductClick = async (id) => {
      if (!confirm("Bu ürünü silmek istediğinize emin misiniz?")) return;
      try { await deleteDoc(doc(db, "products", id)); location.reload(); } catch (e) {}
    };

    function checkUrlHash() {
      const hash = window.location.hash;
      if (hash.startsWith('#product-')) {
        const prodId = hash.replace('#product-', '');
        const targetProduct = loadedProductsMap[prodId];
        if (targetProduct) {
          showProductDetail(prodId, targetProduct);
        }
      } else { const m = document.getElementById('productDetailModal'); if(m) m.classList.add('hidden'); }
    }
    window.addEventListener('hashchange', checkUrlHash);
    // İlk açılışta da tetiklenmesi için:
    setTimeout(checkUrlHash, 2000);
  </script>

  <script>
    function addToCart(id, name, price, img, maxStock) {
      const existing = cart.find(item => item.id === id);
      if (existing) {
        if (existing.quantity >= maxStock) return alert(`Stokta en fazla ${maxStock} adet mevcut.`);
        existing.quantity += 1;
      } else {
        if (maxStock <= 0) return alert("Bu ürün tükenmiştir!");
        cart.push({ id, name, price, img, quantity: 1, maxStock: maxStock });
      }
      updateCartUI();
    }

    function updateCartUI() {
      const list = document.getElementById('cartList'); const countBadge = document.getElementById('cartCount'); const totalText = document.getElementById('cartTotal');
      if(!list) return; list.innerHTML = ""; let total = 0; let count = 0;
      cart.forEach((item) => {
        total += item.price * item.quantity; count += item.quantity;
        list.insertAdjacentHTML('beforeend', `
          <div class="flex items-center gap-4 bg-[#121829] p-3 rounded-2xl border border-gray-800">
            <img src="${item.img}" class="w-16 h-16 object-cover rounded-xl">
            <div class="flex-1"><h5 class="font-bold text-sm">${item.name}</h5><p class="text-xs text-cyan-400 mt-1">${item.price.toLocaleString('tr-TR')} TL x ${item.quantity}</p></div>
            <div class="flex flex-col gap-1">
              <button onclick="changeQuantity('${item.id}', 1)" class="text-gray-400 hover:text-white px-2 py-0.5 bg-[#1b233a] rounded">+</button>
              <button onclick="changeQuantity('${item.id}', -1)" class="text-gray-400 hover:text-white px-2 py-0.5 bg-[#1b233a] rounded">-</button>
            </div>
          </div>`);
      });
      if(countBadge) countBadge.innerText = count; if(totalText) totalText.innerText = `${total.toLocaleString('tr-TR')} TL`;
    }

    function changeQuantity(id, amount) {
      const item = cart.find(i => i.id === id);
      if (item) {
        if (amount > 0 && item.quantity >= item.maxStock) return alert(`Maksimum stok sınırı.`);
        item.quantity += amount; if (item.quantity <= 0) cart = cart.filter(i => i.id !== id);
      }
      updateCartUI();
    }

    function showProductDetail(id, product) {
      document.getElementById('detailTitle').innerText = product.name; document.getElementById('detailDesc').innerText = product.description;
      document.getElementById('detailPrice').innerText = `${product.price.toLocaleString('tr-TR')} TL`;
      const stockStatus = document.getElementById('detailStockStatus');
      
      if (product.stock <= 0) {
        stockStatus.innerText = "🚨 BU ÜRÜN TÜKENDİ"; stockStatus.className = "text-sm font-semibold mb-6 text-red-500";
        document.getElementById('detailAddBtn').disabled = true; document.getElementById('detailAddBtn').className = "px-5 py-3 bg-gray-800 text-gray-500 font-bold rounded-2xl cursor-not-allowed text-sm";
      } else {
        stockStatus.innerText = `⚡ Stok: ${product.stock} Adet`; stockStatus.className = "text-sm font-semibold mb-6 text-cyan-400";
        document.getElementById('detailAddBtn').disabled = false; document.getElementById('detailAddBtn').className = "px-5 py-3 bg-[#121829] hover:bg-purple-600/20 border border-purple-500/30 text-white font-bold rounded-2xl transition text-sm";
      }

      document.getElementById('detailShareLink').innerText = `${window.location.origin}${window.location.pathname}#product-${id}`;
      document.getElementById('detailAddBtn').onclick = () => { addToCart(id, product.name, product.price, product.images[0] || '', product.stock); closeProductDetail(); };
      document.getElementById('detailDirectBuyBtn').onclick = () => { handleDirectBuy(product.name, `${product.price.toLocaleString('tr-TR')} TL`, id); };
      document.getElementById('detailMainImg').src = product.images[0] || '';

      const thumbsContainer = document.getElementById('detailThumbnails'); thumbsContainer.innerHTML = "";
      product.images.forEach((url) => {
        const imgBtn = document.createElement('button'); imgBtn.className = "w-16 h-16 rounded-xl overflow-hidden border border-gray-800 shrink-0";
        imgBtn.innerHTML = `<img src="${url}" class="w-full h-full object-cover">`; imgBtn.onclick = () => { document.getElementById('detailMainImg').src = url; };
        thumbsContainer.appendChild(imgBtn);
      });
      document.getElementById('productDetailModal').classList.remove('hidden');
    }

    function closeProductDetail() { window.location.hash = ""; }
    function copyProductLink() { navigator.clipboard.writeText(document.getElementById('detailShareLink').innerText).then(() => alert("Kopyalandı! 🚀")); }
  </script>
</body>
</html>
