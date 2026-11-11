# Architecture of my home lab
I have never documented the design decisions and architecture of my home lab, which currently serves as:

- Media server and player
- Backup host
- Professional playground (of course)

However, I will start the documentation now, as an exercise.

Markdown and Mermaid are my tools of choice. They might not be the best option for an enterprise, but they are easy to use and quick to set up. For security reasons, some entries will be redacted automatically - which is another reason for using text-based tools.

*Enjoy!*

## Contents
### Security
- [Supply chain risk](./doc/security/supply_chain_risk.md)


## History
### 2010
- searched for professional archiver (DAR; reliability, maturity, random access, encryption, open source)
- wrote my own backup scheduler (Python 2)
- stored offsite backups on DVDs

### 2012
- re-wrote backup scheduler (Python 3, added tests, in use without problems since 2012)
- started using it for backups of legally relevant documents in my pharmacy
- stored offsite backups on cloud provider
- -> backup scheduler worked without flaws ever since

### ~2014
- switched to OpenZFS (mirrored, self-healing, snapshots)
- -> not a single file lost since

### ~2017
- created media server on single-board computer (manual installation)

### 2024
- created media server on single-board computer (Docker compose, OpenZFS)

### 2025
- stored documents and backups on mirrored file server
- designed sync logic and implemented it via templates ([StempelWerk](https://github.com/mzuther/StempelWerk))
- switched to OpenZFS native encryption
- added network segmentation (in home network and Docker)

### 2026
- deployment via Ansible
- switched from Docker Compose to Kubernetes (K3s)
- started to address supply-chain risk
