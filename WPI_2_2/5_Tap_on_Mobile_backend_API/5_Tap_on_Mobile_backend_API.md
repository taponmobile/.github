[BACK](../4_Worldline_Management_Interface/4_5_Error_codes_and_proper_error_handling.md)

# 5. Tap on Mobile backend API

Implementing the Tap on Mobile integrated authentication mode requires integrating the third-party application backend directly with the ToM backend API. Storing OAuth2 access credentials directly in the mobile application is not allowed.
This integration process requires covering the following areas:

1. ToM backend API OAuth2 authentication;
2. The logic to retrieve and manage merchant terminals structure in 3rd party application backend;
3. The logic to lock free terminal selected for registration.

[NEXT](./5_1_ToM_backend_API_OAuth2_authentication.md)