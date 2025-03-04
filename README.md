# Cryptomarket-
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>CryptoMarket - Live Cryptocurrency Prices</title>

    <!-- Embedded CSS -->
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
            background-color: #121212;
            color: white;
            text-align: center;
        }

        header {
            background-color: #1e1e1e;
            padding: 20px;
        }

        nav ul {
            list-style: none;
            padding: 0;
        }

        nav ul li {
            display: inline;
            margin: 0 15px;
        }

        nav ul li a {
            color: white;
            text-decoration: none;
        }

        .market {
            margin: 20px auto;
            max-width: 800px;
        }

        table {
            width: 100%;
            border-collapse: collapse;
            background: #222;
        }

        th, td {
            padding: 12px;
            border: 1px solid #444;
        }

        th {
            background: #333;
        }

        footer {
            background: #1e1e1e;
            padding: 15px;
            margin-top: 20px;
        }
    </style>

</head>
<body>

    <header>
        <h1>CryptoMarket</h1>
        <nav>
            <ul>
                <li><a href="#">Home</a></li>
                <li><a href="#">Markets</a></li>
                <li><a href="#">News</a></li>
                <li><a href="#">Contact</a></li>
            </ul>
        </nav>
    </header>

    <section class="market">
        <h2>Live Market Prices</h2>
        <table id="crypto-table">
            <thead>
                <tr>
                    <th>Rank</th>
                    <th>Coin</th>
                    <th>Price</th>
                    <th>24h Change</th>
                    <th>Market Cap</th>
                </tr>
            </thead>
            <tbody>
                <!-- Data will be injected here -->
            </tbody>
        </table>
    </section>

    <footer>
        <p>&copy; 2025 CryptoMarket. All rights reserved.</p>
    </footer>

    <!-- Embedded JavaScript -->
    <script>
        document.addEventListener("DOMContentLoaded", () => {
            const apiUrl = "https://api.coingecko.com/api/v3/coins/markets?vs_currency=usd&order=market_cap_desc&per_page=5&page=1&sparkline=false";

            async function fetchCryptoData() {
                try {
                    const response = await fetch(apiUrl);
                    const data = await response.json();
                    const tableBody = document.querySelector("#crypto-table tbody");
                    tableBody.innerHTML = ""; // Clear old data

                    data.forEach((coin, index) => {
                        const row = `
                            <tr>
                                <td>${index + 1}</td>
                                <td>${coin.name} (${coin.symbol.toUpperCase()})</td>
                                <td>$${coin.current_price.toLocaleString()}</td>
                                <td style="color: ${coin.price_change_percentage_24h >= 0 ? 'green' : 'red'};">
                                    ${coin.price_change_percentage_24h.toFixed(2)}%
                                </td>
                                <td>$${coin.market_cap.toLocaleString()}</td>
                            </tr>
                        `;
                        tableBody.innerHTML += row;
                    });
                } catch (error) {
                    console.error("Error fetching cryptocurrency data:", error);
                }
            }

            fetchCryptoData();
            setInterval(fetchCryptoData, 60000); // Update every minute
        });
    </script>

</body>
</html>
