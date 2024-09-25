---
icon: elementor
---

# ElasticSearch

Backup:

\#Install plugin:- sudo ES\_PATH\_CONF=/etc/elasticsearch//usr/share/elasticsearch/bin/elasticsearch-plugin install repository-azure

\#change the configuration: sudo vi /etc/elasticsearch//elasticsearch.yml cloud.azure.storage.default.account: xxxxxxxxxxx cloud.azure.storage.default.key: xxxxxx

\#Restart ES Service: sudo systemctl restart es-node-2\_elasticsearch.service

\#create Repo: curl -XPUT '[http://localhost:9200/\_snapshot/azurebackup](http://localhost:9200/\_snapshot/azurebackup)' -H 'Content-Type: application/json' -d '{ "type": "azure", "settings": { "container": "\<blob\_name>", "base\_path": "\<storage\_account\_name>"} }'

\#create Snapshot: curl -XPUT '[http://localhost:9200/\_snapshot/azurebackup/snapshot\_1](http://localhost:9200/\_snapshot/azurebackup/snapshot\_1)' -H 'Content-Type: application/json' -d '{ "indices":"\*","include\_global\_state":false }'

\#check status of backup curl -XGET '[http://localhost:9200/\_snapshot/azurebackup/\_all](http://localhost:9200/\_snapshot/azurebackup/\_all)'

Restore: #Install plugin:- sudo ES\_PATH\_CONF=/etc/elasticsearch/es-node-2 /usr/share/elasticsearch/bin/elasticsearch-plugin install repository-azure

\#change the configuration: sudo nano /etc/elasticsearch/es-node-2/elasticsearch.yml cloud.azure.storage.default.account: xxxxxxxxxxx cloud.azure.storage.default.key: xxxxxx

\#Restart ES Service: sudo systemctl restart es-node-2\_elasticsearch.service

\#create Repo: curl -XPUT '[http://localhost:9200/\_snapshot/azurebackup](http://localhost:9200/\_snapshot/azurebackup)' -H 'Content-Type: application/json' -d '{ "type": "azure", "settings": { "container": "\<blob\_name>", "base\_path": "\<storage\_account\_name>"} }'

\#Delete unwanted indices curl -XDELETE '[http://localhost:9200/\_all](http://localhost:9200/\_all)'

\#Restore from snapshot curl -XPOST '[http://localhost:9200/\_snapshot/azurebackup/snapshot\_1/\_restore](http://localhost:9200/\_snapshot/azurebackup/snapshot\_1/\_restore)'

\#To check the status of snapshot restore curl -s "[http://localhost:9200/\_snapshot/azurebackup/snapshot\_1/\_status?pretty](http://localhost:9200/\_snapshot/azurebackup/snapshot\_1/\_status?pretty)"

***

\[\[category.storage-team]] \[\[category.confluence]]
