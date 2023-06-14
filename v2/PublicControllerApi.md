
# Market Data Endpoints
## Test Connectivity

```demo
curl -X GET -i /fapi/v1/ping
```

> The above command returns JSON structured like this:

```json
{}
```

**URL:** `/fapi/v1/ping`

**Type:** `GET`


**Content-Type:** `application/x-www-form-urlencoded;charset=UTF-8`

**Description:** Test Connectivity PING




## Check Server Time

```demo
curl -X GET -i /fapi/v1/time
```

> The above command returns JSON structured like this:

```json
{}
```

**URL:** `/fapi/v1/time`

**Type:** `GET`


**Content-Type:** `application/x-www-form-urlencoded;charset=UTF-8`

**Description:** Check Server Time







**Response-fields:**

| Field | Type | Description |
|-------|------|-------------|
|any object|object|any object.|-|

## Current open contract

```demo
curl -X GET -i /fapi/v1/contracts
```

> The above command returns JSON structured like this:

```json
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

**URL:** `/fapi/v1/contracts`

**Type:** `GET`


**Content-Type:** `application/x-www-form-urlencoded;charset=UTF-8`

**Description:** Current open contract

**Query-parameters:**

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
|contractName|string|true|Contract Name E.g. E-BTC-USD|-|






**Response-fields:**

| Field                    | Type             | Description                          |
| ----------------------- | ----------------- | ------------------------------------ |
| symbol                  | string            | Contract name                        |
| status                  | number            | status (0:cannot trade, 1:can trade) |
| type                    | string            | contract type, E: perpetual contract, S: test contract, others are mixed contract  |
| side                    | number            | Contract direction(backwards：0，1：forward) |
| multiplier              | number            | Contract face value                   |
| multiplierCoin          | string            | Contract face value unit              |
| pricePrecision          | number            | Precision of the price                | 
| minOrderVolume          | number            | Minimum order volume                  |
| minOrderMoney           | number            | Minimum order value                   |
| maxMarketVolume         | number            | Market price order maximum volume     |
| maxMarketMoney          | number            | Market price order maximum value      |
| maxLimitVolume          | number            | Limit price order maximum volume      |
| maxValidOrder           | number            | Maximum valid order quantity          |
