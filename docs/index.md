---
title: "Intro"
url: /
menu:
   main:
     weight: 500
---

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
App Catalog supports collaborative data gathering for software teams. You can start with a contract first or obtain the current
state of the world using discovery modules. The API supports read and write operations for modules while allowing powerful search
to get graph of related entries.

It opens up opportunities to declare once and use the contract across suite of devops tools. Teams can
uncover new workflows not used before to solve audit, dev productivity and quality gates while making it fun
for teams with leaderboard.

It provides approach for declaring once and utilising the contract across a suite of DevOps tools. 
Teams can discover novel workflows that haven't been employed previously, addressing audit, development productivity, and quality gates. 
All the while, it adds an element of fun and collaboration for teams through the built-in scorecard and leaderboard mechanism.

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

```yaml
metadata:
    name: ""
    description: ""
    labels: {}
    annotations: {}
    internetFacing: false
    language: go
    contact: {}
```


#### Roles

#### Links

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
