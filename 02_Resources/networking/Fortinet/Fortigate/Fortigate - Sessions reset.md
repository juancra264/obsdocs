Managing sessions on a FortiGate firewall is a powerful way to troubleshoot traffic, identify misbehaving hosts, or clear stuck connections. This process is performed entirely through the Command Line Interface (CLI).

### Step 1: Filter Sessions

To focus on a specific subset of traffic (like a single source IP or a specific destination port), you use the `diagnose sys session filter` command. This creates a virtual "view" for subsequent commands.

1. **Enter the CLI.**
    
2. **Apply filters:** You can combine multiple filters. For example, to filter traffic coming from `192.168.1.50`:
    
    Bash
    
    ```
    diagnose sys session filter src 192.168.1.50
    ```
    
3. **Add more criteria (optional):** To narrow it down to traffic going to port 80:
    
    Bash
    
    ```
    diagnose sys session filter dport 80
    ```
    
4. **Verify your filter:** Before acting on the sessions, ensure your filter is correct:
    
    Bash
    
    ```
    diagnose sys session filter list
    ```
    

### Step 2: View the Filtered Sessions

Once the filter is set, you can view the sessions that match your criteria to ensure you are targeting the correct traffic.

- **List matching sessions:**
    
    Bash
    
    ```
    diagnose sys session list
    ```
    
- **Detailed view:** If you need more technical details (like NAT information or session timeouts), add the `verbose` flag:
    
    Bash
    
    ```
    diagnose sys session list --verbose
    ```
    

### Step 3: Clear/Reset the Filtered Sessions

Once you have verified that the correct sessions are being targeted, you can delete them. This forces the clients to re-establish their connections, which is often used to clear stale states or bypass temporary policy restrictions.

- **Clear the sessions:**
    
    Bash
    
    ```
    diagnose sys session clear
    ```
    
    _Note: This only clears sessions that match the active filters you set in Step 1._
    

### Step 4: Reset the Filter

It is **critical** to clear your filters after you are done. If you leave a filter active, subsequent troubleshooting commands (or even regular monitoring) will only show you the filtered data, which can lead to significant confusion.

- **Reset filters to default (all):**
    
    Bash
    
    ```
    diagnose sys session filter clear
    ```
    

### Summary Checklist

|**Goal**|**Command**|
|---|---|
|**Set Filter**|`diagnose sys session filter <parameter> <value>`|
|**Review Filter**|`diagnose sys session filter list`|
|**View Sessions**|`diagnose sys session list`|
|**Delete Sessions**|`diagnose sys session clear`|
|**Reset Filters**|`diagnose sys session filter clear`|

> **Warning:** Be very careful when running `diagnose sys session clear`. If you forget to set or verify your filters, you will inadvertently drop _all_ sessions passing through the firewall, which will cause a temporary service disruption for all users. Always run `filter list` before executing the `clear` command.