# DC1-POD2-LEAF1A
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
| Management0 | oob_management | oob | mgmt | 10.6.33.20/24 | 10.6.33.1 |

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
   ip address 10.6.33.20/24
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
| - | AMS DC1 DC1_POD2 DC1-POD2-LEAF1A | All | Disabled |

### SNMP Device Configuration

```eos
!
snmp-server location AMS DC1 DC1_POD2 DC1-POD2-LEAF1A
```

# MLAG

## MLAG Summary

| Domain-id | Local-interface | Peer-address | Peer-link |
| --------- | --------------- | ------------ | --------- |
| RACK1_MLAG | Vlan4094 | 172.19.33.39 | Port-Channel151 |

Dual primary detection is enabled. The detection delay is 5 seconds.

## MLAG Device Configuration

```eos
!
mlag configuration
   domain-id RACK1_MLAG
   local-interface Vlan4094
   peer-address 172.19.33.39
   peer-address heartbeat 10.6.33.20 vrf mgmt
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
| 4094 | MLAG_PEER | MLAG |

## VLANs Device Configuration

```eos
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
| Ethernet15/1 | MLAG_PEER_DC1-POD2-LEAF1B_Ethernet15/1 | *trunk | *2-4094 | *- | *['LEAF_PEER_L3', 'MLAG'] | 151 |
| Ethernet16/1 | MLAG_PEER_DC1-POD2-LEAF1B_Ethernet16/1 | *trunk | *2-4094 | *- | *['LEAF_PEER_L3', 'MLAG'] | 151 |

*Inherited from Port-Channel Interface

#### IPv4

| Interface | Description | Type | Channel Group | IP Address | VRF |  MTU | Shutdown | ACL In | ACL Out |
| --------- | ----------- | -----| ------------- | ---------- | ----| ---- | -------- | ------ | ------- |
| Ethernet29/1 | P2P_LINK_TO_DC1-POD2-SPINE1_Ethernet1/1 | routed | - | 172.17.32.153/31 | default | 9214 | false | - | - |
| Ethernet30/1 | P2P_LINK_TO_DC1-POD2-SPINE2_Ethernet1/1 | routed | - | 172.17.32.155/31 | default | 9214 | false | - | - |
| Ethernet31/1 | P2P_LINK_TO_DC1-POD2-SPINE3_Ethernet1/1 | routed | - | 172.17.32.157/31 | default | 9214 | false | - | - |
| Ethernet32/1 | P2P_LINK_TO_DC1-POD2-SPINE4_Ethernet1/1 | routed | - | 172.17.32.159/31 | default | 9214 | false | - | - |

### Ethernet Interfaces Device Configuration

```eos
!
interface Ethernet15/1
   description MLAG_PEER_DC1-POD2-LEAF1B_Ethernet15/1
   no shutdown
   channel-group 151 mode active
!
interface Ethernet16/1
   description MLAG_PEER_DC1-POD2-LEAF1B_Ethernet16/1
   no shutdown
   channel-group 151 mode active
!
interface Ethernet29/1
   description P2P_LINK_TO_DC1-POD2-SPINE1_Ethernet1/1
   no shutdown
   mtu 9214
   no switchport
   ip address 172.17.32.153/31
   ptp enable
   service-profile P2P-QOS-PROFILE
!
interface Ethernet30/1
   description P2P_LINK_TO_DC1-POD2-SPINE2_Ethernet1/1
   no shutdown
   mtu 9214
   no switchport
   ip address 172.17.32.155/31
   ptp enable
   service-profile P2P-QOS-PROFILE
!
interface Ethernet31/1
   description P2P_LINK_TO_DC1-POD2-SPINE3_Ethernet1/1
   no shutdown
   mtu 9214
   no switchport
   ip address 172.17.32.157/31
   ptp enable
   service-profile P2P-QOS-PROFILE
!
interface Ethernet32/1
   description P2P_LINK_TO_DC1-POD2-SPINE4_Ethernet1/1
   no shutdown
   mtu 9214
   no switchport
   ip address 172.17.32.159/31
   ptp enable
   service-profile P2P-QOS-PROFILE
```

## Port-Channel Interfaces

### Port-Channel Interfaces Summary

#### L2

| Interface | Description | Type | Mode | VLANs | Native VLAN | Trunk Group | LACP Fallback Timeout | LACP Fallback Mode | MLAG ID | EVPN ESI |
| --------- | ----------- | ---- | ---- | ----- | ----------- | ------------| --------------------- | ------------------ | ------- | -------- |
| Port-Channel151 | MLAG_PEER_DC1-POD2-LEAF1B_Po151 | switched | trunk | 2-4094 | - | ['LEAF_PEER_L3', 'MLAG'] | - | - | - | - |

### Port-Channel Interfaces Device Configuration

```eos
!
interface Port-Channel151
   description MLAG_PEER_DC1-POD2-LEAF1B_Po151
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
| Loopback0 | EVPN_Overlay_Peering | default | 10.4.33.22/32 |
| Loopback1 | VTEP_VXLAN_Tunnel_Source | default | 10.5.33.22/32 |

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
   ip address 10.4.33.22/32
!
interface Loopback1
   description VTEP_VXLAN_Tunnel_Source
   no shutdown
   ip address 10.5.33.22/32
```

## VLAN Interfaces

### VLAN Interfaces Summary

| Interface | Description | VRF |  MTU | Shutdown |
| --------- | ----------- | --- | ---- | -------- |
| Vlan4094 |  MLAG_PEER  |  default  |  9214  |  false  |

#### IPv4

| Interface | VRF | IP Address | IP Address Virtual | IP Router Virtual Address | VRRP | ACL In | ACL Out |
| --------- | --- | ---------- | ------------------ | ------------------------- | ---- | ------ | ------- |
| Vlan4094 |  default  |  172.19.33.38/31  |  -  |  -  |  -  |  -  |  -  |


### VLAN Interfaces Device Configuration

```eos
!
interface Vlan4094
   description MLAG_PEER
   no shutdown
   mtu 9214
   no autostate
   ip address 172.19.33.38/31
```

## VXLAN Interface

### VXLAN Interface Summary

| Setting | Value |
| ------- | ----- |
| Source Interface | Loopback1 |
| UDP port | 4789 |
| EVPN MLAG Shared Router MAC | mlag-system-id |

### VXLAN Interface Device Configuration

```eos
!
interface Vxlan1
   description DC1-POD2-LEAF1A_VTEP
   vxlan source-interface Loopback1
   vxlan virtual-router encapsulation mac-address mlag-system-id
   vxlan udp-port 4789
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
| mgmt | false |

### IP Routing Device Configuration

```eos
!
ip routing
no ip routing vrf mgmt
```
## IPv6 Routing

### IPv6 Routing Summary

| VRF | Routing Enabled |
| --- | --------------- |
| default | false |
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
| 65001|  10.4.33.22 |

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
| Remote AS | 65001 |
| Next-hop self | True |
| Send community | all |
| Maximum routes | 12000 |

### BGP Neighbors

| Neighbor | Remote AS | VRF | Shutdown | Send-community | Maximum-routes | Allowas-in | BFD |
| -------- | --------- | --- | -------- | -------------- | -------------- | ---------- | --- |
| 172.17.32.152 | 64701 | default | - | Inherited from peer group IPv4-UNDERLAY-PEERS | Inherited from peer group IPv4-UNDERLAY-PEERS | - | - |
| 172.17.32.154 | 64702 | default | - | Inherited from peer group IPv4-UNDERLAY-PEERS | Inherited from peer group IPv4-UNDERLAY-PEERS | - | - |
| 172.17.32.156 | 64703 | default | - | Inherited from peer group IPv4-UNDERLAY-PEERS | Inherited from peer group IPv4-UNDERLAY-PEERS | - | - |
| 172.17.32.158 | 64704 | default | - | Inherited from peer group IPv4-UNDERLAY-PEERS | Inherited from peer group IPv4-UNDERLAY-PEERS | - | - |
| 172.19.33.39 | Inherited from peer group MLAG-IPv4-UNDERLAY-PEER | default | - | Inherited from peer group MLAG-IPv4-UNDERLAY-PEER | Inherited from peer group MLAG-IPv4-UNDERLAY-PEER | - | - |

### Router BGP EVPN Address Family

- VPN import pruning is __enabled__

#### EVPN Peer Groups

| Peer Group | Activate |
| ---------- | -------- |
| EVPN-OVERLAY-PEERS | True |

### Router BGP Device Configuration

```eos
!
router bgp 65001
   router-id 10.4.33.22
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
   neighbor MLAG-IPv4-UNDERLAY-PEER remote-as 65001
   neighbor MLAG-IPv4-UNDERLAY-PEER next-hop-self
   neighbor MLAG-IPv4-UNDERLAY-PEER password 7 vnEaG8gMeQf3d3cN6PktXQ==
   neighbor MLAG-IPv4-UNDERLAY-PEER send-community
   neighbor MLAG-IPv4-UNDERLAY-PEER maximum-routes 12000
   neighbor MLAG-IPv4-UNDERLAY-PEER route-map RM-MLAG-PEER-IN in
   neighbor 172.17.32.152 peer group IPv4-UNDERLAY-PEERS
   neighbor 172.17.32.152 remote-as 64701
   neighbor 172.17.32.152 description DC1-POD2-SPINE1_Ethernet1/1
   neighbor 172.17.32.154 peer group IPv4-UNDERLAY-PEERS
   neighbor 172.17.32.154 remote-as 64702
   neighbor 172.17.32.154 description DC1-POD2-SPINE2_Ethernet1/1
   neighbor 172.17.32.156 peer group IPv4-UNDERLAY-PEERS
   neighbor 172.17.32.156 remote-as 64703
   neighbor 172.17.32.156 description DC1-POD2-SPINE3_Ethernet1/1
   neighbor 172.17.32.158 peer group IPv4-UNDERLAY-PEERS
   neighbor 172.17.32.158 remote-as 64704
   neighbor 172.17.32.158 description DC1-POD2-SPINE4_Ethernet1/1
   neighbor 172.19.33.39 peer group MLAG-IPv4-UNDERLAY-PEER
   neighbor 172.19.33.39 description DC1-POD2-LEAF1B
   redistribute connected route-map RM-CONN-2-BGP
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

### IP IGMP Snooping Device Configuration

```eos
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
| mgmt | disabled |

## VRF Instances Device Configuration

```eos
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
