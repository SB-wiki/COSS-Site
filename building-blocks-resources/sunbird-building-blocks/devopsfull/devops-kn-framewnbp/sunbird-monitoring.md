---
icon: elementor
---

# Sunbird Monitoring

#### Monitoring System overview  <a href="#monitoring-system-overview" id="monitoring-system-overview"></a>

* We are using prometheus operator on Kubernetes to monitor the infrastructure and APIs. For more information on the operator, read here [![](https://github.com/fluidicon.png)GitHub - prometheus-operator/prometheus-operator: Prometheus Operator creates/configures/manages Prometheus clusters atop Kubernetes](https://github.com/prometheus-operator/prometheus-operator)
* The monitoring system system includes many components such as
  * Promethus
  * Grafana
  * Exporters such as node exporter, process exporter, jmx exporter, blackbox exporter etc,.
  * Alertmanager and alert rules
* Sunbird monitoring helm chart is located here - [![](https://github.com/fluidicon.png)sunbird-devops/kubernetes/helm\_charts/monitoring at master · project-sunbird/sunbird-devops](https://github.com/project-sunbird/sunbird-devops/tree/master/kubernetes/helm\_charts/monitoring)
* The system runs on Kubernetes and monitors both kubernetes and non kubernetes components
* Sunbird monitoring ansible role is located here - [![](https://github.com/fluidicon.png)sunbird-devops/kubernetes/ansible/roles/sunbird-monitoring at master · project-sunbird/sunbird-devops](https://github.com/project-sunbird/sunbird-devops/tree/master/kubernetes/ansible/roles/sunbird-monitoring)

#### High level architecture diagram <a href="#high-level-architecture-diagram" id="high-level-architecture-diagram"></a>



<figure><img src="../../../../.gitbook/assets/image-20230114-125438.png" alt=""><figcaption></figcaption></figure>



<figure><img src="../../../../.gitbook/assets/image-20230114-125504.png" alt=""><figcaption></figcaption></figure>

#### What resources are monitored? What metrics are scraped?  <a href="#what-resources-are-monitored-what-metrics-are-scraped" id="what-resources-are-monitored-what-metrics-are-scraped"></a>

* CPU usage of Pods and Nodes
* Memory usage of Pods and Nodes
* Disk usage of Pods and Nodes
* Network usage of Pods and Nodes
* Traffic and API metrics such as latency, request per second, request / response size
* Kafka consumer lag metrics
* Cassandra metrics such as heap, compactions, read and write etc
* Process metrics on the nodes
* Service endpoints and their health

For an exhaustive list of what all is being monitored, refer to the grafana dashboards.

#### What alert rules are configured <a href="#what-alert-rules-are-configured" id="what-alert-rules-are-configured"></a>

* Many alert rules are configured such as
* High cpu usage on nodes
* High memory usage on nodes
* High disk usage on nodes
* Increasing API latencies etc.

For an exhaustive list of alert rules, take a look at this helm chart - [![](https://github.com/fluidicon.png)sunbird-devops/kubernetes/helm\_charts/monitoring/alertrules at master · project-sunbird/sunbird-devops](https://github.com/project-sunbird/sunbird-devops/tree/master/kubernetes/helm\_charts/monitoring/alertrules)

#### What notifications are configured <a href="#what-notifications-are-configured" id="what-notifications-are-configured"></a>

* The above section (alert rules) are configured as notifications
* The notifications are sent to email and slack channel

#### Code base structure and explain what is what  <a href="#code-base-structure-and-explain-what-is-what" id="code-base-structure-and-explain-what-is-what"></a>

Monitoring chart is present here - [![](https://github.com/fluidicon.png)sunbird-devops/kubernetes/helm\_charts/monitoring at master · project-sunbird/sunbird-devops](https://github.com/project-sunbird/sunbird-devops/tree/master/kubernetes/helm\_charts/monitoring)

**additional-scrape-configs**

* This helm chart contains the prometheus scrape configuration, labels, interval and timeout

**alertrules**

* This helm chart contains the alert rules

**azure-ambari-prometheus-exporter**

* This helm chart is used to install ambari exporter which monitors the hadoop cluster like HDInsights

**blackbox-exporter**

* This helm chart is used to monitor service or http(s) endpoints and check if they are healthy or not

**cassandra-jmx-exporter**

* This helm chart is used to monitor cassandra clusters

**dashboards**

* This helm chart contains the grafana dashboards

**elasticsearch-exporter**

* This helm chart is used to monitor elasticsearch cluster

**ingestion-kafka-exporter**

* This helm chart is used to monitor ingestion kaka cluster

**json-path-exporter**

* This helm chart is used to scrape remote jsons and convert them to prometheus metrics

**kafka-exporter**

* This helm chart is used to monitor kafka clusters

**kafka-lag-exporter**

* This helm chart is used to monitor kafka topic / group lag

**kafka-topic-exporter**

* This helm chart is used to monitor kafka topics

**oauth2-proxy**

* This helm chart installs oauth2 proxy in the monitoring namespace

**processing-kafka-exporter**

* This helm chart is used to monitor processing kaka cluster

**prometheus-operator**

* This helm chart installs the prometheus operator along with grafana, node exporter, kube state metrics and alertmanager

**prometheus-redis-exporter**

* This helm chart is used to morning redis nodes

**statsd-exporter**

* This helm chart is used to monitor kong api metrics

**ansible role**

* The anible role install each of the helm chart in a loop
* The ansible role has a template file for each of the helm chart which is used to override environment specific values as well as overriding values specifically for sunbird as the charts are taken from upstream sources
* The role is located here - [![](https://github.com/fluidicon.png)sunbird-devops/kubernetes/ansible/roles/sunbird-monitoring at master · project-sunbird/sunbird-devops](https://github.com/project-sunbird/sunbird-devops/tree/master/kubernetes/ansible/roles/sunbird-monitoring)

#### Overriding the specs <a href="#overriding-the-specs" id="overriding-the-specs"></a>

* To override the spec, define the values defined in the template files in your private repo
* For example if you want to change the name of the monitoring stack, you can close the repo, change the value shown here as per your liking - [![](https://github.com/fluidicon.png)sunbird-devops/kubernetes/ansible/roles/sunbird-monitoring/templates/prometheus-operator.yaml at master · project-sunbird/sunbird-devops](https://github.com/project-sunbird/sunbird-devops/blob/master/kubernetes/ansible/roles/sunbird-monitoring/templates/prometheus-operator.yaml#L9)
* Deploy using the Jenkins job from your fork

#### Defining additional specs <a href="#defining-additional-specs" id="defining-additional-specs"></a>

* You can make use of the provided optional variables to define additional parameters
* For example if you want to have a PV for grafana, you can use this variable and define it in your private repo - [![](https://github.com/fluidicon.png)sunbird-devops/kubernetes/ansible/roles/sunbird-monitoring/templates/prometheus-operator.yaml at master · project-sunbird/sunbird-devops](https://github.com/project-sunbird/sunbird-devops/blob/master/kubernetes/ansible/roles/sunbird-monitoring/templates/prometheus-operator.yaml#L290-L292)
* To understand how to define these variable, refer to the subchart which it will be used. For example in case of the grafana persistence, you can find the definition here - [![](https://github.com/fluidicon.png)sunbird-devops/kubernetes/helm\_charts/monitoring/prometheus-operator/charts/grafana/values.yaml at master · project-sunbird/sunbird-devops](https://github.com/project-sunbird/sunbird-devops/blob/master/kubernetes/helm\_charts/monitoring/prometheus-operator/charts/grafana/values.yaml#L196-L207)
* Take a look at the other set of variables in the template files to understand the usage and capabilities

#### Deploying the monitoring stack  <a href="#deploying-the-monitoring-stack" id="deploying-the-monitoring-stack"></a>

* Use the jenkins job named **Monitoring** under the **Deploy/Kubernetes** directory folder.
* The variables defined in the private repo template under mandatory and optional should be filled which are required for the monitoring stack. Example - slack channel name, smtp configurations etc., if you plan to use the alerting capabilities

#### Service Monitoring <a href="#service-monitoring" id="service-monitoring"></a>

* Service monitoring is done using the service monitor files. Example - [![](https://github.com/fluidicon.png)sunbird-devops/kubernetes/helm\_charts/core/analytics/templates/serviceMonitor.yaml at master · project-sunbird/sunbird-devops](https://github.com/project-sunbird/sunbird-devops/blob/master/kubernetes/helm\_charts/core/analytics/templates/serviceMonitor.yaml)
* Service monitor is a CRD which is setup as part of the prometheus operator chart
* Service monitor uses the named port concept of Kubernetes to identify the port numbers

#### Backup and Restore <a href="#backup-and-restore" id="backup-and-restore"></a>

* There are no jobs or processed that are available to perform the backup and restore
* Take a look at this page to understand how you can manually do backup and restore - [Prometheus PV Backup and Restore on Kubernetes](https://project-sunbird.atlassian.net/wiki/spaces/DevOps/pages/3271164016)
* This can be automated in future to perform automated backup and restore

#### How to's?  <a href="#how-tos" id="how-tos"></a>

**Monitoring new resources**

* If a new node needs to be monitored then
  * Install node exporter on the VM using the **Opsadminstration/Bootstrap** Jenkins job
  * Add the IP of the node under the `node-exporter` ansible group in the inventory
  * Deploy the **Kubernetes/Monitoring** jenkins job with tag as `all`
* If a new service within Kubernetes needs to be monitored (which has the capability to directly emit prometheus metrics), then
  * Add a service monitor file in the helm chart (Already covered in previous section)
  * Redeploy the service

**Scrapping new metrics**&#x20;

* Prometheus automatically scrapes new metrics when the target is added in the configuration
* A target can be
  * An exporter endpoint (example: node exporter endpoint)
  * A service monitor endpoint (example: see service monitor file)

**Adding new dashboards**&#x20;

* To add a new dashboard
  * Go to grafana and create the dashboard
  * Export the dashboard as a json
  * Commit the json in this folder - [![](https://github.com/fluidicon.png)sunbird-devops/kubernetes/helm\_charts/monitoring/dashboards/dashboards at master · project-sunbird/sunbird-devops](https://github.com/project-sunbird/sunbird-devops/tree/master/kubernetes/helm\_charts/monitoring/dashboards/dashboards)
  * Add the dashboard name in values.yaml file under a `dashboards[0-9]` dictionary. Example - [![](https://github.com/fluidicon.png)sunbird-devops/kubernetes/helm\_charts/monitoring/dashboards/values.yaml at master · project-sunbird/sunbird-devops](https://github.com/project-sunbird/sunbird-devops/blob/master/kubernetes/helm\_charts/monitoring/dashboards/values.yaml#L401-L437)
  * Redeploy the monitoring stack using the jenkins job with the tag `dashboards`
  * Restart grafana pod manually if you don't see the changes reflected

**Modify existing dashboard**

* To modify an existing dashboard
  * Export the existing dashboard as a json
  * Import it back to grafana with a new name and a new uuid
  * Modify the dashboard as per your requirements
  * Export the modified dashboard as a json
  * Rename the dashboard file name to same as what is available on github
  * Edit the title to same as original dashboard - [![](https://github.com/fluidicon.png)sunbird-devops/kubernetes/helm\_charts/monitoring/dashboards/dashboards/api-manager.json at master · project-sunbird/sunbird-devops](https://github.com/project-sunbird/sunbird-devops/blob/master/kubernetes/helm\_charts/monitoring/dashboards/dashboards/api-manager.json#L2526)
  * Commit the modified dashboard
  * Redeploy the monitoring stack using the jenkins job with the tag `dashboards`
  * Restart grafana pod manually if you don't see the changes reflected

**How to add alert rules?**&#x20;

* Add new rules files or edit the existing rules file to include your new alert
* Alert rule files are here - [![](https://github.com/fluidicon.png)sunbird-devops/kubernetes/helm\_charts/monitoring/alertrules/templates at master · project-sunbird/sunbird-devops](https://github.com/project-sunbird/sunbird-devops/tree/master/kubernetes/helm\_charts/monitoring/alertrules/templates)

**How to add new service monitor?**&#x20;

* Add the service monitor file in the respective service helm chart templates folder
* See here for an example - [![](https://github.com/fluidicon.png)sunbird-devops/kubernetes/helm\_charts/core/analytics/templates/serviceMonitor.yaml at master · project-sunbird/sunbird-devops](https://github.com/project-sunbird/sunbird-devops/blob/master/kubernetes/helm\_charts/core/analytics/templates/serviceMonitor.yaml)

**How to add notification endpoints ? Mail, slack etc**&#x20;

* These can be added under the alert manager configurations.
* For email, see here - [![](https://github.com/fluidicon.png)sunbird-devops/kubernetes/ansible/roles/sunbird-monitoring/templates/prometheus-operator.yaml at master · project-sunbird/sunbird-devops](https://github.com/project-sunbird/sunbird-devops/blob/master/kubernetes/ansible/roles/sunbird-monitoring/templates/prometheus-operator.yaml#L71-L77)
* For slack, see here - [![](https://github.com/fluidicon.png)sunbird-devops/kubernetes/ansible/roles/sunbird-monitoring/templates/prometheus-operator.yaml at master · project-sunbird/sunbird-devops](https://github.com/project-sunbird/sunbird-devops/blob/master/kubernetes/ansible/roles/sunbird-monitoring/templates/prometheus-operator.yaml#L132-L137)
