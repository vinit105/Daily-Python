> [!NOTE]
> For Better UI Run on browser.

<img srs="./python_image.jpeg" height="200" />
# $${\color{pink}Daily }$$ $${\color{pink}Python}$$
 Python Scripts That Will Automate Our Daily Tasks

Python, with its simple syntax and powerful libraries, is one of the best programming languages for creating automation scripts. 

## $${\color{yellow}Text}$$ $${\color{yellow}Extract}$$ $${\color{yellow} From }$$ $${\color{yellow}Images}$$
Python can be used to extract text from images using the pytesseract library, which can be useful when you need to digitize printed content or extract text from scanned documents.

```
from PIL import Image
import pytesseract

def extract_text_from_image(image_path):
    # Open the image file
    img = Image.open(image_path)
    
    # Use pytesseract to extract text
    text = pytesseract.image_to_string(img)
    
    return text

image_path = 'path_to_your_image.jpg'
extracted_text = extract_text_from_image(image_path)
print("Extracted Text:\n", extracted_text)

```
##  $${\color{yellow}Automating}$$ $${\color{yellow}Backups}$$ $${\color{yellow}To}$$ $${\color{yellow}Google}$$ $${\color{yellow}Drive}$$ 
Automating backups to cloud services like Google Drive is made possible with Python using libraries such as pydrive.

```
from pydrive.auth import GoogleAuth
from pydrive.drive import GoogleDrive

def backup_to_google_drive(file_path):
    gauth = GoogleAuth()
    gauth.LocalWebserverAuth()
    drive = GoogleDrive(gauth)
    file = drive.CreateFile({'title': 'backup_file.txt'})
    file.Upload()
    print("Backup uploaded successfully!")

file = '/path/to/your/file.txt' backup_to_google_drive(file)
```
## $${\color{yellow}Auto-Replys}$$  $${\color{yellow}To}$$  $${\color{yellow}Emails}$$ 
If you often receive emails and want to set up an auto-reply, then use the imaplib and smtplib libraries to automatically reply to emails:
```
import imaplib
import smtplib
from email.mime.text import MIMEText

def auto_reply():
    # Connect to email server
    mail = imaplib.IMAP4_SSL("imap.gmail.com")
    mail.login('youremail@gmail.com', 'yourpassword')
    mail.select('inbox')

    # Search for unread emails
    status, emails = mail.search(None, 'UNSEEN')

    if status == "OK":
        for email_id in emails[0].split():
            status, email_data = mail.fetch(email_id, '(RFC822)')
            email_msg = email_data[0][1].decode('utf-8')

            # Send auto-reply
            send_email("Auto-reply", "Thank you for your email. I'll get back to you soon.", 'sender@example.com')

def send_email(subject, body, to_email):
    sender_email = 'youremail@gmail.com'
    sender_password = 'yourpassword'
    receiver_email = to_email

    msg = MIMEText(body)
    msg['From'] = sender_email
    msg['To'] = receiver_email
    msg['Subject'] = subject

    with smtplib.SMTP_SSL('smtp.gmail.com', 465) as server:
        server.login(sender_email, sender_password)
        server.sendmail(sender_email, receiver_email, msg.as_string())

auto_reply()
```
## $${\color{yellow}Task}$$  $${\color{yellow}Scheduler}$$ $${\color{yellow}(Task Scheduler)}$$  
Scheduling tasks can be done easily using the schedule library, which allows you to automate tasks like sending an email or running a backup script at specific times:
```
import schedule
import time

def job():
    print("Running scheduled task!")

# Schedule the task to run every day at 10:00 AM
schedule.every().day.at("10:00").do(job)

while True:
    schedule.run_pending()
    time.sleep(1)
```

## $${\color{yellow}Batch}$$ $${\color{yellow}Image}$$ $${\color{yellow}Resizing}$$
If you need to resize images in bulk, Python makes it easy with the Pillow library.

```
from PIL import Image
import os
import asyncio
from concurrent.futures import ProcessPoolExecutor

def resize_image(filename, width, height):
    img = Image.open(filename)
    img = img.resize((width, height))
    img.save(f"resized_{filename}")
    return f"Resized {filename}"

async def resize_images(folder_path, width, height):
    with ProcessPoolExecutor() as executor:
        loop = asyncio.get_event_loop()
        tasks = []
        for filename in os.listdir(folder_path):
            if filename.endswith('.jpg'):
                tasks.append(loop.run_in_executor(
                    executor, resize_image, os.path.join(folder_path, filename), width, height))
        results = await asyncio.gather(*tasks)
        print(results)

folder = '/path/to/your/images'
asyncio.run(resize_images(folder, 800, 600))
```
## $${\color{yellow}Task}$$ $${\color{yellow}Reminder/Scheduler}$$.   
Creating a task tracker or reminder system in Python can be accomplished using the datetime and asyncio modules.
```
import asyncio
from datetime import datetime

async def task_reminder(task_name, interval):
    while True:
        print(f"Reminder: {task_name} - {datetime.now()}")
        await asyncio.sleep(interval)

async def main():
    await asyncio.gather(
        task_reminder("Drink Water", 7200),  # Remind every 2 hours
        task_reminder("Take a Break", 3600)  # Remind every 1 hour
    )

asyncio.run(main())
```
## $${\color{yellow}Auto-Generate}$$ $${\color{yellow}Daily}$$ $${\color{yellow}Reports}$$
Automate daily reports by using Python to collect data and format it into a report:
```
import datetime
import aiofiles
import asyncio

async def generate_report(data):
    today = datetime.date.today()
    filename = f"daily_report_{today}.txt"
    async with aiofiles.open(filename, 'w') as file:
        await file.write(f"Report for {today}\n")
        await file.write("\n".join(data))
    print(f"Report generated: {filename}")

data = ["Task 1: Completed", "Task 2: Pending", "Task 3: Completed"]
asyncio.run(generate_report(data))
```
