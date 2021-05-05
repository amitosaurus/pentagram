### **ADR_002-00**:

### Picking the Architecture Style for migrating the monolith

**<u>Status</u>**:	Proposed

**<u>Context</u>**: Based on the architectural characteristics shortlisted in `

[adr_001-00_ArchitectureCharacteristics.md]: https://raw.githubusercontent.com/amitosaurus/pentagram/The_Sysops_Squad_Architecture_AB/The_Sysops_Squad/architecture/adrs/adr_001-00_ArchitectureCharacteristics.md	"Architecture Characteristics"

`, we used the following matrix [ref: https://www.developertoarchitect.com/downloads/worksheets.html] to help visualize our options

![](https://raw.githubusercontent.com/amitosaurus/pentagram/main/imgs/TSS_ArchitecturalStyle.png)



**<u>Decision</u>**:

From the above matrix it is evident that a Event-Driven, Microservices architecture will address most required characteristics needed by the Sysops Squad. Further, hosting some of the most critical of these services on a cloud platform will inherently provide features like scalability, elasticity, availability and operational efficiency.

However, currently the application is very brittle and in the current context moving the existing monolith to a cloud native microservices architecture will introduce a lot of complexity and risk in an already fragile ecosystem.

**<u>Consequences</u>**:

We need to devise a strategy to migrate the existing monolith to a hybrid of a Services based and Event Driven, Microservices based architecture, hosted on a cloud platform.

