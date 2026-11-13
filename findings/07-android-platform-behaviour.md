# Android Platform Behaviour

Manifest evidence confirms:

- foreground `dataSync` service;
- boot, reboot, and package-replaced receiver;
- Quick Settings tile service protected by `BIND_QUICK_SETTINGS_TILE`;
- runtime notification permission declaration;
- Wi-Fi multicast and wake-lock permissions;
- legacy external-storage permissions with SDK caps;
- non-exported FileProvider with URI grants;
- exported share and deep-link activities.

The source corroborates notification channels for service, incoming-transfer, and progress notifications, a multicast lock named `WarpMDNSLock`, network callbacks, and Storage Access Framework integration.

The manifest does not declare a separate `android:permission` on `MainService`; the effective external reachability should be checked against the decoded `exported` default rules and the target SDK behavior. No runtime execution was performed.
