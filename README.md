# Design and Implement a VLSM Addressing Scheme (Cisco Packet Tracer)

[cite_start]This project demonstrates the ability to design and implement a complex **Variable Length Subnet Mask (VLSM)** addressing scheme[cite: 1]. [cite_start]The objective was to optimize a single network address (**10.1.1.0/24**) to meet the specific host requirements of a multi-departmental network while ensuring zero wasted address space between contiguous subnets[cite: 15, 23].

## Environments and Technologies Used

* [cite_start]**Cisco Packet Tracer** (Network Simulation) [cite: 1]
* [cite_start]**Cisco IOS CLI** (Interface Configuration & Verification) [cite: 5]
* [cite_start]**VLSM Subnetting** (Address space optimization) [cite: 4]
* [cite_start]**Network Troubleshooting** (Connectivity verification via ICMP) [cite: 9]

## Objectives and Scenario

[cite_start]The customer required an addressing design for a topology consisting of four LANs and one point-to-point WAN link[cite: 11, 12]. [cite_start]The design had to prioritize efficiency by using the smallest possible subnets that still accommodate the necessary host counts[cite: 24].

### Host Requirements:
* [cite_start]**PS-115 LAN**: 47 Addresses [cite: 19, 20]
* [cite_start]**PD-2 LAN**: 28 Addresses [cite: 18]
* [cite_start]**PD-1 LAN**: 11 Addresses [cite: 18]
* [cite_start]**PS-101 LAN**: 5 Addresses [cite: 18]
* [cite_start]**WAN Link**: 2 Addresses [cite: 26]

---

## High-Level Deployment and Configuration Steps

### Step 1: Design the VLSM Addressing Scheme
[cite_start]To maintain a contiguous network with no unused space, I calculated the subnets in descending order of size[cite: 22, 23]. 
* [cite_start]**Calculation Logic**: For each LAN, I identified the next power of two to determine the subnet mask (e.g., $2^6=64$ for the 47-host requirement)[cite: 26].
* [cite_start]**Efficiency**: I utilized a **/30** prefix for the point-to-point link between routers to provide the most efficient subnetting possible[cite: 24].

### Step 2: Documentation and IP Allocation
[cite_start]I documented the design in a comprehensive table, assigning specific roles to IP addresses as required by the customer[cite: 21, 25]:
* [cite_start]**Police Router**: Assigned the first usable IP for all interfaces[cite: 29].
* [cite_start]**Schools Router**: Assigned the first usable IP for LANs and the **last usable** IP for the WAN link[cite: 30, 31].
* [cite_start]**Switches**: Assigned the second usable IP to the VLAN 1 management interface[cite: 32].
* [cite_start]**Hosts**: Assigned the last usable IP in the subnet[cite: 34].

### Step 3: CLI Implementation
[cite_start]I accessed the Cisco IOS command-line interface to apply the addressing scheme[cite: 5, 7]:
* [cite_start]Configured IP addresses and subnet masks for all physical and virtual interfaces[cite: 2].
* Enabled interfaces using the `no shutdown` command.
* [cite_start]Configured Default Gateways on all switches and end devices to ensure cross-subnet reachability[cite: 33].

### Step 4: Verification and Testing
[cite_start]I performed end-to-end connectivity tests to ensure the network was fully operational[cite: 8]. 
* [cite_start]Verified that all hosts could reach their respective default gateways[cite: 35].
* [cite_start]Confirmed switch management interfaces were reachable from hosts on different LANs[cite: 33].

---

## VLSM Design Table

| Subnet Description | Hosts Needed | CIDR | Subnet Address | Usable Range | Broadcast |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **PS-115 LAN** | 47 | /26 | 10.1.1.0 | 10.1.1.1 - 10.1.1.62 | 10.1.1.63 |
| **PD-2 LAN** | 28 | /27 | 10.1.1.64 | 10.1.1.65 - 10.1.1.94 | 10.1.1.95 |
| **PD-1 LAN** | 11 | /28 | 10.1.1.96 | 10.1.1.97 - 10.1.1.110 | 10.1.1.111 |
| **PS-101 LAN** | 5 | /29 | 10.1.1.112 | 10.1.1.113 - 10.1.1.118 | 10.1.1.119 |
| **WAN Link** | 2 | /30 | 10.1.1.120 | 10.1.1.121 - 10.1.1.122 | 10.1.1.123 |

---

## Deployment and Configuration Screenshots

*(Upload your screenshots to GitHub and link them here)*
* **Topology Overview**: `![Network Topology](link_to_image)`
* **CLI Verification**: `![Show IP Interface Brief](link_to_image)`
* **Connectivity Test**: `![Ping Success](link_to_image)`
