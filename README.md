# awx-network-ee

Example awx-network execution envrironment build using forked & updated images:

- [python-base-image](https://github.com/ryanmerolle/python-base-image) - updated to CentOS stream9 and Python 3.9
- [python-builder-image](https://github.com/ryanmerolle/python-builder-image) - updated to CentOS stream9 and Python 3.9.
- [ansible-builder](https://github.com/ryanmerolle/ansible-builder) - updated to CentOS stream9 and Python 3.9.
- [ansible-runner](https://github.com/ryanmerolle/ansible-runner) - updated to CentOS stream9 and Python 3.9.  Added tags for Ansible 2.13 & eventually 2.14

## Building

```bash
ansible-builder build -t awx-network-ee:2.12
```
