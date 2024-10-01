---
icon: elementor
---

# Vertically Scaling Cassandra

| <p>Run the following commands before the activity from one of the cassandra nodes<br>nodetool clientstats<br>nodetool compactionstats<br>nodetool gcstats<br>nodetool netstats<br>nodetool tpstats<br>nodetool tablestats</p>                                                                                                                                  |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Stop the traffic from outside. Stop nginx-public                                                                                                                                                                                                                                                                                                               |
|                                                                                                                                                                                                                                                                                                                                                                |
| <p>Stop the samza jobs<br>ntpprod.course-batch-updater<br>ntpprod.qrcode-image-generator<br>ntpprod.lms.user-account-merger<br>ntpprod.collection-migration<br>ntpprod.lms.sso-account-updater<br>ntpprod.merge-user-courses<br>ntpprod.lms.indexer<br>ntpprod.publish-pipeline<br>ntpprod.course-certificate-generator<br>ntpprod.post-publish-processor</p>  |
| Run nodetool drain in every cassandra node                                                                                                                                                                                                                                                                                                                     |
| Stop cassandra process in every cassandra node                                                                                                                                                                                                                                                                                                                 |
| Take a disk snapshot of each cassandra VM                                                                                                                                                                                                                                                                                                                      |
| Stop the cassandra VMs and change the instnace type d8sV3                                                                                                                                                                                                                                                                                                      |
| Start the cassandra VMs                                                                                                                                                                                                                                                                                                                                        |
| <p>Run the following commands from one of the cassandra nodes<br>nodetool clientstats<br>nodetool compactionstats<br>nodetool gcstats<br>nodetool netstats<br>nodetool tpstats<br>nodetool tablestats</p>                                                                                                                                                      |
| Run sample cassandra queries                                                                                                                                                                                                                                                                                                                                   |
| <p>Start the samza jobs<br>ntpprod.course-batch-updater<br>ntpprod.qrcode-image-generator<br>ntpprod.lms.user-account-merger<br>ntpprod.collection-migration<br>ntpprod.lms.sso-account-updater<br>ntpprod.merge-user-courses<br>ntpprod.lms.indexer<br>ntpprod.publish-pipeline<br>ntpprod.course-certificate-generator<br>ntpprod.post-publish-processor</p> |
| Start nginx-public to allow traffic                                                                                                                                                                                                                                                                                                                            |

**Common Questions Tech Professionals May Have Based on this Procedure:**

1. What is the purpose of running nodetool commands before and after the activity?
2. Why is it necessary to stop external traffic and Samza jobs before performing the changes?
3. What precautions should be taken when stopping the Cassandra process and taking VM snapshots?
4. How do the instance type changes impact Cassandra VMs performance?
5. What are the expected outcomes when running the sample Cassandra queries after the VMs restart?
6. Can you explain the steps to revert the changes in case of any issues?
7. What monitoring tools can be used to ensure everything is functioning correctly post-upgrade?
