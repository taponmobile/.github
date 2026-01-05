[BACK](./1_3_Before_you_start_integration.MD)
## 1.4 Security remarks
### 1.4.1 Android permissions and settings
As default – the required Android permissions for running the application are set during the installation and registration process. But if the device works under MDM (or similar) types of management software, make sure that required permissions are set up properly.

List of required permissions used (may be extended in future versions of the application):
- NFC (exclusive access to read contactless cards)
- CAMERA (block the screen in case of PIN providing + entropy RNG seeding)
- GEOLOCATION_CHECK + ACCESS_FINE_LOCATION (verification of the transaction's location)
- INTERNET (communication with the host)
- ACCESS_NETWORK_STATE (verification of the network state)
- ACCESSIBILITY_SERVICE (recognizing overlapping apps)

Some vendors may have their own settings that may prevent application running (i.e. Xiaomi application popup windows blockade). Please consult the acquirer in case of problems with proper parameterization of the devices.

Device cannot have debug mode turned on or be rooted (works at standard user settings) – otherwise the error must be reported.

Device has also proper time and date set up. Best to be synchronized with any time server or GSM operator time. If time differs from the real one, then communication with the server will be refused.

### 1.4.2 System baseline and configuration
Devices running the application should be compliant with Google guidelines 
Please ensure that:
- Device is equipped with Hardware Backed Key-Store (aka “safe memory”) – most modern devices after 2018 should have such element
- Device supports GMS services and up-to-date Google Play services are installed
- Android version is still supported, and all newest security patches are installed
- In case of controlled/closed networks – the connection to the server and to Google service servers are turned on/allowed at firewall.
- Device has valid Google certificates uploaded
- Integrity API confirms that device can be used as payment solution
 
### 1.4.3 Secure installation of payment app from the store
The softpos application is distributed via official Google Store. (https://play.google.com/)  New version of the app issued is provided by dedicated URLs (consult with the acquirer, to have proper one) and available in official app store application. Please use the last available versions, having the newest security fixes and new functionalities.

Application has own update policy, that may be set-up by acquirers at any time. It will force the application to update during next start.

Certifications and security settings will be uploaded during first registration of the device. Refer to registration procedure in your application manual.

Application doesn’t need any special treatment as for the initial parameterization (the required permissions will be set-up during registration process – with step by step process). It is not possible to turn off any security settings from the application level. All required configuration is built-in to the application package, and only limited number of changeable parameters are uploaded at the start of the application.

Solution is secured by strong cryptography – all the data exchange, processes, payment related operations are handled within the defined security context. Certificates and keys distribution is done automatically via registration process. It is possible to unregister the device from backend level (via portal), which means removal of all cryptography materials and returning the application to initial state. Repeating of the registration process is then needed to reinitiate secure channels to the backend. 

Application has own mechanisms to automatically update old certificates, so if it is regularly used, there’s no need to do any special operations even if the cryptographic certificates are changed at backend level.

Any  manipulation of the data managed by the app and tries to break security measures inside the application or hardware keystore may lead to blacklist the device and unability to continue the payment operations on it.

If payment application is to be used with any 3rd party application, then make sure it is also installed securely (i.e. via Google Play) or in controlled environments (i.e. inside MDM managed networks). Only intent handling permissions is needed to initiate the operations with payment application.

If your application works in such called “overlay mode” (overlapping the other apps of the screen when running), it may be recognized by the payment app and the operations will be terminated. Please consult with the acquirer if such situation occurs.

3rd party application shouldn’t require perimissions higher than regular user of the device. Rooted devices will be recognized by payment application and you may not continue the operations.


### 1.4.4 NFC usage restrictions 
If the 3rd party application uses the NFC interface, it may collide with the need to obtain exclusive access by the payment application. Due to regulatory and security reasons, NFC reader must be exclusively locked by payment application – and it is released after finishing the payment operation. 3rd party app must consider such behavior and release the NFC access before payment operation is made.

[NEXT](../2_Recommended_architecture_and_implementation_scaling/2_1_Tap_on_Mobile_operation_modes.md)