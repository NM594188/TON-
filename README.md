
import telegram
from telegram.ext import Updater, CommandHandler, MessageHandler, Filters

data = 0

def start(update, context):
    update.message.reply_text('欢迎使用数据统计机器人！请发送数字给我，我会将它们累加起来，并返回总和。')

def reset(update, context):
    global data
    data = 0
    update.message.reply_text('已经重置数据为 0。')

def echo(update, context):
    message = update.message.text
    global data
    try:
        number = float(message)
        data += number
        update.message.reply_text(f'已经累加 {number} 到数据上，当前总和为 {data}。')
    except ValueError:
        update.message.reply_text('无法识别您发送的内容，请发送数字给我。')


bot = telegram.Bot(token='')

updater = Updater(token='', use_context=True)

dispatcher = updater.dispatcher

dispatcher.add_handler(CommandHandler('start', start))
dispatcher.add_handler(CommandHandler('reset', reset))

dispatcher.add_handler(MessageHandler(Filters.text & ~Filters.command, echo))

updater.start_polling()

updater.idle()
