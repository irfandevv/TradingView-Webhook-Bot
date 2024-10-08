<p align="center"><a href="https://github.com/fabston/TradingView-Webhook-Bot" target="_blank"><img src="https://raw.githubusercontent.com/fabston/TradingView-Webhook-Bot/master/assets/logo.png"></a></p>

<p align="center">
    <a href="https://www.python.org/downloads/release/python-380/"><img src="https://img.shields.io/badge/python-3.8-blue.svg?style=plastic" alt="Python version"></a>
    <a href="https://github.com/fabston/TradingView-Webhook-Bot/blob/master/LICENSE"><img src="https://img.shields.io/github/license/fabston/TradingView-Webhook-Bot?style=plastic" alt="GitHub license"></a>
    <a href="https://github.com/fabston/TradingView-Webhook-Bot/issues"><img src="https://img.shields.io/github/issues/fabston/TradingView-Webhook-Bot?style=plastic" alt="GitHub issues"></a>
    <a href="https://github.com/fabston/TradingView-Webhook-Bot/pulls"><img src="https://img.shields.io/github/issues-pr/fabston/TradingView-Webhook-Bot?style=plastic" alt="GitHub pull requests"></a>
    <br /><a href="https://github.com/fabston/TradingView-Webhook-Bot/stargazers"><img src="https://img.shields.io/github/stars/fabston/TradingView-Webhook-Bot?style=social" alt="GitHub stars"></a>
    <a href="https://github.com/fabston/TradingView-Webhook-Bot/network/members"><img src="https://img.shields.io/github/forks/fabston/TradingView-Webhook-Bot?style=social" alt="GitHub forks"></a>
    <a href="https://github.com/fabston/TradingView-Webhook-Bot/watchers"><img src="https://img.shields.io/github/watchers/fabston/TradingView-Webhook-Bot?style=social" alt="GitHub watchers"></a>
</p>

<p align="center">
  <a href="#about">About</a>
  •
  <a href="#features">Features</a>
  •
  <a href="#installation">Installation</a>
  •
  <a href="#images">Images</a>
  •
  <a href="#how-can-i-help">Help</a>
</p>

## Installation
> ⚠️ Best to run the bot on a VPS. I can recommend <a href="https://hetzner.cloud/?ref=tQ1NdT8zbfNY" title="Get €20 in cloud credits">Hetzner</a>'s CX11 VPS for 3.79€/month. [Sign up](https://hetzner.cloud/?ref=tQ1NdT8zbfNY) now and receive **€20 free** credits.
1. Clone this repository `git clone https://github.com/fabston/TradingView-Webhook-Bot.git`
1. Create your virtual environment `python3 -m venv TradingView-Webhook-Bot`
1. Activate it `source TradingView-Webhook-Bot/bin/activate && cd TradingView-Webhook-Bot`
1. Install all requirements `pip install -r requirements.txt`
1. Edit and update [`config.py`](https://github.com/fabston/TradingView-Webhook-Bot/blob/master/config.py)
1. Setup TradingView alerts. An example alert message would be:
    ```json
    {
     "key": "9T2q394M92",
     "telegram": "-1001277977502",
     "discord": "789842341870960670/BFeBBrCt-w2Z9RJ2wlH6TWUjM5bJuC29aJaJ5OQv9sE6zCKY_AlOxxFwRURkgEl852s3",
     "slack": "T00000000/B00000000/XXXXXXXXXXXXXXXXXXXXXXXX",
     "msg": "Long *#{{ticker}}* at `{{close}}`"
    }
    ```
    - `key` is mandatory! It has to match with `sec_key` in [`config.py`](https://github.com/fabston/TradingView-Webhook-Bot/blob/master/config.py). It's an extra security measurement to ensure nobody else is executing your alerts
    - `telegram`, `discord`, `slack` is optional. If it is not set it will fall back to the config.py settings
    - `msg` can be anything. Markdown for [Telegram](https://core.telegram.org/api/entities) and [Discord](https://support.discord.com/hc/en-us/articles/210298617-Markdown-Text-101-Chat-Formatting-Bold-Italic-Underline-) is supported as well
        - TradingViews variables like `{{close}}`, `{{exchange}}` etc. work too. More can be found [here](https://www.tradingview.com/blog/en/introducing-variables-in-alerts-14880/)
    - Your webhook url would be `http://<YOUR-IP>/webhook`
1. If you use a firewall be sure to open the corresponding port
1. Run the bot with `python main.py`
1. [PM2](https://github.com/fabston/TradingView-Webhook-Bot/issues/28#issuecomment-766301062) can help you in running the app in the background / on system boot. 

### Forward Port 80 to 8080 using NGINX

*It is recommended to run flask on a different port like 8080. It is then necessary to forward port 80 to 8080.*

1. Install the necessary packages: `sudo apt-get install nginx`
1. Edit the NGINX configuration file: `sudo nano /etc/nginx/sites-enabled/tv_webhook`
1. Add the following content:
    ```nginx
   server {
       listen 80;
   
       server_name <YOUR-IP>;
   
       location / {
           proxy_pass http://127.0.0.1:8080;  # Forward traffic to port 8080
           proxy_set_header Host $host;
           proxy_set_header X-Real-IP $remote_addr;
           proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;  # Pass client's IP address
           proxy_set_header X-Forwarded-Proto $scheme;
       }
   }
   ```
1. Restart NGINX `sudo service nginx restart`

### Docker
1. Clone this repository `git clone https://github.com/fabston/TradingView-Webhook-Bot.git`
1. Edit and update [`config.py`](https://github.com/fabston/TradingView-Webhook-Bot/blob/master/config.py)
1. `docker-compose build`
1. `docker-compose up`

## Images
![Webhook Bot](https://i.imgur.com/vZA42cc.png)

## How can I help?
All kinds of contributions are welcome 🙌! The most basic way to show your support is to `⭐️ star` the project, or raise [`🐞 issues`](https://github.com/fabston/TradingView-Webhook-Bot/issues/new/choose).

***

<p align="center">
    <a href="https://www.buymeacoffee.com/fabston"><img alt="Buy Me A Coffee" title="☕️" src="https://raw.githubusercontent.com/fabston/TradingView-Webhook-Bot/master/assets/bmac.png" width=200px></a>
</p>
