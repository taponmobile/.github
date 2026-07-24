[BACK](../Appendix_D_Testing_procedure/D_Testing_procedure.md)
# Appendix E - Network settings
Tap on Mobile application connects to various endpoints, depending on the acquirer.

**Sandbox:**

|Acquirer|Endpoint name|Region of availability|
|----------|-----------|-----------|
|Worldline EU|https://sandbox-wl-emea.softpos.eu|European Union|
|Worldline CH|https://sandbox-wl-ch.softpos.eu|Switzerland|
|Worldline UK|https://sandbox-wl-emea.softpos.eu|UK|
|Payone AT|https://sandbox-payone-at.softpos.eu|Austria|
|Payone DE|https://sandbox-payone-at.softpos.eu|Germany|
|KB Smart|https://sandbox-payphone-cz.softpos.eu|Czechia|
|ANZ Worldline|https://taponmobile.portal.sandbox.anzworldline-solutions.com.au|Australia|

**Production:**

|Acquirer|Endpoint name|Region of availability|
|----------|-----------|-----------|
|Worldline EU|https://worldline.softpos.eu|European Union|
|Worldline CH|https://worldline.softpos.eu|Switzerland|
|Worldline UK|https://worldline.softpos.eu|UK|
|Payone AT|https://payone-at.softpos.eu|Austria|
|Payone DE|https://payone-at.softpos.eu|Germany|
|KB Smart|https://portal.payphone.cz|Czechia|
|ANZ Worldline|https://taponmobile.portal.anzworldline-solutions.com.au|Australia|

**Additional services:**

Every Tap on Mobile requires also access to Google Services hosts:
- https://www.googleapis.com
- https://maps.googleapis.com

Some installations are relying on closed networks (based on private APNs / MDM and own firewall configuration) and require allowance to handle google play services traffic. The following network destinations should be allowlisted to ensure proper operation of Google Play Integrity API and the Google Play Services components it depends on.
 
These ports are used by Google Play Services to maintain connections with Google's infrastructure. Blocking them may prevent Google Play Services from operating correctly, which can result in Play Integrity API failures (used by the application for attestation checks).

|FQDN|Ports|Purpose|
|----------|-----------|-----------|
|playintegrity.googleapis.com|TCP/UDP port: 443|Primary Google Play Integrity API endpoint used to request and verify integrity tokens.|
|play-fe.googleapis.com|TCP/UDP port: 443|Google Play backend services used by Google Play Services during the integrity token acquisition process.|
|play.google.com|TCP/UDP: 443 <br> TCP: 5228–5230|Access to Google Play services required by Google Play Services.|
|android.apis.google.com|TCP/UDP: 443 <br> TCP: 5228–5230|Android platform services endpoint used by Google Play Services.|
|mtalk.google.com|TCP/UDP: 443 <br> TCP: 5228–5230|Google Play Services communication endpoint used for persistent connections and service synchronization.|
|*.googleapis.com|TCP/UDP: 443 <br> TCP: 5228–5230|Various Google APIs used internally by Play Services. Google does not guarantee that all requests will use a single hostname. |
|*.googleusercontent.com|TCP/UDP: 443 <br> TCP: 5228–5230|Google-hosted content and service responses required by Play Services. |
|*.gstatic.com|TCP/UDP: 443 <br> TCP: 5228–5230|Static resources used by Google Play Services.|
