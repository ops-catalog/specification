
# Manage Certificates

Manual certificate management leads to:

- Unexpected certificate expirations: Disruptions for developers and potential security risks.
- Inefficient workflows: Support teams scrambling to replace certificates before expiry.
- Increased cognitive load: Teams waste time tracking and managing certificate lifecycles.

**Solution:** Utilise Ops Catalog for automated certificate management.

![Manage Certificates](../assets/images/usecases/3.certificates.svg)

**Use Case**: Automated Certificate Management with Ops Catalog

**Actors**:

- Operations Team: Responsible for provisioning and installing certificates.
- Development Team: Apps rely on certificates.
- Ops Catalog: Automated certificate discovery and management platform.
- Inspector Process: Periodically checks for certificate expiry.

**Process:**

- Operations Team: Provisions certificates and installs them on servers or applications.
- Ops Catalog: Discovers the installed certificate and automatically captures its metadata:

    |Attributes|
    |---|
    |Subject Alternative Names (SANs)|
    |Common Name|
    |Issuer|
    |Created Date|
    |Expiry Date|

- Ops Catalog: Monitors certificate expiry dates.
- Ops Catalog: Triggers alerts to relevant parties (e.g., Support Team) before expiry for timely renewal.

**Owner:** Prod Support/SRE

**Value:** 

Be ahead of the game and know where your certificates are and when they are up for renewal.

- Operations Team: Reduced workload from manual tracking and renewal tasks.
- Development Team: Increased application uptime and reliability due to proactive certificate management.
- Business: Minimised security risks and improved team efficiency.



[<<Back](../usecases.md)

