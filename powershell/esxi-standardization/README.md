# PowerShell ESXi Standardizer

This is a modular PowerShell script designed to **automate and standardize VMware ESXi host configurations** within a vCenter environment.  
It uses a **JSON configuration file** to apply both **global** and **regional** settings across multiple ESXi hosts — ensuring consistency, efficiency, and compliance for IT operations.

---

## 🚀 Features

- 🔧 **DNS & NTP Configuration**: Set via regional configuration
- 🌐 **Networking Policies**: Manage vSwitch, MTU, uplinks, and vMotion
- 📄 **Syslog & Core Dump Setup**: Configure logging and diagnostics
- 🔒 **IPv6 & Security Hardening**: disabling of IPv6 and hardening security policies
- ⚙️ **Advanced Settings**: Apply shell timeouts, hyperthreading options, scratch partition setup
- 🧠 **AI-Enhanced Scripting**: Script logic assisted and refined using ChatGPT

---

## 📦 Requirements

- [VMware PowerCLI](https://developer.vmware.com/powercli) installed
- Administrative privileges on target ESXi host(s) and vCenter
- A valid JSON file with environment-specific configuration values

---
## 📥 Installation

1. Install PowerCLI:
   ```powershell
   Install-Module -Name VMware.PowerCLI -Scope CurrentUser

2. Clone this repository:
git clone https://github.com/najafi-ali/virtualization-scripts.git

3. Prepare your JSON configuration file with global and regional settings.

---

🛠️ Functions Overview

🔹 Main Function

#### `Set-ESXi-StandardConfiguration`
The main function that connects to the specified vCenter server and applies configuration settings to an ESXi host. It coordinates each of the individual configuration functions listed below.

**Parameters:**
- `-vcenter` : Specifies the vCenter server to connect to.
- `-globalconfig` : Path to the global configuration JSON file.
- `-clustername` : Name of the cluster where the ESXi host is located.
- `-hostname` : Name of the ESXi host to apply settings to.

### Global Configuration Functions

These functions handle various global settings on the ESXi host.

- **`Set-ESXi-GlobalConfiguration`**: Applies global settings to the ESXi host.
- **`Set-ESXi-AdvancedSetting`**: Applies advanced settings like shell timeouts and hyperthreading options.
- **`Set-ESXi-CoredumpConfiguration`**: Configures the core dump location and settings.
- **`Set-ESXi-PortGroupActiveUplink`**: Configures the active NIC for a specified port group (e.g., vMotion or NFS).
- **`Set-ESXi-vSwitchPolicy`**: Manages vSwitch policies, such as teaming and security policies.
- **`Disable-ESXi-IPv6Networking`**: Disables IPv6 if specified in the configuration.
- **`Set-ESXi-ScratchPartition`**: Sets the scratch partition configuration on local storage.
- **`Set-ESXi-vSwitchMTU`**: Adjusts the MTU setting for a specified vSwitch.
- **`Get-ESXi-vSwitchActiveUplink`**: Retrieves the status of active uplinks on a specified vSwitch.

### Regional Configuration Functions

These functions are specific to regional settings, typically sourced from the JSON configuration.

- **`Set-ESXi-RegionalConfiguration`**: Applies region-specific settings based on JSON configuration.
- **`Set-ESXi-DNSConfiguration`**: Configures DNS settings for the ESXi host.
- **`Set-ESXi-NTPConfiguration`**: Sets NTP configurations based on regional time servers.
- **`Set-ESXi-SyslogConfiguration`**: Configures syslog server details for logging.
- **`Test-ESXi-SyslogConfiguration`**: Ensures syslog configurations are valid and applied.

### Utility Functions

These functions support the main configuration tasks by providing utilities for file handling, messaging, and configuration data processing.

- **`Join-ESXi-HostToDomain`**: Joins an ESXi host to a domain.
- **`Restart-ESXi-Host`**: Restarts the ESXi host after applying critical settings.
- **`Get-ESXi-HostinMaintenanceMode`**: Checks and manages the maintenance mode status of an ESXi host.
- **`New-ESXi-LogFileHandler`**: Initializes a log file for tracking script execution.
- **`Show-Message`**: Displays messages during the script execution.
- **`Get-ESXi-LocalVMFSDatastore`**: Retrieves local VMFS datastores.
- **`Get-ESXi-RegionFromHostname`**: Determines the region based on host FQDN.
- **`Get-ESXi-GlobalConfigurationFilePath`**: Retrieves the global configuration file path.
- **`Convert-ESXi-GlobalConfigurationKey`**: Converts global configuration keys to match the ESXi host format.

### Maintenance and Domain Management Functions

- **`Set-ESXi-HostToDomain`**: Joins an ESXi host to a domain.
- **`Restart-ESXi-Host`**: Restarts the ESXi host after applying critical settings.
- **`Get-ESXi-HostinMaintenanceMode`**: Checks and manages the maintenance mode status of an ESXi host.


📋 Example Usage

Apply global settings to all hosts in a specific cluster
Set-ESXi-StandardConfiguration -vcenter "vcenter.example.com" `
                               -clustername "ProdCluster" `
                               -globalconfig "C:\config\global.json"

Apply settings to a specific ESXi host
Set-ESXi-StandardConfiguration -vcenter "vcenter.example.com" `
                               -hostname "ESXiHost01" `
                               -globalconfig "C:\config\global.json"

📎 Notes
Script assumes PowerCLI session authentication; use Connect-VIServer if not already connected.
JSON configuration file must be structured according to expected keys (example file included).

