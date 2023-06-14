
# USDⓈ-M Futures:order
## Account Trade List (USER_DATA)(HMAC SHA256)

```demo
curl -X GET -i /fapi/v2/myTrades?contractName=E-SAND-USDC&fromId=&limit=10&startTime=&endTime=
```

> The above command returns JSON structured like this:

```json
{
    "code":"0",
    "msg":"Success",
    "data":[
        {
            "tradeId":12,
            "price":0.9,
            "qty":1,
            "amount":9,
            "contractName":"E-SAND-USDC",
            "side":"BUY",
            "fee":"0.0018",
            "bidId":1558124009467904992,
            "askId":1558124043827644908,
            "bidUserId":10294,
            "askUserId":10467,
            "isBuyer":true,
            "isMaker":true,
            "ctime":1678426306000
        }
    ]
}
```

**URL:** `/fapi/v2/myTrades`

**Type:** `GET`


**Content-Type:** `application/x-www-form-urlencoded;charset=UTF-8`

**Description:** Account Trade List (USER_DATA)(HMAC SHA256)



**Query-parameters:**

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
|contractName|string|true|Contract name E.g. E-BTC-USD|-|
|fromId|long|false|Trade id to fetch from. Default gets most recent trades.|-|
|limit|int|false|Default 100; max 1000.|-|
|startTime|long|false|start time|-|
|endTime|long|false|end time|-|




**Response-fields:**

| Field | Type | Description |
|-------|------|-------------|
|code|string|status code|-|
|msg|string|message content|-|
|data|array|return data|-|
|└─tradeId|long|trade id|-|
|└─price|bigdecimal|Order price|-|
|└─qty|int|Order quantity|-|
|└─amount|bigdecimal|Order amount|-|
|└─contractName|string|contract name|-|
|└─cTime|long|create time|-|
|└─side|string|Order direction. Possible values can only be：BUY（buy long）and SELL（sell short）|-|
|└─fee|string|Trading fees|-|
|└─bidId|long|bid id|-|
|└─askId|long|ask id|-|
|└─bidUserId|int|bid User Id|-|
|└─askUserId|int|ask User Id|-|
|└─isBuyer|boolean|is buy|-|
|└─isMaker|boolean|is maker|-|

## Modify Isolated Position Margin (TRADE)(HMAC SHA256)

```demo
curl -X POST -H 'Content-Type: application/json' -i /fapi/v2/positionMargin --data '{
	'contractName': 'E-SAND-USDC',
	'positionMargin': 10
}'
```

> The above command returns JSON structured like this:

```json
{
    "code": 0,
    "msg": "success"
    "data": null
}
```

**URL:** `/fapi/v2/positionMargin`

**Type:** `POST`


**Content-Type:** `application/json`

**Description:** Modify Isolated Position Margin (TRADE)(HMAC SHA256)




**Body-parameters:**

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
|contractName|string|true|Contract name E.g. E-BTC-USD|-|
|amount|bigdecimal|true|amount|-|



**Response-fields:**

| Field | Type | Description |
|-------|------|-------------|
|code|string|status code|-|
|msg|string|message content|-|
|data|object|return data|-|

## Change Initial Leverage (TRADE)(HMAC SHA256)

```demo
curl -X POST -H 'Content-Type: application/json' -i /fapi/v2/level_edit --data '{
	'contractName': 'E-BTC-USDT',
	'leverage': 10
}'
```

> The above command returns JSON structured like this:

```json
{
    "code": 0,
    "msg": "success",
    "data": null
}
```

**URL:** `/fapi/v2/level_edit`

**Type:** `POST`


**Content-Type:** `application/json`

**Description:** Change Initial Leverage (TRADE)(HMAC SHA256)




**Body-parameters:**

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
|contractName|string|true|Contract name E.g. E-BTC-USD|-|
|leverage|int|true|target initial leverage: int from 1 to 125|-|



**Response-fields:**

| Field | Type | Description |
|-------|------|-------------|
|code|string|status code|-|
|msg|string|message content|-|
|data|object|return data|-|

## Current All Open Orders (USER_DATA)(HMAC SHA256)

```demo
curl -X GET -i /fapi/v2/openOrders?contractName=E-SAND-USDC
```

> The above command returns JSON structured like this:

```json
{
	"code": "0",
	"msg": "Success",
	"data": [{
			"orderId": 1917641,
			"clientOrderId": "2488514315",
			"price": 100,
			"origQty": 10,
			"origAmount": 10,
			"executedQty": 1,
			"avgPrice": 12451,
			"status": "INIT",
			"type": "LIMIT",
			"side": "BUY",
			"action": "OPEN",
			"transactTime": 1686717303975
		}
	]
}
```

**URL:** `/fapi/v2/openOrders`

**Type:** `GET`


**Content-Type:** `application/x-www-form-urlencoded;charset=UTF-8`

**Description:** Current All Open Orders (USER_DATA)(HMAC SHA256)



**Query-parameters:**

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
|contractName|string|true|Contract name E.g. E-BTC-USD|-|




**Response-fields:**

| Field | Type | Description |
|-------|------|-------------|
|code|string|status code|-|
|msg|string|message content|-|
|data|array|return data|-|
|└─orderId|long|Order ID（system generated）|-|
|└─clientOrderId|string|client Order id|-|
|└─price|bigdecimal|Order price|-|
|└─origQty|bigdecimal|Order quantity|-|
|└─origAmount|bigdecimal|Order amount|-|
|└─executedQty|bigdecimal|Filled orders quantity|-|
|└─avgPrice|bigdecimal|Filled orders average price|-|
|└─status|string|Order status. Possible values are：NEW(new order，not filled)、PARTIALLY_FILLED（partially filled）、FILLED（fully filled）、CANCELLED（already cancelled）andREJECTED（order rejected）|-|
|└─type|string|Order type. Possible values can only be:LIMIT(limit price) andMARKET（market price）|-|
|└─side|string|Order direction. Possible values can only be：BUY（buy long）and SELL（sell short）|-|
|└─action|string|OPEN/CLOSE|-|
|└─transactTime|long|Order creation time|-|

## Cancel Order (TRADE)(HMAC SHA256)

```demo
curl -X POST -H 'Content-Type: application/json' -i /fapi/v2/cancel --data '{
    'contractName': 'E-SAND-USDC', 
    'clientOrderId': "",  
    'orderId': 1690615847831143159, 
}
```

> The above command returns JSON structured like this:

```json
{
	"code": "0",
	"msg": "Success",
	"data": {
		"orderId": 1690615847831143159
	}
}
```

**URL:** `/fapi/v2/cancel`

**Type:** `POST`


**Content-Type:** `application/json`

**Description:** Cancel Order (TRADE)(HMAC SHA256)




**Body-parameters:**

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
|contractName|string|true|Contract name E.g. E-BTC-USD|-|
|clientOrderId|string|false|client Order id(clientOrderId and orderId cannot both be empty)|-|
|orderId|long|false|order id(clientOrderId and orderId cannot both be empty)|-|



**Response-fields:**

| Field | Type | Description |
|-------|------|-------------|
|code|string|status code|-|
|msg|string|message content|-|
|data|object|return data|-|
|└─orderId|long|Order ID（system generated）|-|

## Query Order (USER_DATA)(HMAC SHA256)

```demo
curl -X GET -i /fapi/v2/order?contractName=E-SAND-USDT&orderId=1690615710392189353
```

> The above command returns JSON structured like this:

```json
{
    "code":0,
    "msg":"success",
    "data":[
        {
            "orderId":1917641, 
            "price":100,
            "origQty":10,
            "origAmount":10,
            "executedQty":1,
            "avgPrice":10000,
            "status":"INIT", 
            "type":"LIMIT",
            "side":"BUY",
            "action":"OPEN",
            "transactTime":1686716571425 
            "clientOrderId":4949299210
        },
        {
 
        }
    ]
}
```

**URL:** `/fapi/v2/order`

**Type:** `GET`


**Content-Type:** `application/x-www-form-urlencoded;charset=UTF-8`

**Description:** Query Order (USER_DATA)(HMAC SHA256)



**Query-parameters:**

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
|contractName|string|true|Contract name E.g. E-BTC-USD|-|
|clientOrderId|string|false|client Order id(clientOrderId and orderId cannot both be empty)|-|
|orderId|long|false|order id(clientOrderId and orderId cannot both be empty)|-|




**Response-fields:**

| Field | Type | Description |
|-------|------|-------------|
|code|string|status code|-|
|msg|string|message content|-|
|data|object|return data|-|
|└─orderId|long|Order ID（system generated）|-|
|└─clientOrderId|string|client Order id|-|
|└─price|bigdecimal|Order price|-|
|└─origQty|bigdecimal|Order quantity|-|
|└─origAmount|bigdecimal|Order amount|-|
|└─executedQty|bigdecimal|Filled orders quantity|-|
|└─avgPrice|bigdecimal|Filled orders average price|-|
|└─status|string|Order status. Possible values are：NEW(new order，not filled)、PARTIALLY_FILLED（partially filled）、FILLED（fully filled）、CANCELLED（already cancelled）andREJECTED（order rejected）|-|
|└─type|string|Order type. Possible values can only be:LIMIT(limit price) andMARKET（market price）|-|
|└─side|string|Order direction. Possible values can only be：BUY（buy long）and SELL（sell short）|-|
|└─action|string|OPEN/CLOSE|-|
|└─transactTime|long|Order creation time|-|

## New Order (TRADE)(HMAC SHA256)

```demo
curl -X POST -H 'Content-Type: application/json' -i /fapi/v2/order --data '{
    'contractName': 'E-SAND-USDC', 
    'clientOrderId': 7993967859, 
    'side': 'BUY', 
    'type': 'LIMIT', 
    'positionType': 1, 
    'open': 'OPEN', 
    'volume': 100, 
    'amount': 1, 
    'price': 2, 
    'leverage': 5
}'
```

> The above command returns JSON structured like this:

```json
{
	"code": "0",
	"msg": "Success",
	"data": {
		"orderId": 1690615676032452985
	}
}
```

**URL:** `/fapi/v2/order`

**Type:** `POST`


**Content-Type:** `application/json`

**Description:** New Order (TRADE)(HMAC SHA256)




**Body-parameters:**

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
|contractName|string|true|Contract name E.g. E-BTC-USD|-|
|clientOrderId|string|false|Client order identity, a string with length less than 32 bit|-|
|side|string|true|trade direction, BUY/SELL|-|
|type|string|true|Order type, LIMIT,MARKET,IOC,FOK,POST_ONLY|-|
|positionType|int|true|Hold-up position, 1 full position, 2 restrictive position|-|
|open|string|true|Open balancing direction, OPEN/CLOSE|-|
|volume|bigdecimal|true|Order quantity|-|
|amount|bigdecimal|true|Order amount|-|
|price|bigdecimal|true|Order price|-|



**Response-fields:**

| Field | Type | Description |
|-------|------|-------------|
|code|string|status code|-|
|msg|string|message content|-|
|data|object|return data|-|
|└─orderId|long|Order ID（system generated）|-|

## Cancel All Open Orders (TRADE)(HMAC SHA256)

```demo
curl -X POST -i /fapi/v2/allOpenOrders --data 'contractName=E-BTC-USDT'
```

> The above command returns JSON structured like this:

```json
{
	'code': '0',
	'msg': 'Success',
	'data': None
}
```

**URL:** `/fapi/v2/allOpenOrders`

**Type:** `POST`


**Content-Type:** `application/x-www-form-urlencoded;charset=UTF-8`

**Description:** Cancel All Open Orders (TRADE)(HMAC SHA256)



**Query-parameters:**

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
|contractName|string|true|contractame Contract Name E.g. E-BTC-USD|-|




**Response-fields:**

| Field | Type | Description |
|-------|------|-------------|
|code|string|status code|-|
|msg|string|message content|-|
|data|object|return data|-|



