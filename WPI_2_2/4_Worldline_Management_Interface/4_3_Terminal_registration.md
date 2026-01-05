[BACK](./4_2_Checking_application_status.md)
## 4.3 Terminal registration
This function is intended to be used outside of payment acceptance context to determine the current Tap on Mobile application status and assess whether it is properly authenticated and ready to perform payment acceptance functions.

### 4.3.1 WMI_REQUEST - list of supported input parameters
|Field name|Description|Type|Condition|
|----------|-----------|-----------|-----------|
|registrationToken|TID specific registration token retrieved from Tap on Mobile backend (Merchant API); in case this parameter is not present, Tap on Mobile app will collect all required permissions and launch QR-code reader to scan the registration token;|String|Optional|

### 4.3.2 WMI_RESPONSE - list of supported output parameters
|Field name|Description|Type|Condition|
|----------|-----------|-----------|-----------|
|result|Result of the transaction:<br><br>- `WPI_RESULT_SUCCESS` In case of successful transaction<br><br>- `WPI_RESULT_FAILURE` In case of failed transaction<br><br>|String|Mandatory|
|errorCondition|Specific error reason <br><br> For more information check [4.5 Error codes and proper error handling](./4_5_Error_codes_and_proper_error_handling.md)|String|Mandatory|
|remark|Terminal / transaction specific message for detailed error descriptions. Text provided by payment app.|String|Conditional – only for NOT successful transaction|

[NEXT](./4_4_Terminal_unregistration.md)

