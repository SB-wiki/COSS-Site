---
icon: elementor
---

# Manage @ Scale

**Manage at Scale**

This document is to know what to scale and how to scale when utilization reaches a threshold.

**When to Scale:**

* When the load on services/VMS is increased consistently, we need to do scaling activity.

**Request for Additional Resource:**

* Create an Access request Jira ticket for approval in [https://project-diksha.atlassian.net](https://project-diksha.atlassian.net/secure/Dashboard.jspa)
* Assign it to Anand for approval
* Once approved, Create VMs from the Azure portal and follow respective steps below to scale.

**Process of approval to Scale:**

* Create an Access request Jira ticket for approval in [https://project-diksha.atlassian.net](https://project-diksha.atlassian.net/secure/Dashboard.jspa)
* Assign it to Anand for approval
* Once approved, provision the resources and follow respective steps below to scale.

**Scalable Services:**

* Scaling docker swarm(horizontal scaling)
* Scaling Elastic search cluster (Composite search, user org search and logging)
* Scaling Cassandra cluster (KP and LMS)
* Scaling Neo4J cluster
* Scaling YARN cluster
* Scaling Kafka cluster
* Scaling Learning and search service
* Scaling Postgres service (LMS, Kong, keylock)

**Scaling docker swarm**

* **Decision Criteria**

CPU: % more than 90%

Memory: 90%

DISk: if the disk utilization is more than 90% > clear the unwanted logs/stop the VM and increase the Disk size.

* **Steps/Instructions**

**Vertical Scaling:**

* Adding/Update the instance type(memory,vcores)
* Increase replica count for required services.

If all the containers are consuming more resources will do horizontal scaling by adding nodes to the cluster.

**Horizontal Scaling:**

* Create a VM
* Add the New instance IP to the host file
* Run bootstrap job using Jenkins
* provision docker-swarm
* verify the cluster size/count and docker services
* **Time to scale:**
  * **30mins**

**Scaling Elastic search cluster (Composite search, user org search and logging):**

* **Decision Criteria:**
  * CPU: % more than 90%
  * Memory: 90%
  * Disk: if the disk utilization is more than 90% > clear the unwanted logs/stop the VM and increase the Disk size based on the utilization
* **Steps/Instructions**

**Horizontal scaling:**

*
  * Create a VM
  * Add the instance to the host file
  * Run bootstrap job via Jenkins
  * provision Elasticsearch
  * verify the master server configuration file whether the cluster count is equal to the no. of nodes

**Or**

**Vertical scaling:**

*
  * Verify the **heap size** of elasticsearch(java) service > if the es service consuming more memory, need to do vertical scaling
  * stop the instance
  * change the instance type(memory optimized VM)
  * start the VM
  * change the Heap size
  * Restart the es service.
* **Time to scale:**
  * 30mins

**Scaling Cassandra cluster (KP and LMS):**

* **Decision Criteria:**
  * CPU: % more than 75%
  * Memory: 80%
  * Disk: 80%
* **Steps/ Instructions:**
  * It is a vertical scaling, we need to stop the instance. We should give the desired value for CPU, Memory and Disk
* **Time to Scale:**
  * 30mins

**Scaling Neo4J cluster:**

* **Decision Criteria:**
  * CPU: % more than 75%
  * Memory: 75%
* **Steps/Instructions:**
  * Launch a VM, provision the neo4j using Jenkins and then deploy the Neo4j using Jenkins and Start the Neo4j
* **Time to scale:**
  * 30mins to provision and deploy.

**Scaling YARN cluster:**

* **Decision Criteria**
  * When resources are not available to run any container or application, we need to add new resources or nodes to the Yarn manager (cluster)
* **Steps/Instructions :**
  * Create a VM, add to the host (inventory)
  * Run Yarn provision Job.
  * Start the node manager in the new VM so it will connect to the existing cluster.
  * Validation: Run the cmd in the resource manager (yarn manager) to check whether a new node is a part of the cluster.
* **Time to scale:**
  * 30mins

**Scaling Kafka cluster:**

* **Decision Criteria**
  * When Heap size/Disk is almost utilised more than 70%
* **Steps/Instructions :**
  * Stop Monit in all 3/x nodes
  * Stop Kafka process in all 3/x nodes.
  * Stop the zookeeper process in all 3/x nodes.
  * Stop VM
  * Increase memory/disk
  * Add/update heap size limit variable in common.yml.
  * Run Kafka provision (This will just update the Kafka init.d script with latest heap size)
* **Verification:**
  * Verify the changes by running (sudo systemctl status kafka.service) in all nodes.
  * Verify the cluster health by running “/opt/kafka/bin/zookeeper.shell.sh localhost:2181 <<< ls /brokers/ids”
* **Time to scale:**
  * 30mins

**Scaling Learning and search service:**

* Learning Service runs on tomcat and Search Service as a Java application
* **Decision Criteria**
  * _When CPU/Memory is more than 70%_
    * **Steps/Instructions :**
      * Launch VMs
      * Update inventory by adding above VMs IP addresses
      * Provision of the Services using Jenkins jobs (provision/KnowledgePlatform/learning, provision/KnowledgePlatform/search)
      * Deploy the services (Learning/Search)
      * Verify the health of the services
      * Attach to LP and Search Load balancers in Azure.
  * _When 75% of the Disk is utilised_
    * **Steps/Instructions :**
      * Stop the VM for 10 mins
      * Update the disk size on Azure
      * Start the VM
      * Verify if all the services are running.
* **Time to scale:**
  * 30mins

**Scaling Postgres service (LMS, Kong, keylock) :**

* **Decision Criteria :**
  * CPU: % more than 75%
  * Memory: 80%
  * Disk: 80%
* **Steps/Instructions:**
  * It is a vertical scaling, we need to stop the instance. We should give the desired value for CPU, Memory and Disk
* **Time to Scale:**
  * 30mins

**Swarm Reset:**

* **Decision Criteria:**
  * Error message in /var/log/system _“memberlist: Failed fallback ping: read tcp 11.4.0.17:43420->11.4.0.22:7946: i/o timeout”_
  * Containers restarting
  * High CPU and Memory utilization on agent nodes
