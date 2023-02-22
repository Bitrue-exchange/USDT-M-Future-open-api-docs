# Basic Information

## API Basic Information

* Base endpoint is https://fapi.bitrue.com
* All endpoints return either a JSON object or array. 
* Data is returned in reverse order. Newest first, oldest last.
* All time and timestamp related fields are in milliseconds.

## HTTP Error Codes

* HTTP 4XX return codes are used for malformed requests; the issue is on the sender's side.
* HTTP 429 return code is used when breaking a request rate limit.
* HTTP 418 return code is used when an IP has been auto-banned for continuing to send requests after receiving 429 codes.
* HTTP 5XX return codes are used for internal errors
* HTTP 504 return code is used when the API successfully sent the message but did not get a response within the timeout period. It is important to NOT treat this as a failure operation; the execution status is UNKNOWN and could have been a success.
* All endpoints can possibly return an ERROR, the error payload is as follows:

``` json
{
  "code": -1121,
  "msg": "Invalid symbol."
}
```


## General Information

* All requests are based on the Https protocol, and the Content-Type in the request header information needs to be uniformly set to:'application/json'
* For the interface of the GET method, the parameters must be sent in the query string
* For the interface of the POST method, the parameters must be sent in the request body
* Parameters may be sent in any order.


## LIMITS

* There will be a limited frequency description below each interface.
* A 429 will be returned when either rate limit is violated.

## Endpoint Security Type

* Each endpoint has a security type that determines the how you will interact with it.
* API-keys are passed into the Rest API via the `X-CH-APIKEY` header.
* API-keys and secret-keys **are case sensitive**.

| Security Type                   |   Description                                            |
| ------------------------------- | -------------------------------------------------------- |
| NONE                            | Endpoint can be accessed freely.                         |
| TRADE                           | Endpoint requires sending a valid API-Key and signature. |
| USER_DATA                       | Endpoint requires sending a valid API-Key and signature. |
| USER_STREAM                     | Endpoint requires sending a valid API-Key.               |
| MARKET_DATA                     | Endpoint requires sending a valid API-Key.               |


## SIGNED (TRADE and USER_DATA) endpoint security

* When calling the `TRADE` or `USER_DATA` interface, the signature parameter should be passed in the `X-CH-SIGN` field in the HTTP header.
* The signature uses the HMAC SHA256 algorithm. The `API-Secret` corresponding to the `API-KEY` is used as the HMAC SHA256 key.
* The request header of `X-CH-SIGN` is based on timestamp + method + requestPath + body string  (+ means string connection) as the operation object
* The value of timestamp is the same as the `X-CH-TS` request header, method is the request method, and the letters are all uppercase: `GET/POST`
* requestPath is the request interface path. For example: /fapi/v1/order
* body is the string of the request body (post only)
* The signature is **not case sensitive**

## Timing Security

* The signature interface needs to pass the timestamp in the `X-CH-TS` field in the HTTP header, and its value should be the unix timestamp of the request sending time e.g. `1528394129373`
* An additional parameter, `recvWindow`, may be sent to specify the number of milliseconds after timestamp the request is valid for. If `recvWindow` is not sent, **it defaults to 5000**.
* In addition, if the server calculates that the client's timestamp is more than one second ‘in the future’ of the server’s time, it will also reject the request.
* The logic is as follows:

``` java
if (timestamp < (serverTime + 1000) && (serverTime - timestamp) <= recvWindow) {
  // process request
} else {
  // reject request
}
```

* Serious trading is about timing.  Networks can be unstable and unreliable, which can lead to requests taking varying amounts of time to reach the servers. With recvWindow, you can specify that the request must be processed within a certain number of milliseconds or be rejected by the server. 

* **It recommended to use a small recvWindow of 5000 or less!**

## SIGNED Endpoint Examples for POST /fapi/v1/order

Here is a step-by-step example of how to send a vaild signed payload from the Linux command line using `echo`, `openssl`, and `curl`.


| Key                             | Value                               |
| ------------------------------- | ----------------------------------- |
| apiKey                          | vmPUZE6mv9SD5V5e14y7Ju91duEh8A      |
| secretKey                       | 902ae3cb34ecee2779aa4d3e1d226686    |


| Parameter                       | Value                               |
| ------------------------------- | ----------------------------------- |
| symbol                          | BTCUSDT                             |
| side                            | BUY                                 |
| type                            | LIMIT                               |
| volume                          | 1                                   |
| price                           | 9300                                |

## Signature example

* body: 

``` json
{"symbol":"BTCUSDT","price":"9300","volume":"1","side":"BUY","type":"LIMIT"}
```

* HMAC SHA256 Signature:

``` shell
[linux]$ echo -n "1588591856950POST/sapi/v1/order/test{\"symbol\":\"BTCUSDT\",\"price\":\"9300\",\"volume\":\"1\",\"side\":\"BUY\",\"type\":\"LIMIT\"}" | openssl dgst -sha256 -hmac "902ae3cb34ecee2779aa4d3e1d226686"
(stdin)= c50d0a74bb9427a9a03933d0eded03af9bf50115dc5b706882a4fcf07a26b761
```

* Curl command :
``` shell
  [linux]$ curl -H "X-CH-APIKEY: c3b165fd5218cdd2c2874c65da468b1e" -H "X-CH-SIGN: c50d0a74bb9427a9a03933d0eded03af9bf50115dc5b706882a4fcf07a26b761" -H "X-CH-TS: 1588591856950" -H "Content-Type:application/json" -X POST 'http://fapi.bitrue.com/fapi/v1/order/test' -d '{"symbol":"BTCUSDT","price":"9300","quantity":"1","side":"BUY","type":"LIMIT"}'
 ```

# Example
Demo for Bitrue Futures Open APIs:
[Java](https://github.com/Bitrue-exchange/futures_api_examples)
[Python](https://github.com/Bitrue-exchange/futures_api_examples)


# Public API

## Security: None

Endpoints under Public section can be accessed freely **without** requiring any `API-key` or `signature`

#### /fapi/v1/ping



This endpoint checks connectivity to the host

###### parameters

###### response

``` json
{}
```

#### /fapi/v1/time

Security: None
Endpoints under Public section can be accessed freely **without** requiring any `API-key` or `signature`

This endpoint  check server Time

###### parameters

###### response

``` json
{
    "serverTime":1607702400000,
    "timezone":"Coordinated Universal Time"
}
```

| name                    | type              | example                                | description              |
| ----------------------- | ----------------- | -------------------------------------- | ------------------------ |
| serverTime              | long              | 1607702400000                          | server timestamp         |
| timezone                | string            | Coordinated Universal Time             | server time zone         |


#### /fapi/v1/contracts

Security: None
Endpoints under Public section can be accessed freely **without** requiring any `API-key` or `signature`

This endpoint checks server Time

###### parameters

###### response

``` json
[
    {
        "symbol": "H-HT-USDT",
        "pricePrecision": 8,
        "side": 1,
        "maxMarketVolume": 100000,
        "multiplier": 6,
        "minOrderVolume": 1,
        "maxMarketMoney": 10000000,
        "type": "H",
        "maxLimitVolume": 1000000,
        "maxValidOrder": 20,
        "multiplierCoin": "HT",
        "minOrderMoney": 0.001,
        "maxLimitMoney": 1000000,
        "status": 1
    }
]
```

| name                    | type              | example                  | description                          |
| ----------------------- | ----------------- | ------------------------ | ------------------------------------ |
| symbol                  | string            | E-BTC-USDT               | Contract name                        |
| status                  | number            | 1                        | status (0:cannot trade, 1:can trade) |
| type                    | string            | S                        | contract type, E: perpetual contract, S: test contract, others are mixed contract  |
| side                    | number            | 1                        | Contract direction(backwards：0，forwards:1) |
| multiplier              | number            | 0.5                      | Contract face value                   |
| multiplierCoin          | string            | BTC                      | Contract face value unit              |
| pricePrecision          | number            | 4                        | Precision of the price                | 
| minOrderVolume          | number            | 10                       | Minimum order volume                  |
| minOrderMoney           | number            | 10                       | Minimum order value                   |
| maxMarketVolume         | number            | 100000                   | Market price order maximum volume     |
| maxMarketMoney          | number            | 100000                   | Market price order maximum value      |
| maxLimitVolume          | number            | 100000                   | Limit price order maximum volume      |
| maxValidOrder           | number            | 100000                   | Maximum valid order quantity          |


# Market

## Security: None

Market section can be accessed freely **without** requiring any `API-key` or `signature`.

#### /fapi/v1/depth

Market depth data  

###### Parameters

| name                  | type          | memo                                    |
| --------------------- | ------------- | --------------------------------------- |
| limit                 |  integer      |  Default 100, Max 100                   |
| contractName         |  string       |  Contract Name E.g. E-BTC-USDT          |

###### Response

``` json
{
  "bids": [
    [
      "3.90000000",   // price
      "431.00000000"  // quantity
    ],
    [
      "4.00000000",
      "431.00000000"
    ]
  ],
  "asks": [
    [
      "4.00000200",  // price
      "12.00000000"  // quantity
    ],
    [
      "5.10000000",
      "28.00000000"
    ]
  ]
}
```

| name                    | type              | example                  | description                          |
| ----------------------- | ----------------- | ------------------------ | ------------------------------------ |
| time                    | long              | 1595563624731            | Current Timestamp  (ms)              |
| bids                    | list              | Look below               | Order book purchase info             |
| asks                    | list              | Look below               | Order book selling info              |


The fields bids and asks are lists of order book price level entries, sorted from best to worst.

| name                    | type              | example                  | description                          |
| ----------------------- | ----------------- | ------------------------ | ------------------------------------ |
| ' '                     | float             | 131.1                    | Price level                          |
| ' '                     | float             | 2.3                      | Total order quantity for this price level |


#### /fapi/v1/ticker

24 hour price change statistics

###### Parameters

| name                  | type          | memo                                    |
| --------------------- | ------------- | --------------------------------------- |
| contractName         |  string       |  Contract Name E.g. E-BTC-USDT          |

###### Response

``` json
{
    "high": "9279.0301",
    "vol": "1302",
    "last": "9200",
    "low": "9279.0301",
    "rose": "0",
    "time": 1595563624731
}
```

| name                    | type              | example                  | description                          |
| ----------------------- | ----------------- | ------------------------ | ------------------------------------ |
| time                    | long              | 1595563624731            | Open time                            |
| high                    | float             | 9900                     | Highest price                         |
| low                     | float             | 8800.34                  | Lowest price                          |
| last                    | float             | 8900                     | Newest price                         | 
| vol                     | float             | 4999                     | Trade volume                         |
| rose                    | string            | +0.5                     | Price variation                      |


#### /fapi/v1/klines

kline/charts data

###### Parameters

| name                  | type          | memo                                    |
| --------------------- | ------------- | --------------------------------------- |
| contractName          |  string       | Contract Name E.g. E-BTC-USDT           |
| interval              | string        | Identifies the sent value as: 1min,5min,15min,30min,1h,1day,1week,1month |
| limit                 | integer       | Default 100, Max 300                    |


###### Response

``` json
[
    {
        "high": "6228.77",
        "vol": "111",
        "low": "6228.77",
        "idx": 1594640340,
        "close": "6228.77",
        "open": "6228.77"
    },
    {
        "high": "6228.77",
        "vol": "222",
        "low": "6228.77",
        "idx": 1587632160,
        "close": "6228.77",
        "open": "6228.77"
    },
    {
        "high": "6228.77",
        "vol": "333",
        "low": "6228.77",
        "idx": 1587632100,
        "close": "6228.77",
        "open": "6228.77"
    }
]
```

| name                    | type              | example                  | description                          |
| ----------------------- | ----------------- | ------------------------ | ------------------------------------ |
| idx                     | long              | 1595563624731            | Start timestamp(ms)                  |
| high                    | float             | 9900                     | Higher price                         |
| low                     | float             | 8800.34                  | Lower price                          |
| close                   | float             | 8900                     | Close price                         | 
| vol                     | float             | 4999                     | Trade volume                         |


# Trading

## Security: TRADE​

All interfaces under the transaction require `signature` and `API-key` verification​​


#### /fapi/v1/order (POST)

Creation of single new orders

###### Parameters

* Header:

| name                  | type          | memo                                    |
| --------------------- | ------------- | --------------------------------------- |
| X-CH-TS               | string        | Time stamp                              |
| X-CH-APIKEY           | string        | Your API-key                            |
| X-CH-SIGN             | string        | Signature                               |


* Body:

| name                  | type          | memo                                    |
| --------------------- | ------------- | --------------------------------------- |
| volume                | integer       | Order quantity                          |
| price                 | number        | Order price                             |
| contractName          | string        | Contract name E.g. E-BTC-USDT           |
| type                  | string        | Order type, LIMIT/MARKET                |
| side                  | string        | trade direction, BUY/SELL               |
| open                  | string        | Open balancing direction, OPEN/CLOSE    |
| positionType          | number        | Hold-up position, 1 full position, 2 restrictive position           |
| clientOrderId         | string        | Client order identity, a string with length less than 32 bit        |
| timeInForce           | string        | LIMIT / MARKET                         |


###### Response:

``` json
{
    "orderId": 256609229205684228
}
```


#### /fapi/v1/cancel (POST)

Cancel order. 
Rate limit: 20 times/ 2 seconds

###### Parameters

* Header:

| name                  | type          | memo                                    |
| --------------------- | ------------- | --------------------------------------- |
| X-CH-TS               | string        | Time stamp                              |
| X-CH-APIKEY           | string        | Your API-key                            |
| X-CH-SIGN             | string        | Signature                               |


* Body:

| name                  | type          | memo                                    |
| --------------------- | ------------- | --------------------------------------- |
| contractName          | string        | Contract name E.g. E-BTC-USDT           |
| orderId               | string        | Order Id                                |



###### Response:

``` json
{
    "orderId": 256609229205684228
}
```

#### /fapi/v1/openOrders (GET)

Open orders

retrieve all open order in a contract name.

###### Parameters

* Header:

| name                  | type          | memo                                    |
| --------------------- | ------------- | --------------------------------------- |
| X-CH-TS               | string        | Time stamp                              |
| X-CH-APIKEY           | string        | Your API-key                            |
| X-CH-SIGN             | string        | Signature                               |


* Query:

| name                  | type          | memo                                    |
| --------------------- | ------------- | --------------------------------------- |
| contractName          | string        | Contract name E.g. E-BTC-USDT           |




###### Response:

``` json
[
    {
       "side": "BUY",
       "executedQty": 0,
       "orderId": 259396989397942275,
       "price": 10000.0000000000000000,
       "origQty": 1.0000000000000000,
       "avgPrice": 0E-8,
       "transactTime": "1607702400000",
       "action": "OPEN",
       "contractName": "E-BTC-USDT",
       "type": "LIMIT",
       "status": "INIT"
    }
]
```


| name                    | type              | example                  | description                          |
| ----------------------- | ----------------- | ------------------------ | ------------------------------------ |
| orderId                 | long | 150695552109032492 |  Order ID(system generated) |
| contractName            | string | E-BTC-USDT | Contract Name  |
| price                   | float | 4765.29  | Order price   |
| origQty                 | float | 1.01     | Order quantity   |
| executedQty             | float  | 1.01 | Filled orders quantity |
| avgPrice                | float  | 4754.24  | Filled orders average price |
| type                    | string | LIMIT    | Order type. Possible values can only be:LIMIT(limit price) and MARKET（market price）|
| side                    | string | BUY      |Order direction. Possible values can only be: BUY（buy long）and SELL（sell short）  |
| status                  | string | NEW      |Order status. Possible values are：NEW(new order，not filled),PARTIALLY_FILLED(partially filled), FILLED（fully filled, CANCELLED（already cancelled）and REJECTED（order rejected）|
| action                  | string | OPEN     | OPEN/CLOSE   |
| transactTime            | long |1607702400000 |Order creation time |


#### /fapi/v1/order (GET)

Order details


###### Parameters

* Header:

| name                  | type          | memo                                    |
| --------------------- | ------------- | --------------------------------------- |
| X-CH-TS               | string        | Time stamp                              |
| X-CH-APIKEY           | string        | Your API-key                            |
| X-CH-SIGN             | string        | Signature                               |


* Query:

| name                  | type          | memo                                    |
| --------------------- | ------------- | --------------------------------------- |
| contractName          | string        | Contract name E.g. E-BTC-USDT           |
| orderId               | string        | Order ID                                |




###### Response:

``` json
[
    {
       "side": "BUY",
       "executedQty": 0,
       "orderId": 259396989397942275,
       "price": 10000.0000000000000000,
       "origQty": 1.0000000000000000,
       "avgPrice": 0E-8,
       "transactTime": "1607702400000",
       "action": "OPEN",
       "contractName": "E-BTC-USDT",
       "type": "LIMIT",
       "status": "INIT"
    }
]

```


| name                    | type              | example                  | description                          |
| ----------------------- | ----------------- | ------------------------ | ------------------------------------ |
| orderId                 | long | 150695552109032492 |  Order ID（system generated）|
| contractName            | string | E-BTC-USDT | Contract Name  |
| price                   | float | 4765.29  | Order price   |
| origQty                 | float | 1.01     | Order quantity   |
| executedQty             | float  | 1.01 | Filled orders quantity |
| avgPrice                | float  | 4754.24  | Filled orders average price |
| type                    | string | LIMIT    | Order type. Possible values can only be:LIMIT(limit price) andMARKET（market price）|
| side                    | string | BUY      |Order direction. Possible values can only be：BUY（buy long）and SELL（sell short）  |
| status                  | string | NEW      |Order status. Possible values are：NEW(new order，not filled)、PARTIALLY_FILLED（partially filled）、FILLED（fully filled）、CANCELLED（already cancelled）andREJECTED（order rejected）|
| action                  | string | OPEN     | OPEN/CLOSE   |
| transactTime            | long |1607702400000 |Order creation time |


# Account

## Security: USER_DATA​

All interfaces under the account require `signature` and `API-key` verification​​


#### /fapi/v1/account (GET)

Account info

Rate limit rules: 20 times/2s


###### Parameters

* Header:

| name                  | type          | memo                                    |
| --------------------- | ------------- | --------------------------------------- |
| X-CH-TS               | string        | Time stamp                              |
| X-CH-APIKEY           | string        | Your API-key                            |
| X-CH-SIGN             | string        | Signature                               |



###### Response:

``` json
{
    "account": [
        {
            "marginCoin": "USDT",
            "accountNormal": 999.5606,
            "accountLock": 23799.5017,
            "partPositionNormal": 9110.7294,
            "totalPositionNormal": 0,
            "achievedAmount": 4156.5072,
            "unrealizedAmount": 650.6385,
            "totalMarginRate": 0,
            "totalEquity": 99964804.560,
            "partEquity": 13917.8753,
            "totalCost": 0,
            "sumMarginRate": 873.4608,
            "positionVos": [
                {
                    "contractId": 1,
                    "contractName": "E-BTC-USDT",
                    "contractSymbol": "BTC-USDT",
                    "positions": [
                        {
                            "id": 13603,
                            "uid": 10023,
                            "contractId": 1,
                            "positionType": 2,
                            "side": "BUY",
                            "volume": 69642.0,
                            "openPrice": 11840.2394,
                            "avgPrice": 11840.3095,
                            "closePrice": 12155.3005,
                            "leverageLevel": 24,
                            "holdAmount": 7014.2111,
                            "closeVolume": 40502.0,
                            "pendingCloseVolume": 0,
                            "realizedAmount": 8115.9125,
                            "historyRealizedAmount": 1865.3985,
                            "tradeFee": -432.0072,
                            "capitalFee": 2891.2281,
                            "closeProfit": 8117.6903,
                            "shareAmount": 0.1112,
                            "freezeLock": 0,
                            "status": 1,
                            "ctime": "2020-12-11T17:42:10",
                            "mtime": "2020-12-18T20:35:43",
                            "brokerId": 21,
                            "marginRate": 0.2097,
                            "reducePrice": 9740.8083,
                            "returnRate": 0.3086,
                            "unRealizedAmount": 2164.5289,
                            "openRealizedAmount": 2165.0173,
                            "positionBalance": 82458.2839,
                            "settleProfit": 0.4883,
                            "indexPrice": 12151.1175,
                            "keepRate": 0.005,
                            "maxFeeRate": 0.0025
                        }
                    ]
                }
            ]
        }
    ]
}

```



| name                    | type              | description                  |
| ----------------------- | ----------------- | ---------------------------- |
| account                 | []                | Balance collection           |


account field:

| name                    | type              | example                  | description                          |
| ----------------------- | ----------------- | ------------------------ | ------------------------------------ |
| marginCoin              | string            | USDT                     | Margin coin                          |
| accountNormal           | float             | 10.05                    | Balance account                      |
| accountLock             | float             | 10.07                    | Margin frozen account                |
| partPositionNormal      | float             | 10.07                    | Restricted position margin balance   |
| totalPositionNormal     | float             | 10.07                    | Full position initial margin         |
| achievedAmount          | float             | 10.07                    | Profit and losses occurred           |
| unrealizedAmount        | float             | 10.05                    | Unfilled profit and losses           |
| totalMarginRate         | float             | 10.05                    | Full position margin rate            |
| totalEquity             | float             | 10.07                    | Full position equity                 |
| partEquity              | float             | 10.07                    | Restricted position equity           |
| totalCost               | float             | 10.07                    | Full position costs                  |
| sumMarginRate           | float             | 10.07                    | All accounts margin rate             |
| positionVos             | [ ]               |                          | ​Position contract record             |

positionVos field:

| name                    | type              | example                  | description                          |
| ----------------------- | ----------------- | ------------------------ | ------------------------------------ |
| contractId              |  integer          | 2                        | Contract id                          |
| contractName            | string            | E-BTC-USDT               | Contract name                        |
| contractSymbol          | string            | BTC-USDT                 | Contract coin pair                   |
| positions               | [ ]               |                          | Position details                     |


positions field:


| name                    | type              | example                  | description                          |
| ----------------------- | ----------------- | ------------------------ | ------------------------------------ |
| closePrice              | float             | 1.05                     | Balancing average price              |
| leverageLevel           | float             | 1.05                     | Leverage multiple                    |
| holdAmount              | float             | 1.05                     | Hold position margin                 |
| closeVolume             | float             | 1.05                     | Balanced quantity                    |
| pendingCloseVolume      | float             | 1.05                     | The number of pending closing orders |
| realizedAmount          | float             | 1.05                     | Profit and losses occurred           |
| historyRealizedAmount   | float             | 1.05                     | Historic accumulated profit and losses | 
| tradeFee                | float             | 1.05                     | Trading fees                         |
| capitalFee              | float             | 1.05                     | Capital costs                        |
| closeProfit             | float             | 1.05                     | Balancing profit and loss            |
| shareAmount             | float             | 1.05                     | Amount to share                      |
| freezeLock              | integer           | 0                        | Position freeze status: 0 normal, 1 liquidation freeze, 2 delivery freeze |
| status                  | integer           | 0                        | Position effectiveness，0 ineffective 1 effective  | 
| ctime                   | time              | ​                         | Creation time                         |
| mtime                   | time              | ​                         | Update time                           |
| brokerId                | integer           | 1023                     | Client id                             |
| lockTime                | time              |                          | liquidation lock time                 |
| marginRate              | float             | 1.05                     | Margin rate                           |
| reducePrice             | float             | 1.05                     | Price reduction                       |
| returnRate              | float             | 1.05                     | Return rate (profit rate)             |
| unRealizedAmount        | float             | 1.05                     | Unfilled profit and losses            | 
| openRealizedAmount      | float             | 1.05                     | Open position unfilled  profit and losses |
| positionBalance         | float             | 1.05                     | Position value                        |
| indexPrice              | float             | 1.05                     | Newest marked price                   |
| keepRate                | float             | 1.05                     | Scaled minimum kept margin rate       |
| maxFeeRate              | float             | 1.05                     | Balancing maximum fees rate           |

