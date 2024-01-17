The kind ```Resource``` can have the following classes :
Schema, Keyspace, Collection, Index, Topic, Queue, Repository	

An example resource definition for a Schema:
```yaml
apiVersion: "v1"
kind: Resource
class: Schema
metadata: 
  name: "onboarding"
  description: "Schema and DB connection used by onboarding use case"
  license: "private"
dependencies:
  upstream: []
  providedBy: postgres.pg-2 
  triggers: []
classification:
    type: "Schema"
    tag: ["origination", "onboarding", "customer"]
    domain: "origination"
    team: "loaders"
    capability: "origination"
```

Note, resources can be linked back to the exact provider (eg Storage or other objects) by ```dependencies.providedBy``` attribute.
