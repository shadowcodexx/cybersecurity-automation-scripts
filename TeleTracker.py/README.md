# TeleTracker

**Real-time Telegram Monitoring Tool**  

TeleTrackers is a Python-based tool that monitors public Telegram channels in real-time for messages containing predefined keywords related to security, extremism, or suspicious activities. All detected messages are logged into a CSV file for analysis.  

##  Key Features

- Monitors **Telegram public channels** in real-time  
- Supports **multilingual keywords**   
- Location-specific monitoring   
- Logs alerts with **Date, Channel Name, Keyword, and Message**  
- Easy to extend for additional keywords or channels

## How to use?
1. Copy the entire code bellow
2. Paste it to terminal of VSCode or pyCharm
3. Make necessory changes in keywords
4. Add channel name in the area for client
5. Add your api and hash
6. Run the code

## DISCLAIMER
- TeleTrackers is developed solely for ethical, legal, and research purposes.

- It is intended only for monitoring public Telegram channels to aid in OSINT and cybersecurity research.

- Any misuse, including hacking, harassment, privacy violations, or illegal activity, is strictly prohibited.

- The author, shadowcodex, does not assume any responsibility for misuse or legal consequences arising from improper use.

- By using this tool, you agree to comply with all applicable laws and Telegram’s Terms of Service.

- Use responsibly, ethically, and at your own risk.

```
from telethon import TelegramClient, events
import csv


api_id = 123456            #your api id
api_hash = "abcdefghijklmnopqrst"      #your api hash
phone = "+__ 9087654321" #your phone number

keywords = [
    "keyword1", "keyword2", "keyword3"
]

csv_file = "teletrackers_monitoring.csv"
with open(csv_file, "w", encoding="utf-8", newline="") as f:
    csv_writer = csv.writer(f)
    csv_writer.writerow(["Date", "Channel", "Keyword", "Message"])

client = TelegramClient("teletrackers_session", api_id, api_hash)

@client.on(events.NewMessage)
async def handler(event):
    if event.message.text:
        text = event.message.text.lower()
        for k in keywords:
            if k.lower() in text:
                print(f"[ALERT] {k} detected in {event.chat.title} ({event.chat_id})")
                with open(csv_file, "a", encoding="utf-8", newline="") as f:
                    log_writer = csv.writer(f)
                    log_writer.writerow([event.date, event.chat.title, k, event.message.text.replace("\n", " ")])

print(" TeleTrackers is running... Monitoring Telegram in real-time ")
print("Logs will be saved to:", csv_file)

async def main():

    entity = await client.get_entity("channel you want to monitor")
    print("Monitoring channel:", entity.title)

    # History
    async for message in client.iter_messages(entity, limit=100):  # you can increase limit
        if message.text:
            text = message.text.lower()
            for k in keywords:
                if k.lower() in text:
                    print(f"[HISTORY ALERT] {k} detected in {entity.title} ({entity.id})")
                    with open(csv_file, "a", encoding="utf-8", newline="") as f:
                        log_writer = csv.writer(f)
                        log_writer.writerow([message.date, entity.title, k, message.text.replace("\n", " ")])

    # RealTime
    @client.on(events.NewMessage(chats=entity))
    async def handler(event):
        if event.message.text:
            text = event.message.text.lower()
            for k in keywords:
                if k.lower() in text:
                    print(f"[ALERT] {k} detected in {event.chat.title} ({event.chat_id})")
                    with open(csv_file, "a", encoding="utf-8", newline="") as f:
                        log_writer = csv.writer(f)
                        log_writer.writerow([event.date, event.chat.title, k, event.message.text.replace("\n", " ")])

    await client.run_until_disconnected()

with client:
    client.loop.run_until_complete(main())
```

