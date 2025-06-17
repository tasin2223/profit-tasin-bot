# profit-tasin-bot
# main.py
from telegram import Update
from telegram.ext import ApplicationBuilder, CommandHandler, ContextTypes

ALLOWED_USER_ID = 6965817634

async def start(update: Update, context: ContextTypes.DEFAULT_TYPE):
    if update.effective_user.id != ALLOWED_USER_ID:
        await update.message.reply_text("❌ Sorry, এই Bot শুধু @tara_50003 এর জন্য।")
        return
    await update.message.reply_text("👋 স্বাগতম! EUR/USD সিগন্যাল পেতে `/signal` লিখুন।")

async def signal(update: Update, context: ContextTypes.DEFAULT_TYPE):
    if update.effective_user.id != ALLOWED_USER_ID:
        return
    await update.message.reply_text("📊 EUR/USD (M1)\n📈 CALL\n🕒 12:35\n📌 কারন: Breakout আপ হয়েছে।")

if __name__ == '__main__':
    app = ApplicationBuilder().token("🔐PASTE_YOUR_TOKEN_HERE").build()
    app.add_handler(CommandHandler("start", start))
    app.add_handler(CommandHandler("signal", signal))
    app.run_polling()
