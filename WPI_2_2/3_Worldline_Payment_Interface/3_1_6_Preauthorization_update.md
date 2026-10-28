[BACK](./3_1_5_Preauthorization.md)
### 3.1.6 WPI preauthorization update
The Service Type for a preauthorization update transaction is `WPI_SVC_UPDATE_PRE_AUTHORIZATION`.

A successful preauthorization update replaces the previous preauthorization. The `requestedAmount` is incremental, while the mobile API expects the new total preauthorization amount; therefore, the mobile application must obtain the preauthorization details from the Main Server and calculate the incremental amount.

**Prerequisites:**
- ToM application correctly installed.
- Terminal properly registered (paired with the ToM backend system).
- An active, authorized, unexpired preauthorization is available for update.
- Transaction currency and parameters must be in accordance with the terminal profile.
- An existing preauthorization, which the merchant has the right to modify

#### 3.1.6.1 WPI_REQUEST - list of supported input parameters

The mandatory fields for preauthorization update are `currency`, `requestedAmount`, `amountType` and `paymentSolutionReference`.

|Field name|Description|Type|Condition|
|----------|-----------|----|---------|
|currency|Currency of the amount. Alpha code value is defined in ISO 4217 (e.g. EUR).|String|Mandatory|
|requestedAmount|Total payment amount as minor unit.  .|Integer|Mandatory|
|amountType|New preauthorization amount: WPI_AMOUNT_TYPE_REPLACEMENT; Other types are not supported|String| Mandatory|
|reference|Reference (external transaction id).|String|Optional|
|receiptFormat|Transaction confirmation format.|Array|Optional|
|checkoutId|Checkout identifier.|String (UUID)|Conditional - mandatory when checkout verification is enabled for the acquirer|
|paymentSolutionReference|Transaction-specific unique identification (UUID) of the preauthorization to update.|String (UUID)|Mandatory|

#### 3.1.6.2 WPI_RESPONSE - list of supported output parameters

Version 1.3 of the source document notes that `amountType` was removed from `WPI_SVC_UPDATE_PRE_AUTHORIZATION` in WPI version 2.2; it is therefore not included below.

|Field name|Description|Type|Condition|
|----------|-----------|----|---------|
|result|Result of the transaction: `WPI_RESULT_SUCCESS` for a successful transaction or `WPI_RESULT_FAILURE` for a failed transaction.|String|Mandatory|
|errorCondition|Specific error reason.|String|Mandatory|
|remark|Terminal / transaction specific message for detailed error descriptions. Text provided by the payment app.|String|Conditional - mandatory for an unsuccessful transaction|
|actionCode|Specific action to be performed by the business application.|String|Conditional - only for a successful transaction|
|timestamp|Date and time of the transaction, indicated by the acquirer. Format according to ISO 8601.|String (DateTime ISO 8601)|Conditional - only for a successful transaction|
|currency|Alpha currency code of the transaction, defined in ISO 4217.|String|Conditional - only for a successful transaction|
|authorizedAmount|Amount of the transaction without a decimal separator. Fractional digits are determined by the currency code.|Integer|Conditional - only for a successful transaction|
|amountType|New preauthorization amount: WPI_AMOUNT_TYPE_REPLACEMENT; Other types are not supported| String|Conditional - only for a successful transaction|
|brandName|Brand name of the used payment method.|String|Conditional - only for a successful transaction|
|customerLanguage|The merchant's default language (alpha-2 code).|String|Conditional - only for a successful transaction|
|applicationIdentifier|Payment card application identifier (AID).|String|Conditional - only for a successful transaction|
|applicationLabel|Payment card application label.|String|Conditional - only for a successful transaction|
|receipt|Details for the receipt.|Array|Conditional - only for a successful transaction|
|paymentSolutionReference|Transaction-specific unique identification (UUID) of the preauthorization update.|String (UUID)|Conditional - mandatory for a successful transaction|
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

[NEXT](./3_1_7_Preauthorization_completion.md)
