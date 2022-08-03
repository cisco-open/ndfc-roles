# ndfc_rest_fabric_access_mode_set

NOTE: This is not working currently.  We're looking into it...

Given ``fabric_name`` set the fabric access_mode to true or false via var ``read_only``

### Role Variables

Variable        | Type   | Description
----------------|--------|----------------------------------------
fabric_name     | str()  | The fabric to be queried
read_only       | bool() | The fabric access mode (true or false)

Fabric parameters, including ``fabric_name`, are defined in the following file:

``./roles/ndfc_common/vars/main.yml``

See the following for details:

[./roles/ndfc_common/README.md](https://github.com/allenrobel/ndfc-roles/tree/master/roles/ndfc_common/README.md)

### Licensing

GNU General Public License v3.0 or later.

See [LICENSE](https://www.gnu.org/licenses/gpl-3.0.txt) for full text.

### Author Information

Allen Robel (@packetcalc)
