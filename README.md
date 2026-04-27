# Design and Implement a VLSM Addressing Scheme (Cisco Packet Tracer)
 <img width="690" height="267" alt="image" src="https://github.com/user-attachments/assets/7b02c7d9-27c1-4c7f-b05e-7bf3c1fd18b2" />
 
## Project Overview
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
* Regional Router Verification: Performed CLI checks on both the Police and Schools routers to confirm that all LAN and WAN interfaces were 'up/up' with correct VLSM IP assignments.
* Routing Table Integrity: Confirmed that the routers established a successful routing adjacency (EIGRP), allowing traffic to flow across the point-to-point WAN link.

---

## VLSM Design Table

<img width="730" height="381" alt="image" src="https://github.com/user-attachments/assets/f040c450-899d-429c-aab4-7f61d61d84d3" />


---

## Deployment and Configuration Screenshots

* **Topology Overview**:
<img width="690" height="267" alt="image" src="https://github.com/user-attachments/assets/7b02c7d9-27c1-4c7f-b05e-7bf3c1fd18b2" />

--
* **Police Router CLI Verification**:
<img width="641" height="466" alt="image" src="https://github.com/user-attachments/assets/2ad1cf4d-97d7-4d01-b58e-fb010f2eabc7" />

--
* **Schools Router CLI Verification**:
<img width="643" height="465" alt="image" src="https://github.com/user-attachments/assets/c5a4028a-16f1-446d-83ce-a0833b34d803" />

--
 * **Layer 3 Routing Verification (Traceroute)**: 
I used the `tracert` command to map the path taken by packets across the network. This confirms that traffic is correctly exiting the local gateway, traversing the point-to-point WAN link, and reaching the destination subnet as intended by the VLSM design.
<img width="430" height="360" alt="image" src="https://github.com/user-attachments/assets/15180fe9-181b-4211-b53a-5186fc26b6b5" />

--
* **Connectivity Test**:
I performed ICMP echo requests (pings) between end-devices in geographically separated LANs. The successful 0% loss rate confirms that the VLSM subnets are correctly defined, interfaces are active, and the EIGRP routing protocol is properly distributing routes across the WAN.
<img width="452" height="367" alt="image" src="https://github.com/user-attachments/assets/f93f764b-c7ef-47ff-9506-62450d99a09b" />



