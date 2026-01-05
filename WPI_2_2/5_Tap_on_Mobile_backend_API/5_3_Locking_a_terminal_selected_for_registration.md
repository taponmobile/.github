[BACK](./5_2_Retrieving_and_managing_merchants_terminal_structure.md)

## 5.3 Locking a terminal selected for registration

The decision on the TID selected for registration should be followed by the generation of a registration token. Creating a registration token moves the TID to ‘locked’ status. It means that throughout the registration token validity, TID cannot be manually registered in standalone mode.

ToM API function for the registration token generation operation is **POST /api/v1/terminals/{id}/registration-token**, where id is a terminal UUID stored in ToM backend.

**Important note:** registration token’s expiry timestamp may be extended by calling **POST /api/v1/terminals/{id}/registration-token/refresh** ToM API function. This operation maintains previous token value and new validity timestamp is returned in the response.

### 5.3.1 Request Parameters

Complete list of request elements is available in ToM API specification (https://sandbox-wl-emea.softpos.eu/swagger-ui/index.html?configUrl=/v3/api-docs/swagger-config#/Terminals%20Registrations/registrationToken). Table below summarizes most important fields.

|Parameter|Description|Type|Condition|
|---------|-----------|----|---------|
|id|Terminal UUID stored in the ToM backend|String (UUID)|Mandatory|

|Parameter|Description|Type|Condition|
|---------|-----------|----|---------|
|email|Optional parameter allowing to provide an email address of the user who should receive a welcome email containing the registration token in QR-code format; an empty body should be used when no user notification is required|String|Optional|

### 5.3.2 Response Parameters

Complete list of response elements is available in ToM API specification (https://sandbox-wl-emea.softpos.eu/swagger-ui/index.html?configUrl=/v3/api-docs/swagger-config#/Terminals%20Registrations/registrationToken). Table below summarizes most important fields.

|Parameter|Description|Type|Condition|
|---------|-----------|----|---------|
|token|Generated registration token to be used in the Tap on Mobile application for registering the selected TID|String|Mandatory|
|expiry_date|Registration token expiry timestamp|String (timestamp)|Mandatory|
|created|Registration token creation timestamp|String (timestamp)|Mandatory|


[NEXT](../Appendix_A_How_to_register_application_manually/A_How_to_register_application_manually.md)
