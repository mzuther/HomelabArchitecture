# Supply chain risk
*Note: this file was auto-generated and redacted from the original file.*

## Chain of trust
```mermaid
flowchart LR
    classDef explicit_trust fill:DarkGreen;
    classDef implicit_trust fill:Navy;
    classDef unverified fill:Maroon;

    subgraph UnverifiedOrigins["Unverified origins"]
        subgraph UnverifiedRepositoryOrigins["Software repositories"]
            GitHubUnverified["`**GitHub**<br>Repositories`"]:::unverified
            PyPiUnverified["`**PyPi**<br>Repository`"]:::unverified
            DockerHubUnverified["`**Docker Hub**<br>Image registry`"]:::unverified
            K8sHubUnverified["`**Kubernetes (k8s)**<br>Image registry`"]:::unverified
        end

        subgraph UnverifiedTools["Tools - Unverified"]
            GitHubUnverified --> CosignUnverified["`**Cosign**<br>Software attestation`"]:::unverified

            PyPiUnverified --> Ansible["`**Ansible**<br>IaC tool`"]:::unverified
            PyPiUnverified --> StempelWerk["`**StempelWerk**<br>Automatic code generation`"]:::unverified
        end
    end

    subgraph TrustedOrigins["Trusted origins"]
        subgraph ExplicitlyTrustedHosting["External providers"]
            SaasProvider["`**[REDACTED]**<br>SaaS provider`"]:::explicit_trust
        end

        subgraph TrustedRepositoryOrigins["Software repositories"]
            DebianRepositories["`**Debian**<br>Repositories`"]:::explicit_trust --> OSRepositories["`**[REDACTED]**<br>Repositories`"]:::explicit_trust

            DebianRepositories --> DebianExtrepo["`**Debian extrepo**<br>Repository`"]:::explicit_trust
        end

        subgraph ExplicitlyTrustedSystemTools["Tools - Explicit trust"]
            OSRepositories --> APT["`**APT**<br>Package manager`"]:::explicit_trust
            OSRepositories --> Shells["`**Shells**<br>sh / Bash / SSH`"]:::explicit_trust
            OSRepositories --> Python["`**Python**<br>Programming language`"]:::explicit_trust

            OSRepositories --> DiskArchiver["`**Disk Archiver (DAR)**<br>Backup tool`"]:::explicit_trust
            OSRepositories --> Rsync["`**rsync**<br>Backup tool`"]:::explicit_trust
            OSRepositories --> OpenZfs["`**OpenZFS**<br>Redundant file system`"]:::explicit_trust
            OSRepositories --> FileServer["`**[REDACTED]**<br>File server`"]:::explicit_trust
        end

        subgraph ImplicitlyTrustedTools["Tools - Implicit trust"]
            DebianExtrepo --> GitHubCLI["`**GitHub CLI**<br>Software attestation`"]:::implicit_trust
            DebianExtrepo --> Mise["`**mise**<br>Package manager`"]:::implicit_trust
            DebianExtrepo --> UV["`**uv**<br>Package manager`"]:::implicit_trust

            SaasProvider --> SoftwareForge["`**[REDACTED]**<br>Software forge`"]:::implicit_trust
        end

        subgraph VerifiedTools["Tools - Verified"]
            CosignUnverified --> Cosign["`**Cosign**<br>Software attestation`"]:::implicit_trust
            GitHubCLI --> Cosign
        end
    end
```
