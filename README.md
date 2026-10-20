# Crypto Price Tracker

A Python script that monitors a cryptocurrency price and sends a Telegram notification when it moves above or below thresholds you set.

## Features

- Choose any cryptocurrency supported by CoinGecko
- Set your own upper and lower price limits
- Checks the price every 60 seconds
- Sends a Telegram alert once when a limit is crossed, with no repeated spam
- Handles invalid input and network errors without crashing

## Built With

- Python 3
- [requests](https://requests.readthedocs.io/)
- [python-dotenv](https://github.com/theskumar/python-dotenv)
- [CoinGecko API](https://www.coingecko.com/en/api) and the Telegram Bot API

## Setup

```bash
git clone https://github.com/shalva18/crypto-price-tracker.git
cd crypto-price-tracker
pip install -r requirements.txt
```

1. Get a free Demo API key from CoinGecko.
2. Create a Telegram bot with @BotFather and note the token.
3. Send any message to your bot, then find your chat ID using the Bot API `getUpdates` method.
4. Copy `.env.example` to `.env` and fill in your values.

## Usage

```bash
python main.py
```

Enter the coin id (for example `bitcoin`), the minimum price and the maximum price. Press `Ctrl+C` to stop.

## Roadmap

- [ ] Track several coins at once
- [ ] Show whether the upper or lower limit was crossed
- [ ] Save settings between runs

## Disclaimer

This tool is for information only and is not financial advice.
