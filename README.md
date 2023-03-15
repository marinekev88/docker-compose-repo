# docker-compose-repo
Repository holding docker-compose configs

# dell poweredge settings 
***Solution***

ENABLE/DISABLE Third-Party PCIe card based default system fan response:

1.      Download and install OpenManage BMC Utility. 

2.      Enable the "IPMI over LAN" in iDRAC of the target machine, this can ben done via iDRAC Web GUI or BIOS Setup. 

3.      Go to the installation folder of OpenManage BMC Utility, run the following commands: 

Set Third-Party PCIe Card Default Cooling Response Logic To Disabled

ipmitool -I lanplus -H <HOST_IP> -U <USER_NAME> -P <PASSWORD> raw 0x30 0xce 0x00 0x16 0x05 0x00 0x00 0x00 0x05 0x00 0x01 0x00 0x00 

Set Third-Party PCIe Card Default Cooling Response Logic To Enabled

ipmitool -I lanplus -H <HOST_IP> -U <USER_NAME> -P <PASSWORD> raw 0x30 0xce 0x00 0x16 0x05 0x00 0x00 0x00 0x05 0x00 0x00 0x00 0x00 

Get Third-Party PCIe Card Default Cooling Response Logic Status

ipmitool -I lanplus -H <HOST_IP> -U <USER_NAME> -P <PASSWORD> raw 0x30 0xce 0x01 0x16 0x05 0x00 0x00 0x00 

The response data is:

16 05 00 00 00 05 00 01 00 00 (Disabled)

16 05 00 00 00 05 00 00 00 00 (Enabled)
