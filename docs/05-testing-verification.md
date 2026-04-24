# 5. Testing and Network Verification

This section covers comprehensive network connectivity testing using ping commands and DHCP verification.

## 🎯 Testing Objectives

- Verify DHCP IP assignment on all PCs
- Test connectivity within the same VLAN
- Test inter-VLAN routing (different departments)
- Test wireless device connectivity
- Verify internet access via cloud device

## 📋 Pre-Testing Checklist

Before running tests, ensure all prior configuration is complete:

- [ ] Switch VLANs created and ports assigned
- [ ] Router subinterfaces configured for all VLANs
- [ ] DHCP pools configured on router
- [ ] Wireless router connected and SSID is "OfficeNet"
- [ ] Both laptops have Wi-Fi modules and are connected
- [ ] All devices show green connection indicators

## 🔍 DHCP Verification

### Step 1: Configure PCs for DHCP

Each PC must be set to obtain IP automatically:

For each of the 6 PCs and 2 Laptops:

1. **Click on the PC or Laptop**
2. Go to the **Desktop** tab
3. Click **IP Configuration** (network settings icon)
4. You should see IP settings dialog

5. Look for the toggle switch or radio button
   - Current state: **Static** (manual IP)
   - Desired state: **DHCP** (automatic)

6. **Change from Static to DHCP**
7. Wait 3-5 seconds for the configuration to process
8. Watch for message: **"DHCP request successful"**
9. An IP address should now be displayed (e.g., 192.168.10.2)

**Record the IP addresses:**

| Device | Expected VLAN | Expected Range | Actual IP |
|--------|--------------|-----------------|-----------|
| HR PC 1 | 10 | 192.168.10.2-254 | __________ |
| HR PC 2 | 10 | 192.168.10.2-254 | __________ |
| HR PC 3 | 10 | 192.168.10.2-254 | __________ |
| Sales PC 1 | 20 | 192.168.20.2-254 | __________ |
| Sales PC 2 | 20 | 192.168.20.2-254 | __________ |
| Sales PC 3 | 20 | 192.168.20.2-254 | __________ |
| Laptop 0 | 30 | 192.168.30.2-254 | __________ |
| Laptop 1 | 30 | 192.168.30.2-254 | __________ |

### DHCP Success Indicators

✅ **Good Signs:**
- "DHCP request successful" message
- IP address shows in valid range for VLAN
- Repeating the test gets same IP (static lease)

❌ **Problem Signs:**
- "DHCP request failed" message
- No IP address displayed
- IP shows 0.0.0.0 (failed assignment)

### Common DHCP Issues

| Issue | Likely Cause | Solution |
|-------|--------------|----------|
| All PCs getting 0.0.0.0 | Router DHCP not configured | Verify router config in section 3 |
| PCs in wrong VLAN range | Port assignment incorrect | Check switch VLAN assignment |
| Some PCs get IP, others don't | Port shutdown on switch | Check disabled ports list |
| Laptops can't get IP | Not on WIRELESS_POOL | Verify wireless router on VLAN 30 |

## 🔌 Connection Verification Commands

### How to Open Command Prompt

1. Click on any **PC or Laptop**
2. Go to the **Desktop** tab
3. Click the **Command Prompt** icon (black box/terminal)
4. A terminal window will open

### Command Format

All connectivity tests use the **ping** command:

```
ping <destination_ip_address>
```

Press **Enter** after typing each command.

## 🧪 Test Scenarios

### Test 1: Same VLAN Connectivity (HR to HR)

**Purpose:** Verify devices on the same VLAN can communicate

**From:** HR PC 1
**To:** HR PC 2

1. Open Command Prompt on **HR PC 1**
2. Note the IP address of **HR PC 2** (e.g., 192.168.10.3)
3. Type: `ping 192.168.10.3` (use actual IP)
4. Press Enter

**Expected Output:**
```
Pinging 192.168.10.3 with 32 bytes of data:
Reply from 192.168.10.3: bytes=32 time=1ms TTL=128
Reply from 192.168.10.3: bytes=32 time=1ms TTL=128
Reply from 192.168.10.3: bytes=32 time=1ms TTL=128
Reply from 192.168.10.3: bytes=32 time=1ms TTL=128

Ping statistics for 192.168.10.3:
    Packets sent = 4
    Packets received = 4
    % packet loss = 0%
    Minimum = 1ms, Maximum = 1ms, Average = 1ms
```

✅ **Success:** All 4 replies received, 0% packet loss

### Test 2: Gateway/Router Connectivity

**Purpose:** Verify devices can reach their VLAN's gateway (router)

**From:** HR PC 1
**To:** HR Gateway

1. Open Command Prompt on **HR PC 1**
2. Type: `ping 192.168.10.1` (HR gateway)
3. Press Enter

**Expected Output:**
All 4 pings successful, 0% packet loss

**Why This Matters:**
- Confirms router subinterface is active
- Confirms switch trunk is working
- Confirms VLAN tagging is correct

### Test 3: Inter-VLAN Routing (HR to Sales)

**Purpose:** Verify router can route traffic between VLANs

**From:** HR PC 1 (VLAN 10)
**To:** Sales PC 1 (VLAN 20)

1. Open Command Prompt on **HR PC 1**
2. Note the IP of **Sales PC 1** (e.g., 192.168.20.2)
3. Type: `ping 192.168.20.2` (use actual Sales PC IP)
4. Press Enter

**Expected Output:**

⚠️ **NOTE:** In Packet Tracer, the first ping may timeout (this is normal):

```
Pinging 192.168.20.2 with 32 bytes of data:
Request timed out.                          ← First ping may fail
Reply from 192.168.20.2: bytes=32 time=2ms TTL=127
Reply from 192.168.20.2: bytes=32 time=2ms TTL=127
Reply from 192.168.20.2: bytes=32 time=2ms TTL=127
```

✅ **Success:** 3 out of 4 replies (first timeout is normal due to ARP resolution)

**If You Run Ping Again:**
```
Pinging 192.168.20.2 with 32 bytes of data:
Reply from 192.168.20.2: bytes=32 time=1ms TTL=127
Reply from 192.168.20.2: bytes=32 time=1ms TTL=127
Reply from 192.168.20.2: bytes=32 time=1ms TTL=127
Reply from 192.168.20.2: bytes=32 time=1ms TTL=127
```

✅ **Success:** All 4 replies on second attempt

**What This Proves:**
- Router-on-a-Stick configuration is working
- Switch trunk port is functional
- VLAN 10 and VLAN 20 can communicate via router

### Test 4: Wireless to Wired (Laptop to PC)

**Purpose:** Verify wireless devices can reach wired network

**From:** Laptop 0 (Wireless)
**To:** HR PC 1 (VLAN 10)

1. Open Command Prompt on **Laptop 0**
2. Note the IP of **HR PC 1** (e.g., 192.168.10.2)
3. Type: `ping 192.168.10.2` (use actual HR PC 1 IP)
4. Press Enter

**Expected Output:**
Similar to Test 3 - first ping may timeout, subsequent replies successful

✅ **Success:** At least 3 replies received

**What This Proves:**
- Wireless router DHCP is working
- Wireless devices can reach VLAN 30
- Router can route from VLAN 30 to VLAN 10

### Test 5: Reverse Wireless Test (Wired to Wireless)

**Purpose:** Verify wired devices can reach wireless network

**From:** HR PC 1 (VLAN 10)
**To:** Laptop 0 (VLAN 30)

1. Open Command Prompt on **HR PC 1**
2. Note the IP of **Laptop 0** (e.g., 192.168.30.2)
3. Type: `ping 192.168.30.2` (use actual Laptop 0 IP)
4. Press Enter

**Expected Output:**
Same as other inter-VLAN tests

✅ **Success:** At least 3 replies received (first may timeout)

### Test 6: Opposite Department (Sales to HR)

**Purpose:** Verify inter-VLAN routing works in all directions

**From:** Sales PC 1 (VLAN 20)
**To:** HR PC 1 (VLAN 10)

1. Open Command Prompt on **Sales PC 1**
2. Note the IP of **HR PC 1** (e.g., 192.168.10.2)
3. Type: `ping 192.168.10.2` (use actual IP)
4. Press Enter

**Expected Output:**
At least 3 replies successful

✅ **Success:** Departments can communicate bidirectionally

## 📊 Comprehensive Test Summary

| Test # | From | To | Type | Expected Result |
|--------|------|-----|------|-----------------|
| 1 | HR PC 1 | HR PC 2 | Same VLAN | 4/4 replies |
| 2 | HR PC 1 | Router (192.168.10.1) | Gateway | 4/4 replies |
| 3 | HR PC 1 | Sales PC 1 | Inter-VLAN | 3-4/4 replies |
| 4 | Laptop 0 | HR PC 1 | Wireless→Wired | 3-4/4 replies |
| 5 | HR PC 1 | Laptop 0 | Wired→Wireless | 3-4/4 replies |
| 6 | Sales PC 1 | HR PC 1 | Reverse VLAN | 3-4/4 replies |

## ✅ Final Verification Checklist

After completing all tests:

- [ ] All 8 devices received valid DHCP IPs
- [ ] IPs are in correct ranges for their VLANs
- [ ] Same-VLAN ping (Test 1) successful (4/4)
- [ ] Gateway ping (Test 2) successful (4/4)
- [ ] Inter-VLAN ping (Test 3) successful (3-4/4)
- [ ] Wireless-to-wired ping (Test 4) successful (3-4/4)
- [ ] Wired-to-wireless ping (Test 5) successful (3-4/4)
- [ ] Opposite department ping (Test 6) successful (3-4/4)

## 🎓 What These Tests Prove

✅ **DHCP Configuration:**
- DHCP server is running on router
- Clients can request and receive IPs
- DHCP is VLAN-aware (each VLAN gets correct range)

✅ **Switch Configuration:**
- Ports are correctly assigned to VLANs
- Trunk port properly carries all VLAN traffic
- Port security is working (unused ports disabled)

✅ **Router Configuration:**
- Subinterfaces are active and routing traffic
- 802.1Q tagging is working correctly
- Inter-VLAN routing is functional

✅ **Wireless Configuration:**
- Wireless router received IP from DHCP
- Wireless clients can connect to network
- Wireless traffic is routed correctly to other VLANs

✅ **Overall Network:**
- Network segmentation by VLAN is working
- Security grouping (HR vs Sales) is effective
- Wireless integration is seamless

## 🔴 Troubleshooting Failed Pings

### All Pings Fail (0% success)

**Possible Causes:**
- DHCP not working (device has no valid IP)
- Physical cable disconnected (red indicator)
- Switch or router not configured
- VLAN ports not assigned correctly

**Solution:**
- Verify DHCP IPs are assigned (check IP Configuration)
- Check all connection indicators are green
- Review switch and router configurations in previous sections
- Verify port assignments match cable connections

### Inter-VLAN Pings Fail (Test 3-6 fail)

**Possible Causes:**
- Router subinterfaces not configured
- Trunk port not enabled on switch
- 802.1Q encapsulation not set on router
- Excluded address range incorrect

**Solution:**
- Verify all three subinterfaces exist on router
- Check trunk port configuration on switch
- Confirm dot1Q encapsulation on all subinterfaces
- Verify gateway IPs are in excluded-address list

### Wireless Pings Fail

**Possible Causes:**
- Wireless router not connected to switch
- Wireless router didn't get IP from DHCP
- Laptop Wi-Fi module not installed
- VLAN 30 not configured on switch or router

**Solution:**
- Verify wireless router has green connection to switch port Fa0/7
- Check wireless router IP using GUI
- Verify laptop has WPC300N module (not Ethernet)
- Confirm VLAN 30 exists on switch and router

## 📝 Lab Completion Notes

After successful testing:

1. **Save your Packet Tracer file** - All configuration is now complete
2. **Document your results** - Record successful ping tests
3. **Note timing** - Some pings may take longer on first attempt
4. **Analyze performance** - Observe latency differences between same-VLAN and inter-VLAN

## 🎉 Success Indicators

If you can successfully:
- ✅ Ping between devices in same VLAN
- ✅ Ping between devices in different VLANs
- ✅ Ping from wireless devices to wired devices
- ✅ Ping from wired devices to wireless devices

**Then your network is fully configured and operational!**

---

**Lab Complete!** You have successfully designed and implemented a multi-VLAN network with inter-VLAN routing, DHCP, and wireless connectivity.
