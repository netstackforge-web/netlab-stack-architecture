# **Switch & Port Map**

Sanitized physical port and uplink reference (exact management/LAN IPs live in local untracked files).

## Core & Management Switches

| Switch / Role | Model / Type | Uplink / LAGG Ports | Downstream / OOBM Ports | Notes |
| :--- | :--- | :--- | :--- | :--- |
| **10G Core Switch** | 10G Managed Switch | LAGG(LACP) to Firewall/Router; LAGG(LACP) to P520 Hypervisor; LAGG(LACP) to NVR | Feeds OOBM Switch, 10-Port PoE Access Switch, and 5G/1G PoE Access Switch | Central high-speed switching fabric |
| **Out-of-Band Mgmt Switch** | Managed Switch | Uplink from 10G Core Switch | OOBM links to Firewall/Router, P520 Hypervisor, and NVR | Isolated management plane |

## Access & PoE Switches

| Switch / Role | Type / Speed | Uplink From Core | Port / Link Assignments | Notes |
| :--- | :--- | :--- | :--- | :--- |
| **5G/1G PoE Access Switch** | 5G / 1G PoE Access Switch | From 10G Core Switch | PoE port to IP Camera; **OOBM-Vlan-Trunk** link to Cisco AP | Supports wired camera and OOBM & IoT Vlans are trunked wireless AP |
| **10-Port PoE Access Switch** | 10-Port PoE Access Switch | From 10G Core Switch | PoE ports to IP Camera 1 & IP Camera 2; PoE/IoT port to Zigbee PoE; IoT network link; **OOBM, IoT, trusted and Guest Vlans are Trunk** link to Cudy AP | Aggregates PoE cameras, IoT, Zigbee PoE, and Cudy AP trunk |

## Wireless & Edge Endpoints

| Endpoint / AP | Connection Type | Connected Upstream To | Downstream / Attached Devices | Notes |
| :--- | :--- | :--- | :--- | :--- |
| **Cisco AP** | **OOBM & IoT Vlans are Trunk** link | 5G/1G PoE Access Switch | Wireless clients | Carries tagged/trunked VLANs |
| **Cudy AP** | **OOBM, IoT, Guest & Trusted are Trunk** link | 10-Port PoE Access Switch | Doorbell, Wi-Fi Camera, **ratgdo** (via Wi-Fi) | Carries trunked traffic and Wi-Fi IoT/camera endpoints |
| **Zigbee PoE** | PoE / IoT | 10-Port PoE Access Switch | Zigbee mesh devices | Powered over Ethernet |
| **IoT Network** | Wired / Segmented | 10-Port PoE Access Switch | IoT devices | Kept separate from core/management planes |
| **IP Camera (x1)** | PoE | 5G/1G PoE Access Switch | — | Wired PoE camera |
| **IP Camera 1 & 2 (x2)** | PoE | 10-Port PoE Access Switch | — | 2 X  wired PoE cameras |

