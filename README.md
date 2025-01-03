# Hot
Bitcoin
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Crypto Tracker</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      margin: 0;
      padding: 0;
      background-color: #1e1e2f;
      color: white;
      text-align: center;
    }
    header {
      background-color: #2a2a40;
      padding: 1rem;
    }
    header h1 {
      margin: 0;
    }
    .crypto-container {
      display: flex;
      flex-wrap: wrap;
      justify-content: center;
      margin: 2rem auto;
      max-width: 1200px;
    }
    .crypto-card {
      background-color: #32324e;
      border-radius: 8px;
      padding: 1rem;
      margin: 1rem;
      width: 250px;
      box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
    }
    .crypto-card h2 {
      margin-top: 0;
      color: #f4b400;
    }
    footer {
      background-color: #2a2a40;
      padding: 1rem;
      margin-top: 2rem;
    }
  </style>
</head>
<body>
  <header>
    <h1>Crypto Tracker</h1>
    <p>أسعار العملات الرقمية وأهم الإضافات القادمة</p>
  </header>
  <div class="crypto-container" id="crypto-container">
    <p>Loading data...</p>
  </div>
  <footer>
    <p>Developed by Your Name</p>
  </footer>

  <script>
    async function fetchCryptoData() {
      try {
        const response = await fetch('https://api.coingecko.com/api/v3/coins/markets', {
          method: 'GET',
          headers: { 'Content-Type': 'application/json' },
          qs: { vs_currency: 'usd', order: 'market_cap_desc', per_page: 10, page: 1 }
        });
        const data = await response.json();

        const container = document.getElementById('crypto-container');
        container.innerHTML = ''; // Clear loading text
        data.forEach(coin => {
          const card = document.createElement('div');
          card.className = 'crypto-card';
          card.innerHTML = `
            <h2>${coin.name} (${coin.symbol.toUpperCase()})</h2>
            <p>Price: $${coin.current_price}</p>
            <p>Market Cap: $${coin.market_cap.toLocaleString()}</p>
          `;
          container.appendChild(card);
        });
      } catch (error) {
        console.error('Error fetching crypto data:', error);
        document.getElementById('crypto-container').innerHTML = '<p>Failed to load data.</p>';
      }
    }

    fetchCryptoData();
  </script>
</body>
</html>
