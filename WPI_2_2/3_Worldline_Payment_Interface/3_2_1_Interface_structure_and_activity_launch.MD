[BACK](./3_1_5_4_Checkouts.md)
## 3.2 Information operations
###	3.2.1 Interface structure and activity launch

For informational purpose `com.worldline.payment.action.PROCESS_INFORMATION` intent should be used.

|Type|Category|Intent|Purpose|
|----------|-----------|-----------|-----------|
|Information|Background Actions : These actions perform background processing that usually does not require user interaction, but sometimes can require user interaction<br>**Notice:** Android intents are used|com.worldline.payment.action.PROCESS_INFORMATION|Background management of payment solution specific information|

Here is intent creation code:

```java
    public Intent formatInformationRequest(String sessionId, WpiPurchaseRequest req) {
        String json = GSON.toJson(req);

        Intent intent = new Intent("com.worldline.payment.action.PROCESS_INFORMATION");
        intent.addFlags(Intent.FLAG_ACTIVITY_REORDER_TO_FRONT);
        intent.putExtra("WPI_SERVICE_TYPE", "WPI_SVC_LAST_TRANSACTION");
        intent.putExtra("WPI_REQUEST", json);
        intent.putExtra("WPI_VERSION", "2.2");
        intent.putExtra("WPI_SESSION_ID", sessionId);
        intent.putExtra("SHOW_OVERLAY ", false)

        return intent;
    }
```
Intent contains a set of extras and needs to have `FLAG_ACTIVITY_REORDER_TO_FRONT` set.

|Extra|Descritpion|Type|Condition|
|----------|-----------|-----------|-----------|
|WPI_SERVICE_TYPE|	Specify the subtype of action to be executed. Currently supported one service type: `WPI_SVC_LAST_TRANSACTION`	- function to recovery the result of the previous intent call|String|Mandatory|
|WPI_REQUEST|The request contains JSON structured data that is mandatory for the given service type.<br><br> For `WPI_SVC_LAST_TRANSACTION` empty JSON (`{}`) should be sent.|String|Mandatory|
|WPI_VERSION| Used WPI version (current: 2.2)|String|Mandatory|
|WPI_SESSION_ID|For `WPI_SVC_LAST_TRANSACTION` seesion_id from previous intent request should be sent|String|Mandatory|
|SHOW_OVERLAY|The flag controls whether a transparent overlay (false) or a spinner (true) should be displayed at the start of the intent.|Boolean|Optional|

 To launch intent `registerForActivityResult` method should be used. In the response, the intent returns the following data.

|Extra|Descritpion|Type|Condition|
|----------|-----------|-----------|-----------|
|WPI_SERVICE_TYPE|Specify the subtype of action to be executed. For `WPI_SVC_LAST_TRANSACTION` this will be the service type of the recovered transaction not "WPI_SVC_LAST_TRANSACTION"	|String|Mandatory|
|WPI_RESPONSE|The response contains JSON structured data from previous intent call (The Financial Payment Response object of the corresponding SESSION_ID)|String|Mandatory|
|WPI_VERSION|Used WPI version|String|Mandatory|
|WPI_SESSION_ID|Identifier of a WPI exchange, this session id will be the same as the one sent in the request|String|Mandatory|

 And here is response parsing sample code:

```java
    public WpiPurchaseResponse parsePurchaseResponse(ActivityResult result) {
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

        String json = intent.getStringExtra("WPI_RESPONSE");

        WpiPurchaseResponse resp = GSON.fromJson(json, WpiPurchaseResponse.class);
        resp.setSessionId(intent.getStringExtra("WPI_SESSION_ID"));

        return resp;
    }
```

|Please remember|
|----------|
|The important thing to note is that ToM can only handle one intent invocation at a time (of any intent type — it doesn’t matter whether it’s a financial or informational function). Therefore, it is crucial to make the next request only after receiving the response from the previous one.|
  
  
[NEXT](./3_2_2_Last_transaction.MD)





