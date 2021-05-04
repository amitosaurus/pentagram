In the Sysop Ecosystem Multiple actors interact with the system to achieve required functionalities. Broadly there are two different workflow streams which happen in Sysop.  The sequence diagrams worked as a reference for defining our  data workflow and service communication in Distributed Architecture model. It has been ensured that our evolutionary architecture have required coupling in the migration of monolith to distributed.

# Ticketing Workflow
![](../imgs/TicketingWorkflow.jpg)
Ticketing  workflow steam defines how customers interact with the system for ticket creation and how Sysop Experts and Sysop IT system facilitates the ticket routing, ticket maintenance  and ticket completion. The sequence diagram captured all synchronous and asynchronous message communications that happen in the workflow.


# None-Ticketing Workflow
![](../imgs/NonTicketingWorkflow.jpg)
Non Ticketing workflow defines how Customers interact with the system for support plan , billing  and how the system provides the information. The workflow also defined the business backend operation (reporting etc) required for smooth operation. 

