# Repository Provisioning

Manual creation of Git repositories by admins leads to delays, waiting times for developers, and potential inconsistencies in descriptions, metadata, and access controls.

**Solution**: Ops Catalog automates Git repository creation and management, streamlining development workflows


![Issue Assignment](../assets/images/usecases/8.codefactory.svg)

**Use Case:** Discover and Create Repositories adopting Self-Service approach. 

**Actors:**

- Developers: Focus on writing code without waiting for repository creation.
- Ops Catalog: Automated platform for Git repository management.
- Code Factory Team: Manages Ops Catalog instance for specific teams/projects.

**Process:**

- Developer: Adds a catalog entry in Ops Catalog specifying repository details.
- Ops Catalog:
  - Fulfillment: Creates the Git repository based on the provided information, including descriptions, metadata, and access control policies.
  - Discovery: Discovers existing repositories within the GitOps environment and adds them to the catalog.
- GitOps Management Team:
  - Manages the Ops Catalog instance for their specific team/project (if applicable).
  - Can integrate with the organization-level Ops Catalog for broader discovery and resource sharing.

**Owner:** Dev Experience

**Value:** 

Secure repositories management without bottlenecks.

- Increased Productivity: Faster repository setup frees up developer time for coding and innovation.
- Reduced Error Rate: Standardized templates and automated workflows minimize configuration errors.
- Improved Consistency: Ensures all repositories are created with the correct descriptions, metadata, and access controls.
- Reduced Risk: Less reliance on manual admin intervention minimizes human error and security vulnerabilities.


[<<Back](../usecases.md)
