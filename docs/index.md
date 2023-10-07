### App Catalog

App catalog is a modern collaborative catalog solution designed to collect
and make software engineering system metadata available for consumer apps
to facilitate various automation tasks in the area of DevOps.

### What are the problems?

- Modern Applications require new types of attributes for facilitating tooling
- The system does not need to be complex to use it
- The system needs to support more than data entry
- An API first strategy is required to democratise system metadata
- No single approach for App Team, Infra Team and Ops Team
- Traditional Config Management applications are heavy on audit and light on useful data
- Each DevOps tool manages or discovers metadata using their own requirements thus causing duplication and drift

### How does App Catalog solve it?

App Catalog supports collaborative data gathering for software teams. You can start with a contract first or obtain the
current
state of the world using discovery modules. The API supports read and write operations for modules while allowing
powerful search
to get graph of related entries.

It opens up opportunities to declare once and use the contract across suite of devops tools. Teams can
uncover new workflows not used before to solve audit, dev productivity and quality gates while making it fun
for teams with leaderboard.

It provides approach for declaring once and utilising the contract across a suite of DevOps tools.
Teams can discover novel workflows that haven't been employed previously, addressing audit, development productivity,
and quality gates.
All the while, it adds an element of fun and collaboration for teams through the built-in scorecard and leaderboard
mechanism.

### The major components

There are six major categories of attributes in a catalog item.

| Category       | Description                                                                                                               |
|----------------|---------------------------------------------------------------------------------------------------------------------------|
| Metadata       | Catalog Item name, a few key attributes and various options to add additional data in the form of labels and annotations. |
| Roles          | Ownership and Collaborator details along with role they play for the catalog item.                                        |
| Links          | Collection of external links by intent - eg source, quality, test, build                                                  |
| Usage          | Information on upstream, downstream and dependency on resource                                                            |
| Classification | A collection of attributes to categorise the catalog item                                                                 |
| Runtime        | Information on entry points, key URIs and augmentation of discovered data                                                 |

#### Metadata

The metadata section of the document contains the following key attributes.

| Attribute Name        | Description                                                                      |
|-----------------------|----------------------------------------------------------------------------------|
| name                  | Name of the catalog item                                                         |
| description           | Text describing the catalog item                                                 |
| labels                | A map structure that can hold custom attributes to tag this artifact with        |
| labels.tier           | This attribute denotes the catalog runtime tier                                  |
| labels.internetFacing | Attribute that tells us whether the catalog item is accessible from the Internet |
| annotations           | A map structure that can hold additional enrichment data                         |                  |
| language              | Language in which this artifact was coded, if applicable                         |
| logo                  | Catalog item logo name or location                                               |
| contact               | Id that can be used to contact the owners of this catalog item for support       | 

THe below yaml snippet shows an example metadata section of a catalog item.

```yaml
metadata:
  name: "user-service"
  description: "This microservice provides customer information"
  labels:
    tier: web
    internetFacing: true
  annotations: { }
  language: go
  logo: "user-service.svg"
  contact: "user-service@example.io"
```

#### Roles

There can be a number of roles, a team or an individual can play with regards to the maintenance of a project.
While there can be a single owner from accountability perspective, a catalog item
can have many contributors playing different roles.

Few roles such as owner, contributors, support are explicitly laid out and additional roles can be configured as approvers by specifying the intent.

The ```id``` attribute holds the value of a contact ID of a team or individual using the following well known ID
formats.

| Id Type      | Example         | Fully Qualified Example               |
|--------------|-----------------|---------------------------------------|
| username     | @user1          | id://user1, ad://1600920              |
| team         | web-team        | team://web-team                       |
| group        | [approvergroup] | group://approvergroup                 |
| email        | web@company.com | email://web@company.com               |
| chat channel | #slackChannel   | slack:slackChannel, mattermost:channel2 |
| phone        | +6189209999     | tel://+6189209999, mob://+6189209999  |

As there can be a variety of ID providers and chat providers, an ```IDProviderConfig``` object can be specified 
to specify the defaults. 

The below yaml snippet shows roles configuration example for a catalog item.

```yaml 
roles:
  owner:
    id: "@user1"
  contributors:
    - id: "web-team"
    - id: "web@example.com"
  support:
    - id: "#slackChannel"
    - id: "mattermost://web-support"
    - id: "+6189209999"
  approvers:
    - id: "[CodeApprovers]"
      intent: "approvers"
    - id: "some-team"
      intent: "maintenance"
```

#### Links
An item can have many different concerns housed in other systems. We can collect required information using the link object array.

```yaml
links:
  - type: source
    url: git@github.com:owner/abc.git
  - type: artifact
    url: docker://owner/abc
  - type: contract
    url: https://site/contract.json
  - type: build
    url: https://jenkins/owner/example/build/
  - type: docs
    url: https://readthedocs.org/example
```

#### Usage

#### Classification

#### Runtime

### An Example

### Resource

```
- metadata
    - name/description
    - labels {}
    - annotations {}
    - internet facing
    - language 
    - contact

- roles:
    - owner: team/xyz, person
    - contributors: team/xyz
    - support: team/abs
    - approvers - change, maintenance

- links {intent, id}
    - code: source
    - artifact
    - contract
    - build
    - docs

- usage
    - upstream 
    - downstream
    - dependencies resource

- classification
    - type
        - hardware - machine, network, fw rules
        - software - app, database, storage, fw rules, template
        - tech - framework, library, appliance
    - category
    - tag
    - domain
    
- runtime
    - endpoint - intent/url entrypoint, readiness, liveness, correctness
    - environment - prod, non-prod, test etc

- resource
    - type
    - name

```


### Supporting Types

#### Team

#### User

#### IDProviderConfig
