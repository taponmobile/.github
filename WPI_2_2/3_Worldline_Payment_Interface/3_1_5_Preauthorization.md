[BACK](./3_1_4_Reversal.MD)
### 3.1.4 WPI preauthorization
The Service Type for a preauthorization transaction is `WPI_SVC_PRE_AUTHORIZATION`.

**Prerequisites:**
- ToM application correctly installed.
- Terminal properly registered (paired with the ToM backend system).
- Preauthorization enabled for the merchant, terminal and payment brand.
- Transaction currency and parameters must be in accordance with the terminal profile.

#### 3.1.4.1 WPI_REQUEST - list of supported input parameters

The mandatory fields for preauthorization are `currency` and `requestedAmount`.

|Field name|Description|Type|Condition|
|----------|-----------|----|---------|
|currency|Currency of the amount. Alpha code value is defined in ISO 4217 (e.g. EUR).|String|Mandatory|
|requestedAmount|Preauthorization amount as minor unit.|Integer|Mandatory|
|reference|Reference (external transaction id).|String|Optional|
|receiptFormat|Transaction confirmation format.|Array|Optional|
|checkoutId|Checkout identifier.|String (UUID)|Conditional - mandatory when checkout verification is enabled for the acquirer|

#### 3.1.4.2 WPI_RESPONSE - list of supported output parameters

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
|paymentSolutionReference|Transaction-specific unique identification (UUID) of the preauthorization.|String (UUID)|Conditional - mandatory for a successful transaction|
|reference|Reference (external transaction id).|String|Conditional - returned if set for the transaction|
|merchantIdentifier|Merchant unique identifier (MID).|String|Mandatory|
|terminalIdentifier|Terminal unique identifier (TID).|String|Mandatory|
|dccOffered|Indicates whether DCC was active and a DCC selection was shown to the cardholder.|Boolean|Conditional|
|dccUsed|Indicates whether the cardholder accepted the DCC offer.|Boolean|Conditional|
|dccAmount|Cardholder amount in the cardholder's currency.|Integer|Conditional - if `dccUsed` is `true`|
|dccCurrency|Cardholder currency.|String|Conditional - if `dccUsed` is `true`|
|dccExchangeRate|Exchange rate used.|String|Conditional - if `dccUsed` is `true`|
|cardholderVerificationMethod|Cardholder verification method.|String|Conditional - mandatory for a successful transaction|
|cardDataInput|The card data input method.|String|Conditional - mandatory for a successful transaction|
|terminalIdentifierLong|Terminal identifier built as `(Platform Identifier)-(Merchant Identifier)-(Platform Terminal identifier)`.|String|Mandatory|
|onlineToken|Card token|String|C <br><br>(Mandatory if card_token returned by host)|
|expiryDate|Card expiry date|String (format YYMM)|C <br><br>(Mandatory for successful card transaction if provided – not present when hidden (****))|

[NEXT](./3_1_6_Preauthorization_update.md)
