# Design and Implement a VLSM Addressing Scheme (Cisco Packet Tracer)

This project demonstrates the ability to design and implement a complex **Variable Length Subnet Mask (VLSM)** addressing scheme. The objective was to optimize a single network address (**10.1.1.0/24**) to meet the specific host requirements of a multi-departmental network while ensuring zero wasted address space between contiguous subnets.

## Environments and Technologies Used

* **Cisco Packet Tracer** (Network Simulation)
* **Cisco IOS CLI** (Interface Configuration & Verification)
* **VLSM Subnetting** (Address space optimization)
* **Network Troubleshooting** (Connectivity verification via ICMP)

## Objectives and Scenario

The customer required an addressing design for a topology consisting of four LANs and one point-to-point WAN link. The design had to prioritize efficiency by using the smallest possible subnets that still accommodate the necessary host counts.

### Host Requirements:
* **PS-115 LAN**: 47 Addresses
* **PD-2 LAN**: 28 Addresses
* **PD-1 LAN**: 11 Addresses
* **PS-101 LAN**: 5 Addresses
* **WAN Link**: 2 Addresses

---

## High-Level Deployment and Configuration Steps

### Step 1: Design the VLSM Addressing Scheme
To maintain a contiguous network with no unused space, I calculated the subnets in descending order of size. 
* **Calculation Logic**: For each LAN, I identified the next power of two to determine the subnet mask (e.g., 2^6 = 64 for the 47-host requirement).
* **Efficiency**: I utilized a **/30** prefix for the point-to-point link between routers to provide the most efficient subnetting possible.

### Step 2: Documentation and IP Allocation
I documented the design in a comprehensive table, assigning specific roles to IP addresses as required by the customer:
* **Police Router**: Assigned the first usable IP for all interfaces.
* **Schools Router**: Assigned the first usable IP for LANs and the **last usable** IP for the WAN link.
* **Switches**: Assigned the second usable IP to the VLAN 1 management interface.
* **Hosts**: Assigned the last usable IP in the subnet.

### Step 3: CLI Implementation
I accessed the Cisco IOS command-line interface to apply the addressing scheme:
* Configured IP addresses and subnet masks for all physical and virtual interfaces.
* Enabled interfaces using the `no shutdown` command.
* Configured Default Gateways on all switches and end devices to ensure cross-subnet reachability.

### Step 4: Verification and Testing
I performed end-to-end connectivity tests to ensure the network was fully operational. 
* Verified that all hosts could reach their respective default gateways.
* Confirmed switch management interfaces were reachable from hosts on different LANs.

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
* **Topology Overview**: <img width="690" height="267" alt="image" src="https://github.com/user-attachments/assets/7b02c7d9-27c1-4c7f-b05e-7bf3c1fd18b2" />

* **CLI Verification**: `![Show IP Interface Brief](link_to_image)`
* **Connectivity Test**: `![Ping Success](link_to_image)`
