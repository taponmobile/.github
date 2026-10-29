## 3.4 Request and Response Examples

### 1. Successful card payment without a tip or DCC

#### Assumptions

- WPI version: `2.2`
- The application is registered on a terminal with TID (Terminal ID) `POSTMAN1` and MID (Merchant ID) `102003271`.
- DCC is disabled on the terminal.
- Tokenization is disabled.
- The terminal currency is PLN.
- The transaction amount is PLN 15.00.
- The CVM threshold is set to PLN 100.
- The payment is made with a VISA card.
- The transaction reference (external transaction ID) is set to `uniqueExtId`.
- `receiptFormat` is not specified in the request, so the default format, `FORMATTED`, is used.

#### WPI_REQUEST

```json
{
  "currency": "PLN",
  "requestedAmount": 1500,
  "reference": "uniqueExtId"
}
```

#### Expected Application Behavior

- If tips are enabled on the terminal, the application displays a screen for entering a tip. In this example, no tip is added. If tips are not available, this screen is skipped automatically.
- If more than one payment method is available on the terminal, the application displays a payment method selection screen. In this example, card payment is selected. If only one payment method is available, it is selected automatically.
- The application displays a screen prompting the customer to tap their card. In this example, the VISA card is read successfully.
- The payment scheme animation is displayed.
- The intent completes.

#### WPI_RESPONCE

```json
{
  "actionCode": "WPI_ACTION_CODE_NONE",
  "applicationIdentifier": "A0000000031010",
  "applicationLabel": "VISA CREDIT",
  "authorizedAmount": 1500,
  "brandName": "WPI_BRAND_NAME_VISA",
  "cardDataInput": "WPI_CARD_DATA_INPUT_PROXIMITY_ICC",
  "cardholderVerificationMethod": "WPI_CVM_NO_CVM",
  "currency": "PLN",
  "customerLanguage": "en",
  "errorCondition": "WPI_ERR_COND_NONE",
  "merchantIdentifier": "102003271",
  "onBehalf": false,
  "paymentSolutionReference": "3371a7ce-a251-44d5-bc11-4e218f85ce0e",
  "receipt": {
    "formatted": {
      "client": "This is to confirm your transaction     \n registered at:                          \n ----------------------------------------\n APM TEST & Merchant                     \n APM street 1                            \n APM city 1234                           \n ----------------------------------------\n 28.10.2026 16:26:11                     \n VISA       438746******9995             \n PLN                                15.00\n Transaction details:                    \n Status:                          CLEARED\n Authorization code:           (00)000671\n ARQC:                   7289513027EE18D8\n AID:                      A0000000031010\n Contactless                             \n Card expiry date:                   2912\n Type:                               SALE\n POS ID:                         POSTMAN1\n MID:                           102003271\n Reference:                   uniqueExtId\n VISA\n ",
      "merchant": "This is to confirm your transaction     \n registered at:                          \n ----------------------------------------\n APM TEST & Merchant                     \n APM street 1                            \n APM city 1234                           \n ----------------------------------------\n 28.10.2026 16:26:11                     \n VISA       438746******9995             \n PLN                                15.00\n Transaction details:                    \n Status:                          CLEARED\n Authorization code:           (00)000671\n ARQC:                   7289513027EE18D8\n AID:                      A0000000031010\n Contactless                             \n Card expiry date:                   2912\n Type:                               SALE\n POS ID:                         POSTMAN1\n MID:                           102003271\n Reference:                   uniqueExtId\n VISA\n "
    }
  },
  "reference": "uniqueExtId",
  "result": "WPI_RESULT_SUCCESS",
  "terminalIdentifier": "POSTMAN1",
  "terminalIdentifierLong": "ToM-POSTMAN1-102003271",
  "timestamp": "2026-10-28T16:26:11+01:00"
}
```
### 2. Successful card over cvm (with pin) payment with a tip and without DCC

#### Assumptions

- WPI version: `2.2`
- The application is registered on a terminal with TID (Terminal ID) `POSTMAN1` and MID (Merchant ID) `102003271`.
- DCC is disabled on the terminal.
- Tokenization is disabled.
- TIP is enabled on terminal
- The terminal currency is PLN.
- The transaction amount is PLN 115.00.
- The CVM threshold is set to PLN 100.
- The payment is made with a VISA card.
- The transaction reference (external transaction ID) is set to `uniqueExtId`.
- `receiptFormat` is set to `FORMATTED`, is used.

#### WPI_REQUEST

```json
{
 "currency": "{{currency}}",
 "requestedAmount": 11500,
 "tipAmount": 500,
 "reference": "uniqueExtId",
 "receiptFormat": ["FORMATTED"]
}
```

#### Expected Application Behavior

- Tip amount was delivwered in request, so the tip selection screen will be skipped.
- If more than one payment method is available on the terminal, the application displays a payment method selection screen. In this example, card payment is selected. If only one payment method is available, it is selected automatically.
- The application displays a screen prompting the customer to tap their card. In this example, the VISA card is read successfully.
- The pin screen is displayed.
- The payment scheme animation is displayed.
- The intent completes.

#### WPI_RESPONCE
```json
{
        "actionCode": "WPI_ACTION_CODE_NONE",
        "applicationIdentifier": "A0000000031010",
        "applicationLabel": "VISA CREDIT",
        "authorizedAmount": 12000,
        "brandName": "WPI_BRAND_NAME_VISA",
        "cardDataInput": "WPI_CARD_DATA_INPUT_PROXIMITY_ICC",
        "cardholderVerificationMethod": "WPI_CVM_PIN_ONLINE",
        "currency": "PLN",
        "customerLanguage": "en",
        "errorCondition": "WPI_ERR_COND_NONE",
        "merchantIdentifier": "102003271",
        "onBehalf": false,
        "paymentSolutionReference": "fd9d7be8-6e82-4db6-b967-3824b49ea58d",
        "receipt": {
            "formatted": {
                "client": "This is to confirm your transaction     \n registered at:                          \n ----------------------------------------\n APM TEST & Merchant                     \n APM street 1                            \n APM city 1234                           \n ----------------------------------------\n 29.10.2026 14:27:59                     \n VISA       438746******9995             \n Amount:                       PLN 115.00\n Tip Amount:                     PLN 5.00\n Total Amount:                 PLN 120.00\n Transaction details:                    \n Status:                          CLEARED\n Authorization code:           (00)000671\n ARQC:                   1F2DDB016B2F0998\n AID:                      A0000000031010\n Contactless                             \n Card expiry date:                   2912\n Type:                               SALE\n POS ID:                         POSTMAN1\n MID:                           102003271\n Reference:                   uniqueExtId\n VISA\n ",
                "merchant": "This is to confirm your transaction     \n registered at:                          \n ----------------------------------------\n APM TEST & Merchant                     \n APM street 1                            \n APM city 1234                           \n ----------------------------------------\n 29.10.2026 14:27:59                     \n VISA       438746******9995             \n Amount:                       PLN 115.00\n Tip Amount:                     PLN 5.00\n Total Amount:                 PLN 120.00\n Transaction details:                    \n Status:                          CLEARED\n Authorization code:           (00)000671\n ARQC:                   1F2DDB016B2F0998\n AID:                      A0000000031010\n Contactless                             \n Card expiry date:                   2912\n Type:                               SALE\n POS ID:                         POSTMAN1\n MID:                           102003271\n Reference:                   uniqueExtId\n VISA\n "
            }
        },
        "reference": "uniqueExtId",
        "result": "WPI_RESULT_SUCCESS",
        "terminalIdentifier": "POSTMAN1",
        "terminalIdentifierLong": "ToM-POSTMAN1-102003271",
        "timestamp": "2026-10-29T14:27:59+01:00",
        "tipAmount": 500
    }
```
Pay attention to the field specific to tips: tipAmount
