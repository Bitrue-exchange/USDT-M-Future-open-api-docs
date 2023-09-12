User Data Streams
==================
* The base API endpoint is: `https://fapiws-auth.bitrue.com`
* A User Data Stream listenKey is valid for 30 minutes after creation.
* API-keys are passed into the API via the `X-CH-APIKEY` header.
* API-keys are passed into the API via the `X-CH-SIGN` header. It is based on timestamp + method + requestPath + body string (+ means string connection) as the operation object 
* The value of timestamp is the same as the `X-CH-TS` request header, method is the request method, and the letters are all uppercase: GET/POST
* Doing a PUT on a listenKey will extend its validity for 30 minutes.
* Doing a DELETE on a listenKey will close the stream and invalidate the listenKey.
* Doing a POST on an account with an active listenKey will return the currently active listenKey and extend its validity for 30 minutes.
* A listenKey is a stream.
* Users can listen to multiple streams.
* The base websocket endpoint is: `wss://fapiws.bitrue.com`
* User Data Streams are accessed at `/stream?streams=<listenKey>`

## Signature generation
#### Timing Security

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

**It recommended to use a small recvWindow of 5000 or less!**

#### SIGNED Endpoint Examples for POST /sapi/v1/order

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

#### Signature example

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
  [linux]$ curl -H "X-CH-APIKEY: c3b165fd5218cdd2c2874c65da468b1e" -H "X-CH-SIGN: c50d0a74bb9427a9a03933d0eded03af9bf50115dc5b706882a4fcf07a26b761" -H "X-CH-TS: 1588591856950" -H "Content-Type:application/json" -X POST 'http://localhost:30000/sapi/v1/order/test' -d '{"symbol":"BTCUSDT","price":"9300","quantity":"1","side":"BUY","type":"LIMIT"}'
 ```



## Error Codes

Errors consist of two parts:
an error code and a message.
Codes are universal, but messages can vary.

| code   | description   | memo                                     |
| ------ | ------------  | ---------------------------------------- |
| 200    |   SUCCESS     |  200 for success,others are error codes. |
| 503    | SERVICE_ERROR | An unknown error occurred while processing the request. |
| 1022   | INVALID_API_KEY | You are not authorized to execute this request.   |
| 1102   | MANDATORY_PARAM_EMPTY_OR_MALFORMED | A mandatory parameter was not sent, was empty/null, or malformed. |
| -1150  | INVALID_LISTEN_KEY | This listenKey does not exist.   |

## ListenKey

#### CREATE A LISTENKEY (USER_STREAM)

* url

  `POST /user_stream/api/v1/listenKey`

Start a new user data stream. The stream will close after 60 minutes unless a keepalive is sent. If the account has an active listenKey, that listenKey will be returned and its validity will be extended for 60 minutes.

* Response:

```json
{
  "msg": "succ",
  "code": 200,
  "data":
  {
    "listenKey": "ac3abbc8ac18f7977df42de27ab0c87c1f4ea3919983955d2fb5786468ccdb07"
  }
}
```

#### Ping/Keep-alive a ListenKey (USER_STREAM)

* url

  `PUT /user_stream/api/v1/listenKey/{listenKey}`

Keep alive a user data stream to prevent a time out. User data streams will close after 60 minutes. It's recommended to send a ping about every 30 minutes.

* Response:

```json
{
  "msg": "succ",
  "code": 200
}
```

#### Close a ListenKey (USER_STREAM)

* url

  `DELETE /user_stream/api/v1/listenKey/{listenKey}`

Close out a user data stream.

* Response:

```json
{
  "msg": "succ",
  "code": 200
}
```

## keep-alive(websocket)

you should send pong message after receive a `ping` message.

* ping:
```json
{"event":"ping","ts":"1635221621062"}
```

* pong：

```json
{"event":"pong","ts":"1635221621062"}
```

## User stream

User Account stream **subscribe：**
``` 
{"event":"sub","params":{"channel":"user_account_update"}}
```
**response：**

sub success :
``` 
{"event":"user_account_update","status":"ok","ts":1689568979259}
```

## payload
####  order event :
``` 
{
	"e": "ORDER_TRADE_UPDATE", // Event type
	"E": 1568879465651, // Event time (timestamp)
	"o": {
		"s": "BTCUSDT", // Trading pair
		"c": "TEST", // Client-provided order ID
		"S": "SELL", // Order direction
		"o": "MARKET", // Order type (MARKET|LIMIT|IOC|POST_ONLY...)
		"q": "0.001", // Original order quantity (multiplied by face value)
		"p": "0", // Original order price
		"ap": "0", // Average order price (price after execution)
		"x": "NEW", // Specific execution type for this event (new, liquidation, trade, cancel, adl)
		"X": "NEW", // Current status of the order (status)
		"i": 8886774, // Order ID
		"l": "0", // Order quantity filled in the current event
		"z": "0", // Cumulative filled order quantity
		"L": "0", // Price at which the order was filled in the current event
		"N": "USDT", // Fee asset type
		"n": "0", // Fee amount (total fee)
		"T": 1568879465650, // Trade time
		"t": 0, // Trade ID
		"m": false, // Was this trade a maker or taker? (make, take) Reserved field
		"R": false, // Is this a reduce-only order? (default false) Reserved field
		"ps": "LONG", // Position direction (long if present, short if empty)
		"rp": "0" // Realized profit or loss for this trade (current P&L)
	}
}
```

Orders are updated with the executionReport event.

Execution types(`x`):

* NEW - The order has been accepted into the engine.
* CANCELED - The order has been canceled by the user.
* TRADE - Part of the order or all of the order's quantity has filled.
* LIQUIDATION - force liquidation when the position under


#### acount event

```
{
	"e": "ACCOUNT_UPDATE", // Event type
	"E": 1564745798939, // Event time
	"T": 1564745798938, // Matching time (tentative)
	"a": // Account update event
	{
		"m": "ORDER", // Event trigger reason (enum: see table)
		"B": [ // Balance information
			{
				"a": "USDT", // Asset name
				"cw": "122624.12345678", // Cross-margin balance
				"lb": "0.000", // Locked balance
				"iw": "100.12345678", // Isolated margin wallet balance
				"bc": "50.12345678" // Balance change not related to profit and loss or trading fees
			}, // Only send relevant account balances.
			{
				"a": "BUSD",
				"cw": "122624.12345678",
				"lb": "0.0000",
				"iw": "100.12345678",
				"bc": "50.12345678"
			}
		],
		"P": [{
			"s": "BTCUSDT", // Trading pair
			"pa": "0", // Position amount
			"ep": "0.00000", // Entry price
			"lp": "28343.33", // Last settlement price
			"cr": "200", // Cumulative realized profit and loss (history_realized_amount) including fees
			"up": "0", // Unrealized profit and loss for the position (lp -> current)
			"mt": "1", // Margin type, position type (1 Cross, 2 Isolated)
			"iw": "0.00000000", // If isolated, isolated margin for the position
			"ps": "SHORT|LONG" // Position direction (SHORT|LONG)
		}]
	}
}
```





