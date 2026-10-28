[BACK](./3_1_8_Preauthorization_reversal.md)
### 3.1.9 WPI preauthorization completion cancellation
The Service Type for a preauthorization completion cancellation transaction is `WPI_SVC_CANCEL_PAYMENT_COMPLETION`.

The `paymentSolutionReference` must identify the preauthorization completion to cancel. A completion can be cancelled only according to the rules of the authorization protocol and before the applicable cut-off time on the same day.

A successful cancellation returns the related preauthorization or preauthorization update to `AUTHORIZED` status.

**Cancellation conditions:**
- For AHUB, the completion must be in `AUTHORIZED` status and submitted before the cut-off time defined for the merchant or acquirer.
- For GICC, the completion may be in `AUTHORIZED` or `CLEARED` status and must be cancelled before the acquirer cut-off time.
- An existing pre-authorization, which the merchant has the right to modify

#### 3.1.9.1 WPI_REQUEST - list of supported input parameters

The mandatory field for preauthorization completion cancellation is `paymentSolutionReference`.

|Field name|Description|Type|Condition|
|----------|-----------|----|---------|
|paymentSolutionReference|Transaction-specific unique identification (UUID) of the preauthorization completion to cancel.|String (UUID)|Mandatory|

#### 3.1.9.2 WPI_RESPONSE - list of supported output parameters

|Field name|Description|Type|Condition|
|----------|-----------|----|---------|
|result|Result of the transaction: `WPI_RESULT_SUCCESS` for a successful transaction or `WPI_RESULT_FAILURE` for a failed transaction.|String|Mandatory|
|errorCondition|Specific error reason.|String|Mandatory|
|remark|Terminal / transaction specific message for detailed error descriptions.|String|Conditional - mandatory for an unsuccessful transaction|
|actionCode|Specific action to be performed by the business application.|String|Conditional - only for a successful transaction|
|merchantIdentifier|Merchant unique identifier (MID).|String|Mandatory|
|terminalIdentifier|Terminal unique identifier (TID).|String|Mandatory|
|terminalIdentifierLong|Terminal identifier built as `(Platform Identifier)-(Merchant Identifier)-(Platform Terminal identifier)`.|String|Mandatory|

[BACK](./3_1_10_1_Receipt_Format.md)
