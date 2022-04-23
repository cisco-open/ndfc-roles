ndfc_devices_delete
=========

Loops over a list of device dictionaries, feeding them to cisco.dcnm.dcnm_inventory with state = deleted.

Requirements
------------

Role Variables
--------------

See the following dictionaries in ndfc_common/vars/main.yml

leafs
spines
border_gateways

Format of each object in the list is:

      - name: leaf_1
        ip: 10.168.0.23
        role: leaf

Where:
   name: the device name
   ip: the seed_ip (device's mgmt0 interface)
   role: the device's position in the fabric topology (leaf, spine, border_gateway, etc)


Dependencies
------------

None

Example Playbook
----------------

unit_test_ndfc_devices_delete.yml

License
-------

BSD

Author Information
------------------

Allen Robel (@packetcalc)
