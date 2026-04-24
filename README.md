# Packet Tracer Network Design Lab

A comprehensive guide to designing and configuring a multi-VLAN network with inter-VLAN routing, DHCP, and wireless connectivity using Cisco Packet Tracer.

## 📋 Project Overview

This lab demonstrates enterprise network design principles by creating a segmented network for an organization with multiple departments (HR and Sales) plus wireless connectivity. The network uses VLANs for traffic separation, router-on-a-stick for inter-VLAN communication, and DHCP for automatic IP assignment.

### Network Topology
<img width="800" alt="Network Topology Screenshot" src="https://github.com/user-attachments/assets/545aaf7f-6e8f-4e81-a02b-0adb66ea4f2d"/>

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

### Setup Steps

1. **Design the Network** → Follow [01-network-design.md](docs/01-network-design.md)
2. **Configure Switch** → Follow [02-switch-configuration.md](docs/02-switch-configuration.md)
3. **Configure Router** → Follow [03-router-configuration.md](docs/03-router-configuration.md)
4. **Setup Wireless** → Follow [04-wireless-setup.md](docs/04-wireless-setup.md)
5. **Test Network** → Follow [05-testing-verification.md](docs/05-testing-verification.md)
