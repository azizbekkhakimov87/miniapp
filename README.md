import telebot
from telebot.types import InlineKeyboardMarkup, InlineKeyboardButton
from datetime import datetime

TOKEN = "BOT_TOKENINGIZNI_QOYING"
bot = telebot.TeleBot(8448936121:AAEgGKLh5LArf4dGSxbJ4mcQHzR3crb7KJQ)

@bot.message_handler(commands=['start'])
def start(message):
    web_app_url = "https://azizbekkhakimov87.github.io/miniapp/"
    
    markup = InlineKeyboardMarkup()
    btn = InlineKeyboardButton(
        "📱 Web App'ni ochish",
        web_app={"url": web_app_url}
    )
    markup.add(btn)
    
    text = f"""
👋 Salom {message.from_user.first_name}!

Web App orqali xabar yuborish uchun tugmani bosing.

🌐 Manzil: {web_app_url}

📱 Funksiyalar:
• Xabar yuborish
• Tezkor xabarlar
• Test rejimi
• Foydalanuvchi ma'lumotlari
"""
    
    bot.reply_to(message, text, reply_markup=markup)
    print(f"Start: {message.from_user.first_name} ({message.from_user.id})")

@bot.message_handler(content_types=['web_app_data'])
def webapp_data(message):
    data = message.web_app_data.data
    user = message.from_user
    
    response = f"""
✅ Web App'dan xabar qabul qilindi!

📨 Xabar:
{data}

👤 Yuboruvchi: {user.first_name}
🆔 ID: {user.id}
🕐 Vaqt: {datetime.now().strftime('%H:%M:%S')}

🎉 Tabriklayman! Web App to'liq ishlayapti.
"""
    
    bot.reply_to(message, response)
    print(f"Web App: {user.first_name} - {data}")

@bot.message_handler(func=lambda m: True)
def echo(message):
    bot.reply_to(message, f"📝 Siz: {message.text}")

if __name__ == '__main__':
    print("="*50)
    print("🤖 Web App Bot ishga tushdi")
    print("="*50)
    bot.polling()
