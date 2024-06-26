Objects cataloged as Store kind will have some capability to provide storage of data.
The Kind ```Store``` has the following types under it:
Disk, SFTP, NFS, StorageService (S3, GCS), Database (Postgres, Cassandra), Messaging (Kafka, JMS)

To avoid levels of indirection, the attribute ```class``` is directly set to one of the implementations for each category of product under Store. For instance, the below example uses ```class: Kafka``` instead of ```class: Messaging``` as there is no immediate benefit to keeping messaging. Perhaps, Category can be determined on the fly if and when that is required.

All attributes applicable to components are also valid for Storage objects.

```yaml
apiVersion: "v1"
kind: Store
class: Kafka
metadata: 
  name: "kafka"
  description: "SaaS service for log aggregation and analysis"
  license: "Apache 2.0"
dependencies:
  upstream: []
  downstream: []
  triggers: []
classification:
    tag: ["messaging", "stream"]
    domain: "storage"
    team: "keepers"
    capability: "Operations"
    businessUnit: "tech"
```
