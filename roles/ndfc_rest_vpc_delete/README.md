# ndfc_rest_vpc_delete

Delete vpc peering ``vpc_name`` in fabric ``fabric_name``

### Role Variables

Variable        | Type  | Description
----------------|-------|----------------------------------------
vpc_name        | str() | The name of the vpc peering to delete

``vpc_name`` are defined in the following file:

``./roles/ndfc_common/vars/main.yml``

Specifically:

``vpc_name`` is defined in the ``vpc_peers`` list

See the following for details:

[./roles/ndfc_common/README.md](https://github.com/allenrobel/ndfc-roles/tree/master/roles/ndfc_common/README.md)

### Example Playbook

This currently does not work.  We're investigating it and will update the repo once a resolution is found.

```yaml
```

### Licensing

GNU General Public License v3.0 or later.

See [LICENSE](https://www.gnu.org/licenses/gpl-3.0.txt) for full text.

### Author Information

Allen Robel (@packetcalc)
