[BACK](./3_1_5_1_Receipt_Format.md)

#### 3.1.5.2 Transactions on Behalf
Multimerchant functionality allows selected terminals to perform transactions on behalf of other merchants/terminals.

The functionality can be enabled by an Administrator for selected clients. In this case, a merchant can be associated with two types of terminals:

- Primary terminal — it is linked to a specific device during the registration process and can be paired with partner terminals of other merchants; transactions can be performed both on its own behalf and on behalf of a selected partner terminal.
- Partner terminal — the application cannot be registered on it; partner transactions can be performed on its behalf.

A transaction performed on behalf of another terminal:
- has the `on_behalf` flag set to true.
- has the `partner_tid` and `partner_mid` fields populated — they contain the data of the partner terminal on whose behalf the transaction was performed.

**Important:** Refund and reversal of the on behalf transaction should be also performed on behalf the same terminal.

To perform an on-behalf transaction using WPI, the WPI_REQUEST must include `onBehalf` set to true and one of the following four fields:
- `partnerTid`	Partner terminal TID
- `partnerMid`	Partner terminal MID (The reference must be unique — it must point to exactly one paired terminal.)
- `partnerTerminalUuid`	Partner terminal UUID
- `partnerTerminalExtId`	Partner terminal external Id (The reference must be unique — it must point to exactly one paired terminal.)

An example of the minimal set of parameters required to perform an on-behalf transaction:
```json
{
    "currency": "EUR",
    "requestedAmount": 1500,
    "onBehalf": true,
    "partnerTid": "WLTP0009"
}
```

[NEXT](./3_1_5_3_Tipping.md)