[BACK](../1_Introduction/1_4_Security_remarks.MD)

## 2.1 Tap on Mobile operation modes
Due to regulatory constraints, the Tap on Mobile application uses a single, common distribution channel: the Google Play Store. This means that all offered operation modes must be consistently supported within the same product. Therefore, it is important to understand the dependencies between the relevant operation modes (i.e. standalone and integrated authentication). The Tap on Mobile application logic checks and relies on the selected operation mode.

### 2.1.1 Standalone operation mode
In standalone operation mode, the application has been manually enrolled by the user via the built-in UI registration options. This mode requires the user to establish a 4-digit application access code, which is then required for any authentication operations. If supported by the current product configuration, the access code can be replaced by device biometric options.

Standalone operation mode is blocked for user when:
- application was registered using WMI,
- application was registered manually and any financial operation was performed using WPI. This rule can be switched off using merchant configuration, but this is not recommended.
In this case, after launching the application, a dedicated screen will inform the user that it is running in integrated mode.

### 2.1.2 Integrated operation mode
The integrated operation mode encompasses all use cases in which the application is enrolled using WMI. WPI functions are also supported for terminals using this mode. However, there are several crucial rules for the proper usage and understanding of integrated mode, i.e.:

1. The ToM application registered in integrated mode cannot be accessed from the application GUI (except the login screen when launched manually);
2. After registration, the ToM application is responsible for its own authentication and session validity, so the login/authentication function does not need to be covered by a third-party application;
3. During registration in integrated mode, the ToM application checks the package name of the third-party application being registered and binds to it;
4. While the ToM application is exclusively bound to a certain third-party application package name, all WPI and selected WMI requests incoming from other application packages will be rejected with a dedicated error condition code.

    Notice: The WMI_SVC_REGISTER service is exempt from this rule, allowing the ToM application to be automatically redirected to another third-party application package running on the same device.

To allow assessing which action is required, WMI offers a dedicated function to retrieve the current ToM application status. It is strongly recommended to retrieve this information outside of payment acceptance context.


### 2.1.3 Operation modes summary
This section outlines ToM application behavior for selected functions in available operation modes.

| |Standalone operation mode (manual registration)| Integrated operation mode (WMI registration)|
|----------|-----------|-----------|
|Manual desktop application launch|- ToM login screen (for unauthenticated app)<br><br>- ToM home screen (for authenticated app)|- ToM login screen <br><br>- dedicated screen informing that the application runs in an integrated mode|
|WPI functions| Supported (for whitelisted package names) | Supported only for 3rd party application package name that registered the ToM application|
|ToM application login upon calling WPI functions|- **[global behavior]** seamless – ToM app uses 4 digit access code set during registration or during 1st login activity; <br><br>- **[optional behavior upon request]** ToM login screen and manual provision of 4 digit access code every time the authentication is required|- Not applicable; handled internally by the ToM application|
|Manual desktop launch after calling WPI functions|- **[global behavior]**: dedicated screen informing the user that ToM application is running in an integrate mode<br><br>- **[optional behavior upon request]:** ToM login screen (for unauthenticated app)<br> ToM home screen (for authenticated app)|- dedicated screen informing that the application runs in an integrated mode|
|Unregistration capabilities|No WPI requests processed:<br><br>- Unsubscribe option available from login screen (for unauthenticated app);<br><br>- Unregister function in app settings (for authenticated app);<br><br>- Unregistering from merchant portal;<br><br><br><br>WPI requests already processed:<br><br>- Unsubscribe option available from a dedicated screen informing the user that ToM application is running in an integrated mode;<br><br>- Unregistering from merchant portal;|- WMI_SVC_AUTH_UNREGISTER function; <br><br>- WMI_SVC_REGISTER function (available to all 3rd party packages and purging the previous registration process); <br><br>- Unsubscribe option available from login screen (for unauthenticated app); <br><br>- Unregistering from merchant portal;|

[NEXT](./2_2_Implementation_scaling.md)