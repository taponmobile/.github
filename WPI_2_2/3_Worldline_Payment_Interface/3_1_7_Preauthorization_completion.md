[BACK](./3_1_6_Preauthorization_update.md)
### 3.1.8 WPI preauthorization completion
The Service Type for a preauthorization completion transaction is `WPI_SVC_PAYMENT_COMPLETION`.

The completion amount must not exceed the amount of the referenced preauthorization. The `paymentSolutionReference` must identify the preauthorization or its latest successful update.

**Prerequisites:**
- ToM application correctly installed.
- Terminal properly registered (paired with the ToM backend system).
- An active, authorized, unexpired preauthorization is available for completion.
- Transaction currency and parameters must be in accordance with the terminal profile.
- An existing pre-authorization, which the merchant has the right to modify

#### 3.1.8.1 WPI_REQUEST - list of supported input parameters

The mandatory fields for preauthorization completion are `currency`, `requestedAmount` and `paymentSolutionReference`.

|Field name|Description|Type|Condition|
|----------|-----------|----|---------|
|currency|Currency of the amount. Alpha code value is defined in ISO 4217 (e.g. EUR).|String|Mandatory|
|requestedAmount|Total payment amount as minor unit. Must be less than or equal to the previously authorized amount.|Integer|Mandatory|
|reference|Reference (external transaction id).|String|Optional|
|receiptFormat|Transaction confirmation format.|Array|Optional|
|checkoutId|Checkout identifier.|String (UUID)|Conditional - mandatory when checkout verification is enabled for the acquirer|
|paymentSolutionReference|Transaction-specific unique identification (UUID) of the preauthorization or latest successful preauthorization update.|String (UUID)|Mandatory|

#### 3.1.8.2 WPI_RESPONSE - list of supported output parameters

|Field name|Description|Type|Condition|
|----------|-----------|----|---------|
|result|Result of the transaction: `WPI_RESULT_SUCCESS` for a successful transaction or `WPI_RESULT_FAILURE` for a failed transaction.|String|Mandatory|
|errorCondition|Specific error reason.|String|Mandatory|
|remark|Terminal / transaction specific message for detailed error descriptions. Text provided by the payment app.|String|Conditional - mandatory for an unsuccessful transaction|
|actionCode|Specific action to be performed by the business application.|String|Conditional - only for a successful transaction|
|timestamp|Date and time of the transaction, indicated by the acquirer. Format according to ISO 8601.|String (DateTime ISO 8601)|Conditional - only for a successful transaction|
|currency|Alpha currency code of the transaction, defined in ISO 4217.|String|Conditional - only for a successful transaction|
|authorizedAmount|Amount of the transaction without a decimal separator. Fractional digits are determined by the currency code.|Integer|Conditional - only for a successful transaction|
|brandName|Brand name of the used payment method.|String|Conditional - only for a successful transaction|
|customerLanguage|The merchant's default language (alpha-2 code).|String|Conditional - only for a successful transaction|
|applicationIdentifier|Payment card application identifier (AID).|String|Conditional - only for a successful transaction|
|applicationLabel|Payment card application label.|String|Conditional - only for a successful transaction|
|receipt|Details for the receipt.|Array|Conditional - only for a successful transaction|
|paymentSolutionReference|Transaction-specific unique identification (UUID) of the preauthorization completion.|String (UUID)|Conditional - mandatory for a successful transaction|
|reference|Reference (external transaction id).|String|Conditional - returned if set for the transaction|
|merchantIdentifier|Merchant unique identifier (MID).|String|Mandatory|
|terminalIdentifier|Terminal unique identifier (TID).|String|Mandatory|
|dccOffered|Indicates whether DCC was offered. The source specifies `false` (no DCC offer presentation).|Boolean|Conditional|
|dccUsed|Indicates whether the DCC offer was applied to the transaction.|Boolean|Conditional|
|dccAmount|Cardholder amount in the cardholder's currency.|Integer|Conditional - if `dccUsed` is `true`|
|dccCurrency|Cardholder currency.|String|Conditional - if `dccUsed` is `true`|
|dccExchangeRate|Exchange rate used.|String|Conditional - if `dccUsed` is `true`|
|cardholderVerificationMethod|`WPI_CVM_NO_CVM`.|String|Conditional - mandatory for a successful transaction|
|cardDataInput|`WPI_CARD_DATA_INPUT_REFERENCE_BASED`.|String|Conditional - mandatory for a successful transaction|
|terminalIdentifierLong|Terminal identifier built as `(Platform Identifier)-(Merchant Identifier)-(Platform Terminal identifier)`.|String|Mandatory|

[NEXT](./3_1_8_Preauthorization_reversal.md)
