[BACK](./1_1_Supported_perations.MD)
## 1.2 Versioning

### Wordline Payment Interface (WPI)

The WPI uses versioning with the format Y.X (e.g., 1.0, 2.1) to track and manage different releases of our software. 
- Y (Major Version): Signifies a significant milestone with potential breaking changes. Example: a version 2.x request cannot be used with version 1.x. 
- X (Minor Version): Represents a release with new features or improvements that should be backward compatible within the same major version. But there are exceptions to this - version 2.2 is not fully compatible with version 2.1

The published version of the documentation **describes WPI version 2.2.**

Tap on Mobile application versions supports following WPI versions:
|Tap on Mobile Version|WPI 1.0|WPI 2.0|WPI 2.1|WPI 2.2|
|----------|-----------|-----------|-----------|-----------|
|2.1.25 - 2.1.29 | YES | - | - | - |
|2.1.30 - 2.1.33 | YES | YES | - | - |
|2.1.34| YES | YES | Partially supported in terms of DCC| - |
|4.1.35| YES | YES | YES | - |
|Since 5.4.0 | YES | YES | YES | YES |


**NOTICE:** In the first quarter of 2025, version 1.0 of WPI will be phased out.

### Wordline Managment Interface (WPI)
WMI is not versioned. Full downward compatibility is maintained as new functionality is added.

[NEXT](./1_3_Before_you_start_integration.MD)