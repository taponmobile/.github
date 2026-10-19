[BACK](./6_2_Interface_structure_and_activity_launch.md)
## 6.3 Read the card data
MPPA_SVC_READ_CARD intent displays approach card screen and performs card processing

**Prerequisites:**
- ToM application correctly installed.
- Terminal properly registered (paired with the ToM backend system).
- Transaction parameters (currency, etc.) must be in accordance with the terminal profile.

### 6.3.1 MPPA_REQUEST - list of supported input parameters

In `MPPA_SVC_READ_CARD`, at a minimum, the currency, requested amount and transaction_type are needed. The full list of parameters is described in the table below.

|Field name|Description|Type|Condition|
|----------|-----------|-----------|-----------|
|nonce|Request identifier. If provided in request, the exact same value will be returned in the response.|string|Optional|
|transaction_type|Transaction type|Enum ("CREDIT", "DEBIT")|Mandatory|
|amount|Transaction amount in least denomination units (e.g. eurocents for Euro)|integer (int64)|Mandatory|
|currency|Currency code alpha 3 (i.e. ‘EUR’). Must always be the same as terminal currency|String|Mandatory|
|external_transaction_id|External transaction id from caller application (pattern: ^[-_a-zA-Z0-9]{1,128}$)|string|Optional|


### 6.3.2 MPPA_RESPONSE - list of supported output parameters
|Field name|Description|Type|Condition|
|----------|-----------|-----------|-----------|
|nonce|Echo from request|String|Optional|
|error_code|Processing result as defined in ‘MPPA error codes’. MPPA_OK means successful transaction.|String|Mandatory|
|remark|Error description. ‘OK’ for MPPA_OK.|String|Mandatory|
|transaction_type|Transaction type – echo from request|Enum ("CREDIT", "DEBIT")|Mandatory for MPPA_OK|
|ptp_token|PTP token|String (JWT)|Mandatory for MPPA_OK|
|pin_token|Pin token|String (JWT)|Mandatory for MPPA_OK|
|amount|Transaction amount in least denomination units (e.g. eurocents for Euro)|integer (int64)|Mandatory for MPPA_OK|
|currency|Currency code alpha 3 (i.e. ‘EUR’).|String|Mandatory for MPPA_OK|
|external_transaction_id|External transaction id|String|Optional for MPPA_OK|
|id_transaction|ToM transaction id. For cancellation original transaction id is returned|String|Mandatory for MPPA_OK|
|transaction_date|Transaction datetime in local time (i.e. "2025-07-29T14:53:16+0200")|String (datetime)|Mandatory for MPPA_OK|
|transaction_status|Transaction status.<br><br>For **PIN_REQUESTED** - pin collection intent should be sent before card data collection<br><br>**PTP_READ** – card read completed.|String|Mandatory for MPPA_OK|
|ptp_non_sensitive_tags|PTP non sensitive tags returned by host|String (Base64)|Mandatory for MPPA_OK|
|masked_pan|Masked pan containing BIN on first 8 characters.|String|Mandatory for MPPA_OK|
|kernel_outcome|Kernel processing outcome |String - Eum ("NA", "SELECT_NEXT", "TRY_AGAIN", "APPROVED", "DECLINED", "ONLINE_REQUEST", "TRY_ANOTHER_INTERFACE", "END_APPLICATION", "OUTCOME_REQUEST_SIGNATURE", "REQUEST_ONLINE_PIN", "ONLINE_REQUEST_TWO_PRESENTMENTS", "ONLINE_REQUEST_PRESENT_AND_HOLD", "END_APPLICATION_WITH_RESTART", "OUTCOME_EXTENSION_EXECUTE_ 3RD_PARTY_MASTERCARD_KERNEL", "TRANSACTION_PROCESSING_ERROR")|Optional - only if communication with the card took place and kernel returned outcome|

[NEXT](./6_4_PIN_collect.md)
