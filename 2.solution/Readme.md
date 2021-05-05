## Solution

### Design Purpose
The journey to scale the current Syspos monolith is not a trivial one. There are many options and constraints to abide by. At core the architecture team is refactoring the existing design to achieve greater quality attributes. For example, to improve user experience during ticket creationation we are carving out the Ticket Creation component into an independent service so that more resources can be allocated to it and hence achieve better performance or response time. 
The purpose of the design is to describe the current system (the monolith), propose a new system that solves the challenges with the current monolith and provide guides of the construction process. 

## Overview of the current monolith system
### C4 Component Model
C4 stands for context, containers, components and code. It is a set of hierarchical diagrams that you can use to describe your software architecture at different zoom levels, each useful for different audience The C4 modelling is used here to describe and define architectures in an abstract and simple way.

#### C4-L1 System Context Diagram
![](../imgs/C4-L1-System%20Context%20Diagram.jpg)
C4-L1 System Context Diagram is the top-level diagram  of SysOp Squad System and is also the most abstract. It show the big picture, how different users interact with the SysOp Squad System as a whole, and how the System fits together with other existing software systems

Below are the external users who interact with the system

- Administrator: It is the User who maintains the internal users of the system, including the list of experts and their corresponding skillset, location, and availability. Additionally , manages all of the billing and static reference data.

- Customer: Registers for the Sysops Squad service, maintains their customer profile, support contracts, and billing information
They enter problem tickets into the system, and also fill out surveys after the work has been completed.

- Experts: Assigned problem tickets and fix problems based on the ticket. They also interact with the knowledge base to search for
solutions to customer problems and also enter notes about repairs.

- Call Center Agent: A call center representative Inquire ticket status and can create a new Ticket on customer behalf

- Payment Gateway: It is a third party payment service provider. SysOps system interact with Payment Gateway
to process customer annual feet

- Notification System: It is the software system which is used to send notifications SMS or Email
to customers and experts.

#### C4-L2 System Container Diagram
![](../imgs/C4-L2-Container%20Diagram.jpg)
Containers are bigger parts of the application that could potentially be deployed separately.
A container is a standalone piece of software in your system that executes code or stores data
The Container diagram shows the high-level shape of the software architecture and how responsibilities are distributed across it. It also shows the major technology choices and how the containers communicate with one another.

C4-L2 System Container Diagram contains following containers: 

- Mobile Application: used to view problem tickets assigned to an expert. It also has access to knowledge base to search existing solutions
Moreover, expert can update ticket status up on resolution using it It interacts with API application to perform those tasks

- Web Application: A web application that provides all SysOps squad functionalities to users (Customer, Administrator, Manager, Call Center Agent)
based on their role through interactive UI.

  - It collaborates  with API application container to perform all business operations
  - It interacts with Reporting Engine to generate and view Financial and Analytics reports
  - It interact with Payment gateway component for secure payment processing
  - It interacts with Notification System to send email and sms
  - It generates business events and interact with Event Manager for asynchronous processing

- Event Manager: This component handles business events for asynchronous processing

- Database: Database container is used as a storage system to persist all user and customer data

- Reporting Engine
  - It is the container which generates and view financial and analytical reports
  - It interacts with Database container to fetch the data

- API Application
This container holds all APIs to perform all business operations. It interacts with Database container to fetch and persit data

### Primary Functional Requirements
The core of the Sysops system is to route experts to failing equipment to help customers achieve better quality of life. UC-6, UC-7,UC-8 and UC-9 demonstrate the core functionality of the system. A system that can not accommodate these use cases is considered a failure.      

### Ranking of the Quality Attribute Scenarios

Scenario ID | Importance to Customer| Difficulty of implementation according to architecture
------------| ----------------------|--------------------------------------------------------
QAS-1 | High | High
QAS-2 | Medium | Low
QAS-3 | High | Medium
QAS-4 | Medium | High
QAS-5 | Low | Low
QAS-6 | Low | Low
QAS-7 | Low | High

### Trade-offs
1. Decision: One Front end UI vs Multi front ends
    1. Options:
        1. Multiple Front Ends
        1. (+Configurability)
        1. (+Usability)
        1. -Maintainability
    1. Rational: Created Multiple Frond End UIs for Ticket creation and backend support operations for better usability and configurability. Maintainability was tradeof   
1. Decision: Strict Contacts vs Value based Contracts
    1. Options:
        1. Loose Contracts
        1. (+Requires Fitness Functions)
        1. (+Loose Coupling)
        1. - Better Control
    1. Rational: Decided to go with a loose contracts as architecture was evolving to be micro services. Ensured loose coupling and established fitness functions.
1. Decision: Choreography vs Orcestration
    1. Options:
        1. Orchestration
        1. (+Centralized workflow)
        1. (+Loose Coupling)
        1. (+Better Control of sagas and error handling)
        2. -Distributed Workflow
        3. -Better Reponsiveness
    1. Rational: Choose to implement a central message broker for better Centralized workflow. Performance was tradeoff however proper design consideration will be done for traffic prioritization.  

### ADRs
To capture critical architectural decisions made during the evolution of this proposal, we maintained ADRs.

A key difference in our naming convention is the provision for tracking the superseded ADRs, along with the original.

Our ADR naming convention is:

​			``` adr_nnn-xx_IdentifyingTag```

... where...

​    ***adr*** is a keyword indicating that the file is an ADR

​	***nnn*** is a 3 digit sequence number to track the ADR

​    ***xx*** is a 2 digit number to track all superseded instances of the ADR.
​         Thus an ADR superseding `adr_051-00_UseOfRuleEngine.md`would be `adr_051-01_UseOfRuleEngine.md`

   ***IdentifyingTag*** is a tag that tells us a little about the Architectural Decision that is captured

All our ADRs can be found [here](/adrs)



## Overview of the Proposed Solution

We propose to migrate the current architecture in Phases (please check ADRs that document our thought process behind this), with transition between phases driven by data from fitness functions.

The following phases for migration have been determined -

### Phase 0

Introduce fitness functions in the existing architecture to draw a baseline for every measurable characteristic that we need to track

### Phase 1

Break the existing monolith into multiple services, all using the same common DB and interacting using a Message Broker (that will also serve as an Orchestrator & help with workflows in our event-driven system)

![](https://raw.githubusercontent.com/amitosaurus/pentagram/main/imgs/TSS_Migration_Phase-1.png)



### Phase 2

Create bounded contexts for certain services with each of them having their own DB and (pragmatically) allow select services to share a DB

![](https://raw.githubusercontent.com/amitosaurus/pentagram/main/imgs/TSS_Migration_Phase-2.png)



### Phase 3

With the rest of the system staying the same, convert the ticketing service into a microservice and deploy it on the cloud

![](https://raw.githubusercontent.com/amitosaurus/pentagram/main/imgs/TSS_Migration_Phase-3.png)



### Phase 4 (As Needed Over Time)

Based on data obtained from fitness functions, other services can be converted to microservices as well and moved to the cloud

