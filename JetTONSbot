import requests
import urllib.parse
import json
import time
from datetime import datetime, timedelta
import pyfiglet

result = pyfiglet.figlet_format('JetTONS')
print(result)
print("\nScript By : @abiedarmawan\n")

token = 'data.txt'
def count_lines(token):
    with open(token, 'r') as file:
        return sum(1 for line in file)

line_count = count_lines(token)
print("-"*40)
print(f"total jumlah akun : {line_count}")
print("-"*40)
url = "https://api.jettons.bot/api/tg_webapp/game/claim"

headers = {
    "Accept": "*/*",
    "Accept-Language": "en-US,en;q=0.9",
    "Cache-Control": "no-cache",
    "Content-Type": "application/json",
    "Pragma": "no-cache",
    "Priority": "u=1, i",
    "Sec-Ch-Ua": "\"Not/A)Brand\";v=\"8\", \"Chromium\";v=\"126\", \"Microsoft Edge\";v=\"126\", \"Microsoft Edge WebView2\";v=\"126\"",
    "Sec-Ch-Ua-Mobile": "?0",
    "Sec-Ch-Ua-Platform": "\"Windows\"",
    "Sec-Fetch-Dest": "empty",
    "Sec-Fetch-Mode": "cors",
    "Sec-Fetch-Site": "same-site"
}

def get_user_balance(init_data):
    payload = {"init_data": init_data}
    response = requests.post(url, json=payload, headers=headers)
    
    if response.status_code == 200:
        response_data = response.json()
        if response_data.get('success'):
            user_data = payload["init_data"].split("user=")[1].split("&")[0]
            user_json = json.loads(urllib.parse.unquote(user_data))
            username = user_json.get("username", "Unknown")
            balance = response_data['game_state']['balance']
            
            print(f'Username: {username}')
            print(f'Balance: {balance}')
        else:
            print("Error: Respons tidak berhasil")
    else:
        print(f"Error: Gagal mengakses API (Status: {response.status_code})")

    print('-' * 40)

def process_all_accounts():
    with open('data.txt', 'r') as file:
        init_data_list = [line.strip() for line in file if line.strip()]

    for init_data in init_data_list:
        get_user_balance(init_data)

def countdown(seconds):
    for i in range(seconds, -1, -1):
        hours, remainder = divmod(i, 3600)
        minutes, seconds = divmod(remainder, 60)
        print(f'Next run in {hours:02}:{minutes:02}:{seconds:02}', end='\r')
        time.sleep(1)
    print('')

# Menentukan interval waktu (30 menit)
interval = 10 * 60


while True:
    process_all_accounts()
    countdown(interval)
