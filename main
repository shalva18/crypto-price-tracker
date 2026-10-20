import os
import time
import requests
from dotenv import load_dotenv




def get_users_input():
    crypto =input("enter cryptos name you want to get notified: ").strip().lower()
    prices = True
    while prices:
        
       try:
        
          min_price = float(input("enter minimum price you want to get notification: "))
          max_price = float(input("enter maximum price you want to get notification: "))
          
       
       
          while not max_price >  min_price:
              print("maximum must be higher than minimum")
              min_price = float(input("enter minimum price you want to get notification: "))
              max_price = float(input("enter maximum price you want to get notification: "))
          prices = False
       except ValueError:
        print("min price and max price must be numbers")
    return crypto,min_price,max_price


load_dotenv()
API_KEY = os.getenv("COINGECKO_API_KEY")
BOT_TOKEN = os.getenv("TELEGRAM_BOT_TOKEN")
CHAT_ID = os.getenv("TELEGRAM_CHAT_ID")

def get_price(crypto):
    url = "https://api.coingecko.com/api/v3/simple/price"
    params = {"ids": crypto, "vs_currencies": "usd"}
    headers = {"x-cg-demo-api-key": API_KEY}
    try:
        response = requests.get(url, params=params, headers=headers, timeout=10)
        response.raise_for_status()
        data = response.json()
    except requests.RequestException as error:
        print("Could not get price:", error)
        return None

    if crypto not in data:
        print("Unknown crypto:", crypto)
        return None

    return data[crypto]["usd"]

def send_telegram(message):
    url = f"https://api.telegram.org/bot{BOT_TOKEN}/sendMessage"
    payload = {"chat_id": CHAT_ID, "text": message}

    try:
        response = requests.post(url, data=payload, timeout=10)
        response.raise_for_status()
    except requests.RequestException as error:
        print("Could not send Telegram message:", type(error).__name__)
        





def monitor(crypto, min_price, max_price, interval=60):
    alert_sent = False

    while True:
        price = get_price(crypto)

        if price is not None:
            print(f"{crypto}: {price}")
            outside = price >= max_price or price <= min_price

            if outside and not alert_sent:
                message = f"ALERT: {crypto} is at {price}"
                print(message)
                send_telegram(message)
                alert_sent = True
            elif not outside:
                alert_sent = False

        time.sleep(interval)

if __name__ == "__main__":
    crypto, min_price, max_price = get_users_input()
    monitor(crypto, min_price, max_price)


