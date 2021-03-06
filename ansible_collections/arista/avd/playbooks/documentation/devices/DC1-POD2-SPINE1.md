# DC1-POD2-SPINE1
# Table of Contents

- [Management](#management)
  - [Management Interfaces](#management-interfaces)
  - [Management API HTTP](#management-api-http)
- [Authentication](#authentication)
  - [Local Users](#local-users)
- [Monitoring](#monitoring)
  - [SNMP](#snmp)
- [Spanning Tree](#spanning-tree)
  - [Spanning Tree Summary](#spanning-tree-summary)
  - [Spanning Tree Device Configuration](#spanning-tree-device-configuration)
- [Internal VLAN Allocation Policy](#internal-vlan-allocation-policy)
  - [Internal VLAN Allocation Policy Summary](#internal-vlan-allocation-policy-summary)
  - [Internal VLAN Allocation Policy Configuration](#internal-vlan-allocation-policy-configuration)
- [Interfaces](#interfaces)
  - [Ethernet Interfaces](#ethernet-interfaces)
  - [Loopback Interfaces](#loopback-interfaces)
- [Routing](#routing)
  - [Service Routing Protocols Model](#service-routing-protocols-model)
  - [IP Routing](#ip-routing)
  - [IPv6 Routing](#ipv6-routing)
  - [Static Routes](#static-routes)
  - [Router BGP](#router-bgp)
- [Multicast](#multicast)
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
| Management0 | oob_management | oob | mgmt | 10.6.33.10/24 | 10.6.33.1 |

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
   ip address 10.6.33.10/24
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
| - | AMS DC1 DC1_POD2 DC1-POD2-SPINE1 | All | Disabled |

### SNMP Device Configuration

```eos
!
snmp-server location AMS DC1 DC1_POD2 DC1-POD2-SPINE1
```

# Spanning Tree

## Spanning Tree Summary

STP mode: **none**

## Spanning Tree Device Configuration

```eos
!
spanning-tree mode none
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

# Interfaces

## Ethernet Interfaces

### Ethernet Interfaces Summary

#### L2

| Interface | Description | Mode | VLANs | Native VLAN | Trunk Group | Channel-Group |
| --------- | ----------- | ---- | ----- | ----------- | ----------- | ------------- |

*Inherited from Port-Channel Interface

#### IPv4

| Interface | Description | Type | Channel Group | IP Address | VRF |  MTU | Shutdown | ACL In | ACL Out |
| --------- | ----------- | -----| ------------- | ---------- | ----| ---- | -------- | ------ | ------- |
| Ethernet1/1 | P2P_LINK_TO_DC1-POD2-LEAF1A_Ethernet29/1 | routed | - | 172.17.32.152/31 | default | 9214 | false | - | - |
| Ethernet2/1 | P2P_LINK_TO_DC1-POD2-LEAF1B_Ethernet29/1 | routed | - | 172.17.32.160/31 | default | 9214 | false | - | - |
| Ethernet3/1 | P2P_LINK_TO_DC1-POD2-LEAF2A_Ethernet29/1 | routed | - | 172.17.32.168/31 | default | 9214 | false | - | - |
| Ethernet4/1 | P2P_LINK_TO_DC1-POD2-LEAF2B_Ethernet29/1 | routed | - | 172.17.32.176/31 | default | 9214 | false | - | - |
| Ethernet5/1 | P2P_LINK_TO_DC1-POD2-LEAF3A_Ethernet29/1 | routed | - | 172.17.32.184/31 | default | 9214 | false | - | - |
| Ethernet6/1 | P2P_LINK_TO_DC1-POD2-LEAF3B_Ethernet29/1 | routed | - | 172.17.32.192/31 | default | 9214 | false | - | - |
| Ethernet7/1 | P2P_LINK_TO_DC1-POD2-LEAF4A_Ethernet29/1 | routed | - | 172.17.32.200/31 | default | 9214 | false | - | - |
| Ethernet8/1 | P2P_LINK_TO_DC1-POD2-LEAF4B_Ethernet29/1 | routed | - | 172.17.32.208/31 | default | 9214 | false | - | - |
| Ethernet9/1 | P2P_LINK_TO_DC1-POD2-LEAF5A_Ethernet29/1 | routed | - | 172.17.32.216/31 | default | 9214 | false | - | - |
| Ethernet10/1 | P2P_LINK_TO_DC1-POD2-LEAF5B_Ethernet29/1 | routed | - | 172.17.32.224/31 | default | 9214 | false | - | - |
| Ethernet11/1 | P2P_LINK_TO_DC1-POD2-LEAF6A_Ethernet29/1 | routed | - | 172.17.32.232/31 | default | 9214 | false | - | - |
| Ethernet12/1 | P2P_LINK_TO_DC1-POD2-LEAF6B_Ethernet29/1 | routed | - | 172.17.32.240/31 | default | 9214 | false | - | - |
| Ethernet13/1 | P2P_LINK_TO_DC1-POD2-LEAF7A_Ethernet29/1 | routed | - | 172.17.32.248/31 | default | 9214 | false | - | - |
| Ethernet14/1 | P2P_LINK_TO_DC1-POD2-LEAF7B_Ethernet29/1 | routed | - | 172.17.33.0/31 | default | 9214 | false | - | - |
| Ethernet15/1 | P2P_LINK_TO_DC1-POD2-LEAF8A_Ethernet29/1 | routed | - | 172.17.33.8/31 | default | 9214 | false | - | - |
| Ethernet16/1 | P2P_LINK_TO_DC1-POD2-LEAF8B_Ethernet29/1 | routed | - | 172.17.33.16/31 | default | 9214 | false | - | - |
| Ethernet17/1 | P2P_LINK_TO_DC1-POD2-LEAF9A_Ethernet29/1 | routed | - | 172.17.33.24/31 | default | 9214 | false | - | - |
| Ethernet18/1 | P2P_LINK_TO_DC1-POD2-LEAF9B_Ethernet29/1 | routed | - | 172.17.33.32/31 | default | 9214 | false | - | - |
| Ethernet19/1 | P2P_LINK_TO_DC1-POD2-LEAF10A_Ethernet29/1 | routed | - | 172.17.33.40/31 | default | 9214 | false | - | - |
| Ethernet20/1 | P2P_LINK_TO_DC1-POD2-LEAF10B_Ethernet29/1 | routed | - | 172.17.33.48/31 | default | 9214 | false | - | - |
| Ethernet21/1 | P2P_LINK_TO_DC1-POD2-LEAF11A_Ethernet29/1 | routed | - | 172.17.33.56/31 | default | 9214 | false | - | - |
| Ethernet22/1 | P2P_LINK_TO_DC1-POD2-LEAF11B_Ethernet29/1 | routed | - | 172.17.33.64/31 | default | 9214 | false | - | - |
| Ethernet23/1 | P2P_LINK_TO_DC1-POD2-LEAF12A_Ethernet29/1 | routed | - | 172.17.33.72/31 | default | 9214 | false | - | - |
| Ethernet24/1 | P2P_LINK_TO_DC1-POD2-LEAF12B_Ethernet29/1 | routed | - | 172.17.33.80/31 | default | 9214 | false | - | - |
| Ethernet25/1 | P2P_LINK_TO_DC1-POD2-LEAF13A_Ethernet29/1 | routed | - | 172.17.33.88/31 | default | 9214 | false | - | - |
| Ethernet26/1 | P2P_LINK_TO_DC1-POD2-LEAF13B_Ethernet29/1 | routed | - | 172.17.33.96/31 | default | 9214 | false | - | - |
| Ethernet27/1 | P2P_LINK_TO_DC1-POD2-LEAF14A_Ethernet29/1 | routed | - | 172.17.33.104/31 | default | 9214 | false | - | - |
| Ethernet28/1 | P2P_LINK_TO_DC1-POD2-LEAF14B_Ethernet29/1 | routed | - | 172.17.33.112/31 | default | 9214 | false | - | - |
| Ethernet29/1 | P2P_LINK_TO_SUPER-SPINE1_Ethernet5/1 | routed | - | 172.16.32.19/31 | default | 9214 | false | - | - |
| Ethernet30/1 | P2P_LINK_TO_SUPER-SPINE2_Ethernet5/1 | routed | - | 172.16.32.83/31 | default | 9214 | false | - | - |
| Ethernet31/1 | P2P_LINK_TO_SUPER-SPINE3_Ethernet5/1 | routed | - | 172.16.32.147/31 | default | 9214 | false | - | - |
| Ethernet32/1 | P2P_LINK_TO_SUPER-SPINE4_Ethernet5/2 | routed | - | 172.16.32.211/31 | default | 9214 | false | - | - |

### Ethernet Interfaces Device Configuration

```eos
!
interface Ethernet1/1
   description P2P_LINK_TO_DC1-POD2-LEAF1A_Ethernet29/1
   no shutdown
   mtu 9214
   no switchport
   ip address 172.17.32.152/31
   ptp enable
   service-profile P2P-QOS-PROFILE
!
interface Ethernet2/1
   description P2P_LINK_TO_DC1-POD2-LEAF1B_Ethernet29/1
   no shutdown
   mtu 9214
   no switchport
   ip address 172.17.32.160/31
   ptp enable
   service-profile P2P-QOS-PROFILE
!
interface Ethernet3/1
   description P2P_LINK_TO_DC1-POD2-LEAF2A_Ethernet29/1
   no shutdown
   mtu 9214
   no switchport
   ip address 172.17.32.168/31
   ptp enable
   service-profile P2P-QOS-PROFILE
!
interface Ethernet4/1
   description P2P_LINK_TO_DC1-POD2-LEAF2B_Ethernet29/1
   no shutdown
   mtu 9214
   no switchport
   ip address 172.17.32.176/31
   ptp enable
   service-profile P2P-QOS-PROFILE
!
interface Ethernet5/1
   description P2P_LINK_TO_DC1-POD2-LEAF3A_Ethernet29/1
   no shutdown
   mtu 9214
   no switchport
   ip address 172.17.32.184/31
   ptp enable
   service-profile P2P-QOS-PROFILE
!
interface Ethernet6/1
   description P2P_LINK_TO_DC1-POD2-LEAF3B_Ethernet29/1
   no shutdown
   mtu 9214
   no switchport
   ip address 172.17.32.192/31
   ptp enable
   service-profile P2P-QOS-PROFILE
!
interface Ethernet7/1
   description P2P_LINK_TO_DC1-POD2-LEAF4A_Ethernet29/1
   no shutdown
   mtu 9214
   no switchport
   ip address 172.17.32.200/31
   ptp enable
   service-profile P2P-QOS-PROFILE
!
interface Ethernet8/1
   description P2P_LINK_TO_DC1-POD2-LEAF4B_Ethernet29/1
   no shutdown
   mtu 9214
   no switchport
   ip address 172.17.32.208/31
   ptp enable
   service-profile P2P-QOS-PROFILE
!
interface Ethernet9/1
   description P2P_LINK_TO_DC1-POD2-LEAF5A_Ethernet29/1
   no shutdown
   mtu 9214
   no switchport
   ip address 172.17.32.216/31
   ptp enable
   service-profile P2P-QOS-PROFILE
!
interface Ethernet10/1
   description P2P_LINK_TO_DC1-POD2-LEAF5B_Ethernet29/1
   no shutdown
   mtu 9214
   no switchport
   ip address 172.17.32.224/31
   ptp enable
   service-profile P2P-QOS-PROFILE
!
interface Ethernet11/1
   description P2P_LINK_TO_DC1-POD2-LEAF6A_Ethernet29/1
   no shutdown
   mtu 9214
   no switchport
   ip address 172.17.32.232/31
   ptp enable
   service-profile P2P-QOS-PROFILE
!
interface Ethernet12/1
   description P2P_LINK_TO_DC1-POD2-LEAF6B_Ethernet29/1
   no shutdown
   mtu 9214
   no switchport
   ip address 172.17.32.240/31
   ptp enable
   service-profile P2P-QOS-PROFILE
!
interface Ethernet13/1
   description P2P_LINK_TO_DC1-POD2-LEAF7A_Ethernet29/1
   no shutdown
   mtu 9214
   no switchport
   ip address 172.17.32.248/31
   ptp enable
   service-profile P2P-QOS-PROFILE
!
interface Ethernet14/1
   description P2P_LINK_TO_DC1-POD2-LEAF7B_Ethernet29/1
   no shutdown
   mtu 9214
   no switchport
   ip address 172.17.33.0/31
   ptp enable
   service-profile P2P-QOS-PROFILE
!
interface Ethernet15/1
   description P2P_LINK_TO_DC1-POD2-LEAF8A_Ethernet29/1
   no shutdown
   mtu 9214
   no switchport
   ip address 172.17.33.8/31
   ptp enable
   service-profile P2P-QOS-PROFILE
!
interface Ethernet16/1
   description P2P_LINK_TO_DC1-POD2-LEAF8B_Ethernet29/1
   no shutdown
   mtu 9214
   no switchport
   ip address 172.17.33.16/31
   ptp enable
   service-profile P2P-QOS-PROFILE
!
interface Ethernet17/1
   description P2P_LINK_TO_DC1-POD2-LEAF9A_Ethernet29/1
   no shutdown
   mtu 9214
   no switchport
   ip address 172.17.33.24/31
   ptp enable
   service-profile P2P-QOS-PROFILE
!
interface Ethernet18/1
   description P2P_LINK_TO_DC1-POD2-LEAF9B_Ethernet29/1
   no shutdown
   mtu 9214
   no switchport
   ip address 172.17.33.32/31
   ptp enable
   service-profile P2P-QOS-PROFILE
!
interface Ethernet19/1
   description P2P_LINK_TO_DC1-POD2-LEAF10A_Ethernet29/1
   no shutdown
   mtu 9214
   no switchport
   ip address 172.17.33.40/31
   ptp enable
   service-profile P2P-QOS-PROFILE
!
interface Ethernet20/1
   description P2P_LINK_TO_DC1-POD2-LEAF10B_Ethernet29/1
   no shutdown
   mtu 9214
   no switchport
   ip address 172.17.33.48/31
   ptp enable
   service-profile P2P-QOS-PROFILE
!
interface Ethernet21/1
   description P2P_LINK_TO_DC1-POD2-LEAF11A_Ethernet29/1
   no shutdown
   mtu 9214
   no switchport
   ip address 172.17.33.56/31
   ptp enable
   service-profile P2P-QOS-PROFILE
!
interface Ethernet22/1
   description P2P_LINK_TO_DC1-POD2-LEAF11B_Ethernet29/1
   no shutdown
   mtu 9214
   no switchport
   ip address 172.17.33.64/31
   ptp enable
   service-profile P2P-QOS-PROFILE
!
interface Ethernet23/1
   description P2P_LINK_TO_DC1-POD2-LEAF12A_Ethernet29/1
   no shutdown
   mtu 9214
   no switchport
   ip address 172.17.33.72/31
   ptp enable
   service-profile P2P-QOS-PROFILE
!
interface Ethernet24/1
   description P2P_LINK_TO_DC1-POD2-LEAF12B_Ethernet29/1
   no shutdown
   mtu 9214
   no switchport
   ip address 172.17.33.80/31
   ptp enable
   service-profile P2P-QOS-PROFILE
!
interface Ethernet25/1
   description P2P_LINK_TO_DC1-POD2-LEAF13A_Ethernet29/1
   no shutdown
   mtu 9214
   no switchport
   ip address 172.17.33.88/31
   ptp enable
   service-profile P2P-QOS-PROFILE
!
interface Ethernet26/1
   description P2P_LINK_TO_DC1-POD2-LEAF13B_Ethernet29/1
   no shutdown
   mtu 9214
   no switchport
   ip address 172.17.33.96/31
   ptp enable
   service-profile P2P-QOS-PROFILE
!
interface Ethernet27/1
   description P2P_LINK_TO_DC1-POD2-LEAF14A_Ethernet29/1
   no shutdown
   mtu 9214
   no switchport
   ip address 172.17.33.104/31
   ptp enable
   service-profile P2P-QOS-PROFILE
!
interface Ethernet28/1
   description P2P_LINK_TO_DC1-POD2-LEAF14B_Ethernet29/1
   no shutdown
   mtu 9214
   no switchport
   ip address 172.17.33.112/31
   ptp enable
   service-profile P2P-QOS-PROFILE
!
interface Ethernet29/1
   description P2P_LINK_TO_SUPER-SPINE1_Ethernet5/1
   no shutdown
   mtu 9214
   no switchport
   ip address 172.16.32.19/31
   ptp enable
   service-profile P2P-QOS-PROFILE
!
interface Ethernet30/1
   description P2P_LINK_TO_SUPER-SPINE2_Ethernet5/1
   no shutdown
   mtu 9214
   no switchport
   ip address 172.16.32.83/31
   ptp enable
   service-profile P2P-QOS-PROFILE
!
interface Ethernet31/1
   description P2P_LINK_TO_SUPER-SPINE3_Ethernet5/1
   no shutdown
   mtu 9214
   no switchport
   ip address 172.16.32.147/31
   ptp enable
   service-profile P2P-QOS-PROFILE
!
interface Ethernet32/1
   description P2P_LINK_TO_SUPER-SPINE4_Ethernet5/2
   no shutdown
   mtu 9214
   no switchport
   ip address 172.16.32.211/31
   ptp enable
   service-profile P2P-QOS-PROFILE
```

## Loopback Interfaces

### Loopback Interfaces Summary

#### IPv4

| Interface | Description | VRF | IP Address |
| --------- | ----------- | --- | ---------- |
| Loopback0 | EVPN_Overlay_Peering | default | 10.4.32.10/32 |

#### IPv6

| Interface | Description | VRF | IPv6 Address |
| --------- | ----------- | --- | ------------ |
| Loopback0 | EVPN_Overlay_Peering | default | - |


### Loopback Interfaces Device Configuration

```eos
!
interface Loopback0
   description EVPN_Overlay_Peering
   no shutdown
   ip address 10.4.32.10/32
```

# Routing
## Service Routing Protocols Model

Multi agent routing protocol model enabled

```eos
!
service routing protocols model multi-agent
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
| 64701|  10.4.32.10 |

| BGP Tuning |
| ---------- |
| no bgp default ipv4-unicast |
| distance bgp 20 200 200 |
| graceful-restart restart-time 300 |
| graceful-restart |
| maximum-paths 4 ecmp 4 |

### Router BGP Peer Groups

#### IPv4-UNDERLAY-PEERS

| Settings | Value |
| -------- | ----- |
| Address Family | ipv4 |
| Send community | all |
| Maximum routes | 12000 |

### BGP Neighbors

| Neighbor | Remote AS | VRF | Shutdown | Send-community | Maximum-routes | Allowas-in | BFD |
| -------- | --------- | --- | -------- | -------------- | -------------- | ---------- | --- |
| 172.16.32.18 | 64501 | default | - | Inherited from peer group IPv4-UNDERLAY-PEERS | Inherited from peer group IPv4-UNDERLAY-PEERS | - | - |
| 172.16.32.82 | 64502 | default | - | Inherited from peer group IPv4-UNDERLAY-PEERS | Inherited from peer group IPv4-UNDERLAY-PEERS | - | - |
| 172.16.32.146 | 64503 | default | - | Inherited from peer group IPv4-UNDERLAY-PEERS | Inherited from peer group IPv4-UNDERLAY-PEERS | - | - |
| 172.16.32.210 | 64504 | default | - | Inherited from peer group IPv4-UNDERLAY-PEERS | Inherited from peer group IPv4-UNDERLAY-PEERS | - | - |
| 172.17.32.153 | 65001 | default | - | Inherited from peer group IPv4-UNDERLAY-PEERS | Inherited from peer group IPv4-UNDERLAY-PEERS | - | - |
| 172.17.32.161 | 65001 | default | - | Inherited from peer group IPv4-UNDERLAY-PEERS | Inherited from peer group IPv4-UNDERLAY-PEERS | - | - |
| 172.17.32.169 | 65002 | default | - | Inherited from peer group IPv4-UNDERLAY-PEERS | Inherited from peer group IPv4-UNDERLAY-PEERS | - | - |
| 172.17.32.177 | 65002 | default | - | Inherited from peer group IPv4-UNDERLAY-PEERS | Inherited from peer group IPv4-UNDERLAY-PEERS | - | - |
| 172.17.32.185 | 65003 | default | - | Inherited from peer group IPv4-UNDERLAY-PEERS | Inherited from peer group IPv4-UNDERLAY-PEERS | - | - |
| 172.17.32.193 | 65003 | default | - | Inherited from peer group IPv4-UNDERLAY-PEERS | Inherited from peer group IPv4-UNDERLAY-PEERS | - | - |
| 172.17.32.201 | 65004 | default | - | Inherited from peer group IPv4-UNDERLAY-PEERS | Inherited from peer group IPv4-UNDERLAY-PEERS | - | - |
| 172.17.32.209 | 65004 | default | - | Inherited from peer group IPv4-UNDERLAY-PEERS | Inherited from peer group IPv4-UNDERLAY-PEERS | - | - |
| 172.17.32.217 | 65005 | default | - | Inherited from peer group IPv4-UNDERLAY-PEERS | Inherited from peer group IPv4-UNDERLAY-PEERS | - | - |
| 172.17.32.225 | 65005 | default | - | Inherited from peer group IPv4-UNDERLAY-PEERS | Inherited from peer group IPv4-UNDERLAY-PEERS | - | - |
| 172.17.32.233 | 65006 | default | - | Inherited from peer group IPv4-UNDERLAY-PEERS | Inherited from peer group IPv4-UNDERLAY-PEERS | - | - |
| 172.17.32.241 | 65006 | default | - | Inherited from peer group IPv4-UNDERLAY-PEERS | Inherited from peer group IPv4-UNDERLAY-PEERS | - | - |
| 172.17.32.249 | 65007 | default | - | Inherited from peer group IPv4-UNDERLAY-PEERS | Inherited from peer group IPv4-UNDERLAY-PEERS | - | - |
| 172.17.33.1 | 65007 | default | - | Inherited from peer group IPv4-UNDERLAY-PEERS | Inherited from peer group IPv4-UNDERLAY-PEERS | - | - |
| 172.17.33.9 | 65008 | default | - | Inherited from peer group IPv4-UNDERLAY-PEERS | Inherited from peer group IPv4-UNDERLAY-PEERS | - | - |
| 172.17.33.17 | 65008 | default | - | Inherited from peer group IPv4-UNDERLAY-PEERS | Inherited from peer group IPv4-UNDERLAY-PEERS | - | - |
| 172.17.33.25 | 65009 | default | - | Inherited from peer group IPv4-UNDERLAY-PEERS | Inherited from peer group IPv4-UNDERLAY-PEERS | - | - |
| 172.17.33.33 | 65009 | default | - | Inherited from peer group IPv4-UNDERLAY-PEERS | Inherited from peer group IPv4-UNDERLAY-PEERS | - | - |
| 172.17.33.41 | 65010 | default | - | Inherited from peer group IPv4-UNDERLAY-PEERS | Inherited from peer group IPv4-UNDERLAY-PEERS | - | - |
| 172.17.33.49 | 65010 | default | - | Inherited from peer group IPv4-UNDERLAY-PEERS | Inherited from peer group IPv4-UNDERLAY-PEERS | - | - |
| 172.17.33.57 | 65011 | default | - | Inherited from peer group IPv4-UNDERLAY-PEERS | Inherited from peer group IPv4-UNDERLAY-PEERS | - | - |
| 172.17.33.65 | 65011 | default | - | Inherited from peer group IPv4-UNDERLAY-PEERS | Inherited from peer group IPv4-UNDERLAY-PEERS | - | - |
| 172.17.33.73 | 65012 | default | - | Inherited from peer group IPv4-UNDERLAY-PEERS | Inherited from peer group IPv4-UNDERLAY-PEERS | - | - |
| 172.17.33.81 | 65012 | default | - | Inherited from peer group IPv4-UNDERLAY-PEERS | Inherited from peer group IPv4-UNDERLAY-PEERS | - | - |
| 172.17.33.89 | 65013 | default | - | Inherited from peer group IPv4-UNDERLAY-PEERS | Inherited from peer group IPv4-UNDERLAY-PEERS | - | - |
| 172.17.33.97 | 65013 | default | - | Inherited from peer group IPv4-UNDERLAY-PEERS | Inherited from peer group IPv4-UNDERLAY-PEERS | - | - |
| 172.17.33.105 | 65014 | default | - | Inherited from peer group IPv4-UNDERLAY-PEERS | Inherited from peer group IPv4-UNDERLAY-PEERS | - | - |
| 172.17.33.113 | 65014 | default | - | Inherited from peer group IPv4-UNDERLAY-PEERS | Inherited from peer group IPv4-UNDERLAY-PEERS | - | - |

### Router BGP Device Configuration

```eos
!
router bgp 64701
   router-id 10.4.32.10
   no bgp default ipv4-unicast
   distance bgp 20 200 200
   graceful-restart restart-time 300
   graceful-restart
   maximum-paths 4 ecmp 4
   neighbor IPv4-UNDERLAY-PEERS peer group
   neighbor IPv4-UNDERLAY-PEERS password 7 AQQvKeimxJu+uGQ/yYvv9w==
   neighbor IPv4-UNDERLAY-PEERS send-community
   neighbor IPv4-UNDERLAY-PEERS maximum-routes 12000
   neighbor 172.16.32.18 peer group IPv4-UNDERLAY-PEERS
   neighbor 172.16.32.18 remote-as 64501
   neighbor 172.16.32.18 description SUPER-SPINE1_Ethernet5/1
   neighbor 172.16.32.82 peer group IPv4-UNDERLAY-PEERS
   neighbor 172.16.32.82 remote-as 64502
   neighbor 172.16.32.82 description SUPER-SPINE2_Ethernet5/1
   neighbor 172.16.32.146 peer group IPv4-UNDERLAY-PEERS
   neighbor 172.16.32.146 remote-as 64503
   neighbor 172.16.32.146 description SUPER-SPINE3_Ethernet5/1
   neighbor 172.16.32.210 peer group IPv4-UNDERLAY-PEERS
   neighbor 172.16.32.210 remote-as 64504
   neighbor 172.16.32.210 description SUPER-SPINE4_Ethernet5/2
   neighbor 172.17.32.153 peer group IPv4-UNDERLAY-PEERS
   neighbor 172.17.32.153 remote-as 65001
   neighbor 172.17.32.153 description DC1-POD2-LEAF1A_Ethernet29/1
   neighbor 172.17.32.161 peer group IPv4-UNDERLAY-PEERS
   neighbor 172.17.32.161 remote-as 65001
   neighbor 172.17.32.161 description DC1-POD2-LEAF1B_Ethernet29/1
   neighbor 172.17.32.169 peer group IPv4-UNDERLAY-PEERS
   neighbor 172.17.32.169 remote-as 65002
   neighbor 172.17.32.169 description DC1-POD2-LEAF2A_Ethernet29/1
   neighbor 172.17.32.177 peer group IPv4-UNDERLAY-PEERS
   neighbor 172.17.32.177 remote-as 65002
   neighbor 172.17.32.177 description DC1-POD2-LEAF2B_Ethernet29/1
   neighbor 172.17.32.185 peer group IPv4-UNDERLAY-PEERS
   neighbor 172.17.32.185 remote-as 65003
   neighbor 172.17.32.185 description DC1-POD2-LEAF3A_Ethernet29/1
   neighbor 172.17.32.193 peer group IPv4-UNDERLAY-PEERS
   neighbor 172.17.32.193 remote-as 65003
   neighbor 172.17.32.193 description DC1-POD2-LEAF3B_Ethernet29/1
   neighbor 172.17.32.201 peer group IPv4-UNDERLAY-PEERS
   neighbor 172.17.32.201 remote-as 65004
   neighbor 172.17.32.201 description DC1-POD2-LEAF4A_Ethernet29/1
   neighbor 172.17.32.209 peer group IPv4-UNDERLAY-PEERS
   neighbor 172.17.32.209 remote-as 65004
   neighbor 172.17.32.209 description DC1-POD2-LEAF4B_Ethernet29/1
   neighbor 172.17.32.217 peer group IPv4-UNDERLAY-PEERS
   neighbor 172.17.32.217 remote-as 65005
   neighbor 172.17.32.217 description DC1-POD2-LEAF5A_Ethernet29/1
   neighbor 172.17.32.225 peer group IPv4-UNDERLAY-PEERS
   neighbor 172.17.32.225 remote-as 65005
   neighbor 172.17.32.225 description DC1-POD2-LEAF5B_Ethernet29/1
   neighbor 172.17.32.233 peer group IPv4-UNDERLAY-PEERS
   neighbor 172.17.32.233 remote-as 65006
   neighbor 172.17.32.233 description DC1-POD2-LEAF6A_Ethernet29/1
   neighbor 172.17.32.241 peer group IPv4-UNDERLAY-PEERS
   neighbor 172.17.32.241 remote-as 65006
   neighbor 172.17.32.241 description DC1-POD2-LEAF6B_Ethernet29/1
   neighbor 172.17.32.249 peer group IPv4-UNDERLAY-PEERS
   neighbor 172.17.32.249 remote-as 65007
   neighbor 172.17.32.249 description DC1-POD2-LEAF7A_Ethernet29/1
   neighbor 172.17.33.1 peer group IPv4-UNDERLAY-PEERS
   neighbor 172.17.33.1 remote-as 65007
   neighbor 172.17.33.1 description DC1-POD2-LEAF7B_Ethernet29/1
   neighbor 172.17.33.9 peer group IPv4-UNDERLAY-PEERS
   neighbor 172.17.33.9 remote-as 65008
   neighbor 172.17.33.9 description DC1-POD2-LEAF8A_Ethernet29/1
   neighbor 172.17.33.17 peer group IPv4-UNDERLAY-PEERS
   neighbor 172.17.33.17 remote-as 65008
   neighbor 172.17.33.17 description DC1-POD2-LEAF8B_Ethernet29/1
   neighbor 172.17.33.25 peer group IPv4-UNDERLAY-PEERS
   neighbor 172.17.33.25 remote-as 65009
   neighbor 172.17.33.25 description DC1-POD2-LEAF9A_Ethernet29/1
   neighbor 172.17.33.33 peer group IPv4-UNDERLAY-PEERS
   neighbor 172.17.33.33 remote-as 65009
   neighbor 172.17.33.33 description DC1-POD2-LEAF9B_Ethernet29/1
   neighbor 172.17.33.41 peer group IPv4-UNDERLAY-PEERS
   neighbor 172.17.33.41 remote-as 65010
   neighbor 172.17.33.41 description DC1-POD2-LEAF10A_Ethernet29/1
   neighbor 172.17.33.49 peer group IPv4-UNDERLAY-PEERS
   neighbor 172.17.33.49 remote-as 65010
   neighbor 172.17.33.49 description DC1-POD2-LEAF10B_Ethernet29/1
   neighbor 172.17.33.57 peer group IPv4-UNDERLAY-PEERS
   neighbor 172.17.33.57 remote-as 65011
   neighbor 172.17.33.57 description DC1-POD2-LEAF11A_Ethernet29/1
   neighbor 172.17.33.65 peer group IPv4-UNDERLAY-PEERS
   neighbor 172.17.33.65 remote-as 65011
   neighbor 172.17.33.65 description DC1-POD2-LEAF11B_Ethernet29/1
   neighbor 172.17.33.73 peer group IPv4-UNDERLAY-PEERS
   neighbor 172.17.33.73 remote-as 65012
   neighbor 172.17.33.73 description DC1-POD2-LEAF12A_Ethernet29/1
   neighbor 172.17.33.81 peer group IPv4-UNDERLAY-PEERS
   neighbor 172.17.33.81 remote-as 65012
   neighbor 172.17.33.81 description DC1-POD2-LEAF12B_Ethernet29/1
   neighbor 172.17.33.89 peer group IPv4-UNDERLAY-PEERS
   neighbor 172.17.33.89 remote-as 65013
   neighbor 172.17.33.89 description DC1-POD2-LEAF13A_Ethernet29/1
   neighbor 172.17.33.97 peer group IPv4-UNDERLAY-PEERS
   neighbor 172.17.33.97 remote-as 65013
   neighbor 172.17.33.97 description DC1-POD2-LEAF13B_Ethernet29/1
   neighbor 172.17.33.105 peer group IPv4-UNDERLAY-PEERS
   neighbor 172.17.33.105 remote-as 65014
   neighbor 172.17.33.105 description DC1-POD2-LEAF14A_Ethernet29/1
   neighbor 172.17.33.113 peer group IPv4-UNDERLAY-PEERS
   neighbor 172.17.33.113 remote-as 65014
   neighbor 172.17.33.113 description DC1-POD2-LEAF14B_Ethernet29/1
   redistribute connected route-map RM-CONN-2-BGP
   !
   address-family ipv4
      neighbor IPv4-UNDERLAY-PEERS activate
```

# Multicast

# Filters

## Prefix-lists

### Prefix-lists Summary

#### PL-LOOPBACKS-EVPN-OVERLAY

| Sequence | Action |
| -------- | ------ |
| 10 | permit 10.4.32.0/24 eq 32 |

### Prefix-lists Device Configuration

```eos
!
ip prefix-list PL-LOOPBACKS-EVPN-OVERLAY
   seq 10 permit 10.4.32.0/24 eq 32
```

## Route-maps

### Route-maps Summary

#### RM-CONN-2-BGP

| Sequence | Type | Match and/or Set |
| -------- | ---- | ---------------- |
| 10 | permit | match ip address prefix-list PL-LOOPBACKS-EVPN-OVERLAY |

### Route-maps Device Configuration

```eos
!
route-map RM-CONN-2-BGP permit 10
   match ip address prefix-list PL-LOOPBACKS-EVPN-OVERLAY
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
