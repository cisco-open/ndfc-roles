# ndfc_rest_fabric_access_mode_set

Given ``fabric_name`` set the fabric access_mode to true or false via var ``read_only``

### Role Variables

Variable        | Type    | Description
----------------|---------|----------------------------------------
fabric_name     | string  | The fabric to be queried
read_only       | boolean | The fabric access mode (true or false)

Fabric parameters are defined in the following file:

- [./inventory/group_vars/ndfc/01_fabrics.yml](/inventory/group_vars/ndfc/01_fabrics.yml)

See the following for details:

[./inventory/group_vars/README.md](/inventory/group_vars/README.md)

### Licensing

GNU General Public License v3.0 or later.

See [LICENSE](https://www.gnu.org/licenses/gpl-3.0.txt) for full text.

### Author Information

Allen Robel (@packetcalc)
