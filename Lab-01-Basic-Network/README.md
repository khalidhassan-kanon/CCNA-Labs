# Lab-01: Basic Network Connectivity

## Objective

Build a simple Local Area Network (LAN) using two PCs and one switch, then verify connectivity using ICMP ping.

## Network Topology

PC1 ---- Switch ---- PC2

### Devices Used

| Device      | Quantity |
| ----------- | -------- |
| PC          | 2        |
| Switch 2950 | 1        |

## IP Addressing

| Device | IP Address   | Subnet Mask   |
| ------ | ------------ | ------------- |
| PC1    | 192.168.1.10 | 255.255.255.0 |
| PC2    | 192.168.1.20 | 255.255.255.0 |

## Configuration Steps

### Step 1

Connect both PCs to the switch using Copper Straight-Through cables.

### Step 2

Step 2: Assign static IPv4 addresses and subnet masks to both PCs.

### Step 3

Verify connectivity using the ping command.

Command executed from PC2:

ping 192.168.1.10

### Step 4

Check the ARP table before and after the ping test.

Command:

arp -a

## Verification

* Physical links are up.
* Both hosts can successfully ping each other.
* ARP entries are dynamically learned after communication.

## Screenshots

### Topology

<img width="870" height="278" alt="image" src="https://github.com/user-attachments/assets/3e661861-ec4c-4f17-a621-1d38f43d8f6a" />

### Successful Ping

<img width="697" height="477" alt="image" src="https://github.com/user-attachments/assets/ff02e1e9-eec7-44ed-8dd5-2d1254d3168c" />


### ARP Table
<img width="656" height="141" alt="image" src="https://github.com/user-attachments/assets/05de3be3-efbf-498e-ba32-88ebb648b1b8" />


## Concepts Learned

* LAN communication
* IPv4 addressing
* MAC addresses
* ARP
* ICMP
* Layer 2 switching

## Potential Issues

- Incorrect IP addressing
- Wrong subnet mask
- Faulty cable connection
- Disabled network interface

These issues were not encountered during this lab.

## Validation

- Verified physical connectivity
- Verified IP addressing
- Verified successful ICMP communication
- Verified ARP table population

## Conclusion

Successfully created a basic LAN environment and verified end-to-end connectivity between two hosts through a switch.
