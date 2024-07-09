When upgrading from NDFC 12.1.1e to NDFC 12.1.2e, you may experience a key error, as follows, when adding a child fabric to an MSD fabric using the role ``ndfc_rest_fabric_msd_child_add``.

```bash
Traceback (most recent call last):
  File "<string>", line 1962, in addFabricAsMemberEntryCheck
KeyError: 'ENABLE_PVLAN'
```

This occurs when older versions of this repo are used.

### Explanation

A new key was introduced in NDFC 12.1.2e: ``ENABLE_PVLAN``

Older versions of this repo did not set this key (since it didn't exist in NDFC 12.1.1e) when creating fabrics with the following roles:

- ``ndfc_rest_fabric_msd_create``
- ``ndfc_rest_fabric_switch_create``

A DDTS was filed and Closed, which provides more detail.

[CSCwe26995 - addFabricAsMemberEntryCheck: KeyError: 'ENABLE_PVLAN'](https://bst.cisco.com/quickview/bug/CSCwe26995)

The current version of this repo includes ``ENABLE_PVLAN`` key when creating fabrics, so will not encounter this error.
