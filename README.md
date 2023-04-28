# awx-network-ee

This now uses the updated ansible-builder v3 refactor.

This new version of ansible-builder addresses a lot of the issues with not being able to build ansible execution environments if you are using a custom built image with your internal package repos.

## Building

```bash
ansible-builder build -t awx-network-ee:latest -v 3
```
