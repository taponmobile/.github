[BACK](./3_1_1_Interface_structure_and_activity_launch.MD)
### 3.1.2 Payment
The Service Type for a purchase transaction is `WPI_SVC_PAYMENT`.

**Prerequisites:**
- ToM application correctly installed.
- Terminal properly registered (paired with the ToM backend system).
- Transaction parameters (currency, etc.) must be in accordance with the terminal profile.

#### 3.1.2.1 WPI_REQUEST - list of supported input parameters

In `WPI_SVC_PAYMENT`, at a minimum, the currency and requested amount are needed. The full list of parameters is described in the table below.

|Field name|Description|Type|Condition|
|----------|-----------|-----------|-----------|
|currency|Currency of the amount. Alpha code value is defined in ISO 4217 (e.g. EUR)|String|Mandatory|
|requestedAmount|Total payment amount as minor unit. The fractional digits are evaluated based in the currency. For example, 11.91€ must be sent as 1191 and the currency as EUR. <br><br>(tip amount is excluded)|Integer|Mandatory|
|tipAmount|The tip amount to be used as minor unit. This amount has the same currency as the transaction amount.<br><br> For more information check [3.1.5.3 Tipping](./3_1_5_3_Tipping.md)|Integer|Optional|
|reference|Reference (external transaction id) to be sent to the payment solution for reconciliation<br><br>Due to the limitation of acquiring systems, only following characters are supported: ('a'..'z', 'A'..'Z', '0'..'9', hex 40 - hex FF) <br><br>max. length of this field is 30 characters|String|Optional|
|receiptFormat|Transaction confirmation format. The possible options are a set of data in JSON format to build the confirmation, a text-based confirmation, or displaying the transaction confirmation in the application.<br><br> For more information check [3.1.5.1 Receipt Format](./3_1_5_1_Receipt_Format.md)|Array|Optional|
|onBehalf|Multi-merchant mode - on behalf transaction flag<br><br> For more information check [3.1.5.2 Transactions on Behalf](./3_1_5_2_Transactions_on_Behalf.md)|Boolean|Optional – required when transaction should be performed ‘on behalf’ in multi-merchant mode.|
|partnerTid|Multi-merchant mode - partner terminal TID<br><br> For more information check [3.1.5.2 Transactions on Behalf](./3_1_5_2_Transactions_on_Behalf.md)|String|Conditional|
|partnerMid|Multi-merchant mode - partner terminal MID<br><br> For more information check [3.1.5.2 Transactions on Behalf](./3_1_5_2_Transactions_on_Behalf.md)|String|Conditional|	
|partnerTerminalUuid|Multi-merchant mode - partner terminal UUID<br><br> For more information check [3.1.5.2 Transactions on Behalf](./3_1_5_2_Transactions_on_Behalf.md)|String (UUID)|Conditional|
|partnerTerminalExtId|Multi-merchant mode - partner terminal external Id<br><br> For more information check [3.1.5.2 Transactions on Behalf](./3_1_5_2_Transactions_on_Behalf.md)|String|Conditional|
|checkoutId|Checkout identifier<br><br> For more information check [3.1.5.4 Checkouts](./3_1_5_4_Checkouts.md)|String (UUID)|Optional – required when merchant operates under acquirer configured with checkout verification.|

#### 3.1.2.2 WPI_RESPONSE - list of supported output parameters
|Field name|Description|Type|Condition|
|----------|-----------|-----------|-----------|
|result|Result of the transaction:<br><br>- `WPI_RESULT_SUCCESS` In case of successful transaction<br><br>- `WPI_RESULT_FAILURE` In case of failed transaction<br><br>|String|Mandatory|
|errorCondition|Specific error reason <br><br> For more information check [3.3 Error codes and proper error handling](./3_3_Error_codes_and_proper_error_handling.md)|String|Mandatory|
|remark|Terminal / transaction specific message for detailed error descriptions. Text provided by payment app.|String|Conditional – only for NOT successful transaction|
|actionCode|Specific action to be performed by the business application (always returned `WPI_ACTION_CODE_NONE`)|String|Conditional – only for successful transaction|
|timestamp|Date and time of the transaction, indicated by the acquirer. <br><br> Format according to ISO 8601|String (ISO 8601|Conditional – only for successful transaction|
|currency|Currency code of the transaction. Alpha code value defined in ISO 4217 e.g. EUR|String|Conditional – only for successful transaction|
|authorizedAmount|Amount of the transaction. The fraction is taken from the currency code. <br><br>Example: <br>Currency = EUR <br>requestedAmount = 3190<br>=> 31,90 €|Integer|Conditional – only for successful transaction|
|brandName|Brand name of used payment method <br><br> For more information check [Appendix C.1 Brand Name](../Appendix_C_Dictionaries/C_1_brandName.md)|String|Conditional – only for successful transaction|
|customerLanguage|The merchant’s default language (set in the merchant’s data)<br><br>Format according to ISO 630-1 (alpha-2 code)|String|Conditional – only for successful transaction|
|applicationIdentifier|Payment card application identifier dependent on the used card e.g. for MasterCard A00000041010|String|Conditional – only for successful transaction in which a payment card was used|
|applicationLabel|Payment card application label, depending on the used card e.g. MasterCard DEBIT|String|Conditional – only for successful transaction in which a payment card was used|
|receipt|Details for the receipt.<br><br> For more information check [3.1.5.1 Receipt Format](./3_1_5_1_Receipt_Format.md)|Array|Conditional: <br><br>- always present for successful transactions <br><br>- always present if card was tapped|
|paymentSolutionReference|Transaction specific and unique identification (format: UUID)| String (UUID)|Conditional <br><br>- always present for successful transactions<br><br>- optional for failed transactions|
|reference|	Reference (external transaction id) - set based on the value of the field with the same name sent in the request|String|Optional - presented if provided in the request|
|merchantIdentifier|Merchant unique identifier (MID)|String|Mandatory|
|terminalIdentifier|Terminal unique identifier (MID)|String|Mandatory|
|tipAmount|The tip amount added to authorisation amount as minor unit. This amount has the same currency as the transaction amount. The fraction is taken from the currency code.|Integer|Conditional - in case of tip is active and entered by the cardholder during transaction processing or provided in the request|
|dccOffered|True - in case of DCC is active and DCC selection was shown towards the cardholder|Boolean|Conditional - in case of DCC is active and DCC selection was shown towards the cardholder|
|dccUsed|True - in case of DCC was selected by the cardholder|Boolean|Conditional - in case of DCC was selected by the cardholder|	
|dccAmount|Cardholder amount (Amount in cardholder currency|Integer|Conditional - in case of DCC is active and the cardholder has selected his own currency|	
|dccCurrency|Cardholder currency |String|Conditional - in case of DCC is active and the cardholder has selected his own currency|	
|dccExchangeRate|Used exchange rate|String|Conditional - in case of DCC is active and the cardholder has selected his own currency|	
|cardholderVerificationMethod|Cardholder verification method<br><br> For more information check [Appendix C.2 Cardholder Verification Method](../Appendix_C_Dictionaries/C_2_cardholderVerificationMethod.md)|String	Conditional - in case of successful transaction|
|cardDataInput|The card data input method:<br><br>- `WPI_CARD_DATA_INPUT_PROXIMITY_ICC` - for card transactions<br><br>- `WPI_CARD_DATA_INPUT_ALTERNATIVE_PAYMENT_METHOD` - for BLIK and APM transactions |String|Conditional - in case of successful transaction|
|onBehalf |	Inform if transaction was made on behalf of partner merchant – on partner terminal|Boolean|Conditional - mandatory for transaction performed on-behalf|
|terminalIdentifierLong|Terminal identifier built as (Platform Identifier)-(Merchant Identifier)-(Platform Terminal identifier)|String|Mandatory|

[NEXT](./3_1_3_Refund_and_Credit.MD)