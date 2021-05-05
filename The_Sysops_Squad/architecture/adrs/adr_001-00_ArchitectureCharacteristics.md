### **ADR_001-00**:

### Picking the most relevant characteristics needed in the migrated architecture

**<u>Status</u>**:	Proposed

**<u>Context</u>**: From the scenario shared, we have highlighted problem areas & gaps that need to be addressed

![highlights from a bad situation](https://raw.githubusercontent.com/amitosaurus/pentagram/The_Sysops_Squad_Architecture_AB/The_Sysops_Squad/architecture/images/Sysops_Squad_Bad_Situation_Highlights.png)

**<u>Decision</u>**:

With the current context, the following "*ilities*" have been deemed most relevant -

![](https://raw.githubusercontent.com/amitosaurus/pentagram/main/imgs/TSS_ArchitectureCharacteristics.png)



To elaborate the need for some of these characteristics,

- ***Evolvability***
  - To make it feasible (and easy) to adapt to evolving needs and over time, not turn back into "*a large monolith application that was developed many years ago*"
- ***Observability*** - Debuggability, Traceability
  - To help perform RCA for lost tickets
- ***Reliability*** - Data Integrity
  - To make sure the right experts are assigned to the ticket
- ***Agility*** - Modularity, Testability, Deployability
  - To be able to make changes to parts of the system quickly without effecting the rest of the system
  - To improve time to market
  - To identify & fix issues early and reduce production issues
- ***Operability*** - Resiliency, Manageability, Recoverability, Fault Tolerance
  - To make production operations smoother and more predictable 
- ***Availability***
  - To ensure that web-based and call-based ticket entries are always possible
- ***Elasticity***
  - To handle spikes of requests coming into the system without crashing
- ***Security***
  - To safely perform credit card transactions and bill customers regularly (even though this has not been deemed to be a challenge in the existing system)

**<u>Consequences</u>**:

Based on the above decision, we will narrow down the architectural styles that can be used while moving away from the existing monolith. While not all "*ilities*" can be accommodated simultaneously, certain tradeoffs will be made and priorities will be determined when picking the architectural style [in adr_002-00_ArchitectureStyle.md].