import logging
from telegram import Update
from telegram.ext import Updater, CommandHandler, MessageHandler, Filters, CallbackContext

# Replace 'YOUR_TOKEN' with your actual Telegram bot token
TOKEN = '6172774358:AAGVqYVmEPfiv2uqedy1bq25yKl7D-HfDvU'

# Enable logging
logging.basicConfig(format='%(asctime)s - %(name)s - %(levelname)s - %(message)s', level=logging.INFO)
logger = logging.getLogger(__name__)

# Define the link you want to send in response to any text
link = "https://t.me/+zMm34ITOtq9iN2E1"  # Replace this with your desired link

# Define the message handler
def respond_with_link(update: Update, context: CallbackContext) -> None:
    # Send the link as a response to any text message
    update.message.reply_text(f"Hello! Here's the link you requested: {link}")

def start(update: Update, context: CallbackContext) -> None:
    # Send the link as a response to the /start command
    update.message.reply_text(f"Hello! Here's the link you requested: {link}")

def main() -> None:
    # Create the Updater and pass it your bot's token and explicitly set use_context=True
    updater = Updater(TOKEN, use_context=True)

    # Get the dispatcher to register handlers
    dispatcher = updater.dispatcher

    # Register the start command handler
    start_handler = CommandHandler("start", start)
    dispatcher.add_handler(start_handler)

    # Register the message handler to respond with the link
    message_handler = MessageHandler(Filters.text & ~Filters.command, respond_with_link)
    dispatcher.add_handler(message_handler)

    # Start the Bot
    updater.start_polling()

    # Run the bot until the user presses Ctrl-C
    updater.idle()

if __name__ == '__main__':
    main()
