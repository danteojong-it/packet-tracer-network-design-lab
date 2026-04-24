# Packet Tracer Network Design Lab

A comprehensive guide to designing and configuring a multi-VLAN network with inter-VLAN routing, DHCP, and wireless connectivity using Cisco Packet Tracer.

## 📋 Project Overview

This lab demonstrates enterprise network design principles by creating a segmented network for an organization with multiple departments (HR and Sales) plus wireless connectivity. The network uses VLANs for traffic separation, router-on-a-stick for inter-VLAN communication, and DHCP for automatic IP assignment.

### Network Topology
![Network Topology](assets/network-topology.png)

## 🎯 Learning Objectives

- Design a multi-VLAN network architecture
- Configure Cisco switches with VLANs and port assignments
- Implement inter-VLAN routing using router subinterfaces
- Configure DHCP pools for automatic IP assignment
- Set up secure wireless networks with WPA2 encryption
- Test network connectivity using ping verification

## 📊 Network Design

### IP Addressing & Subnetting Plan

| VLAN | Department | Network | Gateway | DHCP Pool |
|------|-----------|---------|---------|-----------|
| 10 | HR | 192.168.10.0/24 | 192.168.10.1 | 192.168.10.2 - 254 |
| 20 | Sales | 192.168.20.0/24 | 192.168.20.1 | 192.168.20.2 - 254 |
| 30 | Wireless | 192.168.30.0/24 | 192.168.30.1 | 192.168.30.2 - 254 |

### Hardware Requirements

- **1x Router** (Cisco 2911 or 1941)
- **1x Switch** (Cisco 2960)
- **1x Wireless Router** (WRT300N)
- **6x PCs** (3 for HR, 3 for Sales)
- **2x Laptops** (for wireless network)
- **1x Cloud Device** (simulates internet)

### Cable Connections

| Connection | Port 1 | Port 2 | Cable Type |
|-----------|--------|--------|-----------|
| HR PC 1 → Switch | PC Eth | Switch Fa0/1 | Copper Straight-Through |
| HR PC 2 → Switch | PC Eth | Switch Fa0/2 | Copper Straight-Through |
| HR PC 3 → Switch | PC Eth | Switch Fa0/3 | Copper Straight-Through |
| Sales PC 1 → Switch | PC Eth | Switch Fa0/4 | Copper Straight-Through |
| Sales PC 2 → Switch | PC Eth | Switch Fa0/5 | Copper Straight-Through |
| Sales PC 3 → Switch | PC Eth | Switch Fa0/6 | Copper Straight-Through |
| Wireless Router → Switch | WAN | Switch Fa0/7 | Copper Straight-Through |
| Switch → Router | Gig0/1 | Gig0/0 | Copper Straight-Through |
| Router → Cloud | Gig0/1 | Ethernet | Copper Straight-Through |

## 📚 Documentation

Complete step-by-step guides are organized in the following documents:

1. **[Network Design & Device Placement](docs/01-network-design.md)** - Hardware setup and physical connections
2. **[Switch Configuration](docs/02-switch-configuration.md)** - VLAN creation and port assignment
3. **[Router Configuration](docs/03-router-configuration.md)** - Inter-VLAN routing and DHCP setup
4. **[Wireless Setup](docs/04-wireless-setup.md)** - Wireless network configuration and security
5. **[Testing & Verification](docs/05-testing-verification.md)** - Ping tests and connectivity validation

## 🚀 Quick Start

### Prerequisites
- Cisco Packet Tracer installed (version 8.0 or later)
- Basic understanding of networking concepts

### Setup Steps

1. **Design the Network** → Follow [01-network-design.md](docs/01-network-design.md)
2. **Configure Switch** → Follow [02-switch-configuration.md](docs/02-switch-configuration.md)
3. **Configure Router** → Follow [03-router-configuration.md](docs/03-router-configuration.md)
4. **Setup Wireless** → Follow [04-wireless-setup.md](docs/04-wireless-setup.md)
5. **Test Network** → Follow [05-testing-verification.md](docs/05-testing-verification.md)

## 🔍 Key Concepts

### VLANs (Virtual LANs)
- Separate network traffic by department
- VLAN 10 for HR, VLAN 20 for Sales, VLAN 30 for Wireless
- Reduces broadcast domain size and improves security

### Router-on-a-Stick
- Single physical interface connected to switch trunk
- Multiple subinterfaces (.10, .20, .30) for VLAN routing
- Uses 802.1Q encapsulation for VLAN tagging

### DHCP (Dynamic Host Configuration Protocol)
- Automatic IP address assignment to clients
- Gateway and network parameters distributed automatically
- Reduces manual configuration errors

### Wireless Security
- SSID: **OfficeNet** (hidden or broadcast)
- Security Mode: **WPA2 Personal**
- Passphrase: **Office123**

## 📸 Configuration Snapshots

### Switch Configuration Log
![Switch Config](assets/switch-config-log.png)

### Router Configuration Log
![Router Config](assets/router-config-log.png)

### Device Connections
![Device Connections](assets/device-connections.png)

## ✅ Expected Results

### DHCP Assignment
- HR PCs receive IPs in range 192.168.10.2 - 192.168.10.254
- Sales PCs receive IPs in range 192.168.20.2 - 192.168.20.254
- Wireless devices receive IPs in range 192.168.30.2 - 192.168.30.254

### Connectivity Tests
- ✅ HR PC can ping router gateway (192.168.10.1)
- ✅ HR PC can ping Sales PC (inter-VLAN routing works)
- ✅ HR PC can ping wireless laptop (VLAN 30)
- ✅ Wireless laptops connected to OfficeNet SSID
- ✅ All devices can reach simulated internet (Cloud)

## 🛠️ Troubleshooting

### PCs Not Getting DHCP IPs
- Check if router DHCP pools are configured correctly
- Verify PCs have DHCP enabled (not Static)
- Ensure switch ports are assigned to correct VLANs

### Inter-VLAN Ping Fails
- Verify router subinterfaces are configured for all VLANs
- Check trunk port on switch is configured correctly
- Ensure 802.1Q encapsulation is applied to all subinterfaces

### Wireless Devices Won't Connect
- Confirm SSID is set to "OfficeNet"
- Verify WPA2 security and passphrase "Office123"
- Check wireless router has IP from DHCP pool (VLAN 30)

## 📖 Additional Resources

- [Cisco Packet Tracer Documentation](https://www.netacad.com/courses/packet-tracer)
- [VLAN Configuration Guide](https://www.cisco.com/c/en/us/support/docs/switches/catalystexpress-500g-12p-switch/47937-vlan-configure.html)
- [Router Subinterface Configuration](https://www.cisco.com/c/en/us/support/docs/switches/catalyst-6000-series-switches/23948-171.html)

## 📝 Lab Notes & Observations

- Document any configuration changes or troubleshooting steps
- Record ping test results and timing
- Note any timeout patterns (typically first ping times out in Packet Tracer)

## 👤 Author

**danteojong-it**

## 📄 License

This project is open source and available under the MIT License.

---

**Last Updated:** April 24, 2026
