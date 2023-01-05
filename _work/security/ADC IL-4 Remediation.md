Date: 01/04/2023
Written by: Anthony Armijo
DOC REF: [[CSA-APT5-CITRIXADC-V1.pdf]]
___
* This is in regards to recent vulnerabilities for ADC (INSERT CVEs HERE)
* This reports steps taken for discovering threat actor activity as well as to mitigate the known vulnerabilities.

# Threat Hunting
## File Integrity Checks

```bash
# This code pulls md5 hashes of key executables.
# Compare these to known good hashes from Citrix
cd /netscaler ; for i in "nsppe nsaad nsconf nsreadfile nsconmsg"; do md5 ${i} ; done

MD5 (nsppe) = c8609797da92849d9ea1110b9892b17e
md5: nsaad: No such file or directory
MD5 (nsconf) = 7be780b2bc3844dc92ad9466050992ef
MD5 (nsreadfile) = f78960fdc43ab0f1d00d8957a5386cb3
MD5 (nsconmsg) = 6c580ea4c08982cee8475cf40fd5f3a5
```

( ) test

```bash
# This codes checks for APT5 tampering
# One line return indicates tampering. No output is good.
procstat -v $(pgrep -o -i nsppe) | grep "0x10400000 " | grep "rwx"

# NO OUTPUT REPORTED
```
## Behavioural Checks
NSA suggests organizations leverage off-device logging for all system logs, including dmesg and ns.log, as well as actively monitor them for the following activity:
- Instances of `pb_policy` appearing in logs without being linked to admin activity
- Logs utilizing `pb_policy` within the `ns.log` file that show:
	- `<local10.info> [hostname] pb_policy: Changing pitboss policy from X to Y`
	- `<local10.info> [hostname] pb_policy: Changing pitboss policy from Y to X`


```bash
# Command below can help indicate presence of actor activity within logs:
find / -type f -name "res*" | grep -E 'res($|\.[a-z]{3})$'

/var/python/lib/python2.7/site-packages/gevent-1.2.2-py2.7-freebsd-11.4-RELEASE-amd64.egg/gevent/resolver_ares.pyc

```