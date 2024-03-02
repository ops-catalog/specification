# Create Data Resources

Manual provisioning of data platform resources (schemas, keyspaces, etc.) is time-consuming and prone to errors

**Solution:** Ops Catalog enables self-service provisioning of data platform resources using a standardized catalog specification.

![Issue Assignment](../assets/images/usecases/9.dataplatform.svg)

**Usecase:** Organizations seeking to automate and streamline the process of providing data resources to developers and data engineers.

**Actor:**

- Developers and Data Engineers: Add catalog items for desired infrastructure elements.
- Ops Catalog: Manages the Discovery and Fulfillment modes, enabling self-service provisioning.

**Process:**

- Catalog Creation: Data platform teams provide discovery and fulfillment configuration for various data components.
- Self-Service Request: Developers/engineers add the desired catalog item to their project.
- Automated Discovery: Ops Catalog discovers resources from discovery targets and catalogs them.
- Automated Provisioning: Ops Catalog provisions the requested resource based on the catalog specification.


**Owner:** Data Platform Owners

**Value:** 

Discover and Provision Data Platform resources minimising manual effort and enhancing efficiency.

- Faster Provisioning: Reduces the time to obtain data resources.
- Error Reduction: Minimizes manual errors, ensuring consistency.
- Improved Efficiency: Frees up data platform teams from routine provisioning tasks.



[<<Back](../usecases.md)
