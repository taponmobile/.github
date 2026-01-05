[BACK](./1_Introduction.MD)
### 1.1.1 Wordline Management Interface (WMI)
**Intent:** com.worldline.management.action.PROCESS_OPERATION

The Tap on Mobile application, after installation and before first use, requires completing a registration process, which is intended to link the installed application with a specific payment terminal defined in the payment system.

The registration process can be carried out manually in the application by the user or in an integrated mode using the functions available within the Wordline Management Interface intent.

WMI offers the following services:
|Service type|Description|
|----------|-----------|
|WMI_SVC_CHECK_STATUS|Service type for checking current Tap on Mobile application status|
|WMI_SVC_REGISTER|Service type for initiating the terminal enrollment sequence|
|WMI_SVC_AUTH_UNREGISTER|Service type for unregistering the terminal by the 3rd party application package used previously for enrollment|

[More information about WMI](../4_Worldline_Management_Interface/4_1_Interface_structure_and_activity_launch.MD)
 
### 1.1.2 WPI Financial operations
**Intent:** com.worldline.payment.action.PROCESS_TRANSACTION

The Wordline Payment Interface – Financial Operations intent, as the name suggests, groups the services responsible for carrying out financial transactions.

It offers the following services:
|Service type|Description|
|----------|-----------|
|WPI_SVC_PAYMENT|Service type for a purchase|
|WPI_SVC_CANCEL_PAYMENT|Service type for a reversal of a previous transaction|
|WPI_SVC_REFUND|Service type for a refund of a previous transaction or for credit operation|



### 1.1.3 WPI Information Operations 
**Intent:** com.worldline.payment.action.PROCESS_INFORMATION

The Wordline Payment Interface – Information Operationd intent groups additional informational functions.

It offers the following services:
|Service type|Description|
|----------|-----------|
|WPI_SVC_LAST_TRANSACTION| Used to return the last (previous) transaction result. In case of the last payment transaction response is not known any more, it can be requested by this service. It will return the last financial transaction response independent of the result, failed or success. This is a recovery feature as the payment solution will remember the last SESSION_ID as well as corresponding transaction response. |

[NEXT](./1_2_Versioning.MD)


