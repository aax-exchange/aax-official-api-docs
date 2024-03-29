RESTFul Services
================
AAX coin2coin Exchange REST API

**Version:** 1.0

**Terms of service:**  
http://www.aax.com

**Contact information:**  
atomintl  
www.aax.com  
atomintl at aax.com  

### Security
---
**Authorization**  

|apiKey|*API Key*|
|---|---|
|Name|Authorization|
|In|header|



### /api/v1/orders
---
##### ***POST***
**Summary:** Place an order

**Description:** The result/status should be obtained by querying user's order history

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| type | query | MARKET / LIMIT / STOP-LIMIT | Yes | string |
| symbol | query | BTCUSD | Yes | string |
| price | query | 6719.89 | No | string |
| quantity | query | 1000.01 | Yes | string |
| baseCurrency | query | BTC | Yes | string |
| quoteCurrency | query | USD | Yes | string |
| side | query | BUY / SELL | Yes | string |
| stopPrice | query | 7000.00 | No | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | OK | [Result](#result) |

**Security**

| Security Schema | Scopes |
| --- | --- |
| Authorization | global |

### /api/v1/orders/cancel/{orderId}
---
##### ***POST***
**Summary:** Cancel an order

**Description:** The OMS will be notified for the cancellation as well

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| orderId | path | 88a9da4f-4ad7-483d-b24b-1a42d7672ee6 | Yes | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | OK | [Result](#result) |

**Security**

| Security Schema | Scopes |
| --- | --- |
| Authorization | global |

### /api/v1/users/detail
---
##### ***GET***
**Summary:** Query the detail orders for current logged-in user

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| pageNo | query | pageNo | No | integer |
| clientOrderNo | query | clientOrderNo | No | string |
| baseCurrency | query | baseCurrency | No | string |
| quoteCurrency | query | quoteCurrency | No | string |
| startDate | query | startDate | No | dateTime |
| endDate | query | endDate | No | dateTime |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | OK | [Result](#result) |

**Security**

| Security Schema | Scopes |
| --- | --- |
| Authorization | global |



### /api/v1/users/my-orders
---
##### ***GET***
**Summary:** Query the historical order of the current logged in user

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| searchType | query | searchType | No | integer |
| pageNo | query | pageNo | No | integer |
| baseCurrency | query | baseCurrency | No | string |
| quoteCurrency | query | quoteCurrency | No | string |
| side | query | side | No | string |
| status | query | status | No | integer |
| startDate | query | startDate | No | dateTime |
| endDate | query | endDate | No | dateTime |
| userId | query | userId | No | string |
| realName | query | realName | No | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | OK | [Result](#result) |

**Security**

| Security Schema | Scopes |
| --- | --- |
| Authorization | global |

### /api/v1/users/my-orders/export
---
##### ***GET***
**Summary:** export orders of the current logged in user

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| searchType | query | searchType | No | integer |
| pageNo | query | pageNo | No | integer |
| baseCurrency | query | baseCurrency | No | string |
| quoteCurrency | query | quoteCurrency | No | string |
| side | query | side | No | string |
| status | query | status | No | integer |
| startDate | query | startDate | No | dateTime |
| endDate | query | endDate | No | dateTime |
| userId | query | userId | No | string |
| realName | query | realName | No | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | OK | [Result](#result) |

**Security**

| Security Schema | Scopes |
| --- | --- |
| Authorization | global |

### /api/v1/users/order-history/{status}/{pageNo}
---
##### ***GET***
**Summary:** Query the status/info of the historical orders for current logged-in user

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| status | path | status | Yes | integer |
| pageNo | path | pageNo | Yes | integer |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | OK | [Result](#result) |

**Security**

| Security Schema | Scopes |
| --- | --- |
| Authorization | global |

### /api/v1/users/orders/{status}/{pageNo}
---
##### ***GET***
**Summary:** Obtain the status/info of the orders being processed for current logged-in user

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| status | path | status | Yes | integer |
| pageNo | path | pageNo | Yes | integer |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | OK | [Result](#result) |

**Security**

| Security Schema | Scopes |
| --- | --- |
| Authorization | global |

### /api/v1/users/profile
---
##### ***GET***
**Summary:** Obtain user profile

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | OK | [Result](#result) |

**Security**

| Security Schema | Scopes |
| --- | --- |
| Authorization | global |



Market Data Services
================
Websocket APIs

**Version:** 2.0  

## Overview
All websocket data can be accessed via wss://{example_host}/ws/2/{streamName1}/{streamName2}

One or multiple streams can be subscribed in each connection. There are different streams for different market data and each has independent update intervals. The followings are a list of streams available:

- Orderbook    (snapshot & fast snapshot)
- Trades       (real-time & near-real-time)
- Tickers      (real-time)
- Candlesticks (real-time)

Notes: The number of streams on the URL is limited to 5 (including 5)

All streams are also available in restful APIs via https://{example_host}/{streamName}?limit=100, with one additional stream for recently traded list as shown below:

**Example trades event**
```
{
  "e": "BTCUSDT@trades",
  "trades": [      
    {
      "t": 123456789000,    // trade time (milliseconds)
      "p": "6573.2",        // Price (Buy: positive, Sell: negative) e.g. -6573.2 for Sell
      "q": "15"             // Quantity
    }
  ]
}
```

## Subscribe streams
Instead of specifying stream names in the URL, you can also subscribe and unsubscribe any streams on-demand, by sending:

**Example**
```
{"e":"subscribe","stream":"BTCUSDT@book_50"}
or
{"e":"unsubscribe","stream":"BTCUSDT@book_50"}
```

Then you will receive a reply event:
```
{"e":”reply”,"status":"ok","subscribe":"BTCUSDT@book_50"}
or
{"e":”reply”,"status":"error","unsubscribe":"BTCUSDT@book_50"}
```

## Empty event
Server may send empty event to client if there is nothing to send right after the connection is newly established.

**Example**
```
{"e":"empty"}
```

## System event
Server may send system event to client to indicate a system status change. Possible status are:

- active (System is active and normal)
- inactive (Market data is not available)

**Example**
```
{"e":"system","status":[{"spots":"active"},{"futures":"active"}]}
or
{"e":"system","status":[{"all":"active"}]}
```


## Orderbook Stream (snapshot)
  
Snapshot of the top N<sup>1</sup> bids and asks, updated every N<sup>2</sup> milliseconds.

- **Stream Name:** {symbol}@book_{level}
- **Supported levels (N<sup>1</sup>):** 20, 50
- **Update interval (N<sup>2</sup>):** 300 ms
- **Example:** BTCUSDT@book_50
- [Restful API Demo](https://api.aax.com/marketdata/v1.1/BTCUSDT@book_50)

**Example event**
```
{
  "e": "BTCUSDT@book_50",
  "t": 123456789000,    // Event time (milliseconds)
  "bids": [             // Bids to be updated
    [
      "0.0024",         // price level to be updated
      "10"              // quantity
    ]
  ],
  "asks": [             // Asks to be updated
    [
      "0.0026",         // price level to be updated
      "100"             // quantity
    ]
  ]
}
```


## Orderbook Stream (fast snapshot)
  
Snapshot of the top N<sup>1</sup> bids and asks, updated every N<sup>2</sup> milliseconds.

- **Stream Name:** {symbol}@fast_book_{level}
- **Supported levels (N<sup>1</sup>):** 20, 50
- **Update interval (N<sup>2</sup>):** 100 ms
- **Example:** BTCUSDT@fast_book_50
- [Restful API Demo](https://api.aax.com/marketdata/v1.1/BTCUSDT@fast_book_50)

**Example event**
```
{
  "e": "BTCUSDT@fast_book_50",
  "t": 123456789000,    // Event time (milliseconds)
  "bids": [             // Bids to be updated
    [
      "0.0024",         // price level to be updated
      "10"              // quantity
    ]
  ],
  "asks": [             // Asks to be updated
    [
      "0.0026",         // price level to be updated
      "100"             // quantity
    ]
  ]
}
```


## Trades Stream
  
Individual trades when an order is executed. For each new connection, server shall send the last 50 trades to it. There is a rate limit of how many trades server will send to clients.

Always this trade stream updated every 300ms milliseconds.

- **Stream Name:** {symbol}@trade
- **Example:** BTCUSDT@trade
- [Restful API Demo (last trade)](https://api.aax.com/marketdata/v1.1/BTCUSDFP@trade)
- [Restful API Demo (multiple trades)](https://api.aax.com/marketdata/v1.1/BTCUSDFP@trades?limit=2000)

**Example event**
```
{
  "e": "BTCUSDT@trade",
  "t": 1631675297816,    // Event time (milliseconds)
  "p": "46573.2",        // Price (Buy: positive, Sell: negative) e.g. -6573.2 for Sell
  "q": "1.5",            // Quantity
  "s": "buy",            // Direction (buy/sell for spot, long/short for futures)
  "i": "T1iO5HeaDC"      // Trade ID  
}
```

## Trades Stream (real-time)
  
Individual trades when an order is executed. For each new connection, server never send prev old trades to it. This is a realtime stream that sends the realtime-trade since client connected.

Notes: This stream is only open to IP whitelists.

- **Stream Name:** {symbol}@fast_trade
- **Example:** BTCUSDT@fast_trade
- [Restful API Demo (last trade)](https://api.aax.com/marketdata/v1.1/BTCUSDT@fast_trade)

**Example event**
```
{
  "e": "BTCUSDT@fast_trade",
  "t": 1631675297816,    // Event time (milliseconds)
  "p": "46573.2",        // Price (Buy: positive, Sell: negative) e.g. -6573.2 for Sell
  "q": "1.5",            // Quantity
  "s": "buy",            // Direction (buy/sell for spot, long/short for futures)
  "i": "T1iO5HeaDC"      // Trade ID
}
```

## Candlesticks Stream (real-time)
  
Real-time candlesticks.

- **Stream Name:** {symbol}@{timeframe}_candles
- **Supported timeframes:** 1m, 3m, 5m, 15m, 30m, 1h, 2h, 3h, 4h, 8h, 1d
- **Update interval:** 1 second
- **Example:** BTCUSDT@1m_candles
- [Restful API Demo](https://api.aax.com/marketdata/v1.1/BTCUSDT@1m_candles)

**Example event**
```
{
    "e": "BTCUSDT@1m_candles",
    "t": 123456789000,    // Event time (milliseconds)
    "s": “123456789",     // start time of the candlestick (seconds)
    "o": “6573.2",        // Open price
    "h": “6573.2",        // High price
    "l": “6573.2",        // Low price
    "c": “6573.2",        // Close price
    "v": “1500",          // Traded volume (price x qty for spot, qty for futures)
}
```

**Example case 1**

Below is an example of data sent from server, whenever price changed within 15 minutes (in this example), server shall push new data for the same candlestick, see the 2nd message in the example. Until time expired and another candlestick created, see the 3rd message.

Volume is the accumulated volume traded since the start time of a candlestick.
```
{"c":"3603.40000000","e":"BTCUSDT@15m_candles","h":"3603.50000000","l":"3329.60000000","o":"3329.60000000","s":1550198700,"t":1550198911,"v":"97.65297000"}
{"c":"3604.30000000","e":"BTCUSDT@15m_candles","h":"3604.30000000","l":"3329.60000000","o":"3329.60000000","s":1550198700,"t":1550199187,"v":"195.32950000"}
{"c":"3604.30000000","e":"BTCUSDT@15m_candles","h":"3604.30000000","l":"3604.30000000","o":"3604.30000000","s":1550199600,"t":1550199600,"v":"0.00000000"}
```

## Tickers Stream
  
Summary of all available symbols. It contains open, high, low, close and volumes of the last 24hrs.
Server initially sends all the tickers to client immediately after connected, and then it sends only the tickers that are changed since last update every N seconds. 

- **Stream Name:** tickers
- **Update interval (N):** 2 seconds
- [Restful API Demo](https://api.aax.com/marketdata/v1.1/tickers)

**Example event**
```
{
    "e": "tickers",
    "t": 123456789000,    // Event time (milliseconds)    
    "tickers" : [
      {
        "s": “BTCUSDT",       // Symbol   
        "o": "6573.2",        // Open price
        "h": "6573.2",        // High price
        "l": "6573.2",        // Low price
        "c": "6573.2",        // Close price
        "v": "1500",          // Quote volume (price x qty for spot, qty for futures)
        "a": "9859500",       // Volume amount in USD
        "d": "2.361"          // Difference in percentages ((close-open)/open) * 100.0
      }    
    ]
}
```


## MDS Inbound Requests
  
MDS can accept inbound requests for:
 - Index Price
 - Mark Price


Index Price example request:
```
curl -d '{"time": 1564143433, "symbol": "BTCUSDFP", "index": 9000.12}' -H 'content-type: application/json;' http://127.0.0.1:2345/v1/futures/index
```

Mark Price example request:
```
curl -d '{"time": 1564143433, "symbols": {"BTCUSDFP": 9000.12,"ETHUSDFP": 200.12}}' -H 'content-type: application/json;' http://127.0.0.1:2345/v1/futures/mark
```

## Index Price Stream
  

- **Stream Name:** {symbol}_INDEX@{timeframe}_candles
- **Supported timeframes:** 1m, 3m, 5m, 15m, 30m, 1h, 2h, 3h, 4h, 8h, 1d
- **Update interval:** 1 second
- **Example:** BTCUSDFP_INDEX@1m_candles
- [Restful API Demo](https://api.aax.com/marketdata/v1.1/EOSBTC_INDEX@1m_candles)

**Example event**
```
{
    "e": "BTCUSDFP_INDEX@1m_candles",
    "t": 123456789000,    // Event time (milliseconds)
    "s": "123456789",     // start time of the candlestick (seconds)
    "o": "6573.2",        // Open price
    "h": "6573.2",        // High price
    "l": "6573.2",        // Low price
    "c": "6573.2",        // Close price
    "v": "1500",          // Traded volume (price x qty for spot, qty for futures)
}
```

## Mark Price Stream
  

- **Stream Name:**  {symbol}@mark
- **Update interval:** Variable
- **Example:** BTCUSDFP@mark
- [Restful API Demo](https://api.aax.com/marketdata/v1.1/BTCUSDFP@mark)

**Example event**
```
{
  "e":"BTCUSDFP@mark",  // event name
  "p":"9000.12000000",  // price
  "t":1572858173963     // Event time (milliseconds)
}
```

## Delta Order Book
  

Order book changes of the top N<sup>1</sup> bids and asks, updated every N<sup>2</sup> milliseconds. If the quantity is 0, remove that price level. If the same price level exists in client's application, update the latest quantity. There is no guarantee the price levels are in any order. It is guaranteed that after merging each message, the bid and ask sides shall not exceed N<sup>1</sup> levels. Make sure you clear your local copy of the order book on re-connection. The first message is guaranteed to be a snapshot of the whole book of top N<sup>1</sup> levels, subsequent messages are always delta updates.

- **Stream Name:** {symbol}@delta_book.{level}
- **Supported levels (N<sup>1</sup>):** 50
- **Update interval (N<sup>2</sup>):** 300 ms (default)
- **Example:** BTCUSDT@delta_book.50
- [Restful API Demo](https://api.aax.com/marketdata/v1.1/BTCUSDFP@delta_book.50)

**Example event**
```
{
  "e":"BTCUSDT@delta_book.50",              // event name
  "bids": [ [9000.12345678, 0.123456] ],    // array of price and qty on bid side
  "asks": [ [9001, 0.83] ],                 // array of price and qty on ask side
  "t":1572858173963,                        // Event time (milliseconds)
  "is_snapshot": true                       // snapshot flag (The first message only)
}
```

## Delta Order Book (fast)

Same as the above'Delta Order Book'. Except the stream name and the update interval.

- **Stream Name:** {symbol}@delta_book_fast
- **Supported levels (N<sup>1</sup>):** 50
- **Update interval (N<sup>2</sup>):** 2 ms (default)
- **Example:** BTCUSDT@delta_book_fast


## Historical Candlesticks

Parameters:
- **symbol** Compulsory
- **timeframe** Compulsory
- **start - timestamp of the first candlestick** Optional
- **end - timestamp of the last candlestick** Optional
- **count - number of candlesticks** Optional

Parameter combinations:
- **start + end:** 
- **count + end:** 

**Example Response**
```
{"data":[
  // each element in the array is an array of open,high,low,close,volume,start_time_of_the_candlestick
  //
  [2.3014,2.3014,2.2925,2.2925,998965.396659,1592540760],  // first candlestick
  [2.2925,2.3014,2.2925,2.3014,2034506.3287,1592540820]    // 2nd candlestick and so on..
 ],
 "success":true,  // whether the request is accepted and successful
 "t":1592979595   // the generation time of this response
 }


