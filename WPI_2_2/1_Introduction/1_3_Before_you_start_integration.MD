[BACK](./1_2_Versioning.MD)

## 1.3 Before you start integration
Before starting the development certain preconditions need to be met, i.e.:
- 3rd party app developers should have an access to sandbox Worldline Tap on Mobile application;
- 3rd party app package needs to be whitelisted in sandbox environment;
- Organization structure for test merchant should be configured in sandbox environment;
- OAuth2 access credentials for ToM backend need to be provisioned and exchanged;


Tap on Mobile package names (Worldline Acquiring entities use different mobile application package names):
|Acquirer|Android Package name |Region of availability|
|----------|-----------|-----------|
|Worldline EU|eu.softpos.softposwrapper.wl|European Union|
|Worldline CH|eu.softpos.softposwrapper.wl|Switzerland|
|CAWL|eu.softpos.softposwrapper.cawl|France|
|Crédit Agricole|eu.softpos.softposwrapper.cawl|France|
|Payone|eu.softpos.softposwrapper.payone|Austria; Germany|
|KB Smart|eu.softpos.softposwrapper.kb|Czechia|
|ANZ Worldline|eu.softpos.softposwrapper.wlanz|Australia|
|ING Italy|eu.softpos.softposwrapper.ingit|Italy|

[NEXT](./1_4_Security_remarks.MD)