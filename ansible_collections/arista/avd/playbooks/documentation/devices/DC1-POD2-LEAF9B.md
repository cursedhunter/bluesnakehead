# DC1-POD2-LEAF9B
# Table of Contents

- [Management](#management)
  - [Management Interfaces](#management-interfaces)
  - [Management API HTTP](#management-api-http)
- [Authentication](#authentication)
  - [Local Users](#local-users)
- [Monitoring](#monitoring)
  - [SNMP](#snmp)
- [MLAG](#mlag)
  - [MLAG Summary](#mlag-summary)
  - [MLAG Device Configuration](#mlag-device-configuration)
- [Spanning Tree](#spanning-tree)
  - [Spanning Tree Summary](#spanning-tree-summary)
  - [Spanning Tree Device Configuration](#spanning-tree-device-configuration)
- [Internal VLAN Allocation Policy](#internal-vlan-allocation-policy)
  - [Internal VLAN Allocation Policy Summary](#internal-vlan-allocation-policy-summary)
  - [Internal VLAN Allocation Policy Configuration](#internal-vlan-allocation-policy-configuration)
- [VLANs](#vlans)
  - [VLANs Summary](#vlans-summary)
  - [VLANs Device Configuration](#vlans-device-configuration)
- [Interfaces](#interfaces)
  - [Ethernet Interfaces](#ethernet-interfaces)
  - [Port-Channel Interfaces](#port-channel-interfaces)
  - [Loopback Interfaces](#loopback-interfaces)
  - [VLAN Interfaces](#vlan-interfaces)
  - [VXLAN Interface](#vxlan-interface)
- [Routing](#routing)
  - [Service Routing Protocols Model](#service-routing-protocols-model)
  - [Virtual Router MAC Address](#virtual-router-mac-address)
  - [IP Routing](#ip-routing)
  - [IPv6 Routing](#ipv6-routing)
  - [Static Routes](#static-routes)
  - [Router BGP](#router-bgp)
- [BFD](#bfd)
  - [Router BFD](#router-bfd)
- [Multicast](#multicast)
  - [IP IGMP Snooping](#ip-igmp-snooping)
- [Filters](#filters)
  - [Prefix-lists](#prefix-lists)
  - [Route-maps](#route-maps)
- [ACL](#acl)
- [VRF Instances](#vrf-instances)
  - [VRF Instances Summary](#vrf-instances-summary)
  - [VRF Instances Device Configuration](#vrf-instances-device-configuration)
- [Quality Of Service](#quality-of-service)
- [EOS CLI](#eos-cli)

# Management

## Management Interfaces

### Management Interfaces Summary

#### IPv4

| Management Interface | description | Type | VRF | IP Address | Gateway |
| -------------------- | ----------- | ---- | --- | ---------- | ------- |
| Management0 | oob_management | oob | mgmt | 10.6.33.37/24 | 10.6.33.1 |

#### IPv6

| Management Interface | description | Type | VRF | IPv6 Address | IPv6 Gateway |
| -------------------- | ----------- | ---- | --- | ------------ | ------------ |
| Management0 | oob_management | oob | mgmt | -  | - |

### Management Interfaces Device Configuration

```eos
!
interface Management0
   description oob_management
   no shutdown
   vrf mgmt
   ip address 10.6.33.37/24
```

## Management API HTTP

### Management API HTTP Summary

| HTTP | HTTPS |
| ---- | ----- |
| False | True |

### Management API VRF Access

| VRF Name | IPv4 ACL | IPv6 ACL |
| -------- | -------- | -------- |
| mgmt | - | - |

### Management API HTTP Configuration

```eos
!
management api http-commands
   protocol https
   no shutdown
   !
   vrf mgmt
      no shutdown
```

# Authentication

## Local Users

### Local Users Summary

| User | Privilege | Role |
| ---- | --------- | ---- |
| admin | 15 | network-admin |

### Local Users Device Configuration

```eos
!
username admin privilege 15 role network-admin secret sha512 $6$82gqIqw8b3nibNrk$MoZO0S8QMQN8uwnR8v48dbGrL0Ec/6q36tSx8y9IsExi4L.HtmokW9rX8VehLxhg542mNTBKqxMBF.LgnCTm4.
```

# Monitoring

## SNMP

### SNMP Configuration Summary

| Contact | Location | SNMP Traps | State |
| ------- | -------- | ---------- | ----- |
| - | AMS DC1 DC1_POD2 DC1-POD2-LEAF9B | All | Disabled |

### SNMP Device Configuration

```eos
!
snmp-server location AMS DC1 DC1_POD2 DC1-POD2-LEAF9B
```

# MLAG

## MLAG Summary

| Domain-id | Local-interface | Peer-address | Peer-link |
| --------- | --------------- | ------------ | --------- |
| RACK9_MLAG | Vlan4094 | 172.19.33.70 | Port-Channel151 |

Dual primary detection is enabled. The detection delay is 5 seconds.

## MLAG Device Configuration

```eos
!
mlag configuration
   domain-id RACK9_MLAG
   local-interface Vlan4094
   peer-address 172.19.33.70
   peer-address heartbeat 10.6.33.37 vrf mgmt
   peer-link Port-Channel151
   dual-primary detection delay 5 action errdisable all-interfaces
   reload-delay mlag 300
   reload-delay non-mlag 330
```

# Spanning Tree

## Spanning Tree Summary

STP mode: **rstp**

### Global Spanning-Tree Settings

- Global RSTP priority: 4096
- Spanning Tree disabled for VLANs: **4094**

## Spanning Tree Device Configuration

```eos
!
spanning-tree mode rstp
no spanning-tree vlan-id 4094
spanning-tree priority 4096
```

# Internal VLAN Allocation Policy

## Internal VLAN Allocation Policy Summary

| Policy Allocation | Range Beginning | Range Ending |
| ------------------| --------------- | ------------ |
| ascending | 1006 | 1199 |

## Internal VLAN Allocation Policy Configuration

```eos
!
vlan internal order ascending range 1006 1199
```

# VLANs

## VLANs Summary

| VLAN ID | Name | Trunk Groups |
| ------- | ---- | ------------ |
| 100 | Cust_A_Data | - |
| 133 | Cust_A_OP_M2 | - |
| 167 | Cust_A_M2C2 | - |
| 200 | Cust_B_Data | - |
| 233 | Cust_B_M2 | - |
| 267 | Cust_B_M2C2 | - |
| 666 | bitbucket | - |
| 999 | vmotion | - |
| 3099 | MLAG_iBGP_Cust_A_VRF | LEAF_PEER_L3 |
| 3199 | MLAG_iBGP_Cust_B_VRF | LEAF_PEER_L3 |
| 4094 | MLAG_PEER | MLAG |

## VLANs Device Configuration

```eos
!
vlan 100
   name Cust_A_Data
!
vlan 133
   name Cust_A_OP_M2
!
vlan 167
   name Cust_A_M2C2
!
vlan 200
   name Cust_B_Data
!
vlan 233
   name Cust_B_M2
!
vlan 267
   name Cust_B_M2C2
!
vlan 666
   name bitbucket
!
vlan 999
   name vmotion
!
vlan 3099
   name MLAG_iBGP_Cust_A_VRF
   trunk group LEAF_PEER_L3
!
vlan 3199
   name MLAG_iBGP_Cust_B_VRF
   trunk group LEAF_PEER_L3
!
vlan 4094
   name MLAG_PEER
   trunk group MLAG
```

# Interfaces

## Ethernet Interfaces

### Ethernet Interfaces Summary

#### L2

| Interface | Description | Mode | VLANs | Native VLAN | Trunk Group | Channel-Group |
| --------- | ----------- | ---- | ----- | ----------- | ----------- | ------------- |
| Ethernet15/1 | MLAG_PEER_DC1-POD2-LEAF9A_Ethernet15/1 | *trunk | *2-4094 | *- | *['LEAF_PEER_L3', 'MLAG'] | 151 |
| Ethernet16/1 | MLAG_PEER_DC1-POD2-LEAF9A_Ethernet16/1 | *trunk | *2-4094 | *- | *['LEAF_PEER_L3', 'MLAG'] | 151 |

*Inherited from Port-Channel Interface

#### IPv4

| Interface | Description | Type | Channel Group | IP Address | VRF |  MTU | Shutdown | ACL In | ACL Out |
| --------- | ----------- | -----| ------------- | ---------- | ----| ---- | -------- | ------ | ------- |
| Ethernet29/1 | P2P_LINK_TO_DC1-POD2-SPINE1_Ethernet18/1 | routed | - | 172.17.33.33/31 | default | 9214 | false | - | - |
| Ethernet30/1 | P2P_LINK_TO_DC1-POD2-SPINE2_Ethernet18/1 | routed | - | 172.17.33.35/31 | default | 9214 | false | - | - |
| Ethernet31/1 | P2P_LINK_TO_DC1-POD2-SPINE3_Ethernet18/1 | routed | - | 172.17.33.37/31 | default | 9214 | false | - | - |
| Ethernet32/1 | P2P_LINK_TO_DC1-POD2-SPINE4_Ethernet18/1 | routed | - | 172.17.33.39/31 | default | 9214 | false | - | - |

### Ethernet Interfaces Device Configuration

```eos
!
interface Ethernet15/1
   description MLAG_PEER_DC1-POD2-LEAF9A_Ethernet15/1
   no shutdown
   channel-group 151 mode active
!
interface Ethernet16/1
   description MLAG_PEER_DC1-POD2-LEAF9A_Ethernet16/1
   no shutdown
   channel-group 151 mode active
!
interface Ethernet29/1
   description P2P_LINK_TO_DC1-POD2-SPINE1_Ethernet18/1
   no shutdown
   mtu 9214
   no switchport
   ip address 172.17.33.33/31
   ptp enable
   service-profile P2P-QOS-PROFILE
!
interface Ethernet30/1
   description P2P_LINK_TO_DC1-POD2-SPINE2_Ethernet18/1
   no shutdown
   mtu 9214
   no switchport
   ip address 172.17.33.35/31
   ptp enable
   service-profile P2P-QOS-PROFILE
!
interface Ethernet31/1
   description P2P_LINK_TO_DC1-POD2-SPINE3_Ethernet18/1
   no shutdown
   mtu 9214
   no switchport
   ip address 172.17.33.37/31
   ptp enable
   service-profile P2P-QOS-PROFILE
!
interface Ethernet32/1
   description P2P_LINK_TO_DC1-POD2-SPINE4_Ethernet18/1
   no shutdown
   mtu 9214
   no switchport
   ip address 172.17.33.39/31
   ptp enable
   service-profile P2P-QOS-PROFILE
```

## Port-Channel Interfaces

### Port-Channel Interfaces Summary

#### L2

| Interface | Description | Type | Mode | VLANs | Native VLAN | Trunk Group | LACP Fallback Timeout | LACP Fallback Mode | MLAG ID | EVPN ESI |
| --------- | ----------- | ---- | ---- | ----- | ----------- | ------------| --------------------- | ------------------ | ------- | -------- |
| Port-Channel151 | MLAG_PEER_DC1-POD2-LEAF9A_Po151 | switched | trunk | 2-4094 | - | ['LEAF_PEER_L3', 'MLAG'] | - | - | - | - |

### Port-Channel Interfaces Device Configuration

```eos
!
interface Port-Channel151
   description MLAG_PEER_DC1-POD2-LEAF9A_Po151
   no shutdown
   switchport
   switchport trunk allowed vlan 2-4094
   switchport mode trunk
   switchport trunk group LEAF_PEER_L3
   switchport trunk group MLAG
   service-profile P2P-QOS-PROFILE
```

## Loopback Interfaces

### Loopback Interfaces Summary

#### IPv4

| Interface | Description | VRF | IP Address |
| --------- | ----------- | --- | ---------- |
| Loopback0 | EVPN_Overlay_Peering | default | 10.4.33.39/32 |
| Loopback1 | VTEP_VXLAN_Tunnel_Source | default | 10.5.33.38/32 |

#### IPv6

| Interface | Description | VRF | IPv6 Address |
| --------- | ----------- | --- | ------------ |
| Loopback0 | EVPN_Overlay_Peering | default | - |
| Loopback1 | VTEP_VXLAN_Tunnel_Source | default | - |


### Loopback Interfaces Device Configuration

```eos
!
interface Loopback0
   description EVPN_Overlay_Peering
   no shutdown
   ip address 10.4.33.39/32
!
interface Loopback1
   description VTEP_VXLAN_Tunnel_Source
   no shutdown
   ip address 10.5.33.38/32
```

## VLAN Interfaces

### VLAN Interfaces Summary

| Interface | Description | VRF |  MTU | Shutdown |
| --------- | ----------- | --- | ---- | -------- |
| Vlan100 |  set from structured_config on svi (was Cust_A_OP_Zone_1)  |  Cust_A_VRF  |  -  |  false  |
| Vlan133 |  Cust_A_OP_M2  |  Cust_A_VRF  |  -  |  false  |
| Vlan167 |  Cust_A_M2C2  |  Cust_A_VRF  |  -  |  true  |
| Vlan200 |  set from structured_config on svi (was Cust_B_OP_Zone_1)  |  Cust_B_VRF  |  -  |  false  |
| Vlan233 |  Cust_B_M2  |  Cust_B_VRF  |  -  |  false  |
| Vlan267 |  Cust_B_M2C2  |  Cust_B_VRF  |  -  |  true  |
| Vlan3099 |  MLAG_PEER_L3_iBGP: vrf Cust_A_VRF  |  Cust_A_VRF  |  9214  |  false  |
| Vlan3199 |  MLAG_PEER_L3_iBGP: vrf Cust_B_VRF  |  Cust_B_VRF  |  9214  |  false  |
| Vlan4094 |  MLAG_PEER  |  default  |  9214  |  false  |

#### IPv4

| Interface | VRF | IP Address | IP Address Virtual | IP Router Virtual Address | VRRP | ACL In | ACL Out |
| --------- | --- | ---------- | ------------------ | ------------------------- | ---- | ------ | ------- |
| Vlan100 |  Cust_A_VRF  |  -  |  10.0.10.1/24  |  -  |  -  |  -  |  -  |
| Vlan133 |  Cust_A_VRF  |  -  |  10.1.12.1/24  |  -  |  -  |  -  |  -  |
| Vlan167 |  Cust_A_VRF  |  -  |  10.1.11.1/24  |  -  |  -  |  -  |  -  |
| Vlan200 |  Cust_B_VRF  |  -  |  10.32.1.1/24  |  -  |  -  |  -  |  -  |
| Vlan233 |  Cust_B_VRF  |  -  |  10.32.12.1/24  |  -  |  -  |  -  |  -  |
| Vlan267 |  Cust_B_VRF  |  -  |  10.32.11.1/24  |  -  |  -  |  -  |  -  |
| Vlan3099 |  Cust_A_VRF  |  172.19.33.71/31  |  -  |  -  |  -  |  -  |  -  |
| Vlan3199 |  Cust_B_VRF  |  172.19.33.71/31  |  -  |  -  |  -  |  -  |  -  |
| Vlan4094 |  default  |  172.19.33.71/31  |  -  |  -  |  -  |  -  |  -  |


### VLAN Interfaces Device Configuration

```eos
!
interface Vlan100
   description set from structured_config on svi (was Cust_A_OP_Zone_1)
   no shutdown
   vrf Cust_A_VRF
   ip address virtual 10.0.10.1/24
   ip helper-address 10.0.10.10
   ip helper-address 10.1.10.10
!
interface Vlan133
   description Cust_A_OP_M2
   no shutdown
   vrf Cust_A_VRF
   ip address virtual 10.1.12.1/24
   ip helper-address 10.1.12.10
   comment
   Comment created from raw_eos_cli under SVI 112 in VRF Common_VRF
   EOF

!
interface Vlan167
   description Cust_A_M2C2
   shutdown
   vrf Cust_A_VRF
   ip address virtual 10.1.11.1/24
   ip helper-address 10.1.11.10
!
interface Vlan200
   description set from structured_config on svi (was Cust_B_OP_Zone_1)
   no shutdown
   vrf Cust_B_VRF
   ip address virtual 10.32.1.1/24
   ip helper-address 10.32.1.10
!
interface Vlan233
   description Cust_B_M2
   no shutdown
   vrf Cust_B_VRF
   ip address virtual 10.32.12.1/24
   ip helper-address 10.32.12.10
!
interface Vlan267
   description Cust_B_M2C2
   shutdown
   vrf Cust_B_VRF
   ip address virtual 10.32.11.1/24
   ip helper-address 10.32.11.10
!
interface Vlan3099
   description MLAG_PEER_L3_iBGP: vrf Cust_A_VRF
   no shutdown
   mtu 9214
   vrf Cust_A_VRF
   ip address 172.19.33.71/31
!
interface Vlan3199
   description MLAG_PEER_L3_iBGP: vrf Cust_B_VRF
   no shutdown
   mtu 9214
   vrf Cust_B_VRF
   ip address 172.19.33.71/31
!
interface Vlan4094
   description MLAG_PEER
   no shutdown
   mtu 9214
   no autostate
   ip address 172.19.33.71/31
```

## VXLAN Interface

### VXLAN Interface Summary

| Setting | Value |
| ------- | ----- |
| Source Interface | Loopback1 |
| UDP port | 4789 |
| EVPN MLAG Shared Router MAC | mlag-system-id |

#### VLAN to VNI, Flood List and Multicast Group Mappings

| VLAN | VNI | Flood List | Multicast Group |
| ---- | --- | ---------- | --------------- |
| 100 | 10100 | - | - |
| 133 | 10133 | - | - |
| 167 | 10167 | - | - |
| 200 | 20200 | - | - |
| 233 | 20233 | - | - |
| 267 | 20267 | - | - |

#### VRF to VNI and Multicast Group Mappings

| VRF | VNI | Multicast Group |
| ---- | --- | --------------- |
| Cust_A_VRF | 100 | - |
| Cust_B_VRF | 200 | - |

### VXLAN Interface Device Configuration

```eos
!
interface Vxlan1
   description DC1-POD2-LEAF9B_VTEP
   vxlan source-interface Loopback1
   vxlan virtual-router encapsulation mac-address mlag-system-id
   vxlan udp-port 4789
   vxlan vlan 100 vni 10100
   vxlan vlan 133 vni 10133
   vxlan vlan 167 vni 10167
   vxlan vlan 200 vni 20200
   vxlan vlan 233 vni 20233
   vxlan vlan 267 vni 20267
   vxlan vrf Cust_A_VRF vni 100
   vxlan vrf Cust_B_VRF vni 200
```

# Routing
## Service Routing Protocols Model

Multi agent routing protocol model enabled

```eos
!
service routing protocols model multi-agent
```

## Virtual Router MAC Address

### Virtual Router MAC Address Summary

#### Virtual Router MAC Address: 00:1c:73:00:dc:12

### Virtual Router MAC Address Configuration

```eos
!
ip virtual-router mac-address 00:1c:73:00:dc:12
```

## IP Routing

### IP Routing Summary

| VRF | Routing Enabled |
| --- | --------------- |
| default | true |
| Cust_A_VRF | true |
| Cust_B_VRF | true |
| mgmt | false |

### IP Routing Device Configuration

```eos
!
ip routing
ip routing vrf Cust_A_VRF
ip routing vrf Cust_B_VRF
no ip routing vrf mgmt
```
## IPv6 Routing

### IPv6 Routing Summary

| VRF | Routing Enabled |
| --- | --------------- |
| default | false |
| Cust_A_VRF | false |
| Cust_B_VRF | false |
| mgmt | false |

## Static Routes

### Static Routes Summary

| VRF | Destination Prefix | Next Hop IP             | Exit interface      | Administrative Distance       | Tag               | Route Name                    | Metric         |
| --- | ------------------ | ----------------------- | ------------------- | ----------------------------- | ----------------- | ----------------------------- | -------------- |
| mgmt  | 0.0.0.0/0 |  10.6.33.1  |  -  |  1  |  -  |  -  |  - |

### Static Routes Device Configuration

```eos
!
ip route vrf mgmt 0.0.0.0/0 10.6.33.1
```

## Router BGP

### Router BGP Summary

| BGP AS | Router ID |
| ------ | --------- |
| 65009|  10.4.33.39 |

| BGP Tuning |
| ---------- |
| no bgp default ipv4-unicast |
| distance bgp 20 200 200 |
| graceful-restart restart-time 300 |
| graceful-restart |
| maximum-paths 4 ecmp 4 |

### Router BGP Peer Groups

#### EVPN-OVERLAY-PEERS

| Settings | Value |
| -------- | ----- |
| Address Family | evpn |
| Next-hop unchanged | True |
| Source | Loopback0 |
| BFD | True |
| Ebgp multihop | 5 |
| Send community | all |
| Maximum routes | 0 (no limit) |

#### IPv4-UNDERLAY-PEERS

| Settings | Value |
| -------- | ----- |
| Address Family | ipv4 |
| Send community | all |
| Maximum routes | 12000 |

#### MLAG-IPv4-UNDERLAY-PEER

| Settings | Value |
| -------- | ----- |
| Address Family | ipv4 |
| Remote AS | 65009 |
| Next-hop self | True |
| Send community | all |
| Maximum routes | 12000 |

### BGP Neighbors

| Neighbor | Remote AS | VRF | Shutdown | Send-community | Maximum-routes | Allowas-in | BFD |
| -------- | --------- | --- | -------- | -------------- | -------------- | ---------- | --- |
| 172.17.33.32 | 64701 | default | - | Inherited from peer group IPv4-UNDERLAY-PEERS | Inherited from peer group IPv4-UNDERLAY-PEERS | - | - |
| 172.17.33.34 | 64702 | default | - | Inherited from peer group IPv4-UNDERLAY-PEERS | Inherited from peer group IPv4-UNDERLAY-PEERS | - | - |
| 172.17.33.36 | 64703 | default | - | Inherited from peer group IPv4-UNDERLAY-PEERS | Inherited from peer group IPv4-UNDERLAY-PEERS | - | - |
| 172.17.33.38 | 64704 | default | - | Inherited from peer group IPv4-UNDERLAY-PEERS | Inherited from peer group IPv4-UNDERLAY-PEERS | - | - |
| 172.19.33.70 | Inherited from peer group MLAG-IPv4-UNDERLAY-PEER | default | - | Inherited from peer group MLAG-IPv4-UNDERLAY-PEER | Inherited from peer group MLAG-IPv4-UNDERLAY-PEER | - | - |
| 172.19.33.70 | Inherited from peer group MLAG-IPv4-UNDERLAY-PEER | Cust_A_VRF | - | Inherited from peer group MLAG-IPv4-UNDERLAY-PEER | Inherited from peer group MLAG-IPv4-UNDERLAY-PEER | - | - |
| 172.19.33.70 | Inherited from peer group MLAG-IPv4-UNDERLAY-PEER | Cust_B_VRF | - | Inherited from peer group MLAG-IPv4-UNDERLAY-PEER | Inherited from peer group MLAG-IPv4-UNDERLAY-PEER | - | - |

### Router BGP EVPN Address Family

- VPN import pruning is __enabled__

#### EVPN Peer Groups

| Peer Group | Activate |
| ---------- | -------- |
| EVPN-OVERLAY-PEERS | True |

### Router BGP VLANs

| VLAN | Route-Distinguisher | Both Route-Target | Import Route Target | Export Route-Target | Redistribute |
| ---- | ------------------- | ----------------- | ------------------- | ------------------- | ------------ |
| 100 | 10.4.33.39:10100 | 10100:10100 | - | - | learned |
| 133 | 10.4.33.39:10133 | 10133:10133 | - | - | learned |
| 167 | 10.4.33.39:10167 | 10167:10167 | - | - | learned |
| 200 | 10.4.33.39:20200 | 20200:20200 | - | - | learned |
| 233 | 10.4.33.39:20233 | 20233:20233 | - | - | learned |
| 267 | 10.4.33.39:20267 | 20267:20267 | - | - | learned |

### Router BGP VRFs

| VRF | Route-Distinguisher | Redistribute |
| --- | ------------------- | ------------ |
| Cust_A_VRF | 10.4.33.39:100 | connected |
| Cust_B_VRF | 10.4.33.39:200 | connected |

### Router BGP Device Configuration

```eos
!
router bgp 65009
   router-id 10.4.33.39
   no bgp default ipv4-unicast
   distance bgp 20 200 200
   graceful-restart restart-time 300
   graceful-restart
   maximum-paths 4 ecmp 4
   neighbor EVPN-OVERLAY-PEERS peer group
   neighbor EVPN-OVERLAY-PEERS next-hop-unchanged
   neighbor EVPN-OVERLAY-PEERS update-source Loopback0
   neighbor EVPN-OVERLAY-PEERS bfd
   neighbor EVPN-OVERLAY-PEERS ebgp-multihop 5
   neighbor EVPN-OVERLAY-PEERS password 7 q+VNViP5i4rVjW1cxFv2wA==
   neighbor EVPN-OVERLAY-PEERS send-community
   neighbor EVPN-OVERLAY-PEERS maximum-routes 0
   neighbor IPv4-UNDERLAY-PEERS peer group
   neighbor IPv4-UNDERLAY-PEERS password 7 AQQvKeimxJu+uGQ/yYvv9w==
   neighbor IPv4-UNDERLAY-PEERS send-community
   neighbor IPv4-UNDERLAY-PEERS maximum-routes 12000
   neighbor MLAG-IPv4-UNDERLAY-PEER peer group
   neighbor MLAG-IPv4-UNDERLAY-PEER remote-as 65009
   neighbor MLAG-IPv4-UNDERLAY-PEER next-hop-self
   neighbor MLAG-IPv4-UNDERLAY-PEER password 7 vnEaG8gMeQf3d3cN6PktXQ==
   neighbor MLAG-IPv4-UNDERLAY-PEER send-community
   neighbor MLAG-IPv4-UNDERLAY-PEER maximum-routes 12000
   neighbor MLAG-IPv4-UNDERLAY-PEER route-map RM-MLAG-PEER-IN in
   neighbor 172.17.33.32 peer group IPv4-UNDERLAY-PEERS
   neighbor 172.17.33.32 remote-as 64701
   neighbor 172.17.33.32 description DC1-POD2-SPINE1_Ethernet18/1
   neighbor 172.17.33.34 peer group IPv4-UNDERLAY-PEERS
   neighbor 172.17.33.34 remote-as 64702
   neighbor 172.17.33.34 description DC1-POD2-SPINE2_Ethernet18/1
   neighbor 172.17.33.36 peer group IPv4-UNDERLAY-PEERS
   neighbor 172.17.33.36 remote-as 64703
   neighbor 172.17.33.36 description DC1-POD2-SPINE3_Ethernet18/1
   neighbor 172.17.33.38 peer group IPv4-UNDERLAY-PEERS
   neighbor 172.17.33.38 remote-as 64704
   neighbor 172.17.33.38 description DC1-POD2-SPINE4_Ethernet18/1
   neighbor 172.19.33.70 peer group MLAG-IPv4-UNDERLAY-PEER
   neighbor 172.19.33.70 description DC1-POD2-LEAF9A
   redistribute connected route-map RM-CONN-2-BGP
   !
   vlan 100
      rd 10.4.33.39:10100
      route-target both 10100:10100
      redistribute learned
   !
   vlan 133
      rd 10.4.33.39:10133
      route-target both 10133:10133
      redistribute learned
   !
   vlan 167
      rd 10.4.33.39:10167
      route-target both 10167:10167
      redistribute learned
   !
   vlan 200
      rd 10.4.33.39:20200
      route-target both 20200:20200
      redistribute learned
   !
   vlan 233
      rd 10.4.33.39:20233
      route-target both 20233:20233
      redistribute learned
   !
   vlan 267
      rd 10.4.33.39:20267
      route-target both 20267:20267
      redistribute learned
   !
   address-family evpn
      neighbor EVPN-OVERLAY-PEERS activate
      route import match-failure action discard
   !
   address-family rt-membership
      neighbor EVPN-OVERLAY-PEERS activate
      neighbor EVPN-OVERLAY-PEERS default-route-target only
   !
   address-family ipv4
      no neighbor EVPN-OVERLAY-PEERS activate
      neighbor IPv4-UNDERLAY-PEERS activate
      neighbor MLAG-IPv4-UNDERLAY-PEER activate
   !
   vrf Cust_A_VRF
      rd 10.4.33.39:100
      route-target import evpn 100:100
      route-target export evpn 100:100
      router-id 10.4.33.39
      neighbor 172.19.33.70 peer group MLAG-IPv4-UNDERLAY-PEER
      redistribute connected
   !
   vrf Cust_B_VRF
      rd 10.4.33.39:200
      route-target import evpn 200:200
      route-target export evpn 200:200
      router-id 10.4.33.39
      neighbor 172.19.33.70 peer group MLAG-IPv4-UNDERLAY-PEER
      redistribute connected
```

# BFD

## Router BFD

### Router BFD Multihop Summary

| Interval | Minimum RX | Multiplier |
| -------- | ---------- | ---------- |
| 300 | 300 | 3 |

### Router BFD Device Configuration

```eos
!
router bfd
   multihop interval 300 min-rx 300 multiplier 3
```

# Multicast

## IP IGMP Snooping

### IP IGMP Snooping Summary

| IGMP Snooping | Fast Leave | Interface Restart Query | Proxy | Restart Query Interval | Robustness Variable |
| ------------- | ---------- | ----------------------- | ----- | ---------------------- | ------------------- |
| Enabled | - | - | - | - | - |

#### IP IGMP Snooping Vlan Summary

| Vlan | IGMP Snooping | Fast Leave | Max Groups | Proxy |
| ---- | ------------- | ---------- | ---------- | ----- |
| 100 | True | - | - | - |

### IP IGMP Snooping Device Configuration

```eos
!
ip igmp snooping vlan 100
```

# Filters

## Prefix-lists

### Prefix-lists Summary

#### PL-LOOPBACKS-EVPN-OVERLAY

| Sequence | Action |
| -------- | ------ |
| 10 | permit 10.4.33.0/24 eq 32 |
| 20 | permit 10.5.33.0/24 eq 32 |

### Prefix-lists Device Configuration

```eos
!
ip prefix-list PL-LOOPBACKS-EVPN-OVERLAY
   seq 10 permit 10.4.33.0/24 eq 32
   seq 20 permit 10.5.33.0/24 eq 32
```

## Route-maps

### Route-maps Summary

#### RM-CONN-2-BGP

| Sequence | Type | Match and/or Set |
| -------- | ---- | ---------------- |
| 10 | permit | match ip address prefix-list PL-LOOPBACKS-EVPN-OVERLAY |

#### RM-MLAG-PEER-IN

| Sequence | Type | Match and/or Set |
| -------- | ---- | ---------------- |
| 10 | permit | set origin incomplete |

### Route-maps Device Configuration

```eos
!
route-map RM-CONN-2-BGP permit 10
   match ip address prefix-list PL-LOOPBACKS-EVPN-OVERLAY
!
route-map RM-MLAG-PEER-IN permit 10
   description Make routes learned over MLAG Peer-link less preferred on spines to ensure optimal routing
   set origin incomplete
```

# ACL

# VRF Instances

## VRF Instances Summary

| VRF Name | IP Routing |
| -------- | ---------- |
| Cust_A_VRF | enabled |
| Cust_B_VRF | enabled |
| mgmt | disabled |

## VRF Instances Device Configuration

```eos
!
vrf instance Cust_A_VRF
!
vrf instance Cust_B_VRF
!
vrf instance mgmt
```

# Quality Of Service

# EOS CLI

```eos
!
interface Loopback1111
  description Loopback created from raw_eos_cli under platform_settings vEOS-LAB in AMS.yml

```
