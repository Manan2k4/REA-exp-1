# Network and Device Discovery

## Evidence

Readable DEX strings include gRPC/protobuf service identifiers. The public source uses JmDNS service resolution and publishes service properties including hostname, port, API version and authentication port. `MainService` acquires `CHANGE_WIFI_MULTICAST_STATE` support through a Wi-Fi multicast lock.

The source implementation's flow is:

1. Start the foreground service and obtain the active interface/IP.
2. Start JmDNS and advertise/resolve the Warpinator service type.
3. Build a `Remote` from resolved service information.
4. Use the advertised gRPC port for protocol calls and auth port for certificate exchange.
5. Establish a gRPC channel with the peer certificate trust material.
6. Track service availability and remove/update peers on JmDNS events or network changes.

The exact service-type literal and port constants should be taken from the APK's decompiled `Server` class before treating them as APK-confirmed. They were not recoverable with the available tooling.

See [diagrams/network-flow.mmd](diagrams/network-flow.mmd).
