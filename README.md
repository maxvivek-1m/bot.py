import telebot
from telebot.types import InlineKeyboardMarkup, InlineKeyboardButton
import os

# Telegram Bot Token (GitHub Secrets me set karein)
BOT_TOKEN =8096813477:AAHxk-ZDk-ojx7W953OaIOqjll6TGBUgghQ os.getenv("8096813477:AAHxk-ZDk-ojx7W953OaIOqjll6TGBUgghQ")

bot = telebot.TeleBot(8096813477:AAHxk-ZDk-ojx7W953OaIOqjll6TGBUgghQ)

@bot.message_handler(commands=['start'])
def send_welcome(message):
    chat_id = message.chat.id
    welcome_text = "👋 Hey There! Welcome To OUR Bot!\n\n" \
                   "⛔ Must Join All Channels To Use This Bot\n\n" \
                   "💣 After Joining, Click On The Joined Button"
    
    # Inline Keyboard
    markup = InlineKeyboardMarkup()
    buttons = [
        InlineKeyboardButton("🔗 Join", url="https://t.me/example1"),
        InlineKeyboardButton("🔗 Join", url="https://t.me/example2"),
        InlineKeyboardButton("🔗 Join", url="https://t.me/example3"),
        InlineKeyboardButton("🔗 Join", url="https://t.me/example4"),
    ]
    markup.add(*buttons)

    joined_button = InlineKeyboardButton("✅ Joined", callback_data="joined")
    markup.add(joined_button)

    bot.send_message(chat_id, welcome_text, reply_markup=markup)

@bot.callback_query_handler(func=lambda call: call.data == "joined")
def joined_callback(call):
    bot.send_message(call.message.chat.id, "🎉 Congrats, You've received 5 points as a joining bonus.")

bot.polling()
