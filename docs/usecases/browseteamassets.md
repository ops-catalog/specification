# Browse Team Assets

CMDB systems suffer from a lack of visibility in the type of data they store. This, coupled with siloed data management practices, leads to the creation of multiple data copies and inconsistencies. These inconsistencies result in stale data, posing significant operational risks.

**Solution:**  A specification to consistently store data across applications, microservices, and all infrastructure components (physical and logical)

![Browse Team Assets](../assets/images/usecases/6.browseteamassets.svg)

**Use Case:** Browse All types of Assets and Identify Owners, Discover Links including local runs and environments at team or division level.

**Actors:**

- Ops Catalog: Manages the comprehensive data specification for infrastructure components.
- Developers and Users: Access information through self-service platforms or Developer Portal.
- Ops Portal Instances: Can act as edge catalogs, which can be discovered by a central Ops Catalog.


**Process:**

- Data Collection: Ops Catalog gathers data adhering to its specification, covering infrastructure components, ownership, and usage instructions.
- Storage: Data is stored centrally within the Ops Catalog.
- API/Portal Access: Self-service platforms consume data via API, while developers and users interact through a Developer Portal.
- Edge Catalog: Team-specific Ops Portals feed data into the central Ops Catalog.


**Owner:** DevOps 

**Value:** 

Have a view of the assets that matter to the team in the format or setup best suited for them.

- Visibility: Increased visibility into infrastructure data.
- Consistency: Elimination of data silos and reduction of stale data.
- Efficiency: Improved efficiency through self-service and streamlined interactions.
- Discoverability: Easier discoverability of applications, services, and their supporting information.



[<<Back](../usecases.md)
