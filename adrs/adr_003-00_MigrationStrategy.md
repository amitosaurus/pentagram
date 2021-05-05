### **ADR_003-00**:

### Migration Strategy

**<u>Status</u>**:	Proposed

**<u>Context</u>**: Based on the Architectural Style picked in

[adr_002-00_ArchitectureStyle]: 

we need to decide on a strategy for migrating the existing architecture to the *new & improved* version.

While the target state promises to address most (if not all) challenges faced with the current system, getting there comes with a certain amount of risk.

We need to migrate the existing monolith that has barely evolved in the last few years, and is extremely fragile to a hybrid event-driven/microservices architecture that is inherently complex (having a single star on simplicity).

In addition, (by Conway's Law), the chances of the existing team not having evolved (like their application) is very high. Adapting to a new architecture and the learning curve that the team will be subject to is a consideration we need to make.

So, the decision needs to be made weather we migrate the application using -

1. **A BIG BANG Approach** - do it all in one shot
   - ***Pros***:
     - Faster results
   - ***Cons***:
     - High Risk
     - Steep Learning Curve
     - High Complexity
2. **A Slow, But Steady Approach** - divide the transition into phases, track using fitness functions for every characteristic to measure the change and make incremental changes in every phase
   - ***Pros***:
     - Low Risk
     - Ability to include micro-tweaks & adjustments along the way *driven by data from fitness functions*
     - Team gets more room for adapting to the new architecture
   - ***Cons***: 
     - Slower results
     - Additional work in determining and picking the right fitness functions

**<u>Decision</u>**:

To mitigate the risk and considering the fragility of the existing system the decision has been made to go with option 2 "***The Slow, But Steady Approach***"

**<u>Consequences</u>**:

As a consequence of this decision, the following phases for migration have been determined -

- <u>Phase 0</u>: Introduce fitness functions in the existing architecture to draw a baseline for every measurable characteristic that we need to track

- <u>Phase 1</u>: Break the existing monolith into multiple services, all using the same common DB and interacting using a Message Broker (that will also serve as an Orchestrator & help with workflows in our event-driven system)

  ![](https://raw.githubusercontent.com/amitosaurus/pentagram/main/imgs/TSS_Migration_Phase-1.png)

  

- <u>Phase 2</u>: Create bounded contexts for certain services with each of them having their own DB and (pragmatically) allow select services to share a DB

  ![](https://raw.githubusercontent.com/amitosaurus/pentagram/main/imgs/TSS_Migration_Phase-2.png)



- <u>Phase 3</u>: With the rest of the system staying the same, convert the ticketing service into a microservice and deploy it on the cloud

  ![](https://raw.githubusercontent.com/amitosaurus/pentagram/main/imgs/TSS_Migration_Phase-3.png)



- <u>Phase 4</u>: (Optional) Based on data obtained from fitness functions, other services can be converted to microservices as well and moved to the cloud

