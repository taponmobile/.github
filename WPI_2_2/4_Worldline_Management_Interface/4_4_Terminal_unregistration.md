[BACK](./4_3_Terminal_registration.md)
## 4.4 Terminal	unregistration
This function is intended to be used only with already registered terminal. It allows to unregister the currently assigned TID from the mobile application instance.

### 4.4.1 WMI_REQUEST - list of supported input parameters
None – might be created for future use;

### 4.4.2 WMI_RESPONSE - list of supported output parameters
|Field name|Description|Type|Condition|
|----------|-----------|-----------|-----------|
|result|Result of the transaction:<br><br>- `WPI_RESULT_SUCCESS` In case of successful transaction<br><br>- `WPI_RESULT_FAILURE` In case of failed transaction<br><br>|String|Mandatory|
|errorCondition|Specific error reason <br><br> For more information check [4.5 Error codes and proper error handling](./4_5_Error_codes_and_proper_error_handling.md)|String|Mandatory|
|remark|Terminal / transaction specific message for detailed error descriptions. Text provided by payment app.|String|Conditional – only for NOT successful transaction|


[NEXT](./4_5_Error_codes_and_proper_error_handling.md)