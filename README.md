# OVERVIEW

# Crypto Price Scraper
A simple Python web scraper that extracts cryptocurrency names and prices from CoinMarketCap and displays the results in a Pandas DataFrame. The script runs continuously and refreshes the data every 24 hours.

# 💡Features
- Scrapes cryptocurrency names and current prices from CoinMarketCap.
- Stores scraped data in a Pandas DataFrame.
- Automatically updates every 24 hours.
- Easy to customize for additional cryptocurrency information.

# ⚙Technologies Used
- Python
- Pandas
- NumPy
- Requests
- BeautifulSoup4

# 👌Usage
Run the script using:

python scraper.py

The script will:

Connect to CoinMarketCap.
Extract cryptocurrency names and prices.
Store the data in a Pandas DataFrame.
Print the DataFrame to the console.
Repeat the process every 24 hours.

To stop the script:

CTRL + C

# ✔Crypto site : [Coinmarketcap](https://coinmarketcap.com/)
![Crypto_site](/Images/crypto_site.png)

# ✔Code
```python
import pandas as pd
import numpy as np
from bs4 import BeautifulSoup
import requests
import time
def crypto_scraping():
    root = requests.get('https://coinmarketcap.com/','html')
    page = BeautifulSoup(root.text)
    all_coin = page.find_all('tr')
    data = []
    for coin in all_coin:
        coin_name = coin.find('p',class_='sc-c1554bc0-0 eWrlhi coin-item-name')
        if coin_name is None:
            continue
        c_name = coin.find('p',class_='sc-c1554bc0-0 eWrlhi coin-item-name').text
        price_span = coin.find('div',class_='sc-631098c-0 ilZTOW')
        if price_span:
            c_price=price_span.find('span').text
        data.append({'Crypto_names':c_name,'Price':c_price}) 
    df = pd.DataFrame(data)
    return df

while True:
    try:
        print(crypto_scraping())
        time.sleep(86400)
    except KeyboardInterrupt:
        print('Scrapping Stopped')
        break

```
# ✔Example Output
![Result](/Images/result.png)

# Notes
- CoinMarketCap frequently updates its website structure. If the scraper stops working, inspect the website and update the HTML class names accordingly.
- Consider using CoinMarketCap's official API for more reliable and scalable data collection.

# Future Improvements
- Export data to CSV or Excel.
- Store historical cryptocurrency prices.
- Add market capitalization and trading volume data.
- Visualize price trends with charts.
- Integrate with cryptocurrency APIs.
