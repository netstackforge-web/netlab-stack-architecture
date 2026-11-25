# Physical Network Layer

Hardware topology, switching fabric, cabling, and physical rack/device layout for the lab.

## Physical Topology

```mermaid
flowchart TD
    ISP[ISP / Edge Gateway] --> FW[Firewall / Router]

    FW <==>|"LAGG"| Core10G[10G Core Switch]
    P520[P520 Hypervisor] <==>|"LAGG"| Core10G
    NVR[NVR] <==>|"LAGG"| Core10G

    Core10G --> OOBM[Out-of-Band Mgmt Switch]
    Core10G --> PoE10[10-Port PoE Access Switch]
    Core10G --> PoE5G1G[5G / 1G PoE Access Switch]

    OOBM -. "OOBM" .-> FW
    OOBM -. "OOBM" .-> P520
    OOBM -. "OOBM" .-> NVR

    PoE5G1G -->|"PoE"| Cam1[IP Camera]
    PoE5G1G <==>|"Trunk"| CiscoAP[Cisco AP]

    PoE10 -->|"PoE"| Cam2[IP Camera 1]
    PoE10 -->|"PoE"| Cam3[IP Camera 2]
    PoE10 -->|"PoE / IoT"| ZigbeePoE[Zigbee PoE]
    PoE10 <==>|"Trunk"| CudyAP[Cudy AP]

    Doorbell[Video Doorbell] --> CudyAP
    ratgdo[ratgdo] -. "Wi-Fi" .-> CudyAP
    
```

## Documentation Index

See the [Switch and Port Map](./switch-and-port-map.md) for port assignments and LAGG/trunk links.

Physical cable standards, [point-to-point links](./cabling-and-rack-layout.md), and hardware placement notes.