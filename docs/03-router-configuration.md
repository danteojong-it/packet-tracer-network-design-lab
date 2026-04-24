# 3. Router Configuration (Inter-VLAN Routing & DHCP)

This section covers configuring the main router for inter-VLAN routing and DHCP services.

## 📖 Overview

The router will:
1. Enable the physical interface connected to the switch
2. Create virtual subinterfaces for each VLAN (Router-on-a-Stick)
3. Configure IP addresses for each VLAN
4. Set up DHCP pools for automatic IP assignment
5. Enable the uplink to the cloud (internet)

## 🖥️ Accessing the Router CLI

1. **Click on Router0** in your topology
2. Click the **CLI** tab
3. Press **Enter** to get the `Router>` prompt
4. If asked about initial configuration, type **no**

## ⚙️ Router Configuration Steps

### Block 1: Enable Physical Interface

```bash
enable
configure terminal
interface gig0/0
no shutdown
exit
```

**What this does:**
- Enters privileged exec mode
- Enters global configuration mode
- Selects the GigabitEthernet0/0 port (connected to switch trunk)
- Enables the interface with `no shutdown`
- Exits interface configuration

### Block 2: Configure VLAN 10 (HR) Subinterface

```bash
interface gig0/0.10
encapsulation dot1Q 10
ip address 192.168.10.1 255.255.255.0
exit
```

**What this does:**
- Creates virtual subinterface gig0/0.10
- Configures 802.1Q VLAN tagging for VLAN 10
- Assigns IP address 192.168.10.1/24 (the gateway)
- This subinterface routes traffic for VLAN 10

### Block 3: Configure VLAN 20 (Sales) Subinterface

```bash
interface gig0/0.20
encapsulation dot1Q 20
ip address 192.168.20.1 255.255.255.0
exit
```

### Block 4: Configure VLAN 30 (Wireless) Subinterface

```bash
interface gig0/0.30
encapsulation dot1Q 30
ip address 192.168.30.1 255.255.255.0
exit
```

### Block 5: Exclude Gateway IPs from DHCP

```bash
ip dhcp excluded-address 192.168.10.1
ip dhcp excluded-address 192.168.20.1
ip dhcp excluded-address 192.168.30.1
```

### Block 6: Create HR DHCP Pool

```bash
ip dhcp pool HR_POOL
network 192.168.10.0 255.255.255.0
default-router 192.168.10.1
exit
```

### Block 7: Create Sales DHCP Pool

```bash
ip dhcp pool SALES_POOL
network 192.168.20.0 255.255.255.0
default-router 192.168.20.1
exit
```

### Block 8: Create Wireless DHCP Pool

```bash
ip dhcp pool WIRELESS_POOL
network 192.168.30.0 255.255.255.0
default-router 192.168.30.1
exit
```

### Block 9: Enable Internet Uplink

```bash
interface gig0/1
no shutdown
exit
```

### Block 10: Save Configuration

```bash
exit
write memory
```

## 📋 Verification Commands

### Check Subinterface Status

```bash
show ip interface brief
```

### Check DHCP Pools

```bash
show ip dhcp pool
```

### Check DHCP Bindings

```bash
show ip dhcp binding
```

## ✅ Configuration Checkpoint

Verify these items before moving forward:

- [ ] Physical interface Gig0/0 is enabled
- [ ] Subinterface Gig0/0.10 created with IP 192.168.10.1/24
- [ ] Subinterface Gig0/0.20 created with IP 192.168.20.1/24
- [ ] Subinterface Gig0/0.30 created with IP 192.168.30.1/24
- [ ] Gateway IPs excluded from DHCP pools
- [ ] HR_POOL created for network 192.168.10.0/24
- [ ] SALES_POOL created for network 192.168.20.0/24
- [ ] WIRELESS_POOL created for network 192.168.30.0/24
- [ ] Interface Gig0/1 (to Cloud) is enabled
- [ ] Configuration saved with `write memory`
- [ ] `show ip interface brief` shows all subinterfaces up

---

**Next Step:** Proceed to [04-wireless-setup.md](04-wireless-setup.md) to configure the wireless router.