There are two types of Components - App and Job. Most artifacts in a team might fall into this category especially if you are running a microservices architecture.

Here is an example Component object.

```json
apiVersion: "v1"
kind: Component
class: App
includes:
  - microservices
metadata: 
  name: "checks"
  description: "Customer Credit Check that calls Account check SaaS"
  license: "private"
  logo: "onboarding-check.png"
  contact: "onboarding@my-account.io"
  tier: "1"
dependencies:
  upstream: []
  downstream: ["check SaaS"]
  triggers: []
classification:
    tag: ["onboarding", "origination"]
    domain: "origination"
    team: "loaders"
    capability: "onboarding"
    businessUnit: "retail"
properties:
  dev: 
    quickstart: "./gradlew runApp"
    local-run: "docker-compose up -d"
  operations:
    idempotent: "true"
contact:
  owner:
    id: "@user10"
  contributors:
    - id: "@user2"
  support:
    - id: "#credit-check"
  participants:
    - id: "[onboarding]"

links:
  - type: "source"
    url: "https://github.com/my-account/checks"
  - type: "build"
    url: "https://jenkins/my-account/checks/build"
  - type: "docs"
    url: "https://scrolls/my-account/checks/intro"
  - type: "artifact"
    url: "https://quay.io/my-account/checks"
```