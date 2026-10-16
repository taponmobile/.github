[BACK](../6_1_Description_of_the_solution.md)

## 6.2 Interface structure and activity launch

The MPPA provides a set of intents that developers can use to build apps that work with the interface.

For management purpose `eu.softpos.softposwrapper.axis` intent should be used.
|Type|Category|Intent|Purpose|
|----------|-----------|-----------|-----------|
|PTP|Display Action - these actions start the payment solution that are require user interaction.<br>**Notice:** Android intents are used|eu.softpos.softposwrapper.axis|Collect card payload or PIN|

Here is intent creation code:

```java
    public Intent formatWmiRequest(String sessionId, MppaPurchaseRequest req) {
        String json = GSON.toJson(req);

        Intent intent = new Intent("eu.softpos.softposwrapper.axis.MPPA_SVC_READ_CARD");
        intent.addFlags(Intent.FLAG_ACTIVITY_REORDER_TO_FRONT);
        intent.putExtra("WMI_SERVICE_TYPE", "MPPA_SVC_READ_CARD");
        intent.putExtra("WMI_REQUEST", json);
        intent.putExtra("SHOW_OVERLAY ", false)

        return intent;
    }
```
Intent contains a set of extras and needs to have `FLAG_ACTIVITY_REORDER_TO_FRONT` set.

|Extra|Descritpion|Type|Condition|
|----------|-----------|-----------|-----------|
|MPPA_COMMAND|	Specify the subtype of action to be executed:<br>- MPPA_SVC_READ_CARD - Displays approach card screen and performs card processing<br><br>- MPPA_SVC_COLLECT_PIN - Displays pin entry screen and performs pin collection<br><br>- MPPA_SVC_CANCEL - Initiate transaction cancellation (cleaning sensitive data on ToM backend side)<br><br>|String|Mandatory|
|MPPA_REQUEST|The request contains JSON structured data that is mandatory for the given service type.<br><br> The JSON structure is described in the following chapters for each function.|String|Mandatory|
|MPPA_SENDER|Sender application package name|String|Mandatory|

 To launch intent `registerForActivityResult` method should be used. In the response, the intent returns the following data.

|Extra|Descritpion|Type|Condition|
|----------|-----------|-----------|-----------|
|MPPA_COMMAND|Command name|String|Mandatory|
|MPPA_RESPONSE|The response contains JSON structured data processed for the requested service type|String|Mandatory|


 And here is response parsing sample code:

```java
    public MppaPurchaseResponse parsePurchaseResponse(ActivityResult result) {
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

        String json = intent.getStringExtra("MPPA_RESPONSE");

        WmiPurchaseResponse resp = GSON.fromJson(json, MppaPurchaseResponse.class);


        return resp;
    }
```
|Please remember|
|----------|
|The important thing to note is that ToM can only handle one intent invocation at a time (of any intent type — it doesn’t matter whether it’s a financial or informational function). Therefore, it is crucial to make the next request only after receiving the response from the previous one.|

[NEXT](./null.md)
