[BACK](./6_7_PTP_transaction_statuses.md)

Following error codes may be returned by MPPA.
|Error code|Description|
|---------|-----------|
|MPPA_OK|Success|
|MPPA_ERR_BUSY|Another intent request is being processed - in such situation both request (ongoing and new) will be finished.|
|MPPA_ERR_CARD_READ|Card was refused during reading (card is not supported or errors during card reading).|
|MPPA_ERR_TERMINAL_DECLINED|Transaction declined by kernel|
|MPPA_ERR_GENERIC|NFC hardware not available other technical error on device.|
|MPPA_ERR_NOT_REGISTERED|Terminal is not registered|
|MPPA_ERR_HOST_REFUSAL|Transaction was refused by ToM host.|
|MPPA_ERR_INTERNAL|Application internal error\other unhandled errors.|
|MPPA_ERR_INVALID_AMOUNT|In request parameters entered invalid transaction amount, e.g. 0 or transaction amount exceeds transaction limit.|
|MPPA_ERR_INVALID_CURRENCY|In request parameters entered invalid currency other than parametrized for terminal.|
|MPPA_ERR_INVALID_TRANSACTION_REQ|- security errors during application start <br><br>- pin collection or cancellation of transaction was called but transaction does not exist, can't be cancelled or transaction status does not allow for pin collection.|
|MPPA_ERR_MISSING_MANDATORY_PARAMETER|One of the mandatory parameters is missing in MPPA_REQUEST|
|MPPA_ERR_NOT_INITIALIZED|The payment solution is not configured and cannot process the request.|
|MPPA_ERR_TRANSACTION_TIMEOUT|Timeout caused by the customer — the time expired for card reading, PIN entry, etc.|
|MPPA_ERR_USER_CANCEL|Transaction cancelled by user before finalization.|
|MPPA_ERR_UPDATE_REQUIRED|A newer version of the application is available, and the user interrupted the intent call to download it.<br><br>- An application update is required, but the user refused the update.|
|MPPA_ERR_INVALID_PIN_TOKEN|PIN token is invalid or expired|
|MPPA_ERR_TRANSACTION_TYPE_NOT_SUPPORTED|Requested transaction type is not supported on terminal e.g. credit is not enabled.|
|MPPA_ERR_ENCRYPTION_FAILURE|Transaction data encryption error, e.g. no access to Cryptohub|
|MPPA_ERR_TRANSACTION_NOT_FOUND|Transaction not found|
|MPPA_ERR_TRANSACTION_CANCEL_FAILED|Transaction cancellation failed|
|MPPA_ERR_NO_SUPPORTED_CARDS|List of supported cards is empty due to missing configuration|

[NEXT](../5_Tap_on_Mobile_backend_API/5_1_ToM_backend_API_OAuth2_authentication.md)
