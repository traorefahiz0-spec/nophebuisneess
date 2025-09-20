<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Nophe Agro – Boutique en ligne</title>
  <script src="https://cdn.tailwindcss.com"></script>
</head>
<body class="bg-gray-50 text-gray-800">

  <!-- Header -->
  <header class="bg-green-700 text-white p-6 flex justify-between items-center">
    <h1 class="text-2xl font-bold">🛒 Nophe Agro</h1>
    <button id="openCart" class="bg-yellow-400 text-black px-4 py-2 rounded-lg font-bold">Mon Panier (0)</button>
  </header>

  <!-- Produits -->
  <section class="max-w-6xl mx-auto py-12">
    <h2 class="text-3xl font-bold text-center mb-8">Nos Produits</h2>
    <div class="grid md:grid-cols-3 gap-8">
      
      <!-- Produit 1 -->
      <div class="bg-white shadow-lg rounded-xl p-6 text-center">
        <img src="https://picsum.photos/200?chicken" alt="Poulets" class="mx-auto rounded-xl">
        <h3 class="mt-4 font-bold">Poulet de chair</h3>
        <p class="text-gray-600">Élevé naturellement – 5000 XOF</p>
        <button onclick="addToCart('Poulet de chair', 5000)" class="mt-4 bg-green-700 text-white px-4 py-2 rounded-lg">Ajouter</button>
      </div>

      <!-- Produit 2 -->
      <div class="bg-white shadow-lg rounded-xl p-6 text-center">
        <img src="https://picsum.photos/200?tomatoes" alt="Tomates" class="mx-auto rounded-xl">
        <h3 class="mt-4 font-bold">Tomates fraîches</h3>
        <p class="text-gray-600">Savoureuses – 2000 XOF / kg</p>
        <button onclick="addToCart('Tomates fraîches', 2000)" class="mt-4 bg-green-700 text-white px-4 py-2 rounded-lg">Ajouter</button>
      </div>

      <!-- Produit 3 -->
      <div class="bg-white shadow-lg rounded-xl p-6 text-center">
        <img src="https://picsum.photos/200?cassava" alt="Farine de manioc" class="mx-auto rounded-xl">
        <h3 class="mt-4 font-bold">Farine de manioc</h3>
        <p class="text-gray-600">Qualité premium – 3000 XOF / kg</p>
        <button onclick="addToCart('Farine de manioc', 3000)" class="mt-4 bg-green-700 text-white px-4 py-2 rounded-lg">Ajouter</button>
      </div>
    </div>
  </section>

  <!-- Panier (Modal) -->
  <div id="cartModal" class="hidden fixed inset-0 bg-black/50 flex justify-center items-center">
    <div class="bg-white p-6 rounded-lg w-96">
      <h2 class="text-2xl font-bold mb-4">🛍️ Mon Panier</h2>
      <ul id="cartItems" class="mb-4 space-y-2"></ul>
      <p class="font-bold">Total : <span id="cartTotal">0</span> XOF</p>

      <!-- Bouton Orange Money -->
      <form method="POST" action="https://api.orange.com/orange-money-webpay/pay">
        <!-- Remplacer par tes vrais identifiants marchands -->
        <input type="hidden" name="merchant_key" value="TON_MERCHANT_ID">
        <input type="hidden" name="order_id" id="order_id" value="">
        <input type="hidden" name="amount" id="amount" value="">
        <input type="hidden" name="currency" value="XOF">
        <input type="hidden" name="return_url" value="https://ton-site.com/success">
        <input type="hidden" name="cancel_url" value="https://ton-site.com/cancel">
        <button type="submit" class="mt-4 w-full bg-orange-500 text-white px-4 py-2 rounded-lg font-bold">
          Payer avec Orange Money 📲
        </button>
      </form>

      <button onclick="closeCart()" class="mt-2 w-full bg-red-500 text-white px-4 py-2 rounded-lg">Fermer</button>
    </div>
  </div>

  <!-- Footer -->
  <footer class="bg-green-700 text-white text-center p-6 mt-12">
    © 2025 Nophe Agro – Vente en ligne
  </footer>

  <!-- Script Panier -->
  <script>
    let cart = [];
    function addToCart(product, price) {
      cart.push({ product, price });
      document.getElementById('openCart').innerText = `Mon Panier (${cart.length})`;
    }
    function openCart() {
      document.getElementById('cartModal').classList.remove('hidden');
      renderCart();
    }
    function closeCart() {
      document.getElementById('cartModal').classList.add('hidden');
    }
    function renderCart() {
      let cartItems = document.getElementById('cartItems');
      let total = 0;
      cartItems.innerHTML = '';
      cart.forEach((item, index) => {
        total += item.price;
        cartItems.innerHTML += `<li>${item.product} – ${item.price} XOF</li>`;
      });
      document.getElementById('cartTotal').innerText = total;
      document.getElementById('amount').value = total; // Montant envoyé à Orange
      document.getElementById('order_id').value = "CMD-" + Date.now(); // ID unique
    }
    document.getElementById('openCart').addEventListener('click', openCart);
  </script>

</body>
</html>

