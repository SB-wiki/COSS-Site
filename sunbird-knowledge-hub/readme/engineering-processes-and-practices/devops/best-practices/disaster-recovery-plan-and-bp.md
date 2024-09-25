---
icon: elementor
---

# Disaster Recovery Plan & BP

Evaluation of Disaster Recovery Mechanisms

\- Most of env is automation, If any manual steps involved how much manual effort time and dependency.

\- it is time to analyze various recovery methods available for each entity and determine the best suitable recovery method for each.

( Time estimations for each restoration )

\- In the case of data systems, for example, the recovery mechanism usually involves having the critical data systems replicated somewhere else in the network and putting them online with the latest backed up data available

( different zones of availibility of db replication)

Replication options:

\- The cold server is basically turned on once to have software installed and configured, and then is turned off until needed.

\- A warm server is a backup server that is turned on periodically to receive updates from the server being backed up. Warm servers are often used for replication and mirroring.

\- A hot server is a backup server that receives regular updates and is standing by ready (on hot standby) to take over immediately in the event of a failover.

Disaster Recovery Committee

The Disaster Recovery Committee should be authorized and responsible for:

● Creating and maintaining the disaster recovery plan

● Detecting and announcing disaster events within the company ● Activating the disaster recovery plan

● Executing the disaster recovery plan

● Monitoring the disaster situation continuously and returning operations to normal at the earliest feasible time

● Restoring normal operations and shutting down disaster recovery operations

● Continuously improving the disaster recovery plan by conducting periodic mock trials and incorporating lessons learned into the plan after an actual disaster

Activation plan on ekstep and sunbird env:

\- Co-ordinator excutor lead to excute the process.

\- List of systems and services that need to be restored

\- Sequence of Recovery Activities.

\- Restore system data

\- Test system functionality

\- Update the stackholders to use.

Reconstitution Phase:

\- Continuously monitor the site.

The Disaster Recovery Plan Document :

\- Document Information:

\- Assumptions : which inclusive and exclusive

\- System Description: simple and clear on workflow of DR

\- Activation Procedures

\- Execution Procedures:

\- Reconstitution Procedures:

Document Maintenance

\- Periodic Mock Drills

\- Experience Capture: The best testing the document will undergo is when an actual disaster happens, and the lessons learned during the disaster recovery are valuable for improving the plan.

\- Periodic Updates : Technologies, systems that the plan covers may change over time may update the document accordingly.
