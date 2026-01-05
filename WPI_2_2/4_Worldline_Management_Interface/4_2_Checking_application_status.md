[BACK](./4_1_Interface_structure_and_activity_launch.MD)
## 4.2 Checking application status
This function is intended to be used outside of payment acceptance context to determine the current Tap on Mobile application status and assess whether it is properly authenticated and ready to perform payment acceptance functions.

### 4.2.1 WMI_REQUEST - list of supported input parameters
None – might be created for future use.


### 4.2.2 WMI_RESPONSE - list of supported output parameters
|Field name|Description|Type|Condition|
|----------|-----------|-----------|-----------|
|result|Result of the transaction:<br><br>- `WPI_RESULT_SUCCESS` In case of successful transaction<br><br>- `WPI_RESULT_FAILURE` In case of failed transaction<br><br>|String|Mandatory|
|errorCondition|Specific error reason <br><br> For more information check [4.5 Error codes and proper error handling](./4_5_Error_codes_and_proper_error_handling.md)|String|Mandatory|
|remark|Terminal / transaction specific message for detailed error descriptions. Text provided by payment app.|String|Conditional – only for NOT successful transaction|
|appStatus|Tap on Mobile application status indicating whether application is already registered.<br><br>For more information check [Appendix C.3 Application statuses](../Appendix_C_Dictionaries/C_3_Application_statuses.md)


[NEXT](./4_3_Terminal_registration.md)






