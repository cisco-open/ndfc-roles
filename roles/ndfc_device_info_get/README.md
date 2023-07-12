# ndfc_device_info_get

Query device ``device_name`` on the NDFC controller

A ``device_info`` dictionary is returned, as described below.

### Role Variables

Variable        | Type   | Description
----------------|--------|----------------------------------------
device_name     | string | The device to be queried

Fabric and device parameters are defined in the following files:

- [./inventory/group_vars/ndfc/01_fabrics.yml](/inventory/group_vars/ndfc/01_fabrics.yml)
- [./inventory/group_vars/ndfc/02_devices.yml](/inventory/group_vars/ndfc/02_devices.yml)

See the following for details:

[./inventory/group_vars/README.md](/inventory/group_vars/README.md)

### Example Playbook

```yaml
# Query NX-OS switch associated with fabric_name + device_name
# and print several items from the returned device_info dictionary
---
- hosts: ndfc
  gather_facts: false
  roles:
    - ndfc_device_info_get
  vars:
    device_name: leaf_1
  tasks:
  - block:
    - debug:
        msg: "logicalName: {{ device_info.logicalName }}"
    - debug:
        msg: "uptime: {{ device_info.upTimeStr }}"
    - debug:
        msg: "serial: {{ device_info.serialNumber }}"
    - debug:
        msg: "version: {{ device_info.release }}"
    - debug:
        msg: "switchDbId: {{ device_info.switchDbID }}"
```

### Licensing

GNU General Public License v3.0 or later.

See [LICENSE](https://www.gnu.org/licenses/gpl-3.0.txt) for full text.

### Author Information

Allen Robel (@packetcalc)

### Example returned object device_info (as of NDFC version 12.0.1)

```json
{
    "device_info": {
        "activeSupSlot": 0,
        "availPorts": 0,
        "colDBId": 0,
        "connUnitStatus": 0,
        "consistencyState": true,
        "contact": "",
        "cpuUsage": 25,
        "deviceType": "Switch_Fabric",
        "displayHdrs": [
            "Name",
            "IP Address",
            "Fabric",
            "WWN",
            "FC Ports",
            "Vendor",
            "Model",
            "Release",
            "UpTime"
        ],
        "displayValues": [
            "cvd_leaf_2311",
            "172.XX.XX.XX",
            "fabric_2",
            "FDOXXXXXXXX",
            "54",
            "Cisco",
            "N9K-C93180YC-EX",
            "10.2(3)",
            "18 days, 23:02:23"
        ],
        "domain": null,
        "domainID": 0,
        "elementType": null,
        "fabricId": 3,
        "fabricName": "fabric_2",
        "fabricTechnology": "VXLANFabric",
        "fcoeEnabled": false,
        "fex": false,
        "fexMap": {},
        "fid": 3,
        "health": -1,
        "hostName": "cvd_leaf_2311",
        "index": 3,
        "interfaces": null,
        "ipAddress": "172.XX.XX.XX",
        "ipDomain": "",
        "isEchSupport": false,
        "isLan": false,
        "isNonNexus": false,
        "isPmCollect": false,
        "isTrapDelayed": false,
        "isVpcConfigured": true,
        "is_smlic_enabled": false,
        "keepAliveState": "Peer is not alive",
        "lastScanTime": 1649700732019,
        "licenseDetail": null,
        "licenseViolation": false,
        "linkName": null,
        "location": "",
        "logicalName": "cvd_leaf_2311",
        "managable": true,
        "mds": false,
        "membership": null,
        "memoryUsage": 35,
        "mgmtAddress": null,
        "mode": "Normal",
        "model": "N9K-C93180YC-EX",
        "modelType": 0,
        "moduleIndexOffset": 9999,
        "modules": null,
        "name": null,
        "network": "LAN",
        "nonMdsModel": "N9K-C93180YC-EX",
        "npvEnabled": false,
        "numberOfPorts": 54,
        "peer": "cvd_leaf_2312",
        "peerSerialNumber": "FDOXXXXXXXX",
        "peerSwitchDbId": 576650,
        "peerlinkState": "Peer link is down",
        "ports": 0,
        "present": true,
        "primaryIP": null,
        "primarySwitchDbID": 0,
        "principal": null,
        "recvIntf": "mgmt0",
        "release": "10.2(3)",
        "role": "None established",
        "sanAnalyticsCapable": false,
        "scope": null,
        "secondaryIP": "",
        "secondarySwitchDbID": 0,
        "sendIntf": "mgmt0",
        "serialNumber": "FDOXXXXXXXX",
        "standbySupState": 0,
        "status": "ok",
        "swWwn": null,
        "swWwnName": "FDOXXXXXXXX",
        "switchDbID": 575610,
        "switchRole": "leaf",
        "switchRoleEnum": "Leaf",
        "sysDescr": "",
        "systemMode": null,
        "uid": 0,
        "unmanagableCause": "",
        "upTime": 163814317,
        "upTimeNumber": 0,
        "upTimeStr": "18 days, 23:02:23",
        "usedPorts": 0,
        "username": null,
        "vdcId": -1,
        "vdcMac": null,
        "vdcName": "",
        "vendor": "Cisco",
        "version": null,
        "vpcDomain": 1,
        "vrf": "management",
        "vsanWwn": null,
        "vsanWwnName": null,
        "wwn": null
    }
}
```