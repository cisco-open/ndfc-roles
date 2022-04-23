ndfc_devices_create
=========

Query a specific device, denoted with fabric_name and device_name.

Return a device_info object as described below.

Requirements
------------

Role Variables
--------------

See the following device dictionary lists in ndfc_common/vars/main.yml

leafs
spines
border_gateways

Format of each object in the list is:

      - name: leaf_1
        ip: 172.22.150.102
        role: leaf

Where:
   name: the device name
   ip: the seed_ip (device's mgmt0 interface)
   role: the device's position in the fabric topology (leaf, spine, border_gateway, etc)

See also:

Dependencies
------------

None

Example Playbook
----------------

unit_test_ndfc_devices_query.yml

License
-------

BSD

Author Information
------------------

Allen Robel (@packetcalc)

Example returned object device_info
-----------------------------------

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
