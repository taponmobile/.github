[BACK](./3_1_3_Refund_and_Credit.MD)
### 3.1.4 Reversal
A reversal can be performed using the `WPI_SVC_CANCEL_PAYMENT` function. 

A reversal is a technical operation that cancels a previously completed card transaction. Depending on the configuration, it is possible to cancel only the last transaction (default configuration) or all transactions performed on the given day. If a reversal cannot be executed, a refund should be used instead.

**Important:** for BLIK/APM transactions, a reversal is not available; in such cases, only a full refund of the transaction amount can be performed.

**Prerequisites:**
- ToM application correctly installed.
- Terminal properly registered (paired with the ToM backend system).
- Transaction parameters (currency, etc.) must be in accordance with the terminal profile.

#### 3.1.4.1 WPI_REQUEST - list of supported input parameters

In `WPI_SVC_CANCEL_PAYMENT` at minimum the paymentSolutionReference (UUID of reversed transaction) is needed.

|Field name|Description|Type|Condition|
|----------|-----------|-----------|-----------|
|paymentSolutionReference| The UUID of the transaction for which the reversal will be executed.|String(UUID)|Mandatory|


#### 3.1.4.2 WPI_RESPONSE - list of supported output parameters
|Field name|Description|Type|Condition|
|----------|-----------|-----------|-----------|
|result|Result of the transaction:<br><br>- `WPI_RESULT_SUCCESS` In case of successful transaction<br><br>- `WPI_RESULT_FAILURE` In case of failed transaction<br><br>|String|Mandatory|
|errorCondition|Specific error reason <br><br> For more information check [3.3 Error codes and proper error handling](./3_3_Error_codes_and_proper_error_handling.md)|String|Mandatory|
|remark|Terminal / transaction specific message for detailed error descriptions. Text provided by payment app|String|Conditional – only for NOT successful transaction|
|actionCode|Specific action to be performed by the business application (always returned `WPI_ACTION_CODE_NONE`)|String|Conditional – only for successful transaction|
|merchantIdentifier|Merchant unique identifier (MID)|String|Mandatory|
|terminalIdentifier|Terminal unique identifier (MID)|String|Mandatory|
|terminalIdentifierLong|Terminal identifier build as (Platform Identifier)-(Merchant Identifier)-(Platform Terminal identifier)|String|Mandatory|

[NEXT](./3_1_5_1_Receipt_Format.md)
