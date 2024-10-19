from telegram import Update
from telegram.ext import ApplicationBuilder, CommandHandler, MessageHandler, filters, ContextTypes

# توكن البوت الخاص بك
TOKEN = "7749332902:AAEuFN4x0sCWdMVzDVwQgLwd3ipxCysgqFc"

# إنشاء التطبيق
app = ApplicationBuilder().token(TOKEN).build()

# النص الجديد المطلوب
full_text = "እንኳን ደህና መጣህ እንኳን ደህና መጣህ እንኳን ደህና መጣህ እንኳን ደህና መጣህ እንኳን ደህና መጣህ እንኳን ደህና መጣህ እንኳን ደህና መጣህ እንኳን ደህና መጣህ እንኳን ደህና መጣህ እንኳን ደህና መጣህ"

async def start(update: Update, context: ContextTypes.DEFAULT_TYPE):
    await context.bot.send_message(chat_id=update.effective_chat.id, text="اكتب لي أي شيء.")

async def echo(update: Update, context: ContextTypes.DEFAULT_TYPE):
    user_text = update.message.text
    combined_text = user_text + full_text
    if len(combined_text) > 138:
        excess_length = len(combined_text) - 138
        combined_text = user_text + full_text[:-excess_length]
    await context.bot.send_message(chat_id=update.effective_chat.id, text=combined_text[:138])

# إضافة معالجات الأوامر
app.add_handler(CommandHandler("start", start))
app.add_handler(MessageHandler(filters.TEXT & ~filters.COMMAND, echo))

# بدء البوت
app.run_polling()
