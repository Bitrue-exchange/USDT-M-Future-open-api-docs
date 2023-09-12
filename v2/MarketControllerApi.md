
# 

## Order Book

```demo
curl -X GET -i /fapi/v1/depth
```

> The above command returns JSON structured like this:

```json
{
  "bids": [
    [
      "3.90000000",
      // price
      "431.00000000"
      // quantity
    ],
    [
      "4.00000000",
      "431.00000000"
    ]
  ],
  "asks": [
    [
      "4.00000200",
      // price
      "12.00000000"
      // quantity
    ],
    [
      "5.10000000",
      "28.00000000"
    ]
  ]
}
```

**URL:** `/fapi/v1/depth`

**Type:** `GET`

**Content-Type:** `application/json`

**Description:** Order Book

**Query-parameters:**

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
|contractName|string|true|Contract Name E.g. E-BTC-USDT |-|
|limit|string|integer|Default 100, Max 100   |-|

**Response-fields:**

| name                    | type              | example                  | description                          |
| ----------------------- | ----------------- | ------------------------ | ------------------------------------ |
| time                    | long              | 1595563624731            | Current Timestamp  (ms)              |
| bids                    | list              | Look below               | Order book purchase info             |
| asks                    | list              | Look below               | Order book selling info              |

The fields bids and asks are lists of order book price level entries, sorted from best to worst.

| name                    | type              | example                  | description                          |
| ----------------------- | ----------------- | ------------------------ | ------------------------------------ |
| ' '                     | float             | 131.1                    | price level                          |
| ' '                     | float             | 2.3                      | Total order quantity for this price level |

## ticker

```demo
curl -X GET -i /fapi/v1/ticker
```

> The above command returns JSON structured like this:

```json
{
  "high": "9279.0301",
  "vol": "1302",
  "last": "9200",
  "low": "9279.0301",
  "rose": "0",
  "time": 1595563624731
}
```

> 24 hour price change statistics:

```json
{
  "high": "9279.0301",
  "vol": "1302",
  "last": "9200",
  "low": "9279.0301",
  "rose": "0",
  "time": 1595563624731
}
```

**URL:** `/fapi/v1/ticker`

**Type:** `GET`

**Content-Type:** `application/json`

**Description:** ticker

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
|contractName|string|true|Contract Name E.g. E-BTC-USDT |-|

**Response-fields:**

| Field                    | Type              | Description                          |
| ----------------------- | ----------------- | ------------------------------------ |
| time                    | long              | Open time                            |
| high                    | float             | Higher price                         |
| low                     | float             | Lower price                          |
| last                    | float             | Newest price                         | 
| vol                     | float             | Trade volume                         |
| rose                    | string            | Price variation                      |

## Kline/Candlestick Data

```demo
curl -X GET -i /fapi/v1/klines
```

> The above command returns JSON structured like this:

```json
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

**URL:** `/fapi/v1/klines`

**Type:** `GET`

**Content-Type:** `application/json`

**Description:** Kline/Candlestick Data

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
|contractName|string| true     |Contract Name E.g. E-BTC-USDT |-|
| interval              | string        | true     | identifies the sent value as: 1min,5min,15min,30min,1h,1day,1week,1month |
| limit                 | integer       | false    | Default 100, Max 300                    |

**Response-fields:**

| Field                    | Type              | Description                          |
| ----------------------- | ----------------- | ------------------------------------ |
| idx                     | long              | Start timestamp(ms)                  |
| high                    | float             | Higher price                         |
| low                     | float             | Lower price                          |
| close                   | float             | close price                         | 
| vol                     | float             | Trade volume                         |



