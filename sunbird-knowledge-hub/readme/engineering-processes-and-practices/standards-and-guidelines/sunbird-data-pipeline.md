---
icon: elementor
---

# Sunbird Data Pipeline

<figure><img src="../../../../.gitbook/assets/Sunbird_DataPipeline_HighLevel_Diagram.png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../../.gitbook/assets/image (1).avif" alt=""><figcaption></figcaption></figure>

####

#### GITBOOK AI

#### Questions to Consider

1. What are the main components illustrated in the Sunbird Data Pipeline High-Level Diagram?
2. How does data flow between the different modules in the Sunbird Data Pipeline?
3. What role does the Data Processing component play in the overall architecture?
4. Can you identify the security measures incorporated in the pipeline?
5. How do the various data sources integrate into the pipeline according to the diagram?

#### Summary of the Sunbird Data Pipeline High-Level Diagram

The Sunbird Data Pipeline High-Level Diagram illustrates the architecture of the data pipeline. It includes the following main components:

* **Data Sources:** Various input sources providing raw data.
* **Ingestion Layer:** Handles data collection and initial storage.
* **Data Processing:** Processes and transforms raw data into meaningful outputs.
* **Storage Layer:** Stores processed data for further use.
* **Analytics and Reporting:** Allows for data analysis and generation of reports.
* **Security Measures:** Ensure data integrity, confidentiality, and compliance.

Overall, the data flows sequentially from data sources through ingestion, processing, and finally to storage and analytics layers, ensuring secure handling at each stage.

#### CHAT GPT

#### **Summary**:

1. **Telemetry API**:
   * Acts as the entry point where telemetry data is ingested.
2. **Telemetry Extractor**:
   * Extracts raw telemetry events from the API.
   * Sends data to backup and preprocessor.
3. **Pipeline Preprocessor**:
   * Processes audit events and streams them through Kafka.
4. **Telemetry Merger**:
   * Merges raw telemetry events and generates unique and duplicate records using Spark Dataflow.
   * Data is sent to Redis for user cache updates or further downstream processing.
5. **Telemetry Demons**:
   * Derived data and demons route telemetry events.
   * The data flows into Druid, a data storage engine for fast queries and storage.
6. **Redis and Elastic Search**:
   * Redis supports caching and data profile updates.
   * Elastic Search stores logs.
7. **Druid**:
   * Central data storage (real-time) that processes events into different outputs such as summary and error events.
8. **Backups**:
   * At various stages, the pipeline includes backup mechanisms for failure recovery, such as:
     * Extractor Backup
     * Duplicate Events Backup
     * Derived Backup
     * Demons Backup
     * Failed Backup

#### **Key Technologies**:

* **Kafka**: Message queueing for telemetry data.
* **Spark Dataflow**: For data merging and transformation.
* **Redis**: Cache storage and device profile APIs.
* **Druid**: Real-time data analytics and storage.
* **Elastic Search**: For logging and search.

***

#### **Possible Questions**:

1. **What is the role of the Telemetry API in this data pipeline?**
   * The Telemetry API serves as the entry point for all incoming telemetry data.
2. **How does the pipeline handle raw and duplicate events?**
   * Raw telemetry events are extracted and processed, while duplicates are identified and backed up for audit or analysis.
3. **What is the function of the Spark Dataflow within the pipeline?**
   * Spark Dataflow helps in merging telemetry events and determining unique or duplicate events.
4. **How is error handling managed in this pipeline?**
   * The pipeline includes backups at multiple stages, such as Extractor Backup, Duplicate Events Backup, and Failed Backup to recover from errors.
5. **What role does Redis play in the pipeline?**
   * Redis is used for updating user cache and device profile APIs to ensure fast data retrieval and management.
6. **Why is Druid used in this pipeline?**
   * Druid is employed for real-time data ingestion and analytics, enabling fast query processing of large datasets.
7. **What backup mechanisms are in place for failure recovery?**
   * There are various backup stages including backups for duplicate events, derived data, and failed operations.
8. **What is the significance of the Pipeline Preprocessor?**
   * It processes audit events and ensures that the raw telemetry data is prepared for further merging and storage.

