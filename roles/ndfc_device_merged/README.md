ndfc_devices_create
=========

Loops over a list of device dictionaries, feeding them to cisco.dcnm.dcnm_inventory with state = merged.

Requirements
------------

Role Variables
--------------

See the following device dictionary lists in ndfc_common/vars/main.yml

fabrics[0].leafs
fabrics[0].spines
fabrics[0].border_gateways

Format of each object in the list is:

      - name: leaf_1
        ip: 172.22.150.102
        role: leaf

Where:
   name: the device name
   ip: the seed_ip (device's mgmt0 interface)
   role: the device's position in the fabric topology (leaf, spine, border_gateway, etc)

See also:

ndfc_devices_create/defaults/main.yml
    auth_proto - the protocol to use to authenticate to each device.  We assume all devices use the same protocol
    max_hops - the number of CDP hops to traverse when discovering devices. We set this to 0 to discover one device at a time. 

Dependencies
------------

None

Example Playbook
----------------

fabric1_create.yml

License
-------

BSD

Author Information
------------------

Allen Robel (@packetcalc)
