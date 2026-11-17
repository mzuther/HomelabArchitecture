# Architecture of my home lab
My home lab has been existing for a couple of years and currently serves as:

- media server and player
- backup host with complex synchronization logic
- professional playground (of course)

As an exercise, I will start documenting my design decisions and architecture here.

I will use Markdown and Mermaid to do so. Although these tools might not be the best option for an enterprise, they are easy to use and quick to set up. For security reasons, some entries will be redacted automatically - yet another reason for using text-based tools.

*Enjoy!*

## Contents
### Backup host
- [Backup synchronization](./doc/backup/synchronization.md)
- [ZFS pool layout](./doc/backup/zfs_pool_layout.md)

### Security
- [Supply chain risk](./doc/security/supply_chain_risk.md)


## History
### 2026
- deployment via Ansible
- switched from Docker Compose to Kubernetes (K3s)
- started to address supply-chain risk

### 2025
- stored documents and backups on mirrored file server
- designed sync logic and implemented it via templates ([StempelWerk](https://github.com/mzuther/StempelWerk))
- switched to OpenZFS native encryption
- added network segmentation (in home network and Docker)

### 2024
- deployed enhanced media server on a different single-board computer (Docker compose, OpenZFS)

### ~2017
- deployed simple media server on single-board computer (manual installation)

### ~2014
- switched to OpenZFS (mirrored, self-healing, snapshots)
- -> not a single file lost since

### 2012
- re-wrote backup scheduler (Python 3, added tests, in use without problems since 2012)
- started using it for backups of legally relevant documents in my pharmacy
- stored offsite backups on cloud provider
- -> backup scheduler worked without flaws ever since
