### **ADR_004-00**:

### Identifying Components

**<u>Status</u>**:	Proposed

**<u>Context</u>**: Based on the the migration strategy finalized in `adr_003-00_MigrationStrategy`, for Stage 1 of our migration plan, we need to break down the architectural components in the existing monolith into different logical groups and define independently deployable services. These may be coarse grained to begin with.

<img src="C:\Users\amito\OneDrive\Documents\GitHub\pentagram\The_Sysops_Squad\architecture\images\Sysops_Squad_Architecture_Component_Breakdown.png" alt="Sysops_Squad_Architecture_Component_Breakdown" style="zoom:67%;" />

**<u>Decision</u>**:

The existing components have been grouped logically as shown below, keeping in mind the fact that some similar components like "Billing payment" and "Billing history" have different requirements in terms of architectural characteristics, and hence they have been separated.

On similar lines as billing, both "Customer profile" and "Expert profile" could be part of a single "Profile Management" component. However, the decision to keep them separate has been made in view of the eventual goal of breaking them off as separate microservices, so that they can be independently managed and maintained.

<img src="C:\Users\amito\OneDrive\Documents\GitHub\pentagram\The_Sysops_Squad\architecture\images\Sysops_Squad_Component_Breakdown.png" alt="Sysops_Squad_Component_Breakdown" style="zoom:60%;" />





**<u>Consequences</u>**:

