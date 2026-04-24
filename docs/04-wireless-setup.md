# 4. Wireless Router Setup

This section covers the configuration of the WRT300N Wireless Router to broadcast the "OfficeNet" SSID and secure it with WPA2, as well as connecting the staff laptops.

## 📖 Overview

The wireless router will:
1. Obtain an IP address automatically from the main router's `WIRELESS_POOL` (VLAN 30).
2. Broadcast a wireless network named **OfficeNet**.
3. Secure the network using **WPA2 Personal** encryption.
4. Provide network access to the staff laptops.

## ⚙️ Wireless Router Configuration (GUI)

### Step 1: Access the Router Settings
1. Click on the **Wireless Router** (WRT300N) in your Packet Tracer workspace.
2. Click on the **GUI** tab at the top of the window.
3. You will land on the **Setup** > **Basic Setup** page.

### Step 2: Internet (WAN) Setup
We need to configure the router to pull its IP address from the main Cisco router.

1. Under the **Internet Setup** section, locate the **Internet Connection Type** dropdown.
2. Change the setting to **Automatic Configuration - DHCP**.
3. Scroll to the very bottom of the page and click **Save Settings**.

### Step 3: Configure the Network Name (SSID)
1. Click the **Wireless** tab from the main menu at the top.
2. You will be on the **Basic Wireless Settings** page.
3. Locate the **Network Name (SSID)** text box.
4. Change the name from "Default" to **OfficeNet** (Note: capitalization matters).
5. Scroll down and click **Save Settings**.

### Step 4: Configure Wireless Security (WPA2)
1. Still under the Wireless tab, click the **Wireless Security** sub-menu link (located right below the main tabs).
2. Locate the **Security Mode** dropdown (it will currently say "Disabled").
3. Change it to **WPA2 Personal**.
4. In the **Passphrase** box that appears, type: **Office123**
5. Scroll down and click **Save Settings**.
6. Close the Wireless Router window.

---

## 💻 Connecting the Staff Laptops

By default, laptops in Packet Tracer have Ethernet ports instead of Wi-Fi cards. We must swap the physical modules before connecting any of them.

### Step 1: Install the Wi-Fi Module
Repeat these steps for **Laptop0** and **Laptop1**:
1. Click on the **Laptop**.
2. Stay on the **Physical** tab.
3. Click the small round **Power Button** on the side of the laptop image to turn it off (the green light will go dark).
4. Drag the existing Ethernet module (the silver rectangle on the side of the laptop) and drop it into the "Modules" list on the left to remove it.
5. Drag the **WPC300N** wireless module from the list and drop it into the empty slot on the laptop.
6. Click the **Power Button** to turn the laptop back on.

### Step 2: Connect to the OfficeNet SSID
Repeat these steps for **Laptop0** and **Laptop1**:
1. Go to the **Desktop** tab.
2. Click on the **PC Wireless** icon.
3. Click the **Connect** tab inside the application.
4. Wait a few seconds for the network to appear. Select **OfficeNet** from the list, then click the **Connect** button below.
5. In the security screen, enter the passphrase: **Office123**
6. Click **Connect**.

---

## ✅ Verification Checkpoint

Verify these items before moving to the final testing phase:
- [ ] Wireless Router Internet Connection Type is set to DHCP.
- [ ] Network SSID is set exactly to "OfficeNet".
- [ ] Security Mode is WPA2 Personal with passphrase "Office123".
- [ ] Both laptops have the WPC300N module installed and are powered on.
- [ ] Both laptops show "Adapter is active" in the PC Wireless app.
- [ ] You can visually see wireless waves connecting the laptops to the router in the Packet Tracer workspace.

**Next Step:** Proceed to [05-testing-verification.md](05-testing-verification.md) to perform end-to-end ping tests across the network.
