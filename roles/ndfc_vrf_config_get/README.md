# ndfc_vrf_config_get

Retrieve the configuration for vrf  ``vrf_name``

## Returns (via set_fact)

Variable        | Type   | Description
----------------|--------|----------------------------------------
vrf_config      | object | A JSON object containing ``vrf_name``'s current configuration

## Role Variables

Variable        | Type   | Description
----------------|--------|----------------------------------------
vrf_name        | string | The vrf's configuration to retrieve

VRF parameters are defined in the following files:

- [./inventory/group_vars/ndfc/04_vrfs.yml](/inventory/group_vars/ndfc/04_vrfs.yml)

See the following for details:

[./inventory/group_vars/README.md](/inventory/group_vars/README.md)

## Example Playbook

```yaml
---
- hosts: ndfc
  gather_facts: false
  roles:
    - ndfc_vrf_config_get
  vars:
    vrf_name: msd_v1
  tasks:
  - block:
    - debug:
        var: vrf_config
```

## Example returned object

```json
{
    "vrf_config": {
        "attach": [
            {
                "ip_address": "172.22.150.102"
            },
            {
                "ip_address": "172.22.150.103"
            },
            {
                "ip_address": "172.22.150.104"
            },
            {
                "ip_address": "172.22.150.105"
            },
            {
                "ip_address": "172.22.150.106"
            },
            {
                "ip_address": "172.22.150.107"
            },
            {
                "ip_address": "172.22.150.108"
            },
            {
                "ip_address": "172.22.150.109"
            },
            {
                "ip_address": "172.22.150.110"
            },
            {
                "ip_address": "172.22.150.111"
            },
            {
                "ip_address": "172.22.150.100"
            },
            {
                "ip_address": "172.22.150.101"
            }
        ],
        "fabric": "MSD",
        "import_evpn_rt": "65001:63031,65002:63032",
        "import_vpn_rt": "65001:63031,65002:63032",
        "name": "msd_v1",
        "service_vrf_template": null,
        "vlan_id": 3031,
        "vrf_extension_template": "Default_VRF_Extension_Universal",
        "vrf_id": 63031,
        "vrf_name": "v1",
        "vrf_template": "Default_VRF_Universal"
    }
}
```

## Licensing

GNU General Public License v3.0 or later.

See [LICENSE](https://www.gnu.org/licenses/gpl-3.0.txt) for full text.

## Author Information

Allen Robel (@packetcalc)
