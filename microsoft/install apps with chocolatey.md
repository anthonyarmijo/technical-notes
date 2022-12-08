```powershell 
# Note that 'iex' is an alias of Invoke-Expression
# This downloads the chocolatey install script from Internet
Set-ExecutionPolicy Bypass -Scope Process -Force; iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))

# install whatever app you want
# https://community.chocolatey.org/packages

# example of using Nano
choco install nano
nano myfile.txt

```