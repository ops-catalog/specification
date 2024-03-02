# Browse Org Assets

Centralized catalog systems often result in stale, less comprehensive data that lacks attributes vital for modern workflows.

**Solution:** Ops Catalog employs a federated management approach where local experts maintain fresh data in edge instances. These instances integrate with a central aggregator for organisation-wide discoverability.

![Browse All Assets](../assets/images/usecases/7.browseorgassets.svg)

**Usecase:** Organisations seeking a comprehensive catalog with up-to-date information and the flexibility to support team-specific workflows.

**Actors:**

- Local experts own and keep their data uptodate.
- IT operations teams setup a global catalog that discovers data from other catalogs
- End-users consume catalog data either via API or through Portals

**Process:**

- Data Ownership: Local experts populate and manage data in their Ops Catalog edge instances.
- Edge Workflows: Edge instances serve team-specific use cases.
- Central Aggregation: Edge instances are discoverable by a central Ops Catalog aggregator.
- Organisation-wide Visibility: The aggregator provides a single point of access to all catalog items.

**Owner:** Infra Teams

**Business Value:** 

Maintain locally, Access Everywhere. Accurate Open data that is accessible.

- Fresh, Accurate Data: Local ownership ensures data remains up-to-date and relevant.
- Comprehensive Catalog: Avoids missing key attributes by including data from various teams.
- Workflow Support: Balances team autonomy with enterprise-level discoverability.




[<<Back](../usecases.md)
