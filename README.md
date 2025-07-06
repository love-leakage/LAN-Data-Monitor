# LAN-Data-Monitor
Here’s how to set a static IP address on your PC, based on your operating system:


---

🖥️ 1. On Windows 10 / 11

✅ Steps:

1. Open Network Settings

Press Windows + R, type ncpa.cpl, press Enter.

OR: Go to Control Panel → Network and Sharing Center → Change adapter settings.



2. Right-click your LAN connection (e.g., “Ethernet”) → Click Properties.


3. Scroll and select Internet Protocol Version 4 (TCP/IPv4) → Click Properties.


4. Choose:
✅ Use the following IP address:

IP address: 192.168.1.101 (or any unique address)

Subnet mask: 255.255.255.0

Default gateway: 192.168.1.1 (usually your router)



5. Set DNS servers:

Preferred DNS: 8.8.8.8

Alternate DNS: 8.8.4.4



6. Click OK → OK → Close.


7. Test it:

Open Command Prompt, type:

ipconfig

Make sure the IP is what you set.





---

🐧 2. On Linux (Ubuntu/Debian)

Option 1: GUI (for Ubuntu Desktop)

1. Go to Settings → Network.


2. Click ⚙️ next to your wired connection.


3. Go to IPv4 tab.


4. Set Method to: Manual.


5. Add:

Address: 192.168.1.101

Netmask: 255.255.255.0

Gateway: 192.168.1.1

DNS: 8.8.8.8



6. Save and reconnect.




---

Option 2: Terminal (for headless/CLI setup)

Edit Netplan config:

sudo nano /etc/netplan/01-netcfg.yaml

Example config:

network:
  version: 2
  ethernets:
    eth0:
      dhcp4: no
      addresses:
        - 192.168.1.101/24
      gateway4: 192.168.1.1
      nameservers:
        addresses: [8.8.8.8, 8.8.4.4]

Then apply:

sudo netplan apply

Check:

ip addr


---

🔁 Optional: Reserve IP via Router (DHCP Reservation)

Login to your router (192.168.1.1)

Find DHCP → Address Reservation

Bind each PC's MAC address to a fixed IP

This way, IP is always same even if PC is set to DHCP



---

⚠️ Important Tips:

Don’t assign the same IP to multiple PCs.

Make sure the IP is outside your router’s DHCP range, or reserve it in router.

Always keep the gateway set correctly (your router IP).