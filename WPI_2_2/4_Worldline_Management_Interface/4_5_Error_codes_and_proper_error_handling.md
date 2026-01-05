[BACK](./4_3_Terminal_unregistration.md)
## 4.5 Error codes and proper error handling

|Error condition|Description|
|-----------|-----------|
|WMI_ERR_COND_NONE|Will always be present if no error occurred, confirms successful result|
|WMI_ERR_COND_AUTH_NOT_POSSIBLE|Valid terminal registration was not found.|
|WMI_ERR_COND_GENERIC|A mobile application generic error that is not explicitly outlined here|
|WMI_ERR_COND_INTERNAL|Backend-driven generic error that is not explicitly outlined here|
|WMI_ERR_COND_INVALID_JSON|Wrong structure of `WMI_REQUEST` json|
|WMI_ERR_COND_NETWORK_ISSUE|Problems with network connection|
|WMI_ERR_COND_SERVICE_NOT_SUPPORTED|Requested service type is not supported by the Payment Application|
|WMI_ERR_COND_TERMINAL_BUSY|Terminal communication is exclusively restricted to another 3rd party application package|
|WMI_ERR_PERMISSION|To old version of Tap on Mobile application. Upgrade to newest is needed|

[NEXT](../5_Tap_on_Mobile_backend_API/5_Tap_on_Mobile_backend_API.md)

