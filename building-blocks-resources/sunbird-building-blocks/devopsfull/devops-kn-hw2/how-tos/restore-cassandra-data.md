---
icon: elementor
---

# Restore Cassandra data

Scenario: We're taking backup ( snapshot of data from each node of the cluster with naming `node-1-data-DD-MM-YY` and uploading it to storage( in our case Azure Blob Storage). The following steps depict how to restore the data.

> Note: This works only on a cluster with the same number of nodes, which means if you have a 7 node cluster; To restore the data you need a 7 node cluster. Though you don't need the same size VM. For example, if you have a 16core 64G machine in prod for a single node, you need only 2 core 4G machines to restore the data. But the node count should be the same.

> Note: For the procedure to be clear, I am assuming that you are going to restore a 7 node cluster backup. Cassandra directory is `/var/lib/cassandra/` and Cassandra configuration file is `/etc/cassandra/cassandra.yaml`

Steps:

1. Download the data for each node respectively. Means node-1 data into the new node-1 machine and node-2 data in the new node-2, so on and so forth.

Follow the steps in all nodes

1. Stop the Cassandra cluster: `sudo systemctl stop cassandra`
2. Remove all data: `sudo rm -rf /var/lib/cassandra/*`
3. In every backup folder, there will a `tokenring.txt` file which contains the token ring for that node. Copy the content of that file and paste in `/etc/cassandra/cassandra.yaml` as `initial_token: <data copied>`.\
   Ref initial\_token: [![](https://docs.datastax.com/en/cassandra-oss/2.1/oxygen-webhelp/template/resources/images/favicon.ico)The cassandra.yaml configuration file](https://docs.datastax.com/en/cassandra-oss/2.1/cassandra/configuration/configCassandra\_yaml\_r.html#configCassandra\_yaml\_r\_\_initial\_token)
4. Change the permission of the cassandra directory\
   `sudo chown -R cassandra:cassandra /var/lib/cassandra`
5. Start Cassandra: `sudo systemctl start cassandra`\
   After some time, check `nodetool status` and all nodes should be `UN` status

Run in only one node

1. Restoring schema: In any node, go to `backupfolder/cassandra_backup/` there will be a `db_schema.sql` file.\
   To restore the schema: `cqlsh -f db_schema.sql`. Once that operation is done, follow the below steps.\
   \


Run in all nodes

1. Stop Cassandra: `sudo systemctl stop cassandra`
2. Download the restoration [script](https://raw.githubusercontent.com/project-sunbird/sunbird-devops/release-3.9.0/deploy/cassandra\_restore\_v2.py)
3. Restore the data: `sudo python3 ./cassandra_restore_v2.py --snapshotdir /path/to/backup_dir/cassandra_backup --datadirectory /var/lib/cassandra/data`\
   It'll run a bunch of operations, and copy the data into the Cassandra data folder.\
   Note: These copy operations are hard links, so you don't need double the space of data.
4. Check the data size\
   `du -sh /var/lib/cassandra/data`
5. Change the permission of data: `sudo chown -R cassandra:cassandra /var/lib/cassandra/*`
6. Start Cassandra `sudo systemctl start cassandra`

Note: if any of the Cassandra nodes didn't start do a stop and start Cassandra. This is because all the nodes started at the same time.
