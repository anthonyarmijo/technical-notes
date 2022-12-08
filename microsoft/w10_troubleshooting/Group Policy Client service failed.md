#rdp #remoteprocedurecall #gpo_client #sign_in

![[07December2022_1670437600 (2).png]]
## Symptoms
- Cannot RDP into machine

## What Works
* PowerShell remoting (PSSession)
* gpupdate /force

## Other Discoveries
- `sfc /scannow` discovers some issues but fails to repair