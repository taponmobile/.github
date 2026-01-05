[BACK](../3_Worldline_Payment_Interface/3_3_Error_codes_and_proper_error_handling.md)

# 4. Worldline Management Interface (WMI)
## 4.1 Interface structure and activity launch

The WPI provides a set of intents that developers can use to build apps that work with the interface.

For financial transaction purpose `com.worldline.management.action.PROCESS_OPERATION` intent should be used.
|Type|Category|Intent|Purpose|
|----------|-----------|-----------|-----------|
|Financial|Display Action - these actions start the payment solution that are processing financial transactions or require user interaction.<br>**Notice:** Android intents are used|com.worldline.payment.action.PROCESS_TRANSACTION|Process a financial transaction|

Here is intent creation code:

```java
    public Intent formatWmiRequest(String sessionId, WpiPurchaseRequest req) {
        String json = GSON.toJson(req);

        Intent intent = new Intent("com.worldline.management.action.PROCESS_OPERATION");
        intent.addFlags(Intent.FLAG_ACTIVITY_REORDER_TO_FRONT);
        intent.putExtra("WMI_SERVICE_TYPE", "WPI_SVC_PAYMENT");
        intent.putExtra("WMI_REQUEST", json);
        intent.putExtra("SHOW_OVERLAY ", false)

        return intent;
    }
```
Intent contains a set of extras and needs to have `FLAG_ACTIVITY_REORDER_TO_FRONT` set.

|Extra|Descritpion|Type|Condition|
|----------|-----------|-----------|-----------|
|WMI_SERVICE_TYPE|	Specify the subtype of action to be executed:<br>- WMI_SVC_CHECK_STATUS - Service type for checking current Tap on Mobile application status<br><br>- WMI_SVC_REGISTER - Service type for initiating the terminal enrollment sequence<br><br>- WMI_SVC_AUTH_UNREGISTER - Service type for unregistering the terminal by the 3rd party application package used previously for enrollment<br><br>|String|Mandatory|
|WMI_REQUEST|The request contains JSON structured data that is mandatory for the given service type.<br><br> The JSON structure is described in the following chapters for each function.|String|Mandatory|
|SHOW_OVERLAY|The flag controls whether a transparent overlay (false) or a spinner (true) should be displayed at the start of the intent.|Boolean|Optional|

 To launch intent `registerForActivityResult` method should be used. In the response, the intent returns the following data.

|Extra|Descritpion|Type|Condition|
|----------|-----------|-----------|-----------|
|WMI_SERVICE_TYPE|Specify the subtype of action to be executed|String|Mandatory|
|WMI_RESPONSE|The response contains JSON structured data processed for the requested service type|String|Mandatory|


 And here is response parsing sample code:

```java
    public WmiPurchaseResponse parsePurchaseResponse(ActivityResult result) {
        if (result.getResultCode() == Activity.RESULT_CANCELED) {
            throw new RuntimeException("Intent cancelled.");
        }
        if (result.getResultCode() != Activity.RESULT_OK) {
            throw new RuntimeException("Invalid result code: " + result.getResultCode());
        }

        Intent intent = result.getData();
        if (intent == null) {
            throw new RuntimeException("Received intent without bundled data");
        }

        String json = intent.getStringExtra("WMI_RESPONSE");

        WmiPurchaseResponse resp = GSON.fromJson(json, WmiPurchaseResponse.class);


        return resp;
    }
```
|Please remember|
|----------|
|The important thing to note is that ToM can only handle one intent invocation at a time (of any intent type — it doesn’t matter whether it’s a financial or informational function). Therefore, it is crucial to make the next request only after receiving the response from the previous one.|

[NEXT](./4_2_Checking_application_status.md)
