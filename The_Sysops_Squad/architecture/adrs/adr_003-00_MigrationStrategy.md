### **ADR_003-00**:

### Migration Strategy

**<u>Status</u>**:	Proposed

**<u>Context</u>**: Based on the Architectural Style picked in

[adr_002-00_ArchitectureStyle]: 

we need to decide on a strategy for migrating the existing architecture to the *new & improved* version.

While the target state promises to address most (if not all) challenges faced with the current system, getting there comes with a certain amount of risk.

We need to migrate the existing monolith that has barely evolved in the last few years, and is extremely fragile to a hybrid event-driven/microservices architecture that is inherently complex (having a single star on simplicity).

In addition, (by Conway's Law), the chances of the existing team not having evolved (like their application) is very high. Adapting to a new architecture and the learning curve that the team will be subject to is a consideration we need to make.

**<u>Decision</u>**:

From the above matrix it is evident that a Event-Driven, Microservices architecture will address most required characteristics needed by the Sysops Squad. Further, hosting some of the most critical of these services on a cloud platform will inherently provide features like scalability, elasticity, availability and operational efficiency.

However, currently the application is very brittle and in the current context moving the existing monolith to a cloud native microservices architecture will introduce a lot of complexity and risk in an already fragile ecosystem.

**<u>Consequences</u>**:

We need to devise a strategy to migrate the existing monolith to a hybrid of a Services based and Event Driven, Microservices based architecture, hosted on a cloud platform.