### Examples
Following are the use cases which have been adapted to follow the operations catalog specification.

#### Use Case 2
This use case shows few components in devops space used to perform deployment using tools like Jenkins, Git and Kubernetes.

![deploy architecture](../assets/images/deploy.svg)

Multiple domains have been introduced in this architecture to show involvement of various teams to fulfill a typical deployment setup.


|Catalog Item|Kind|Class|Domain|Team|Capability|
|---|---|---|---|---|---|
|platform-config|Resource|Repository|tools|platform|Continuous Deployment|
|onboarding-config|Resource|Repository|tools|loaders|Continuous Deployment|
|deployer|Component|App|tools|platform|Continuous Deployment|
|iam Service|Appliance|SaaS|iam|guards|iam|
|jenkins|Appliance|CD|tools|tinkerers|Continuous Deployment|
|git|Appliance|Git|tools|tinkerers|Operations|
|kubernetes|Appliance|Kubernetes|infrastructure|platform|Operations|
|oca|Component|App|tools|tinkerers|Operations|