# Trust boundaries
*Note: this file was auto-generated and redacted from the original file.*

## GitOps (Flux)
Trust boundaries are currently enforced by different Git repositories and their access tokens.

```mermaid
flowchart TD
    Admin@{ shape: person }-->|pushes|GitRepositoryPlatform
    Developer@{ shape: person }-->|pushes|GitRepositoryApps

    subgraph SoftwareForge["Software forge"]
        GitRepositoryPlatform@{ shape: datastore, label: "Git repository (platform)" }
        GitRepositoryApps@{ shape: datastore, label: "Git repository (applications)" }
    end

    subgraph Kubernetes
        subgraph KubernetesSystem["Kubernetes system"]
            Flux-->|watches|GitRepositoryPlatform
            Flux@{ shape: rect }-->|watches|GitRepositoryApps
            Flux-->|calls|KubernetesAPI["Kubernetes API"]
        end

        subgraph KubernetesDeployments["Kubernetes deployments"]
            KubernetesAPI-->|deploys|PlatformDeployment["Deployment (platform)"]
            KubernetesAPI-->|deploys|AppsDeployment["Deployment (applications)"]

            AppsDeployment-->|depends on|PlatformDeployment
        end
    end
```
