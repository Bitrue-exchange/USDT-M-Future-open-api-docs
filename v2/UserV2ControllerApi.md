
# user
## Account Information V2 (USER_DATA)(HMAC SHA256)

```demo
curl -X GET -i /fapi/v2/account
```

> The above command returns JSON structured like this:

```json
{
  "code":"0",
  "msg":"Success",
  "data":{
    "account":[
      {
        "marginCoin":"USDT",
        "coinPrecious":4,
        "accountNormal":1010.4043400372839856,
        "accountLock":2.9827889600000006,
        "partPositionNormal":0,
        "totalPositionNormal":0,
        "achievedAmount":0,
        "unrealizedAmount":0,
        "totalMarginRate":0,
        "totalEquity":1010.4043400372839856,
        "partEquity":0,
        "totalCost":0,
        "sumMarginRate":0,
        "sumOpenRealizedAmount":0,
        "canUseTrialFund":0,
        "sumMaintenanceMargin":null,
        "futureModel":null,
        "positionVos":[

        ]
      },
      {
        "marginCoin":"USDT",
        "coinPrecious":8,
        "accountNormal":9999981.6304078411247375,
        "accountLock":1.4950614966,
        "partPositionNormal":0,
        "totalPositionNormal":1.5610615,
        "achievedAmount":0,
        "unrealizedAmount":0,
        "totalMarginRate":128117.7154579628016855,
        "totalEquity":9999981.6304078411247375,
        "partEquity":0,
        "totalCost":1.5610615,
        "sumMarginRate":128117.7346123843289321,
        "sumOpenRealizedAmount":-3.29999999,
        "canUseTrialFund":0,
        "sumMaintenanceMargin":null,
        "futureModel":null,
        "positionVos":[
          {
            "contractId":62,
            "contractName":"E-BTC-USDT",
            "contractSymbol":"BTC-USDT",
            "adlEnabled":false,
            "positions":[
              {
                "id":175633,
                "uid":10294,
                "contractId":62,
                "positionType":1,
                "side":"BUY",
                "volume":30,
                "openPrice":27117.691603,
                "avgPrice":26017.691606,
                "closePrice":0,
                "leverageLevel":50,
                "openAmount":0,
                "holdAmount":1.5610615,
                "closeVolume":0,
                "pendingCloseVolume":0,
                "realizedAmount":0,
                "historyRealizedAmount":-3.47655433,
                "forceLiquidationVolume":0,
                "forceLiquidationPrice":0,
                "tradeFee":-0.02450636,
                "capitalFee":-0.15204798,
                "closeProfit":0,
                "shareAmount":0,
                "freezeLock":0,
                "status":1,
                "ctime":"2023-06-06T09:48:43",
                "mtime":"2023-06-14T04:39:28",
                "brokerId":1000,
                "usingAccountType":0,
                "marginRate":0.0001,
                "reducePrice":-3350051449.6928050669137353,
                "returnRate":-2.1139461825781778,
                "unRealizedAmount":0,
                "openRealizedAmount":-3.29999999,
                "positionBalance":78.05307482,
                "settleProfit":-3.29999999,
                "keepRate":0.004,
                "maxFeeRate":0.001,
                "indexPrice":26017.691606
              }
            ]
          }
        ]
      }
    ]
  }
}
```

**URL:** `/fapi/v2/account`

**Type:** `GET`


**Content-Type:** `application/json`

**Description:** Account Information V2 (USER_DATA)(HMAC SHA256)







**Response-fields:**

| Field | Type | Description |
|-------|------|-------------|
|code|string|status code|-|
|msg|string|message content|-|
|data|object|return data|-|
|└─account|array|Account V2|-|
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;└─marginCoin|string|Margin coin|-|
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;└─coinPrecious|int|Currency display precision|-|
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;└─accountNormal|bigdecimal|Balance account|-|
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;└─accountLock|bigdecimal|Margin frozen account|-|
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;└─partPositionNormal|bigdecimal|Restricted position margin balance|-|
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;└─totalPositionNormal|bigdecimal|Full position initial margin|-|
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;└─achievedAmount|bigdecimal|Profit and losses occurred|-|
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;└─unrealizedAmount|bigdecimal|Unfilled profit and losses|-|
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;└─totalMarginRate|bigdecimal|Full position margin rate|-|
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;└─totalEquity|bigdecimal|Full position equity|-|
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;└─partEquity|bigdecimal|Restricted position equity|-|
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;└─totalCost|bigdecimal|Full position costs|-|
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;└─sumMarginRate|bigdecimal|All accounts margin rate|-|
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;└─sumOpenRealizedAmount|bigdecimal|Full account position profit and loss|-|
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;└─canUseTrialFund|bigdecimal|Available experience money|-|
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;└─sumMaintenanceMargin|bigdecimal|Full position maintenance margin plus handling fee|-|
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;└─futureModel|enum|Account type|-|
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;└─positionVos|array|Position contract record|-|
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;└─contractId|int|Contract id|-|
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;└─contractName|string|Contract name|-|
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;└─contractSymbol|string|Contract coin pair|-|
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;└─adlEnabled|boolean|adl|-|
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;└─positions|array|positions|-|
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;└─id|int|id|-|
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;└─uid|int|user id|-|
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;└─contractId|int|contract id|-|
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;└─positionType|int|Hold-up position, 1 full position, 2 restrictive position|-|
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;└─side|string|trade direction, BUY/SELL|-|
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;└─volume|bigdecimal|Order quantity|-|
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;└─openPrice|bigdecimal|open price|-|
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;└─avgPrice|bigdecimal|avg price|-|
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;└─closePrice|bigdecimal|Balancing average price|-|
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;└─leverageLevel|int|Leverage multiple|-|
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;└─openAmount|bigdecimal|Opening margin (including variation)|-|
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;└─holdAmount|bigdecimal|Hold position margin|-|
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;└─closeVolume|bigdecimal|Balanced quantity|-|
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;└─pendingCloseVolume|bigdecimal|The number of pending closing orders|-|
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;└─realizedAmount|bigdecimal|Profit and losses occurred|-|
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;└─historyRealizedAmount|bigdecimal|Historic accumulated profit and losses|-|
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;└─forceLiquidationVolume|bigdecimal|Strong flat quantity|-|
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;└─forceLiquidationPrice|bigdecimal|Strong leveling price (average price, trigger price).|-|
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;└─tradeFee|bigdecimal|Trading fees|-|
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;└─capitalFee|bigdecimal|Capital costs|-|
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;└─closeProfit|bigdecimal|Balancing profit and loss|-|
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;└─shareAmount|bigdecimal|Amount to share|-|
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;└─freezeLock|int|Position freeze status: 0 normal, 1 liquidation freeze, 2 delivery freeze|-|
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;└─status|int|Position effectiveness，0 ineffective 1 effective|-|
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;└─ctime|string|Creation time|-|
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;└─mtime|string|Update time|-|
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;└─lockTime|string|liquidation lock time|-|
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;└─positionAmount|bigdecimal|Total position value (full) multiplied by face value|-|
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;└─positionCloseAmount|bigdecimal|Total closing value (full amount) multiplied by face value|-|
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;└─longAccountCount|int|Number of multiple positions|-|
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;└─shortAccountCount|int|Number of open positions|-|
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;└─sumRealized|bigdecimal|The total realized profit and loss of this settlement cycle|-|
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;└─deficitLosses|bigdecimal|Customer account deficit at position settlement|-|
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;└─currentMarginRate|bigdecimal|Current margin ratio|-|
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;└─realEquity|bigdecimal|Balance occupied by current contracts, excluding realized and unrealized gains and losses|-|
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;└─positionId|int|Location ID, associated with the location list id, primary key|-|
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;└─ctime|string|create time|-|
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;└─mtime|string|update time|-|
## Notional and Leverage Brackets (USER_DATA)

```demo
curl -X GET -i /fapi/v2/leverageBracket?contractName=E-SAND-USDT
```

> The above command returns JSON structured like this:

```json
{
    "code":"0",
    "msg":"Success",
    "data":{
        "contractName":"E-SAND-USDT",
        "brackets":[
            {
                "bracket":1,
                "initialLeverage":100,
                "maxPositionValue":10000,
                "minPositionValue":0,
                "maintMarginRatio":0.008
            },
            {
                "bracket":2,
                "initialLeverage":75,
                "maxPositionValue":100000,
                "minPositionValue":10000,
                "maintMarginRatio":0.0085
            },
            {
                "bracket":3,
                "initialLeverage":50,
                "maxPositionValue":500000,
                "minPositionValue":100000,
                "maintMarginRatio":0.012
            },
            {
                "bracket":4,
                "initialLeverage":25,
                "maxPositionValue":1000000,
                "minPositionValue":500000,
                "maintMarginRatio":0.022
            },
            {
                "bracket":5,
                "initialLeverage":10,
                "maxPositionValue":2000000,
                "minPositionValue":1000000,
                "maintMarginRatio":0.05
            },
            {
                "bracket":6,
                "initialLeverage":5,
                "maxPositionValue":5000000,
                "minPositionValue":2000000,
                "maintMarginRatio":0.1
            },
            {
                "bracket":7,
                "initialLeverage":4,
                "maxPositionValue":10000000,
                "minPositionValue":5000000,
                "maintMarginRatio":0.125
            },
            {
                "bracket":8,
                "initialLeverage":3,
                "maxPositionValue":20000000,
                "minPositionValue":10000000,
                "maintMarginRatio":0.15
            },
            {
                "bracket":9,
                "initialLeverage":1,
                "maxPositionValue":9999999998,
                "minPositionValue":20000000,
                "maintMarginRatio":0.25
            }
        ]
    }
}
```

**URL:** `/fapi/v2/leverageBracket`

**Type:** `GET`


**Content-Type:** `application/json`

**Description:** Notional and Leverage Brackets (USER_DATA)



**Query-parameters:**

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
|contractName|string|true|Contract name|-|




**Response-fields:**

| Field | Type | Description |
|-------|------|-------------|
|code|string|status code|-|
|msg|string|message content|-|
|data|object|return data|-|
|└─contractName|string|Contract name|-|
|└─brackets|array|brackets|-|
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;└─bracket|int|Notional bracket|-|
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;└─initialLeverage|bigdecimal|Max initial leverage for this bracket|-|
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;└─maxPositionValue|bigdecimal|Cap notional of this bracket|-|
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;└─minPositionValue|bigdecimal|Notional threshold of this bracket|-|
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;└─maintMarginRatio|bigdecimal|Maintenance ratio for this bracket|-|

## User Commission Rate (USER_DATA)(HMAC SHA256)

```demo
curl -X GET -i /fapi/v2/commissionRate?contractName=E-SAND-USDT
```

> The above command returns JSON structured like this:

```json
{
    "code":"0",
    "msg":"Success",
    "data":{
        "contractName":"E-SAND-USDT",
        "openTakerFeeRate":0.0004,
        "openMakerFeeRate":0.0002,
        "closeTakerFeeRate":0.0004,
        "closeMakerFeeRate":0.0002
    }
}
```

**URL:** `/fapi/v2/commissionRate`

**Type:** `GET`


**Content-Type:** `application/json`

**Description:** User Commission Rate (USER_DATA)(HMAC SHA256)



**Query-parameters:**

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
|contractName|string|true|Contract name|-|




**Response-fields:**

| Field | Type | Description |
|-------|------|-------------|
|code|string|status code|-|
|msg|string|message content|-|
|data|object|return data|-|
|└─contractName|string|contract name|-|
|└─openTakerFeeRate|bigdecimal|open taker fee rate|-|
|└─openMakerFeeRate|bigdecimal|open maker fee rate|-|
|└─closeTakerFeeRate|bigdecimal|close taker fee rate|-|
|└─closeMakerFeeRate|bigdecimal|close maker fee rate|-|

## New Future Account Transfer (USER_DATA)(HMAC SHA256)

```demo
curl -X POST -H 'Content-Type: application/json' -i /fapi/v2/futures_transfer --data '{
	'coinSymbol': 'USDT',
	'amount': 10,
	'transferType': 'wallet_to_contract'
}'
```

> The above command returns JSON structured like this:

```json
{
	'code': '0',
	'msg': 'Success',
	'data': None
}
```

**URL:** `/fapi/v2/futures_transfer`

**Type:** `POST`


**Content-Type:** `application/json`

**Description:** New Future Account Transfer (USER_DATA)(HMAC SHA256)




**Body-parameters:**

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
|coinSymbol|string|true|coin symbol|-|
|amount|bigdecimal|true|transfer amount|-|
|transferType|string|true|transfer type<br/>WALLET_TO_CONTRACT("wallet_to_contract", "币币到合约"),<br/>CONTRACT_TO_WALLET("contract_to_wallet", "合约到币币")|-|
|unionId|string|false|transfer union tag|-|



**Response-fields:**

| Field | Type | Description |
|-------|------|-------------|
|code|string|status code|-|
|msg|string|message content|-|
|data|object|return data|-|

## Get Future Account transfer History List (USER_DATA)(HMAC SHA256)

```demo
curl -X GET -i /fapi/v2/futures_transfer_history?transferType=wallet_to_contract
```

> The above command returns JSON structured like this:

```json
{
	'code': '0',
	'msg': 'Success',
	'data': [{
		'transferType': 'wallet_to_contract',
		'symbol': 'USDT',
		'amount': 1.0,
		'status': 1,
		'ctime': 1685404575000
	}, {
		'transferType': 'wallet_to_contract',
		'symbol': 'USDT',
		'amount': 3.0,
		'status': 1,
		'ctime': 1685495897000
	}, {
		'transferType': 'wallet_to_contract',
		'symbol': 'USDT',
		'amount': 566.0,
		'status': 1,
		'ctime': 1685562991000
	}, {
		'transferType': 'wallet_to_contract',
		'symbol': 'USDT',
		'amount': 66.0,
		'status': 1,
		'ctime': 1685571419000
	}, {
		'transferType': 'wallet_to_contract',
		'symbol': 'USDT',
		'amount': 3.0,
		'status': 1,
		'ctime': 1685573130000
	}]
}
```

**URL:** `/fapi/v2/futures_transfer_history`

**Type:** `GET`


**Content-Type:** `application/json`

**Description:** Get Future Account transfer History List (USER_DATA)(HMAC SHA256)



**Query-parameters:**

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
|coinSymbol|string|false|coin symbol|-|
|beginTime|long|false|default the recent 30-day data|-|
|endTime|long|false|end time|-|
|transferType|string|true|transfer type<br/>WALLET_TO_CONTRACT("wallet_to_contract", "币币到合约"),<br/>CONTRACT_TO_WALLET("contract_to_wallet", "合约到币币")|-|
|page|int|false|default 1|-|
|limit|int|false|Default 10, Max 200|-|




**Response-fields:**

| Field | Type | Description |
|-------|------|-------------|
|code|string|status code|-|
|msg|string|message content|-|
|data|array|return data|-|
|└─transferType|string|转账类型<br/>WALLET_TO_CONTRACT("wallet_to_contract", "币币到合约"),<br/>CONTRACT_TO_WALLET("contract_to_wallet", "合约到币币")|-|
|└─symbol|string|symbol|-|
|└─amount|bigdecimal|transfer amount|-|
|└─afterAmount|bigdecimal|after transfer amount|-|
|└─status|int|Transfer status, 0 payment, 1 success and 2 failure|-|
|└─ctime|long|create time|-|

## User's Force Orders (USER_DATA)

```demo
curl -X GET -i /fapi/v2/forceOrdersHistory?contractName=E-BTC-USDT
```

> The above command returns JSON structured like this:

```json
{
	'code': '0',
	'msg': 'Success',
	'data': [{
		'id': 1690600111070971191,
		'clientId': '0',
		'uid': 11568,
		'positionType': 2,
		'open': 'CLOSE',
		'side': 'SELL',
		'type': 1,
		'leverageLevel': 20,
		'price': 25878.61801778723,
		'volume': 357.0,
		'openTakerFeeRate': 0.0,
		'openMakerFeeRate': 0.0,
		'closeTakerFeeRate': 0.0,
		'closeMakerFeeRate': 0.0,
		'realizedAmount': -44.21710198209588,
		'dealVolume': 357,
		'dealMoney': 923.8666632350041,
		'lockMoney': 0.0,
		'unlockMoney': 0.0,
		'avgPrice': 25878.61801779,
		'tradeFee': 0.0,
		'status': 2,
		'memo': 0,
		'source': 6,
		'ctime': '2023-06-13T20:55:51',
		'mtime': '2023-06-13T12:55:51',
		'brokerId': 1000,
		'usingAccountType': 0,
		'shareRoyaltyRatio': 0.0
	}]
}
```

**URL:** `/fapi/v2/forceOrdersHistory`

**Type:** `GET`


**Content-Type:** `application/json`

**Description:** User's Force Orders (USER_DATA)



**Query-parameters:**

| Parameter | Type | Required | Description                                                 |
|-----------|------|----------|-------------------------------------------------------------|
|contractName|string|true| Contract name E.g. E-BTC-USDT                               |-|
|beginTime|long|false| default the recent 30-day data                              |-|
|endTime|long|false| end time                                                    |-|
|autoCloseType|string|false| "LIQUIDATION" for liquidation orders, "ADL" for ADL orders. |-|
|page|int|false| Default 1                                                   |-|
|limit|int|false| Default 10, Max 200                                         |-|




**Response-fields:**

| Field | Type | Description |
|-------|------|-------------|
|code|string|status code|-|
|msg|string|message content|-|
|data|array|return data|-|
|└─id|int|id|-|
|└─uid|int|user id|-|
|└─contractId|int|contract id|-|
|└─positionType|int|Hold-up position, 1 full position, 2 restrictive position|-|
|└─side|string|trade direction, BUY/SELL|-|
|└─volume|bigdecimal|Order quantity|-|
|└─openPrice|bigdecimal|open price|-|
|└─avgPrice|bigdecimal|avg price|-|
|└─closePrice|bigdecimal|Balancing average price|-|
|└─leverageLevel|int|Leverage multiple|-|
|└─openAmount|bigdecimal|Opening margin (including variation)|-|
|└─holdAmount|bigdecimal|Hold position margin|-|
|└─closeVolume|bigdecimal|Balanced quantity|-|
|└─pendingCloseVolume|bigdecimal|The number of pending closing orders|-|
|└─realizedAmount|bigdecimal|Profit and losses occurred|-|
|└─historyRealizedAmount|bigdecimal|Historic accumulated profit and losses|-|
|└─forceLiquidationVolume|bigdecimal|Strong flat quantity|-|
|└─forceLiquidationPrice|bigdecimal|Strong leveling price (average price, trigger price).|-|
|└─tradeFee|bigdecimal|Trading fees|-|
|└─capitalFee|bigdecimal|Capital costs|-|
|└─closeProfit|bigdecimal|Balancing profit and loss|-|
|└─shareAmount|bigdecimal|Amount to share|-|
|└─freezeLock|int|Position freeze status: 0 normal, 1 liquidation freeze, 2 delivery freeze|-|
|└─status|int|Position effectiveness，0 ineffective 1 effective|-|
|└─ctime|string|Creation time|-|
|└─mtime|string|Update time|-|
|└─brokerId|int|Client id|-|
|└─lockTime|string|liquidation lock time|-|
|└─positionAmount|bigdecimal|Total position value (full) multiplied by face value|-|
|└─positionCloseAmount|bigdecimal|Total closing value (full amount) multiplied by face value|-|
|└─longAccountCount|int|Number of multiple positions|-|
|└─shortAccountCount|int|Number of open positions|-|
|└─sumRealized|bigdecimal|The total realized profit and loss of this settlement cycle|-|
|└─deficitLosses|bigdecimal|Customer account deficit at position settlement|-|
|└─currentMarginRate|bigdecimal|Current margin ratio|-|
|└─realEquity|bigdecimal|Balance occupied by current contracts, excluding realized and unrealized gains and losses|-|
|└─usingAccountType|int|Type of account used (0: contract, 1: with order, 2: Documentary)|-|
|└─coPositionExt|object|Position extension information|-|
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;└─positionId|int|Location ID, associated with the location list id, primary key|-|
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;└─copyTraderUid|int|Merchandiser uid|-|
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;└─shareTraderUid|int|With single member uid|-|
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;└─sharePositionId|int|With a single warehouse id|-|
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;└─shareRoyaltyRatio|double|Proportion of moistening 0-1|-|
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;└─preShareRoyaltyAmount|bigdecimal|Advance the amount of money|-|
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;└─lockPreShareRoyaltyAmount|bigdecimal|Actual freezing of the amount of advance|-|
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;└─copyStatus|int|Documentary status (1: normal, 2: failed to add warehouse receipt, 3: failed to balance warehouse receipt)|-|
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;└─shareRoyaltyStatus|int|Moistening status (0: open position, 1: to be moistened, 2: moistened, 3: unmoistened)|-|
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;└─closePositionType|int|Merchandiser closing type (0: open position, 1: follow trader closing, 2: manual closing, 3: forced closing)|-|
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;└─ctime|string|create time|-|
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;└─mtime|string|update time|-|



