# Ansible Redfish

This automation will allow you to boot a set of systems from a network hosted ISO file via Redfish endpoints.

## Supported Systems

- Dell iDRAC 8
- Dell iDRAC 9
- Dell iDRAC 10
- HPE iLO 6
- HPE iLO 5
- HPE iLO 4
- SuperMicro
- sushy-tools

## Usage

1. Install the needed Collections: `ansible-galaxy install -r collections/requirements.txt`
2. Create some vaulted variables that target your BMC hosts that you'll be connecting to: `ansible-vault create bmc-hosts.secret-vars.yml` - it should look something like this:

```yaml=
---
bmc_hosts:
  # SuperMicro Example
  - name: endurance
    endpoint: endurance.mgmt.kemo.labs
    username: ansible
    password: n0tPassword
    system_type: supermicro

  # iDRAC8 Example
  - name: serenity
    endpoint: serenity.mgmt.kemo.labs
    username: ansible
    password: n0tPassword
    system_type: iDRAC8

  # iDRAC9 Example
  - name: dell-per640
    endpoint: 10.1.2.3
    username: root
    password: calvin
    system_type: iDRAC9

  # iDRAC10 Example
  - name: dell-per670
    endpoint: 10.1.2.3
    username: root
    password: calvin
    system_type: iDRAC10

  # iLO6 Example
  - name: hpe-dl120-g11
    endpoint: 10.1.2.3
    username: Administrator
    password: password
    system_type: iLO6

  # iLO5 Example
  - name: hpe-dl120-g10
    endpoint: 10.1.2.3
    username: Administrator
    password: password
    system_type: iLO5

  # iLO4 Example
  - name: hpe-dl20-g9
    endpoint: 10.1.2.3
    username: Administrator
    password: password
    system_type: iLO4

  # sushy-tools Example
  # name is the UUID of the VM
  - name: 1baa7e2b-9cc6-426f-b0ab-d309b3030f57
    endpoint: 192.168.42.40:8111
    endpoint_protocol: http
    system_type: sushy-tools
```

3. Run the Playbook: `ansible-playbook -e "@bmc-hosts.secret-vars.yml" -e iso_url="http://example.com/path/to/boot.iso" playbooks/boot_iso.yml`

## AAP2 Controller Setup

To easily stand this automation up in an AAP2 Controller/Tower, you can find some additional automation in the `aap-controller-setup` folder.

```bash=
# Install the Collection
ansible-galaxy collection install infra.controller_configuration

# Enter the aap-controller-setup directory
cd aap-controller-setup

# Edit the vars/controller_auth.yml file to point to your Controller/Tower

# Optionally edit the vars/config.vars.yml file

# Run the configuration automation
ansible-playbook configure-controller.yml
```

> Following the configuration you'll need to provide some vaulted variables for your BMC Hosts and pass them into the Job Template in the AAP2 Controller/Tower.

## Known Issues

- On SuperMicro systems you may have an older version of your BMC/BIOS that does not have the updated Redfish libraries.  Update to the latest versions of your BIOS/BMC to get access to Redfish 1.8.0+.
- On SuperMicro systems you may need an additional set of licenses, namely the `SFT-OOB-LIC` and `SFT-DCMS-SINGLE` licenses.  There may or may not be license generators for them available on GitHub.

## Todo

- Add Lenovo Redfish interfacing
- Add Cisco interfacing
- Add IBM interfacing
- Add Gigabyte interfacing
