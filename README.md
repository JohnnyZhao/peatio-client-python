peatio-client-python
====================

peatio client written in python

## Usage ##

### Membership API ###

```python
from lib.client import Client, get_api_path

client = Client(access_key='your access key', secret_key='your secret key')

#get members API url using get_api_path by key 'members'
#API mapping of get_api_path
{
    'my_trades'   : '/api/v2/trades/my.json'
    'members'     : '/api/v2/members/me.json'
    'orders'      : '/api/v2/orders.json'
    'delete_order': '/api/v2/order/delete.json'
    'order_book'  : '/api/v2/order_book.json'
    'clear'       : '/api/v2/orders/clear.json'
    'trades'      : '/api/v2/trades.json'
    'order'       : '/api/v2/order.json'
    'multi_orders': '/api/v2/orders/multi.json'
    'tickers'     : '/api/v2/tickers/{market}.json'
    'markets'     : '/api/v2/markets.json'
    'k'           : '/api/v2/k.json'
}

url = get_api_path('members')


#you can also give url a plain text, just like this:
url = "/api/v2/members/me.json"

#send request
res = client.get(url)

#if your access key and secret are correct, res should be a json like this:

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

### Markets API ###

```python

#get markets
markets =  client.get(get_api_path('markets'))
print markets

#markets should be a json like this

[
    {u'id': u'btccny', u'name': u'BTC/CNY'}, 
    {u'id': u'ptscny', u'name': u'PTS/CNY'}, 
    {u'id': u'dogcny', u'name': u'DOG/CNY'}, 
    {u'id': u'dogbtc', u'name': u'DOG/BTC'}
]

```

### Orders API ###

```python

#get your orders in a specific market

orders = client.get(get_api_path('orders'), {'market': market['id']})
print orders

#orders will be an empty list or json like this

[
    {u'created_at': u'2014-07-05T14:56:25+08:00', 
     u'remaining_volume': u'11.0', 
     u'price': u'0.01', 
     u'side': u'sell', 
     u'volume': u'11.0', 
     u'state': u'wait', 
     u'avg_price': u'0.0', 
     u'executed_volume': u'0.0', 
     u'id': 299751, 
     u'market': u'dogcny'
    }
]

#create new order
#sell 10 dogecoins at price 0.01
params = {'market': 'dogcny', 'side': 'sell', 'volume': 10, 'price': 0.01}
res = client.post(get_api_path('orders'), params)
print res

#buy 10 dogecoins at price 0.001
params = {'market': 'dogcny', 'side': 'buy', 'volume': 10, 'price': 0.001}
res = client.post(get_api_path('orders'), params)
print res

#clear orders
#clear all orders in all markets
res = client.post(get_api_path('clear'))
print res

#delete a specific order by order_id
#first, let's create an sell order
#sell 10 dogecoins at price 0.01
params = {'market': 'dogcny', 'side': 'sell', 'volume': 12, 'price': 0.01}
res = client.post(get_api_path('orders'), params)
print res
order_id = res['id']

#delete this order
params = {"id": order_id}
res = client.post(get_api_path('delete_order'), params)

#create multi orders
params = {'market': 'dogcny', 'orders': [{'side': 'buy', 'volume': 12, 'price': 0.0002}, {'side': 'sell', 'volume': 11, 'price': 0.01}]}
res = client.post(get_api_path('multi_orders'), params)

```

## More demos ##

### for more usage demos, checkout [demo.py](https://github.com/JohnnyZhao/peatio-client-python/blob/master/demo.py) file ###

## Contribute ##

Pull requests are welcomed
