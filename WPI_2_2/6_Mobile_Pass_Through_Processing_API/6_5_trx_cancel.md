[BACK](./6_4_PIN_collect.md)
## 6.5 Cancel the PTP transaction record
MPPA_SVC_CANCEL initiate transaction cancellation (cleaning sensitive data on ToM backend side).

**Prerequisites:**
- ToM application correctly installed.
- Terminal properly registered (paired with the ToM backend system).
- MPPA trancastion is noit in finale status (status different than PTP_COLLECTED).

### 6.5.1 MPPA_REQUEST - list of supported input parameters

In `MPPA_SVC_CANCEL`, at a minimum, the id_transaction are needed. The full list of parameters is described in the table below.

|Field name|Description|Type|Condition|
|----------|-----------|-----------|-----------|
|nonce|Request identifier. If provided in request, the exact same value will be returned in the response.|string|Optional|
|id_transaction|ToM transaction id returned in MPPA_SVC_READ_CARD response (pattern: ^[-a-fA-F0-9]{36}$).|String|Mandatory|


### 6.5.2 MPPA_RESPONSE - list of supported output parameters
|Field name|Description|Type|Condition|
|----------|-----------|-----------|-----------|
|nonce|Echo from request|String|Optional|
|error_code|Processing result as defined in ‘MPPA error codes’. MPPA_OK means successful transaction.|String|Mandatory|
|remark|Error description. ‘OK’ for MPPA_OK.|String|Mandatory|
|amount|Transaction amount in least denomination units (e.g. eurocents for Euro)|integer (int64)|Mandatory for MPPA_OK|
|currency|Currency code alpha 3 (i.e. ‘EUR’).|String|Mandatory for MPPA_OK|
|external_transaction_id|External transaction id|String|Optional for MPPA_OK|
|id_transaction|ToM transaction id. For cancellation original transaction id is returned|String|Mandatory for MPPA_OK|
|transaction_date|Transaction datetime in local time (i.e. "2025-07-29T14:53:16+0200")|String (datetime)|Mandatory for MPPA_OK|
|transaction_status|Transaction status.<br><br>For **PIN_REQUESTED** - pin collection intent should be sent before card data collection<br><br>**PTP_READ** – card read completed.|String|Mandatory for MPPA_OK|
|masked_pan|Masked pan containing BIN on first 8 characters.|String|Mandatory for MPPA_OK|

[NEXT](./6_6_BPPA_interface.md)
