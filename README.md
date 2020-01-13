# WEB-SCRAPPING
Python Web-Scrapping
import requests
from bs4 import BeautifulSoup
import smtplib
import time 

URL = "https://www.amazon.co.uk/500GB-Bundle-Second-DualShock-Controller/dp/B07WMT6T5Z/ref=sr_1_4?crid=14ZTS0QP8SNXQ&keywords=playstation+4&qid=1578935660&sprefix=playstat%2Caps%2C184&sr=8-4"
headers= {"User-Agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/79.0.3945.117 Safari/537.36"}

def check_price():
    page = requests.get(URL, headers=headers)
    soup = BeautifulSoup(page.content, "html.parser")
    
    #title = soup.find(id = "productTitle").get_text()
    price = int(soup.find(id = "priceblock_ourprice").get_text()[1:4])
    #print(title)
    #print(price)
  
    
    if (price> 250):
        send_mail()
    

def send_mail():
    #REQUIRES TWO STEP VERIFICATION, 
    #ENABLING LESS SECURE APP ACCESS
    #REQUIRES APP PASSWORD (Mail and WINDOWS COMPUTER)
    server = smtplib.SMTP("smtp.gmail.com", 587)
    server.ehlo()
    server.starttls()
    server.ehlo()

    server.login("m.rahman180801@gmail.com", "sfuqruqqntjgjrwh")#two step verification password

    subject = "Price Fell Down"
    body = "check the amazon link https://www.amazon.co.uk/500GB-Bundle-Second-DualShock-Controller/dp/B07WMT6T5Z/ref=sr_1_4?crid=14ZTS0QP8SNXQ&keywords=playstation+4&qid=1578935660&sprefix=playstat%2Caps%2C184&sr=8-4 "
    
    msg = f"subject : {subject}\n\n\n{body}"

    server.sendmail(
        "m.rahman180801@gmail.com",
        "m.rahman180801@gmail.com",
        msg
    )
    print("Email HAS BEEN SENT!!")
    
    server.quit()

check_price()


