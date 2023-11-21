### Examples
Following are the use cases which have been adapted to follow the operations catalog specification.

#### Use Case 1
The first use case is a generic account management architecture where there are bunch of services, SaaS services, databases and queue.
In an online system, there could be few capabilities like - Client Experience, Onboarding, Correspondence, Operations, Servicing

![my account capabilities](../assets/images/my-account-capabilities.svg)


Similarly, multiple domains have been introduced in this architecture to show involvement of various teams to fulfill a typical account opening scenario. Namely, the domains used in this example are infra, preferences, storage, account, origination, gateway and frontend. A capability can have multiple domain. A team can also service multiple capabilities and look after multiple domains.


![my account architecture](../assets/images/my-account.svg)



|Catalog Item|Kind|Item Type|Domain|Team|Capability|
|---|---|---|---|---|---|
|mobile app|Component|App|servicing|frontend|Client Experience|
|crm|Service|SaaS|servicing|frontend|Client Experience|
|api gateway|Component|App|gateway|guards|iam|
|iDP|Service|SaaS|gateway|guards|iam|
|api config|Resource|Repository|gateway|guards|iam|
|logs|Service|SaaS|infra|platform|Operations|
|onboarding|Component|App|origination|loaders|Onboarding|
|checks|Component|App|origination|loaders|Onboarding|
|checks SaaS|Service|SaaS|origination|platform|Onboarding|
|account|Component|App|account|accountants|Servicing|
|account listener|Component|App|account|accountants|Servicing|
|notifications|Component|App|preferences|alerters|Correspondence|
|email|Resource|Mailbox|preferences|alerters|Correspondence|
|onboarding queue|Resource|Queue|origination|loaders|Onboarding|
|onboarding database|Resource|Schema|origination|loaders|Onboarding|
|account database|Resource|Schema|account|accountants|Servicing|
|mail SaaS|Service|SaaS|infra|platform|Operations|
|database server|Store|Database|storage|keepers|Operations|
|messaging service|Store|Messaging|storage|keepers|Operations|
|git service|Appliance|Git|infra|platform|Operations|
