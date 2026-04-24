# 1. Network Design and Device Placement

This section covers the physical hardware setup and initial cable connections in Packet Tracer.

## 📦 Hardware Setup

### Adding Devices to Workspace

Follow these steps to add each device to your Packet Tracer workspace:

1. **Open Device Selection Panel** (left sidebar)
2. **Select Routers** category → Drag **2911** or **1941** router to workspace
3. **Select Switches** category → Drag **2960** switch to workspace
4. **Select Wireless Devices** → Drag **WRT300N** wireless router to workspace
5. **Select End Devices** → Drag **6 PCs** and **2 Laptops** to workspace
6. **Select Cloud** → Drag **PT-Cloud** to workspace

### Device Placement Guide

Arrange your devices for clarity:

```
                    [Cloud]
                       |
    [Laptop0] [Laptop1]
         \    /
      [Wireless Router]
           |
      [Main Router]
           |
         [Switch]
        /  |  \
     HR   Sales Wireless
    PCs    PCs
```

## 🔌 Cable Connections

### Cable Types

In Packet Tracer, different cable types are represented by different visual patterns:

| # | Cable Type | Appearance | Used For |
|---|-----------|-----------|----------|
| 1 | Auto-Connect | Orange lightning bolt | Auto-detection (not recommended) |
| 2 | Console | Light blue curved line | Device management/configuration |
| **3** | **Copper Straight-Through** | **Solid black line** | **Most network connections** |
| 4 | Copper Cross-Over | Dashed black line | Legacy switch-to-switch/PC-to-PC |

**For this lab, use the Copper Straight-Through cable (solid black line) for all connections.**

### Step-by-Step Connection Process

#### Step 1: Select the Cable
1. Click the **copper straight-through cable** (solid black line) from the available cables
2. Your cursor will change to indicate cable selection mode

#### Step 2: Connect to First Device
1. Click the PC or device
2. A menu will pop up showing available ports
3. Select **FastEthernet0** (or Ethernet0 for laptops)

#### Step 3: Connect to Second Device
1. Click the destination device (Switch or Router)
2. Select the appropriate port from the menu
3. The connection is now complete

**Note:** Connections initially appear orange and will turn green within 30 seconds, indicating an active link.

## 📋 Connection Map

### PC-to-Switch Connections

Connect PCs to the Switch using copper straight-through cables:

| Device | Origination Port | Destination Port | VLAN | Department |
|--------|-----------------|-----------------|------|-----------|
| HR PC 1 | FastEthernet0 | Fa0/1 | 10 | HR |
| HR PC 2 | FastEthernet0 | Fa0/2 | 10 | HR |
| HR PC 3 | FastEthernet0 | Fa0/3 | 10 | HR |
| Sales PC 1 | FastEthernet0 | Fa0/4 | 20 | Sales |
| Sales PC 2 | FastEthernet0 | Fa0/5 | 20 | Sales |
| Sales PC 3 | FastEthernet0 | Fa0/6 | 20 | Sales |

**Recommended Organization:**
- Connect HR PCs to ports **Fa0/1 through Fa0/3**
- Connect Sales PCs to ports **Fa0/4 through Fa0/6**

This sequential port assignment makes CLI configuration much easier using the "interface range" command.

### Core Infrastructure Connections

| Source | Source Port | Destination | Dest Port | Purpose |
|--------|------------|-------------|-----------|---------|
| Switch | Gig0/1 | Main Router | Gig0/0 | Trunk link for VLANs |
| Wireless Router | Internet/WAN port | Switch | Fa0/7 | Wireless VLAN access |
| Main Router | Gig0/1 | Cloud | Ethernet0 | Internet simulation |

### Wireless Connections

- **Laptop 0** → Wireless Router (via Wi-Fi after configuration)
- **Laptop 1** → Wireless Router (via Wi-Fi after configuration)

These connections are established after wireless router configuration, not physical cables.

## 🖼️ Reference Diagram

See the network topology image for complete physical layout:

![Network Topology](../assets/network-topology.png)

## ✅ Verification Checklist

After physical connections are complete:

- [ ] All 6 PCs have green connection indicators to Switch
- [ ] Wireless Router has green connection to Switch port Fa0/7
- [ ] Main Router has green connection to Switch on Gig0/1
- [ ] Main Router's second Gig port (Gig0/1) connects to Cloud
- [ ] All cables are copper straight-through (solid black lines)
- [ ] Connection circles are green (not orange)

## 📍 Port Reference for Configuration

**Save this port mapping for later CLI configuration:**

```
HR Department (VLAN 10):
  - HR PC 1 → Switch Fa0/1
  - HR PC 2 → Switch Fa0/2
  - HR PC 3 → Switch Fa0/3

Sales Department (VLAN 20):
  - Sales PC 1 → Switch Fa0/4
  - Sales PC 2 → Switch Fa0/5
  - Sales PC 3 → Switch Fa0/6

Infrastructure:
  - Wireless Router → Switch Fa0/7 (VLAN 30)
  - Switch Gig0/1 → Router Gig0/0 (Trunk)
  - Router Gig0/1 → Cloud (Internet)
```

## 🔄 Link Status Monitoring

In Packet Tracer, monitor connection status:

- **Green circle** = Active link (good!)
- **Orange circle** = Link initializing (wait 30 seconds)
- **Red X** = Connection failed (check port selection)
- **No indicator** = Port not connected

## ⚡ Troubleshooting Connection Issues

### Connection Appears Red/Failed
- Right-click the connection and delete it
- Verify you selected the correct cable type (copper straight-through)
- Reconnect ensuring both devices accept the port selection

### Cables Turn Orange and Stay Orange
- This shouldn't happen in Packet Tracer; typically turns green in ~30 seconds
- If stuck, delete the connection and retry

### Can't Find the Copper Cable
- In the cable selection menu, verify you're using the copper straight-through option
- Look for the **solid black line**, not dashed

## 📝 Notes

- Order of connection doesn't matter
- You can reconnect devices at any time in Packet Tracer
- Save your topology frequently during this stage
- Physical connections are prerequisites for all configuration steps

---

**Next Step:** Proceed to [02-switch-configuration.md](02-switch-configuration.md) to configure VLANs and ports on the Switch.
