# Orbit Exchange Automation & Analytics Tool

A high-performance automation suite designed for the **Orbit Exchange** (Betfair white-label) platform. This system combines real-time data scraping, historical price analysis, and automated trading strategies using **Selenium** and **SQLite**.

---

## 🚀 Key Features

* **Automated Session Management:** Saves and loads authentication states via `cookies.pkl` to bypass repetitive logins.
* **Pre-Event Data Scraping:** Monitors odds for every minute (up to 180 minutes before start) and stores them in a structured SQLite database.
* **Trading Strategies:**
    * `PENDULUM`: Monitors price fluctuations across multiple market listeners.
    * `BIG_SHIFT`: Executes rapid Back/Lay orders based on sudden market movements.
    * `COLLECT_DATA`: Dedicated mode for building a historical database of market behavior.
* **Interactive Visualization:** A built-in data browser using `matplotlib` to graph price trends from the database.
* **Anti-Bot & Proxy Support:** Supports SOCKS4 proxies and automatically installs/configures VPN extensions (ZenMate, VeePN) in Firefox.
* **Hybrid GUI:** Uses `tkinter` popups to allow human intervention for critical steps (e.g., connecting VPN, choosing the specific event).

---

## 📁 Project Structure

* `main.py` – The main entry point of the application.
* **src/**
    * `webdriver_configuration.py` – Firefox profile, proxy, and VPN extension setup.
    * `webdriver_navigation.py` – Strategy routing and high-level navigation logic.
    * `webdriver_orbitx_actions.py` – Lower-level interactions (betting, scraping, logging in).
    * `sql_actions.py` – Database CRUD operations for the matches table.
    * `data_display.py` – GUI module for browsing and graphing historical data.
    * `webdriver_waits.py` – Custom Selenium Wait classes integrated with Tkinter alerts and audio alarms.

---

## 🛠 Installation & Setup

### Prerequisites
* Python 3.8+
* Firefox Browser installed.
* Geckodriver added to your system `PATH`.

### Dependencies
```bash
pip install selenium matplotlib
```

### Database Initialization
In `main.py`, uncomment the `create_new_table()` line on the first run to initialize `Matches.sqlite`.

### Credentials
Update your login details in `src/webdriver_orbitx_actions.py`:

```python
username = 'your_username'
password = 'your_password'
```
## 📈 Usage

### Data Collection
1. Set the mode to `COLLECT_DATA` in the startup sequence.
2. The bot will open Orbit Exchange and wait for you to select a match.
3. Once selected, it records the odds every 60 seconds until the match starts.

### Data Analysis
To view your collected data, call `display_data()` in `main.py`. This opens a window where you can scroll through matches and see the price movement graph:

* **X-axis:** Minutes before the match.
* **Y-axis:** Odds value.

### Automated Trading
When running `PENDULUM` or `BIG_SHIFT`, the bot will trigger an audio alarm and a Tkinter popup when specific market conditions are met, allowing you to confirm the execution of the trade.

---

## ⚠️ Disclaimer
This software is for **educational and analytical purposes only**. Trading on betting exchanges involves financial risk. Use of automated bots may be against the Terms of Service of the platform; use at your own discretion.
