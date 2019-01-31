RESTFul Services
================
AAX coin2coin Exchange REST API

**Version:** 1.0

**Terms of service:**  
http://www.atomintl.com

**Contact information:**  
atomintl  
www.atomintl.com  
atomintl at atomintl.com  

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

**Version:** 1.0  

## Overview
All websocket data can be accessed via wss://{example_host}/ws/1/{streamName1}/{streamName2}

One or multiple streams can be subscribed in each connection. There are different streams for different market data and each has independent update intervals. The followings are a list of streams available:

- Orderbook (snapshot)
- Trades
- Tickers (real-time)
- Candlesticks (real-time)


## Orderbook Stream (snapshot)
  
Snapshot of the top N<sup>1</sup> bids and asks, updated every N<sup>2</sup> milliseconds.

- **Stream Name:** {symbol}@book_{level}
- **Supported levels (N<sup>1</sup>):** 20, 50
- **Update interval (N<sup>2</sup>):** 300 ms
- **Example:** BTCUSDT@book_50

**Example event**
```
{
  “e”: “BTCUSDT@book_50”,
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
  
Individual trades when an order is executed.

- **Stream Name:** {symbol}@trade
- **Example:** BTCUSDT@trade

**Example event**
```
{
  “e”: “BTCUSDT@trade”,
  "t": 123456789000,    // Event time (milliseconds)
  "p": “6573.2",        // Price (Buy: positive, Sell: negative) e.g. -6573.2 for Sell
  "q": “15"             // Quantity
}
```

## Candlesticks Stream (real-time)
  
Real-time candlesticks.

- **Stream Name:** {symbol}@{timeframe}_candles
- **Supported timeframes:** 1m, 3m, 5m, 15m, 30m, 1h, 2h, 3h, 4h, 8h, 1d
- **Update interval:** 1 second
- **Example:** BTCUSDT@1m_candles

**Example event**
```
{
    “e”: "BTCUSDT@1m_candles”,
    "t": 123456789000,    // Event time (milliseconds)
    "s": “123456789",     // start time of the candlestick (seconds)
    "o": “6573.2",        // Open price
    "h": “6573.2",        // High price
    "l": “6573.2",        // Low price
    "c": “6573.2",        // Close price
    "v": “1500",          // Traded volume
}
```

## All Tickers Stream
  
Summary of all available symbols. It contains open, high, low, close and volumes of the last 24hrs.
Server initially sends all the tickers to client immediately after connected, and then it sends only the tickers that are changed since last update every N seconds. 

- **Stream Name:** tickers
- **Update interval (N):** 2 seconds

**Example event**
```
{
    “e”: "tickers”,
    "tickers" : [
      {
        "s": “BTCUSDT",       // Symbol   
        "o": “6573.2",        // Open price
        "h": “6573.2",        // High price
        "l": “6573.2",        // Low price
        "c": “6573.2",        // Close price
        "v": “1500",          // Traded volume
      }    
    ]
}
// Notes:
// 24 hrs change = ((close-open)/open) * 100.0
```
