[BACK](./3_1_5_3_Tipping.md)

#### 3.1.5.4 Checkouts

For acquirers having ‘checkout id’ verification enabled, verification of checkout is mandatory during transaction initialization. 

ToM backoffice API has dedicated endpoint `/api/v1/transaction-checkouts` for checkout creation and getting checkout data so integrator could create checkouts. 
When creating a checkout_id, the following data can be provided:

|Name| Description | |
|----------|-----------|-----------|
|id_merchant|Id of merchant|Mndatory|
|id_terminal|Id of terminal|Optional| 
|amount| Transaction amount ‘in cents’ (no decimal numbers)|Optional| 
|currency_alpha_code|Transaction currency code (alpha 3)|Optional| 
|country_alpha_code2|Terminal country code (alpha 2)|Optional| 
|external_id|External id of transaction|Optional| 

Later, during the transaction, each of the provided values is compared with the transaction data and must match.

API `/api/v1/transaction-checkouts` will create checkout_id ad return UUID of it. To perform transaction for acquirers having ‘checkout id’ verification enabled in `WPI_REQUEST` parameter `checkoutId` with this UUID must be added.

[NEXT](./3_2_1_Interface_structure_and_activity_launch.MD)


