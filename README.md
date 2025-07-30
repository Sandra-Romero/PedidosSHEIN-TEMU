<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8" />
  <link rel="icon" href="https://i.pinimg.com/1200x/76/97/ea/7697ea85781035fdc9a5b8ff03237175.jpg" type="image/png">
  <title>PEDIDOS SHEIN/TEMU</title>
  <style>
    body {
      font-family: sans-serif;
      background: #f4f4f4;
      padding: 20px;
    }
    h1 {
      text-align: center;
      color: #ff4081;
    }
    .logo-container {
      display: flex;
      justify-content: center;
      margin-bottom: 50px;
    }
    .imagenlogo {
      background: white;
      border-radius: 8px;
      box-shadow: 0 2px 6px rgba(0,0,0,0.1);
      padding: 10px;
      width: 200px;
      display: block;
    }
    .product-list {
      display: flex;
      flex-wrap: wrap;
      justify-content: center;
      gap: 20px;
    }
    .product {
      background: white;
      border-radius: 8px;
      box-shadow: 0 2px 6px rgba(0,0,0,0.1);
      padding: 10px;
      width: 200px;
      text-align: center;
    }
    .product img {
      width: 100%;
      height: 200px;
      object-fit: cover;
      border-radius: 6px;
    }
    .product-name {
      font-weight: bold;
      margin: 8px 0 4px;
    }
    .product-price {
      color: #ff4081;
      font-size: 1.1em;
    }
    .btn-whatsapp {
      margin-top: 8px;
      background: #25d366;
      color: white;
      padding: 6px 12px;
      border: none;
      border-radius: 4px;
      cursor: pointer;
      font-size: 0.9em;
    }
    .loading-message, .error-message {
      text-align: center;
      color: #555;
      margin-top: 50px;
      font-size: 1.2em;
    }
    .error-message {
      color: #d32f2f;
    }
  </style>
</head>
<body>
  <div class="logo-container">
    <div>
       <img class="imagenlogo" src="https://i.pinimg.com/1200x/76/97/ea/7697ea85781035fdc9a5b8ff03237175.jpg" />
    </div>
      <div>
       <img class="imagenlogo" src="https://play-lh.googleusercontent.com/9v08ai07I8aoFLj5M-90nzWPpvyNzOVgA2ZWF9avdW7oS8L9YqF9trVI44SUn2qGTA0=w240-h480-rw" />
    </div>
   
  </div>

  <div class="product-list" id="product-list">
    <p class="loading-message">Cargando Productos SHEIN/TEMU...</p>
  </div>

  <script>
    const API_URL = "https://script.google.com/macros/s/AKfycby-tz2dAP5yJdyZy4IfddBvtGyefc5RKfTxUwne-sU482iE7NxwgKo4rKO2gJTC0ys/exec";
    const phoneNumber = "50375606041"; // Tu número de WhatsApp

    fetch(API_URL)
      .then(res => res.json())
      .then(data => {
        const list = document.getElementById("product-list");
        list.innerHTML = '';

        data.forEach(item => {
          const message = encodeURIComponent(
            `Hola, quiero pedir este producto:\n${item.Nombre} - $${item.Precio}\n${item.Enlace}`
          );
          const whatsappLink = `https://wa.me/${phoneNumber}?text=${message}`;

          const div = document.createElement("div");
          div.className = "product";
          div.innerHTML = `
            <img src="${item.Imagen}" alt="${item.Nombre}" />
            <div class="product-name">${item.Nombre}</div>
            <div class="product-price">$${item.Precio}</div>
            <button class="btn-whatsapp" onclick="window.open('${whatsappLink}', '_blank')">Pedir por WhatsApp</button>
          `;
          list.appendChild(div);
        });
      })
      .catch(error => {
        document.getElementById("product-list").innerHTML =
          `<p class="error-message">Error al cargar productos: ${error.message}</p>`;
      });
  </script>
</body>
</html>
