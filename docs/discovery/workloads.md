Component Discovery

Workloads can be discovered from a running Kubernetes instance. We make use of a lightweight Kubernetes Object Query Service that gives us metadata on deployments and statefulsets.

Here is a sample discovery config to retrieve data from Kubernetes excluding few workloads while annotating all of them with team data.

```yaml
apiVersion: "v1"
kind: Discovery
metadata:
  name: "k8s-discovery"

type: k8s
instance:
  - name: "k8s"
    filter:
      excludes: ["local-path-.*", "metrics-.*", "coredns", "envoy.*gateway.*"]
    includes:
      - internal
    options:
      host: "k8s-read.ops-catalog.io"
      port: "80"
      ssl: "false"
      secretPrivateKey: "file:./some-location"
      secretPublicKey: "file:./some-public-key"
    classification:
      team: "devops"
      domain: "platform"
      type: "App"
      capability: "operations"
      businessUnit: "tech"
```

k8s-read performs an encryption on TLS certificates for a public key provided in the request header. The private and public keys can be configured with the option attributes ```secretPrivateKey``` and ```secretPublicKey```
