# Troubleshooting

This document records issues encountered while configuring and validating the Enterprise Network Mega Lab.

Each entry documents the observed problem, troubleshooting process, root cause, resolution, and final verification.

---

## Issue 1 — OSPF Neighbor Adjacency

### Symptom

Failed connectivity tests between Office A and Office B PCs within the same VLAN.
Failed connectivity tests between Office PCs and Internet.

### Investigation
<ol>
  <li>I first investigated all cabling (Layer 1). </li>
  <li>I then confirmed that all interface and spanning tree statuses were correctly configured on all relevant network devices (Layer 2).</li>
  <li>Continued into investigating routing tables of relevant Layer 3 network devices, which is where I found that some devices were not sharing routers with one another. Specifically the Distribution and Access layer switches. </li>
  <li>I further investigated common causes of OSPF neighbors not sharing routes such as duplicate router ids, different OSPF areas, and OSPF timer settings that do not match.</li>
</ol>

```text
show ip interface status
show ip interface brief
show spanning-tree
show ip route
show ip ospf 
show ip ospf neighbors
```

### Root Cause

In order to speed up the process of my initial OSPF configurations, I copy and pasted some of my first devices configuration into the other Layer 3 device configurations. This caused redundant router-IDs in the network which stopped the Distribution and Access layer switches from learning OSPF routes.

### Resolution

I listed and document the intended and unique router-IDs for each Layer 3 device in the OSPF topology and configured them manually to ensure no redundant router-IDs were left present in the network.

### Verification

I confirmed the issue was resolved by checking for OSPF configuration, routing tables, and OSPF neighbor adjacencies. This was followed by connectivity tests on end host office PCs.

```text
show ip ospf
show ip ospf neighbor
show ip route
[ping tests on end hosts]
```

---

## Issue 2 — NTP Authentication

### Symptom

Times on access layer switches were not syncing to the NTP Server. However, Distribution layer switches NTP was operating correctly.

### Investigation

<ol>
  <li>I first confirmed that all physical connections (Layer 1) and interfaces statuses (Layer 2) towards the NTP server from the Access layer switches were active and connected properly.</li>
  <li>I knew that NTP was operating correctly on the NTP server because the Distribution layer switches were associating to it. However, I still investigated the NTP servers configuration to ensure authentication settings for the Access layer switches. </li>
  <li>Next, I investigated the NTP configurations on the Access layer switches, specifically looking for common issues that block NTP associations such as an incorrect server IP or authentication misconfigs.</li>
</ol>

```text
show ip int status
show ntp status
show ntp associations
show running-config
```

### Root Cause

The configurations of the Access layer switches revealed that the 'ntp server [ip address] key [key number]' command was not configured, rather the 'ntp server [ip address]' command was. This resulted in the Access layer switches attempting to associate to the NTP server without authenticating with its trusted key to the server while the server required authentication. 

### Resolution

I got rid of the old NTP server configuration and configured the Access layer switches with the correct NTP server command as follows:
```text
no ntp server 10.0.0.76
ntp server 10.0.0.76 key 1
```

### Verification

I confirmed the issue was resolved by checking the ntp status, associations, and configurations after configuration of my resolution.

```text
show ntp status
show ntp associations
show running-config
```
---
