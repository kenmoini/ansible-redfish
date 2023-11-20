# Ansible Redfish

This automation will allow you to boot a set of systems from a network hosted ISO file via Redfish endpoints.

## Supported Systems

- SuperMicro
- Dell iDRAC 8
- Dell iDRAC 9
- HPE iLO 5

## Known Issues

- On SuperMicro systems you may have an older version of your BMC/BIOS that does not have the updated Redfish libraries.  Update to the latest versions of your BIOS/BMC to get access to Redfish 1.8.0+.
- On SuperMicro systems you may need an additional set of licenses, namely the `SFT-OOB-LIC` and `SFT-DCMS-SINGLE` licenses.  There may or may not be license generators for them available on GitHub.

## Todo

- Add Lenovo Redfish interfacing
- Add Fakefish/Sushy-tools interfacing
