# Python Solutions

## Wechat Send Messages to friend Regularly

```python
from __future__ import unicode_literals
import asyncio
from threading import Timer
from wxpy import *
import time
import requests
bot = None


async def login_wechat():
    global bot
    bot = Bot()
def get_friends():
    # my_friend = bot.grops(update=True,contact_only=False).search(u'一渣二佬')[0]    #你群的微信名称，不是备注，也不是微信帐号。
    my_friend = bot.groups().search(u'学习群')[0]    #你群的微信名称，不是备注，也不是微信帐号。
    my_friend.send(u'7/21 在校体温36.5')
    # img
    # my_friend.send_image('bg.jpg')
    # my_friend.send(u'bg.jpg send')
    # zip file
    # my_friend.send_file('zip.zip')
    # my_friend.send(u'file.zip send')

    # status
    # my_status = bot.friends().stats_text()
    # print(my_status)



async def send_news():
    if bot == None:
        await asyncio.gather(login_wechat())

    await asyncio.sleep(0)
    
    friend = bot.groups(update=True,contact_only=False).search()
    # friend = bot.chats().search()
    print(friend)

    await asyncio.sleep(25200)  #等待25200秒再发送
    get_friends()
            
    
  
async def main():
    await asyncio.gather(send_news())

def job():
    asyncio.run(main())
job()


```

