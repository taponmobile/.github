[BACK](./3_1_7_Preauthorization_completion.md)
### 3.1.8 WPI preauthorization cancellation
The Service Type for a preauthorization cancellation is `WPI_SVC_CANCEL_PRE_AUTHORIZATION`.

The request identifies the preauthorization or its latest successful update by `paymentSolutionReference`.

**Prerequisites:**
- ToM application correctly installed.
- Terminal properly registered (paired with the ToM backend system).
- The referenced preauthorization is authorized and has not expired.
- An existing preauthorization, which the merchant has the right to modify

#### 3.1.8.1 WPI_REQUEST - list of supported input parameters

The mandatory field for preauthorization cancellation is `paymentSolutionReference`.

|Field name|Description|Type|Condition|
|----------|-----------|----|---------|
|paymentSolutionReference|Transaction-specific unique identification (UUID) of the preauthorization or latest successful preauthorization update to cancel.|String (UUID)|Mandatory|

#### 3.1.8.2 WPI_RESPONSE - list of supported output parameters

|Field name|Description|Type|Condition|
|----------|-----------|----|---------|
|result|Result of the transaction: `WPI_RESULT_SUCCESS` for a successful transaction or `WPI_RESULT_FAILURE` for a failed transaction.|String|Mandatory|
|errorCondition|Specific error reason.|String|Mandatory|
|remark|Terminal / transaction specific message for detailed error descriptions. Text provided by the payment app.|String|Conditional - mandatory for an unsuccessful transaction|
|actionCode|Specific action to be performed by the business application.|String|Conditional - only for a successful transaction|
|merchantIdentifier|Merchant unique identifier (MID).|String|Mandatory|
|terminalIdentifier|Terminal unique identifier (TID).|String|Mandatory|
|terminalIdentifierLong|Terminal identifier built as `(Platform Identifier)-(Merchant Identifier)-(Platform Terminal identifier)`.|String|Mandatory|

[NEXT](./3_1_9_Preauthorization_completion_reversal.md)
