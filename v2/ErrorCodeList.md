
# Error code list

| Error code | Description |
|------------|-------------|
|0|Success|
|-1000|Unknown error occurred while processing the request|
|-1001|Internal error; unable to process your request. Please try again|
|-1002|You are not authorized to perform this request. The request requires sending an API Key; we recommend attaching X-CH-APIKEY to all request headers|
|-1003|Request frequency exceeds the limit|
|-1004|You are not authorized to perform this request; user does not exist|
|-1006|Received a message that does not conform to the expected format; order status is unknown|
|-1007|Timeout waiting for backend server response. Sending status is unknown; execution status is unknown|
|-1014|Unsupported order combination|
|-1015|Too many orders. Please reduce the number of your orders|
|-1016|Server offline|
|-1017|We recommend attaching Content-Type to all request headers and setting it to application/json|
|-1020|UNSUPPORTED_OPERATION|
|-1021|Invalid timestamp; time offset is too large|
|-1022|Invalid signature|
|-1023|You are not authorized to perform this request. The request requires sending a timestamp; we recommend attaching X-CH-TS to all request headers|
|-1024|You are not authorized to perform this request. The request requires sending a sign; we recommend attaching X-CH-SIGN to all request headers|
|-1025|User has not activated the contract|
|-1100|Illegal characters in the request|
|-1101|Too many parameters sent|
|-1102|Required parameter {0} not sent, empty, or in the wrong format|
|-1103|Unknown parameters sent|
|-1104|Not all sent parameters have been read|
|-1105|Parameter {0} is empty|
|-1106|This parameter does not need to be sent|
|-1111|Precision exceeds the maximum value defined for this asset|
|-1112|No orders exist for the trading pair|
|-1116|Invalid order type|
|-1117|Invalid buy/sell direction|
|-1118|New client order ID is empty|
|-1121|Invalid contract|
|-1136|Order quantity is less than the minimum value|
|-1137|Order quantity exceeds the maximum limit|
|-1138|Order price is out of allowable range|
|-1139|This trading pair does not support market orders|
|-1140|Exceeds the maximum position limit|
|-1141|Duplicate cancellation or invalid order|
|-1145|Order status does not allow cancellation|
|-1146|Current contract cannot be traded temporarily|
|-1147|The current interface does not support coin-margined contracts|
|-1148|The current interface does not support USDT-margined contracts|
|-1149|Your isolated position does not exist|
|-1150|Maximum of {0} decimal places allowed|
|-1151|Transfer amount exceeds the limit|
|-1152|Position leverage adjustment failed|
|-1153|Maximum leverage does not exceed {0}|
|-1154|Order quantity exceeds the maximum limit|
|-1155|Order price deviates significantly from the latest trade price|
|-1156|Closing quantity exceeds the total position quantity|
|-1157|Position frozen, cannot be operated temporarily|
|-1158|Total order quantity exceeds the limit|
|-1159|Maximum of {0} decimal places allowed for order amount|
|-1160|Minimum order amount is {0}|
|-1161|Maximum order amount is {0}|
|-1162|Maximum of {0} decimal places allowed for limit order amount|
|-1163|There are currently open orders; leverage cannot be modified|
|-1164|Order quantity must be greater than {0}|
|-1165|Order type does not match user contract configuration {0}|
|-1166|Order leverage does not match user contract configuration {0}|
|-1167|Order book is too large; self-trade prevention failed|
|-1168|Order book is missing|
|-2013|Order does not exist|
|-2014|Invalid API key format|
|-2015|Invalid API key, IP, or permission|
|-2016|Trading is frozen|
|-2017|Insufficient balance|
|-2100|Parameter issue|
|-2101|User IP is non-compliant and the country is forcibly banned|
|-2102|User IP is soft-banned in the country|


