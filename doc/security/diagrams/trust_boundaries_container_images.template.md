# Trust boundaries
*Note: this file was auto-generated and redacted from the original file.*

## Flow of container images
Trust boundaries are currently enforced by read-write (solid lines) and read-only (dotted lines) personal access tokens.

Retrieval of images from the Kubernetes registry via the gatekeeper registry is planned, as is verification / signing of images and policy-enforcement via **Kyverno**.

```mermaid
sequenceDiagram
    box Maroon EXTERNAL
        participant DOCKER_HUB@{ "type" : "database" }
        participant K8S_REGISTRY@{ "type" : "database" }
    end

    actor Administrator

    box Purple BOUNDARY_ONE
        participant GATEKEEPER_REGISTRY@{ "type" : "database" }
    end

    actor Developer

    box DarkGreen BOUNDARY_TWO
        participant PRIVATE_REGISTRY@{ "type" : "database" }
    end

    actor Kubernetes@{ "type" : "entity" }

    Administrator->>Kubernetes: Install Kubernetes and CSI drivers
    destroy K8S_REGISTRY
    K8S_REGISTRY-->>Kubernetes: Retrieve Kubernetes images

    Developer->>Administrator: Request addition / update of image
    DOCKER_HUB-->>Administrator: Inspect image
    Administrator->>GATEKEEPER_REGISTRY: Trigger image retrieval

    destroy DOCKER_HUB
    DOCKER_HUB-->>GATEKEEPER_REGISTRY: Retrieve base image

    Administrator->>GATEKEEPER_REGISTRY: Trigger image copy
    GATEKEEPER_REGISTRY->>PRIVATE_REGISTRY: Copy base image
    destroy Administrator
    Administrator->>Developer: Inform on decision / completion

    PRIVATE_REGISTRY-->>Developer: Retrieve image
    Developer->>PRIVATE_REGISTRY: Build custom image

    Developer->>Kubernetes: Assign base / custom image to pod
    PRIVATE_REGISTRY-->>Kubernetes: Retrieve image used in pod
```
