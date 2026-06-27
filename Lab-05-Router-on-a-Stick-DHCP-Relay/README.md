<img width="476" height="163" alt="show interfaces trunk" src="https://github.com/user-attachments/assets/906691c1-3258-4a15-a592-741cf6cd405b" />
# Lab-05: Inter-VLAN Routing with Router-on-a-Stick and Centralized DHCP Server

## Objective

Build a multi-VLAN enterprise network using a Cisco Layer 2 switch, a router configured with Router-on-a-Stick (ROAS), and a centralized DHCP server. Configure VLAN segmentation, IEEE 802.1Q trunking, inter-VLAN routing, and DHCP relay (`ip helper-address`) to automatically assign IP addresses to clients in different VLANs.

---

## Topology

<img width="1385" height="690" alt="topolgy" src="https://github.com/user-attachments/assets/a9828b95-db9c-454b-b962-e202ed7fe984" />


Example:

```text
                 DHCP Server
                  10.0.0.2
                      |
               G0/0/1 | 10.0.0.1
                +-----------+
                |  Router   |
                +-----------+
               G0/0/0 (Trunk)
                      |
               Fa0/13 (Trunk)
                +-----------+
                | 2950 L2   |
                |  Switch   |
                +-----------+
      VLAN10   VLAN20   VLAN30   VLAN40
      Fa0/1-3  Fa0/4-6  Fa0/7-9  Fa0/10-12
```

---

## Devices Used

| Device | Model         | Quantity |
| ------ | ------------- | -------- |
| Router | Cisco ISR     | 1        |
| Switch | Cisco 2950-24 | 1        |
| Server | Server-PT     | 1        |
| PC     | PC-PT         | 12       |

---

## VLAN Information

| VLAN ID | Department | Switch Ports    |
| ------- | ---------- | --------------- |
| 10      | Sales      | Fa0/1 - Fa0/3   |
| 20      | Marketing  | Fa0/4 - Fa0/6   |
| 30      | Finance    | Fa0/7 - Fa0/9   |
| 40      | IT         | Fa0/10 - Fa0/12 |

---

## IP Addressing

| Device      | Interface     | IP Address             | Subnet Mask   |
| ----------- | ------------- | ---------------------- | ------------- |
| Router      | G0/0/0.10     | 192.168.128.1          | 255.255.252.0 |
| Router      | G0/0/0.20     | 192.168.132.1          | 255.255.252.0 |
| Router      | G0/0/0.30     | 192.168.136.1          | 255.255.252.0 |
| Router      | G0/0/0.40     | 192.168.140.1          | 255.255.252.0 |
| Router      | G0/0/1        | 10.0.0.1               | 255.255.255.0 |
| DHCP Server | FastEthernet0 | 10.0.0.2               | 255.255.255.0 |
| PCs         | DHCP          | Assigned Automatically | Based on VLAN |

---

## Configuration Steps

### Step 1 - Configure VLANs

* Created VLANs 10, 20, 30, and 40.
* Assigned access ports to their respective VLANs.
* Verified VLAN membership using:

```bash
show vlan brief
```

---

### Step 2 - Configure Trunk Port

Configured FastEthernet0/13 as an IEEE 802.1Q trunk connecting the switch to the router.

```bash
interface FastEthernet0/13
 switchport mode trunk
```

Verified using:

```bash
show interfaces trunk
```

---

### Step 3 - Configure Router-on-a-Stick

Created one subinterface per VLAN.

Example:

```bash
interface GigabitEthernet0/0/0.10
 encapsulation dot1Q 10
 ip address 192.168.128.1 255.255.252.0
 ip helper-address 10.0.0.2
```

Repeated for VLANs 20, 30, and 40.

---

### Step 4 - Configure DHCP Server

Configured four DHCP pools:

* VLAN10
* VLAN20
* VLAN30
* VLAN40

Each pool included:

* Default Gateway
* Starting IP Address
* Subnet Mask
* Maximum Number of Users

The server interface was configured with:

```text
IP Address:      10.0.0.2
Subnet Mask:     255.255.255.0
Default Gateway: 10.0.0.1
```

---

### Step 5 - Configure DHCP Relay

Configured the router to forward DHCP broadcasts to the centralized DHCP server.

```bash
ip helper-address 10.0.0.2
```

---

### Step 6 - Verify Connectivity

Configured PCs for DHCP.

Verified:

* IP address assignment
* Default gateway
* Inter-VLAN communication
* Connectivity to the DHCP server

---

## Verification

Commands used:

### Router

```bash
show ip interface brief
```

Verified interface status.

```bash
show running-config
```

Verified Router-on-a-Stick configuration.

```bash
ping 10.0.0.2
```

Verified connectivity to the DHCP server.

---

### Switch

```bash
show vlan brief
```

Verified VLAN assignments.

```bash
show interfaces trunk
```

Verified trunk operation.

---

### PC

```bash
ipconfig
```

Verified DHCP lease.

```bash
ping
```

Verified connectivity.

```bash
arp -a
```

Verified ARP table entries.

---

## Troubleshooting

### Issue Encountered

PCs failed to obtain IP addresses via DHCP.

### Root Cause

The DHCP server's **Default Gateway** was configured incorrectly.

Because the server could not route replies back to remote VLANs, DHCP Offer packets never reached the clients.

### Resolution

Configured the server with the correct default gateway:

```text
Default Gateway: 10.0.0.1
```

After correcting the gateway:

* DHCP leases were successfully assigned.
* Clients received the correct IP configuration.
* Inter-VLAN communication functioned normally.

---

## Validation

* ✅ VLANs created successfully.
* ✅ Access ports assigned correctly.
* ✅ Trunk operational.
* ✅ Router-on-a-Stick configured.
* ✅ DHCP relay functioning.
* ✅ DHCP server reachable.
* ✅ Clients received correct IP addresses.
* ✅ Successful inter-VLAN routing.
* ✅ End-to-end connectivity verified.

---

## Screenshots

### Packet Tracer Topology

<img width="1385" height="690" alt="topolgy" src="https://github.com/user-attachments/assets/95f98f95-0e8b-4994-a112-eceaaa9e0ae2" />


---

### Switch VLAN Configuration

<img width="558" height="199" alt="show vlan brief" src="https://github.com/user-attachments/assets/a2ecfa9d-2678-46c2-aa95-671a2d247ef4" />


---

### Trunk Verification

<img width="476" height="163" alt="show interfaces trunk" src="https://github.com/user-attachments/assets/0dc044d0-683b-417e-9d20-088105a05e90" />

---

### Router Configuration

<img width="542" height="130" alt="show ip interface brief" src="https://github.com/user-attachments/assets/23eeaffc-a09a-409a-9283-4f3e13714980" />


---

### DHCP Server Configuration

<img width="1723" height="177" alt="POOL" src="https://github.com/user-attachments/assets/b9dedf7d-3546-4b54-ad93-cef4dc06b180" />


---

### Successful DHCP Assignment

<img width="1873" height="194" alt="DHCP_IP" src="https://github.com/user-attachments/assets/37bd7944-dbb7-42bc-bd7f-636b09b84b70" />


---

### Successful Ping Test

<img width="438" height="184" alt="ping" src="https://github.com/user-attachments/assets/d8332cd6-6ec2-4cdf-b4cf-d28a76f65f6d" />
---

## Concepts Learned

* VLAN Configuration
* IEEE 802.1Q Trunking
* Router-on-a-Stick (ROAS)
* Layer 2 vs Layer 3 Switching
* DHCP Relay (`ip helper-address`)
* Centralized DHCP Server
* Inter-VLAN Routing
* Default Gateway Configuration
* ICMP Connectivity Testing
* Network Troubleshooting Methodology

---

## Key Takeaways

* A Layer 2 switch forwards traffic within VLANs but does not perform routing.
* Router-on-a-Stick enables communication between multiple VLANs using router subinterfaces.
* DHCP broadcasts cannot cross routers unless DHCP relay (`ip helper-address`) is configured.
* The DHCP server must have the correct default gateway to respond to clients on remote networks.
* Systematic troubleshooting (testing one network segment at a time) helps isolate configuration issues efficiently.

---

## References

* Cisco Packet Tracer
* Cisco CCNA 200-301 Course Notes
* Cisco IOS Command Reference
* IEEE 802.1Q VLAN Standard
