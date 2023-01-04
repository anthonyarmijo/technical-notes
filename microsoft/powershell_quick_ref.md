
# Check Software

```powershell
# wmiobject method
Get-WmiObject -Class Win32_Product

# get apps from specific vendor
Get-WmiObject -Class Win32_Product | where vendor -eq Microsoft | Select Name, Version

# Registry Method
$InstalledSoftware = Get-ChildItem "**HKLM**:\Software\Microsoft\Windows\CurrentVersion\Uninstall"
foreach($obj in $InstalledSoftware){write-host $obj.GetValue('DisplayName') -NoNewline; write-host " - " -NoNewline; write-host $obj.GetValue('DisplayVersion')}

# Above uses HKLM location. For apps installed in user registry, try below:
$InstalledSoftware = Get-ChildItem "**HKCU**:\Software\Microsoft\Windows\CurrentVersion\Uninstall"  
foreach($obj in $InstalledSoftware){write-host $obj.GetValue('DisplayName') -NoNewline; write-host " - " -NoNewline; write-host $obj.GetValue('DisplayVersion')}
```