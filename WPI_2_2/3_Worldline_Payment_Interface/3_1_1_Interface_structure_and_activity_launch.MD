# 3. Worldline Payment Interface (WPI)
## 3.1 Finacial operations
###	3.1.1 Interface structure and activity launch

The WPI provides a set of intents that developers can use to build apps that work with the interface.

For financial transaction purpose `com.worldline.payment.action.PROCESS_TRANSACTION` intent should be used.
|Type|Category|Intent|Purpose|
|----------|-----------|-----------|-----------|
|Financial|Display Action - these actions start the payment solution that are processing financial transactions or require user interaction.<br>**Notice:** Android intents are used|com.worldline.payment.action.PROCESS_TRANSACTION|Process a financial transaction|

Here is intent creation code:

```java
    public Intent formatPurchaseRequest(String sessionId, WpiPurchaseRequest req) {
        String json = GSON.toJson(req);

        Intent intent = new Intent("com.worldline.payment.action.PROCESS_TRANSACTION");
        intent.addFlags(Intent.FLAG_ACTIVITY_REORDER_TO_FRONT);
        intent.putExtra("WPI_SERVICE_TYPE", "WPI_SVC_PAYMENT");
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
|WPI_SERVICE_TYPE|	Specify the subtype of action to be executed:<br>- `WPI_SVC_PAYMENT`	- Service type for a purchase <br><br>- `WPI_SVC_CANCEL_PAYMENT`	- Service type for a reversal of a previous transaction <br><br>- `WPI_SVC_REFUND` - Service type for a refund of a previous transaction|String|Mandatory|
|WPI_REQUEST|The request contains JSON structured data that is mandatory for the given service type.<br><br> The JSON structure is described in the following chapters for each function.|String|Mandatory|
|WPI_VERSION| Used WPI version (current: 2.2)|String|Mandatory|
|WPI_SESSION_ID|Used as an identifier of a WPI exchange (a request/response) between a client application and a payment application. Is used to recover the status of the exchange in case of an unexpected failure. Is provided by the client.<br>The session id:<br><br>- must be unique <br><br>- must not be reused for subsequent requests (as soon as the cache is expired this would not be an issue, so it is not necessary to keep track of it but as a general rule a unique random string per request should be used)<br><br>If an unexpected failure occurs during an exchange, the session ID can be used to allow the client to restore its state and synchronise the exchange status with the payment application.|String|Mandatory|
|SHOW_OVERLAY|The flag controls whether a transparent overlay (false) or a spinner (true) should be displayed at the start of the intent.|Boolean|Optional|

 To launch intent `registerForActivityResult` method should be used. In the response, the intent returns the following data.

|Extra|Descritpion|Type|Condition|
|----------|-----------|-----------|-----------|
|WPI_SERVICE_TYPE|Specify the subtype of action to be executed|String|Mandatory|
|WPI_RESPONSE|The response contains JSON structured data processed for the requested service type|String|Mandatory|
|WPI_VERSION|Used WPI version|String|Mandatory|
|WPI_SESSION_ID|Identifier of a WPI exchange provided by the client.|String|Mandatory|




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

<!--
If you want to see what a sample working code looks like, you can use the projects below.
|Programming language| Project |
|----------|-----------|
|Compose|https://gitlab.softpos.eu/samples/wpi-example-compose|
|Flutter|https://gitlab.softpos.eu/samples/wpi-example-flutter|
|Java|https://gitlab.softpos.eu/samples/wpi-example-java|
|Kotlin-compose|https://gitlab.softpos.eu/samples/wpi-example-kotlin-compose|
|Kotlin-XML|https://gitlab.softpos.eu/samples/wpi-example-kotlin-xml|
-->

[NEXT](./3_1_2_Payment.MD)
