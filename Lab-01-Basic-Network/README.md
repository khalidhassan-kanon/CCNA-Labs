
# Lab-01: Basic Network Connectivity

## Objective

Build a simple Local Area Network (LAN) using two PCs and one switch, then verify connectivity using ICMP ping.

## Network Topology

PC1 ---- Switch ---- PC2

### Devices Used

| Device      | Quantity |
| ----------- | -------- |
| PC          | 2        |
| Switch 2960 | 1        |

## IP Addressing

| Device | IP Address   | Subnet Mask   |
| ------ | ------------ | ------------- |
| PC1    | 192.168.1.10 | 255.255.255.0 |
| PC2    | 192.168.1.20 | 255.255.255.0 |

## Configuration Steps

### Step 1

Connect both PCs to the switch using Copper Straight-Through cables.

### Step 2

Configure IP addresses on both PCs.

### Step 3

Verify connectivity using the ping command.

Command executed from PC1:

ping 192.168.1.20

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

Insert topology screenshot here.

### Successful Ping

Insert ping screenshot here.

### ARP Table

<img width="305" height="274" alt="image" src="https://github.com/user-attachments/assets/b486db78-3402-4429-a54f-6e7d0e51d3a3" />


## Concepts Learned

* LAN communication
* IPv4 addressing
* MAC addresses
* ARP
* ICMP
* Layer 2 switching

## Troubleshooting

Issue:
Incorrect IP address configuration prevented communication.

Resolution:
Verified IP settings and corrected the addressing scheme.

## Conclusion

Successfully created a basic LAN environment and verified end-to-end connectivity between two hosts through a switch.
