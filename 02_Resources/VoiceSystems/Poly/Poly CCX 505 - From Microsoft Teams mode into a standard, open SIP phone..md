
To register it directly to a Session Border Controller (SBC) or standard SIP server, you need to change the phone’s **Base Profile** from `Teams` to `Generic` (which Poly uses to denote open SIP / UC Software mode).

## Method 1: Change via the Phone UI

If you have physical access to the device and know the local admin password, this is the quickest method:

1. On the phone screen, open the menu and go to **Settings** > **Advanced**.
    
2. Enter the administrator password (the factory default is **`456`**, unless your provisioning server or Teams admin center changed it).
    
3. Select **Administration Settings** > **Network Configuration** > **Base Profile**.
    
4. Change the setting from `Teams` (or `Lync`) to **`Generic`**.
    
5. Save the configuration and exit. The phone will automatically reboot.
    

## Method 2: Change via the Web User Interface (Web UI)

If you prefer managing the device over the network, you can switch it using a web browser:

1. **Find the IP address:** Go to **Settings** > **Device Settings** > **About** (or check your network DHCP leases) to find the phone's local IPv4 address.
    
2. **Enable Web UI (if disabled):** By default on newer Teams firmware, the web interface might be disabled. If you can't reach it, go to **Settings** > **Device Settings** > **Admin Only** > **Network Configuration** on the phone, and toggle **Web User Interface** to **Enabled**.
    
3. Open a browser on the same network and navigate to `https://<Phone-IP-Address>`.
    
4. Log in as **`admin`** with your admin password (default: `456`).
    
5. Navigate to the **Simple Setup** menu tab at the top.
    
6. Locate the **Base Profile** dropdown, switch it to **`Generic`**, and click **Save** at the bottom of the page. The phone will restart.
    

## Method 3: Provisioning via Poly Lens or Central Server

If you are deploying multiple phones, you can push this change globally from your central provisioning environment or the **Poly Lens** cloud portal:

- **In Poly Lens:** Navigate to the device policy or device group settings, find the **Provider** / **Base Profile** field under general settings, and change it to **Generic** (or standard OpenSIP).
    
- **Via configuration files (`.cfg`):** If using an FTP/HTTP provisioning server, you can set the parameter:
    
    XML
    
    ```
    device.baseProfile="Generic"
    ```
    
    Once the phone checks in and pulls the new file, it will switch profiles and reboot.
    

### What to Expect Post-Reboot

Once the CCX 505 boots back up in `Generic` mode, the Microsoft Teams interface will be entirely replaced by Poly's native OpenSIP interface. You will then be able to log into the Web UI to explicitly configure your SIP signaling lines, registration server addresses, transport protocols (TLS/UDP/TCP), and authentication credentials required by your SBC.

_Note: If the phone is still enrolled in a corporate Microsoft Endpoint Manager / Intune environment, ensure you remove or exclude the device profile there so it doesn't try to automatically re-provision or force itself back into Teams mode over time._