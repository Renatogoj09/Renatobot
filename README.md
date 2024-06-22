# Renatobot
Fica só de botas para o tereré
import time
import requests
import numpy as np
from telegram import Bot

# Configurações do Telegram
TOKEN = '7321206553:AAElA11kxZe5pL6HcE45VdKmPvrzYWec8YA'
CHAT_ID = '6281476479'

bot = Bot(token=TOKEN)

# Função para obter dados da Papa Jogo
def obter_dados_papa_jogo():
    url = 'https://api.papajogo.com/endpoint'  # Substitua pela URL real da API
    headers = {
        'Authorization': 'Bearer wp9Age8KL3yEzFcGEUnLO5cJnwVKZw_aem_ZmFrZWR1bW15MTZieXRlcw',
        'Content-Type': 'application/json'
    }
    response = requests.get(url, headers=headers)
    if response.status_code == 200:
        return response.json()
    else:
        print(f"Erro ao obter dados da Papa Jogo: {response.status_code}")
        return None

# Função para gerar sinal baseado nos dados
def gerar_sinal(dados):
    # Exemplo de processamento dos dados para gerar o sinal
    # Aqui você deve implementar a lógica para gerar um sinal com base nos dados obtidos
    assertividade = 0.86
    sinal = 'vermelho' if np.random.rand() < assertividade else 'azul'
    return sinal

# Função para enviar o sinal para o Telegram
def enviar_sinal():
    while True:
        dados = obter_dados_papa_jogo()
        if dados:
            sinal = gerar_sinal(dados)
            mensagem = f"Sinal: {sinal}"
            bot.send_message(chat_id=CHAT_ID, text=mensagem)
        else:
            bot.send_message(chat_id=CHAT_ID, text="Erro ao obter dados da Papa Jogo.")
        time.sleep(3600)  # Envia um sinal a cada hora

if __name__ == '__main__':
    enviar_sinal()
