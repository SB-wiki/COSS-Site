---
icon: elementor
---

# Azure Storage

**Azure Storage Blob:**

Massively scalable and secure object storage for cloud-native workloads, archives, data lakes, high-performance computing and machine learning

**Best practices:**

* Make sure the storage account type supports the scale expected for the application. Ensure egress and ingress limits are in control
* Ensure that SAS tokens generated don't have full access to the storage account. To protect the Azure Storage account resources against unapproved access, configure the stored access policies associated with your service SAS tokens to follow the principle of least privilege by giving these policies the minimal set of permissions required to perform successfully their tasks.
* Setup alert notifications for Create/Update storage accounts to detect unauthorized and suspicious activity
* Enable immutable blob storage feature for blob containers that hold sensitive and business critical data. This makes the data non-erasable and non-modifiable.
* Limit the storage account access by IP
  * ![](<../../../../../.gitbook/assets/0 (5).png>)
* Rotate storage account keys periodically
* Encrypt the storage account using BYOK (Bring your own keys)

Storage account type used in Diksha for content store is **general purpose v1**

Storage metrics in last 30 days

**- Max egress limits for storage account**

Max egress: 7.2 = 57.6 Gb

Max egress for general purpose v1 is 20 Gbps. Its 50 Gbps for general purpose v2

From azure portal the metric is shown as GB But in the limit documentation it is mentioned as Gbps ???

**- Max ingress limits for storage account**

Max ingress: 127.5 MB = 1020 Mb

Max ingress per storage account in the regions other than US and Europe 5 Gbps

Success server latency: 1.4 Min at 3 PM on Aug 19, Aug 6

Check list to have for the improved blob performance [https://docs.microsoft.com/en-us/azure/storage/blobs/storage-performance-checklist#checklist](https://docs.microsoft.com/en-us/azure/storage/blobs/storage-performance-checklist#checklist)

#### **Queries to Azure Support team:** <a href="#id-444jdfr9wiya" id="id-444jdfr9wiya"></a>

1. What is the best approach to migrate a storage account from General purpose v1 to General purpose v2 without downtime?
2. Understanding metrics from the azure monitor for Storage account with respect to Max egress and ingress limits. How can we configure alerts when it is reaching the limits?
3. What is the egress limit for block blob type?
4. How do we track and manage the SAS tokens generated for storage containers and blobs? There is no dashboard or table giving the details of SAS tokens generated so far
5. How to enable immutable blob storage features to avoid accidental deletion of data

#### **Bandwidth and operations per blob** <a href="#id-444jdfr9wiya" id="id-444jdfr9wiya"></a>

A single blob supports up to 500 requests per second. If you have multiple clients that need to read the same blob and you might exceed this limit, then consider using a block blob storage account. A block blob storage account provides a higher request rate, or I/O operations per second (IOPS).

Get the limits for block blob storage account. Talk to azure support team and get the details. Also how do we monitor these metrics?

**Partitioning**

Blob storage uses a range-based partitioning scheme for scaling and load balancing. Each blob has a partition key comprised of the full blob name (account+container+blob). The partition key is used to partition blob data into ranges. The ranges are then load-balanced across Blob storage.

For example, all blobs within a container can be served by a single server until the load on these blobs requires further rebalancing of the partition ranges. Similarly, a group of lightly loaded accounts with their names arranged in lexical order may be served by a single server until the load on one or all of these accounts require them to be split across multiple partition servers.

Each load-balancing operation may impact the latency of storage calls during the operation. The service's ability to handle a sudden burst of traffic to a partition is limited by the scalability of a single partition server until the load-balancing operation kicks in and rebalances the partition key range.

You can follow some best practices to reduce the frequency of such operations.

* If possible, use blob or block sizes greater than 4 MiB for standard storage accounts and greater than 256 KiB for premium storage accounts. Larger blob or block sizes automatically activate high-throughput block blobs. High-throughput block blobs provide high-performance ingest that is not affected by partition naming.
* Examine the naming convention you use for accounts, containers, blobs, tables, and queues. Consider prefixing account, container, or blob names with a three-digit hash using a hashing function that best suits your needs.
* If you organize your data using timestamps or numerical identifiers, make sure that you are not using an append-only (or prepend-only) traffic pattern. These patterns are not suitable for a range-based partitioning system. These patterns may lead to all traffic going to a single partition and limiting the system from effectively load balancing.

For example, if you have daily operations that use a blob with a timestamp such as _yyyymmdd_, then all traffic for that daily operation is directed to a single blob, which is served by a single partition server. Consider whether the per-blob limits and per-partition limits meet your needs, and consider breaking this operation into multiple blobs if needed. Similarly, if you store time series data in your tables, all traffic may be directed to the last part of the key namespace. If you are using numerical IDs, prefix the ID with a three-digit hash. If you are using timestamps, prefix the timestamp with the seconds value, for example, _ssyyyymmdd_. If your application routinely performs listing and querying operations, choose a hashing function that will limit your number of queries. In some cases, a random prefix may be sufficient.

As a best practice, to support scale storage account type should be of
