```python
from telegram.ext import Updater, MessageHandler, Filters
from telegram import ChatMember

TOKEN = '8588514433:AAGmyKCPJSYGUcbamanduSsFwMHTmAJbF6s'
GROUP_ID = -1003392321433

def check_membership(update, context):
    user_id = update.effective_user.id
    try:
        member = context.bot.get_chat_member(GROUP_ID, user_id)
        if member.status in [ChatMember.LEFT, ChatMember.KICKED]:
            update.message.reply_text("برای استفاده از ربات، ابتدا عضو گروه شوید.")
            update.message.delete()
    except:
        update.message.reply_text("خطا در بررسی عضویت.")
        update.message.delete()

def main():
    updater = Updater(TOKEN, use_context=True)
    dp = updater.dispatcher
    dp.add_handler(MessageHandler(Filters.text & ~Filters.command, check_membership))
    updater.start_polling()
    updater.idle()

if _name_ == '_main_':
    main()
```
