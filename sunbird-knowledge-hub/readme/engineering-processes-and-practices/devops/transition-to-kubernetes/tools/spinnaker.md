---
icon: elementor
---

# Spinnaker

#### Spinnaker is a application management and application deployment tool which has the capability of deploying various types of applications as well as manage / provison cloud infrastructure required for deployments  <a href="#spinnaker-spinnakerisaapplicationmanagementandapplicationdeploymenttoolwhichhasthecapabilityofdeploy" id="spinnaker-spinnakerisaapplicationmanagementandapplicationdeploymenttoolwhichhasthecapabilityofdeploy"></a>

#### **Pros:** <a href="#spinnaker-pros" id="spinnaker-pros"></a>

* Provisioning / Mananging the cloud infrastructure required for the deployment
* Application deployment
* Supports various deployment strategies
* Amazing pipeline for deployments which can even update the infrastructure
* Artifact promotion to various environments based on criterias set by us

#### **Cons:** <a href="#spinnaker-cons" id="spinnaker-cons"></a>

* Does not have build capability
* The provisioning / managing the infrastrucure during a deployment feature doesn't suit our use case or deployment strategy
* Many of the pipeline features provided (related to infra) may not be used by us

#### **Usage:** <a href="#spinnaker-usage" id="spinnaker-usage"></a>

* Application Management
* Application Deployment

#### **Application Management:** <a href="#spinnaker-applicationmanagement" id="spinnaker-applicationmanagement"></a>

* View and manage cloud resources
* Core concepts - Server group, Cluster, Application



**Server Group:**

* Deployable artifact - In our case docker image (Can be VM image)
* Other cofigurations like autoscaling policy, number of replicas etc.
* A deployment can consist a collection of all these and can include load balancers and firewalls associated with your deployment

**Cluster:**

* Logical group of server groups

**Application:**

* Collection of clusters

#### **Application Deployment:** <a href="#spinnaker-applicationdeployment" id="spinnaker-applicationdeployment"></a>

* Pipeline which consists of Stages
* Pipeline invocation from a trigger, cron schedule or manual
* Notifications via Email, Slack and SMS

![](https://www.spinnaker.io/concepts/pipelines.png)

![](https://www.spinnaker.io/concepts/pipelines/pipeline-tasks.png)

#### **Deployment Strategies:** <a href="#spinnaker-deploymentstrategies" id="spinnaker-deploymentstrategies"></a>

* Blue / Green
* Rolling
* Canary

![](https://www.spinnaker.io/concepts/deployment-strategies.png)

#### **Spinnaker Wokrflow** <a href="#spinnaker-spinnakerwokrflow" id="spinnaker-spinnakerwokrflow"></a>

#### ![](https://www.spinnaker.io/guides/tutorials/codelabs/hello-deployment/flow.png) <a href="#spinnaker" id="spinnaker"></a>

#### **Spinnaker Components** <a href="#spinnaker-spinnakercomponents" id="spinnaker-spinnakercomponents"></a>

![](http://static1.tothenew.com/blog/wp-content/uploads/2016/09/003.netflix-spinnaker-components-1024x552.png)

#### **Sample Application Page on Spinnaker** <a href="#spinnaker-sampleapplicationpageonspinnaker" id="spinnaker-sampleapplicationpageonspinnaker"></a>

![](https://www.spinnaker.io/concepts/clusters/clusters.png)

#### **Sample Pipeline UI on Spinnaker** <a href="#spinnaker-samplepipelineuionspinnaker" id="spinnaker-samplepipelineuionspinnaker"></a>

![](https://www.spinnaker.io/concepts/pipelines/edit-pipeline.png)

\
