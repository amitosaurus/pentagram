## Solution

### Design Purpose
The journey to scale the current Syspos monolith is not a trivial one. There are many options and constraints to abide by. At core the architecture team is refactoring the existing design to achieve greater quality attributes. For example, to improve user experience during ticket creationation we are carving out the Ticket Creation component into an independent service so that more resources can be allocated to it and hence achieve better performance or response time. 
The purpose of the design is to describe the current system (the monolith), propose a new system that solves the challenges with the current monolith and provide guides of the construction process. 

### Solution Overview
Alis's work goes here


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


