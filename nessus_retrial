import warnings
import requests
from urllib3.exceptions import InsecureRequestWarning
import random
import time
import json
import re
import os
import sys
import string
import time
from bs4 import BeautifulSoup

requests.packages.urllib3.disable_warnings(category=InsecureRequestWarning)
requests.packages.urllib3.disable_warnings()

GET_INBOX = 'https://getnada.com/api/v1/inboxes/'
GET_MESSAGE = 'https://getnada.com/api/v1/messages/'
mailx = str(random.randint(1, 9999999999))
domain = "getnada.com"
name = mailx

email = mailx + '@getnada.com' 
print ("Email Address: "+ email)
print ("\033[1;32;10mNessus Registeration Form \033[1;32;0m")
ht=requests.get("https://www.tenable.com/products/nessus-home", verify=False)
bs=BeautifulSoup(ht.text,'html.parser')
for link in bs.findAll("input",{"name":"token"}):
 if 'name' in link.attrs:
   tkn=link.attrs['value']
 else:
   print("not found")
fname=("John")
lname=("Petrov")
params={"first_name":fname,"last_name":lname,"email":email,"country":"IN","Accept":"Agree","robot":"human","type":"homefeed","token":tkn,"submit":"Register"}
r = requests.post("https://www.tenable.com/products/nessus-home", data=params, verify=False)
if r.status_code == 200:
	bs=BeautifulSoup(r.text,'html.parser')
	keyword=bs.find("title").get_text()
	success=keyword.split('|')
	if str(success[0][:-1]) == 'Thank You for Registering for Nessus Home!':
		print('\033[1;32;10m'+str(success[0][:-1])+'\033[1;32;0m')
	elif bs.find('span',{"style":"color:#FF0000;"}).get_text():
		os.system('clear')
		print('\033[1;31;10m Sorry, This Email Address is already Registered for Nessus Activation Code\033[1;31;0m')

all = mailx + "@" + domain
time.sleep(15)
data = None
r = requests.get(GET_INBOX + all)
uid = (r.json()['msgs'])[0]['uid']
print(uid)
data = None
r = requests.get(GET_MESSAGE + uid)
text = r.json()['html']
regex = r"\w{4}(?:-\w{4}){4}"
activation_code=re.search(regex,text)
#print(text)
print("activation code:" + activation_code.group())
with open('nessus.txt', 'w') as f:
     print(activation_code.group(), file=f)

if os.name == 'nt':
	cmdw = ('C:\\Program Files\\Tenable\\Nessus\\nessuscli fetch --register ' + str(activation_code.group()))
	os.system(cmdw)
	cmdw = ('C:\\Program Files\\Tenable\\Nessus\\nessuscli update')
	os.system(cmdw)
else:
    cmd = ('nessuscli fetch --register ' + str(activation_code.group()) + ';nessuscli update; systemctl restart nessusd')
    os.system(cmd)

