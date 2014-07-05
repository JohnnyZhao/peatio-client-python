peatio-client-python
====================

peatio client written in python

### Usage ###


```python
from lib.client import Client, get_api_path

client = Client(access_key='your access key', secret_key='your secret key')

# get your membership
# get members API url using get_api_path
url = get_api_path('members')
# you can also give url a plain text, just like this:
url = "/api/v2/members/me.json"

# send request
res = client.get(url)

res should be something like this:

{
    u'email': u'zhaoyu.johnny@@gmail.com', 
    u'activated': True, 
    u'sn': u'PEAA*******', 
    u'name': u'JohnnyZhao',
    u'accounts': 
        [
            {u'currency': u'cny', 
             u'balance': u'1000', 
             u'locked': u'0.0'}, 
            {u'currency': u'btc', 
             u'balance': u'31', 
             u'locked': u'0.0'}, 
            {u'currency': u'pts', 
             u'balance': u'60', 
             u'locked': u'0.0'}, 
            {u'currency': u'dog', 
             u'balance': u'23952', 
             u'locked': u'11.0'}
        ], 
}

```
for more demos, checkout demo.py file

