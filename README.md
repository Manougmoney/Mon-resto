
<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8" />
  <title>Resto Express</title>
  <style>
    body { font-family: Arial, sans-serif; max-width: 600px; margin: 20px auto; }
    h1, h2 { color: #d35400; }.plat { margin-bottom: 15px; }
    button { background-color: #e67e22; color: white; border: none; padding: 8px 12px; cursor: pointer; }
    #panier { margin-top: 20px; border-top: 1px solid #ccc; padding-top: 15px; }
    input, textarea { width: 100%; padding: 8px; margin: 8px 0; }
  </style>
</head>
<body>
  <h1>Resto Express</h1>
  <h2>Menu</h2>
  
  <div class="plat">
    <strong>Pizza Margherita</strong> - 8€ 
    <button onclick="ajouterAuPanier('Pizza Margherita', 8)">Commander</button>
  </div>
  
  <div class="plat">
    <strong>Burger Classic</strong> - 7€
    <button onclick="ajouterAuPanier('Burger Classic', 7)">Commander</button>
  </div>
  
  <div id="panier">
    <h3>Panier</h3>
    <ul id="liste-panier"></ul>
    <strong>Total: <span id="total">0</span>€</strong>
  </div>
  
  <h2>Passer la commande</h2>
  <form onsubmit="envoyerCommande(event)">
    <input type="text" id="nom" placeholder="Votre nom" required />
    <input type="tel" id="tel" placeholder="Téléphone" required />
    <textarea id="adresse" placeholder="Adresse de livraison" required></textarea>
    <button type="submit">Envoyer la commande</button>
  </form>

  <script>
    let panier = [];
    function ajouterAuPanier(nom, prix) {
      panier.push({nom, prix});
      afficherPanier();
    }
    function afficherPanier() {
      const listePanier = document.getElementById('liste-panier');
      const totalElem = document.getElementById('total');
      listePanier.innerHTML = '';
      let total = 0;
      panier.forEach((item, i) => {
        listePanier.innerHTML += `<li>${item.nom} - ${item.prix}€</li>`;
        total += item.prix;
      });
      totalElem.textContent = total;
    }
    function envoyerCommande(e) {
      e.preventDefault();
      if (panier.length === 0) {
        alert("Ton panier est vide!");
        return;
      }
      const nom = document.getElementById('nom').value;
      const tel = document.getElementById('tel').value;
      const adresse = document.getElementById('adresse').value;
      alert(`Merci ${nom}!\nCommande reçue: ${panier.length} plats\nLivraison: ${adresse}\nNous vous contacterons au ${tel}.`);
      panier = [];
      afficherPanier();
      e.target.reset();
    }
  </script>
</body>
</html>
