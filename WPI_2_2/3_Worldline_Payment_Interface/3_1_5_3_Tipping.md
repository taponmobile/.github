[BACK](./3_1_5_2_Transactions_on_Behalf.md)

#### 3.1.5.3 Tipping
Tap on Mobile allows adding a tip to a transaction. This functionality can be enabled by an Administrator for selected clients.

If tips are enabled for a terminal, two scenarios are possible:
- In the `WPI_REQUEST`, an additional `tipAmount` tag can be sent — it should contain the tip value. In this case, the tip will be added, and the authorization will be performed for the total amount: `amount` + `tipAmount`.
- If tips are enabled for the terminal but no `tipAmount` is provided in the `WPI_REQUEST`, the transaction flow will start with an additional screen where the user can decide whether to add a tip and specify the tip amount.

Note: If tips are disabled for the terminal but a tipAmount value is sent in the `WPI_REQUEST`, the transaction will end with an error:
```json
{
    "errorCondition": "WPI_ERR_COND_TIP_NOT_SUPPORTED_BY_PAYMENT_SOLUTION",
    "remark": "Terminal does not support tip.",
    "result": "WPI_RESULT_FAILURE",
    (...)
}
```
[NEXT](./3_1_5_4_Checkouts.md)