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

### /api/v1/balances/users/{userId}
---
##### ***GET***
**Summary:** Obtain balances of all currencies on hand by User IDs

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| userId | path | 20 | Yes | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | OK | [Result](#result) |

**Security**

| Security Schema | Scopes |
| --- | --- |
| Authorization | global |

### /api/v1/balances/users/{userId}/currencies/{currencyCode}
---
##### ***GET***
**Summary:** Obtain balance by User ID and Currency

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| userId | path | 20 | Yes | string |
| currencyCode | path | BTC | Yes | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | OK | [Result](#result) |

**Security**

| Security Schema | Scopes |
| --- | --- |
| Authorization | global |

### /api/v1/balances/users/{userId}/currencyTypes/{currencyType}
---
##### ***GET***
**Summary:** Obtain balances of all currencies on hand by User IDs and currency type

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| userId | path | 20 | Yes | string |
| currencyType | path | coin/fiat | Yes | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | OK | [Result](#result) |

**Security**

| Security Schema | Scopes |
| --- | --- |
| Authorization | global |

### /api/v1/coin-pair
---
##### ***GET***
**Summary:** Obtain currency info

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | OK | [Result](#result) |

**Security**

| Security Schema | Scopes |
| --- | --- |
| Authorization | global |

### /api/v1/favorites
---
##### ***GET***
**Summary:** 查询用户自选

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | OK | [Result](#result) |

**Security**

| Security Schema | Scopes |
| --- | --- |
| Authorization | global |

### /api/v1/favorites/
---
##### ***POST***
**Summary:** 保存自选

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| favoritesModel | body | favoritesModel | Yes | [FavoritesModel](#favoritesmodel) |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | OK | [Result](#result) |

**Security**

| Security Schema | Scopes |
| --- | --- |
| Authorization | global |

### /api/v1/favorites/default
---
##### ***GET***
**Summary:** 查询默认自选

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | OK | [Result](#result) |

**Security**

| Security Schema | Scopes |
| --- | --- |
| Authorization | global |

### /api/v1/favorites/{pair}
---
##### ***POST***
**Summary:** 用户增加/删除自选

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| pair | path | BTCUSDT | Yes | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | OK | [Result](#result) |

**Security**

| Security Schema | Scopes |
| --- | --- |
| Authorization | global |

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

### /api/v1/users/detail/export
---
##### ***GET***
**Summary:** export user detail history order

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

### /api/v1/users/login
---
##### ***POST***
**Summary:** Login a user

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| username | query | Login username | Yes | string |
| password | query | Login password | Yes | string |

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

### /api/v1/version
---
##### ***POST***
**Summary:** Query platform version

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| platform | query | platform | Yes | string |
| version | query | version | Yes | string |
| packageSize | query | packageSize | Yes | string |
| acceptLanguage | query | acceptLanguage | Yes | string |
| releaseNote | query | releaseNo | Yes | string |
| isForce | query | isForce | No | boolean |
| updateUrl | query | updateUrl | Yes | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | OK | [Result](#result) |

**Security**

| Security Schema | Scopes |
| --- | --- |
| Authorization | global |

### /api/v1/version/{version}/{platform}
---
##### ***GET***
**Summary:** Query platform version

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| version | path | 1.1.1 | Yes | string |
| platform | path | IOS/Android | Yes | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | OK | [Result](#result) |

**Security**

| Security Schema | Scopes |
| --- | --- |
| Authorization | global |

### Models
---

### FavoritesModel  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| favorites | [ string ] |  | No |

### Result  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| code | integer | Status code | Yes |
| data | object | Return data | No |
| details | object | Error details | No |
| message | string | Return message | No |
| timestamp | string | Time stamp | No |
