# Ubuntu-Server-on-Raspberry-Pi-Setup-Guide-with-Lightweight-GUI-Installation
This guide will walk you through the steps to install Ubuntu Server on your Raspberry Pi, connect to it remotely via SSH, and optionally install a lightweight desktop environment.

## Prerequisites
- Raspberry Pi board
- MicroSD card (8GB or larger)
- HDMI screen and USB keyboard (for initial setup, optional if configuring headless)
- Stable internet connection

## Installation Steps
1. **Download Ubuntu Server Image**
   - Visit the official Ubuntu website and download the Ubuntu Server image for Raspberry Pi.

2. **Flash Image to SD Card**
   - Use a tool like Etcher to flash the downloaded Ubuntu Server image to your microSD card.

3. **Initial Boot and Configuration**
   - Insert the microSD card into your Raspberry Pi and power it on.
   - Wait for the boot process to complete. During the first boot, a tool called cloud-init will handle configuration. This process typically takes less than 2 minutes.

4. **Connect Remotely via SSH**
   - Determine the Raspberry Pi's IP address on the local network.
     - You can find it on your router's dashboard or by running `hostname -I` on the Raspberry Pi if a hostname is set.
   - Use an SSH client to connect to your Raspberry Pi remotely.
     ```
     ssh <username>@<Raspberry Pi's IP address>
     ```
     Replace `<username>` with your username and `<Raspberry Pi's IP address>` with its IP address.
   
5. **Activate SSH (if not enabled)**
   - If SSH is not already enabled, run the following commands on your Raspberry Pi:
     ```
     sudo systemctl enable ssh
     sudo systemctl start ssh
     ```

6. **Install a Lightweight Desktop Environment (Optional)**
   - If you want a graphical interface, you can install a lightweight desktop environment like Lubuntu.
     ```
     sudo apt update
     sudo apt install lubuntu-desktop
     ```
   - Reboot your Raspberry Pi for the changes to take effect.

## Troubleshooting
- **Network Connection Issues**
  - If you encounter network connection issues after boot, you may need to fix the network configuration file.
    - Open the file `/etc/netplan/50-cloud-init.yaml` using a text editor.
    - Ensure the configuration is correct, then apply changes and reboot.
- **Network Troubleshooting**
  - If your Raspberry Pi is not connecting to the network, try the following:
    1. Check physical connections: Ensure the Ethernet cable or Wi-Fi adapter is properly connected.
    2. Restart networking service: Run `sudo systemctl restart networking`.
    3. Check IP address: Run `ip addr` to verify that the Raspberry Pi has obtained an IP address.
    4. Ping test: Use `ping` command to check connectivity to other devices on the network.
    5. Router settings: Check router settings to ensure there are no restrictions or firewall rules blocking the Raspberry Pi's connection.
- **Fix Wi-Fi Configuration**
  - If your Raspberry Pi is having trouble connecting to Wi-Fi, follow these steps:
    1. Open the network configuration file:
       ```
       sudo nano /etc/netplan/50-cloud-init.yaml
       ```
    2. Edit the file to correct the Wi-Fi configuration. Ensure proper indentation for the .yaml file format.
       ```
       wifis:
         wlan0:
           dhcp4: true
           optional: true
           access-points:
             "home network":
               password: "123456789"
       ```
    3. Save and exit the file with `Ctrl + S` and `Ctrl + X`.
    4. Apply the changes:
       ```
       sudo netplan apply
       ```
    5. Reboot your Raspberry Pi:
       ```
       sudo reboot
       ```
    6. After rebooting, your Raspberry Pi should be connected to the Wi-Fi network.

---

By following these steps, you'll have Ubuntu Server running on your Raspberry Pi, ready to be used for various projects or applications. Enjoy your Raspberry Pi experience!

