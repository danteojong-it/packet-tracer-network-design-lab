# 2. Switch Configuration

This section covers VLAN creation, port assignment, and trunk configuration on the Cisco 2960 Switch.

## 🎯 Configuration Objectives

- Create three VLANs (HR, Sales, Wireless)
- Assign ports to respective VLANs
- Configure trunk port for router communication
- Secure unused ports

## 📋 VLAN Planning

| VLAN ID | Name | Ports | Purpose |
|---------|------|-------|---------|
| 10 | HR | Fa0/1-3 | HR Department PCs |
| 20 | Sales | Fa0/4-6 | Sales Department PCs |
| 30 | Wireless | Fa0/7 | Wireless Router |
| N/A | Trunk | Gig0/1 | To Main Router |

## 🖥️ Accessing Switch CLI

1. Click on the **Switch (2960)** in your workspace
2. Select the **CLI** tab
3. If prompted for initial configuration dialog, type **no** and press Enter
4. Press Enter again to see the **Switch>** prompt

## 🔧 Configuration Commands

### Block 1: Create VLANs

Enable privileged mode and enter configuration terminal:

```
enable
configure terminal
vlan 10
name HR
vlan 20
name Sales
vlan 30
name Wireless
exit
```

**Expected Output:**
```
Switch(config-vlan)# name Wireless
Switch(config-vlan)# exit
Switch(config)#
```

![Switch VLAN Configuration](../assets/switch-config-log.png)

### Block 2: Assign HR Ports to VLAN 10

Configure ports Fa0/1 through Fa0/3 as access ports on VLAN 10:

```
interface range fa0/1 - 3
switchport mode access
switchport access vlan 10
exit
```

**What This Does:**
- `interface range fa0/1 - 3` = Select ports 1, 2, and 3
- `switchport mode access` = Set as access ports (not trunk)
- `switchport access vlan 10` = Assign to VLAN 10 (HR)

### Block 3: Assign Sales Ports to VLAN 20

Configure ports Fa0/4 through Fa0/6 as access ports on VLAN 20:

```
interface range fa0/4 - 6
switchport mode access
switchport access vlan 20
exit
```

### Block 4: Assign Wireless Router Port to VLAN 30

Configure port Fa0/7 for the wireless router:

```
interface fa0/7
switchport mode access
switchport access vlan 30
exit
```

### Block 5: Configure Trunk Port to Router

The connection to the main router must be a **trunk port** to carry all three VLANs:

```
interface gig0/1
switchport mode trunk
exit
```

**Why Trunk?**
- Access ports can only belong to ONE VLAN
- Trunk ports carry traffic for MULTIPLE VLANs
- Router-on-a-Stick configuration requires trunk to router

### Block 6: Disable Unused Ports (Security)

Disable ports Fa0/8 through Fa0/24 and Gig0/2 for security:

```
interface range fa0/8 - 24 , gig0/2
shutdown
exit
```

**Why Disable Unused Ports?**
- Prevents unauthorized device connections
- Reduces security vulnerabilities
- Standard network hardening practice

### Block 7: Save Configuration

Exit configuration mode and save:

```
exit
write memory
```

**Alternative save command:**
```
exit
copy running-config startup-config
```

## 📊 Configuration Summary

### Complete CLI Output

Here's what your switch configuration log should show:

```
Switch> enable
Switch# configure terminal
Switch(config)# vlan 10
Switch(config-vlan)# name HR
Switch(config-vlan)# vlan 20
Switch(config-vlan)# name Sales
Switch(config-vlan)# vlan 30
Switch(config-vlan)# name Wireless
Switch(config-vlan)# exit
Switch(config)# interface range fa0/1 - 3
Switch(config-if-range)# switchport mode access
Switch(config-if-range)# switchport access vlan 10
Switch(config-if-range)# exit
Switch(config)# interface range fa0/4 - 6
Switch(config-if-range)# switchport mode access
Switch(config-if-range)# switchport access vlan 20
Switch(config-if-range)# exit
Switch(config)# interface fa0/7
Switch(config-if)# switchport mode access
Switch(config-if)# switchport access vlan 30
Switch(config-if)# exit
Switch(config)# interface gig0/1
Switch(config-if)# switchport mode trunk
Switch(config-if)# exit
Switch(config)# interface range fa0/8 - 24 , gig0/2
Switch(config-if-range)# shutdown
Switch(config-if-range)# exit
Switch(config)# exit
Switch# write memory
```

## 🔍 Verification Commands

### View All Configured VLANs

```
show vlan brief
```

Expected output:
```
VLAN Name                             Status    Ports
---- -------------------------------- --------- -------------------------------
1    default                          active    Fa0/8,Fa0/9,Fa0/10,Fa0/11,
10   HR                               active    Fa0/1,Fa0/2,Fa0/3
20   Sales                            active    Fa0/4,Fa0/5,Fa0/6
30   Wireless                         active    Fa0/7
```

### View Specific Interface Configuration

```
show interface fa0/1 switchport
show interface gig0/1 switchport
```

### View All Interface Status

```
show interface status
```

## ✅ Verification Checklist

After configuration, verify:

- [ ] VLAN 10 created with name "HR"
- [ ] VLAN 20 created with name "Sales"
- [ ] VLAN 30 created with name "Wireless"
- [ ] Ports Fa0/1-3 assigned to VLAN 10
- [ ] Ports Fa0/4-6 assigned to VLAN 20
- [ ] Port Fa0/7 assigned to VLAN 30
- [ ] Port Gig0/1 configured as trunk
- [ ] Ports Fa0/8-24 and Gig0/2 shutdown
- [ ] Configuration saved with `write memory`

## 🔴 Common Configuration Errors

### Error: "VLAN does not exist"
- Ensure VLAN is created with `vlan <number>` before assigning ports

### Error: "Port already belongs to a VLAN"
- Ports can only be in one VLAN; remove from previous VLAN first
- Use `no switchport access vlan` to remove

### Port Not Accepting Assignment
- Verify the port number (e.g., Fa0/1 not Fa0/01)
- Check port is not already in a native VLAN

### Trunk Configuration Fails
- Ensure both sides support 802.1Q (modern Cisco equipment does)
- Verify physical connection exists before configuration

## 📝 Notes

- VLANs separate network traffic and improve security
- Trunk ports can handle multiple VLANs with 802.1Q tagging
- Unused port shutdown is a basic security hardening measure
- Configuration is automatically saved during this lab setup

## 🔗 Port References (For Your Records)

**HR Department (VLAN 10):**
```
Fa0/1 = HR PC 1
Fa0/2 = HR PC 2
Fa0/3 = HR PC 3
```

**Sales Department (VLAN 20):**
```
Fa0/4 = Sales PC 1
Fa0/5 = Sales PC 2
Fa0/6 = Sales PC 3
```

**Special Ports:**
```
Fa0/7 = Wireless Router (VLAN 30)
Gig0/1 = Trunk to Main Router
```

---

**Next Step:** Proceed to [03-router-configuration.md](03-router-configuration.md) to configure inter-VLAN routing and DHCP.