# KnowledgePlatform

falseLog in to the Jenkins and do the following

### Build

* Switch to Build folder and run all jobs

### Provision

* Switch to Provision//KnowledgePlatform and run jobs in following order
  1. Cassandra
  2. CompositeSearch
  3. Neo4j
  4. Zookeeper
  5. Kafka
  6. Learning
  7. Redis
  8. Search

Deploy

* Switch to Deploy/dev/KnowledgePlatform and run all jobs in the following order
  1. CassandraDbUpdate
  2. Neo4j
  3. StartNeo4jCluster
  4. Learning
  5. Search
  6. Neo4jDefinitionUpdate
  7. Neo4jElasticSearchSyncTool
  8. KafkaSetup
  9. Yarn

***

\[\[category.storage-team]] \[\[category.confluence]]
