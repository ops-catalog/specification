Endpoint Kind is a catalog item type to store information about Access points like Ingress, HTTPRoute, TCPRoute, ALBs and similar loadbalancers.

```yaml
apiVersion: v1
class: HttpRoute
kind: Endpoint
metadata:
    name: service-entrypoint
    description: Http Route in Kubernetes Cluster http://k8s.ops-catalog.io:80
    labels: {}
    annotations: {}
dependencies:
    upstream: []
    downstream:
        - k8s-read
        - account
classification:
    type: App
    tag: []
    domain: platform
    team: devops
    capability: operations
properties: {}
includes:
    - internal
runtime:
    endpoint:
        - intent: entrypoint
          location: k8s.ops-catalog.io
links:
    - type: definition
      url: http://k8s.ops-catalog.io:80/api/crd-instance?resource-group=gateway.networking.k8s.io&resource-type=httproutes&resource-version=v1beta1&namespace=default&resource-name=k8s-read-http
```

Specific information about endpoint can be kept in extensions map which could be made available contextually.