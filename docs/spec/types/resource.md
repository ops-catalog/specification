The kind ```Resource``` can have the following classes :
Schema, Keyspace, Collection, Index, Topic, Queue, Repository, Certificate

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
    tag: ["origination", "onboarding", "customer"]
    domain: "origination"
    team: "loaders"
    capability: "origination"
```

Note, resources can be linked back to the exact provider (eg Storage or other objects) by ```dependencies.providedBy``` attribute.


A Cassandra Keyspace resource would look like this:

```yaml
apiVersion: v1
class: Keyspace
kind: Resource
metadata:
    name: notificationstore
    description: Cassandra Keyspace for tables in notificationstore
    labels: {}
    annotations:
        discovery.ops.catalog/replication: |
            {"class":"org.apache.cassandra.locator.NetworkTopologyStrategy","datacenter1":"1"}
    tier: ""
    contact: ""
contact:
    owner: null
dependencies:
    upstream: []
    downstream: []
    providedBy: cassandra.cassandra-1
classification:
    tag: []
    domain: storage
    team: datahoarders
    capability: dataretention
properties:
    lifecycle:
        replication:
            class: org.apache.cassandra.locator.NetworkTopologyStrategy
            datacenter1: "1"
includes:
    - internal

```

Note the attributes under lifecycle namespace which are relevant to Cassandra Keyspace Similarly, a certificate resource is represented like so where the lifecycle namespace contains attributes specific to certificates:

```yaml
apiVersion: v1
class: Certificate
kind: Resource
metadata:
    name: ops-cert
    description: Tls Certificate http://k8s-read:6100
    labels: {}
    tier: ""
    contact: ""
classification:
    tag: []
    domain: platform
    team: devops
    capability: operations
properties:
    lifecycle:
        common-name: docs.ops-catalog.io
        created: "2024-01-18T11:25:20Z"
        expiry: "2024-02-17T11:25:20Z"
        issuer: sparkjob
        san:
            - docs.ops-catalog.io.default.svc
includes:
    - internal
```
