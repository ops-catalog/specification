

Few Possible Use Cases for DevOps and Self-Service Platforms:

|Area|Use Case|Purpose|Recommended Approach|
|---|---|---|---|
|Audit|Audit Report|Generate Inventory List|Use Api Data|
|Ownership|Find Owners|Find Owners for assets and teams|Api call|
|SRE|Issue Assignment|Assign production issues to the correct owners|Api call|
|Code Factory|Create Repository|Do not wait weeks for some admin to create repositories for you|Use Git Fulfillment|
|Operations|Create Resources|Create Resources like Database Schemas, Search Indices, Kafka Topics, Security Groups, Buckets|Use fulfillment - Postgres, Cassandra, S3|
|Operations|Manage Certificates|Manage Certificate lifecycle, provisioning and renewal alerts|Discovery from K8s, vault*|
|Dev Experience|Browse Assets|Browse All types of Assets and Identify Owners, Discover Links including local runs and environments|Call from your UI or backstage|
|Release|Approval Checks|Seek approval from actual owners of the item being deployed|Api call|
|Deployment|Config Mgmt|Use Attributes shared by owners as config for deployment|Store Properties and make API call|
|Operations|Annotate Workloads|Annotate workloads to have rich information at runtime - log dashboards, deployment objects|API call|
|Project Mgmt|Ticketing|Assign tickets to owners and teams for specific topics|Api call|
|Build|Register New Builds |Register New Builds when catalog has a new entry|in progress*|
|IAM|User Mgmt|Discover or Manager User, Groups, Roles|roadmap*|
|IAM|User Mgmt|Discover or Manager User, Groups, Roles|roadmap*|
|Release|Impact Assessment|Calculate true impact and assign tasks to each team for PVT|roadmap*|

 \* - in roadmap or being implemented. Reach out if interested to help with requirement and/or code.

![Ops Catalog Use Cases](./assets/images/opsusecases.svg)
