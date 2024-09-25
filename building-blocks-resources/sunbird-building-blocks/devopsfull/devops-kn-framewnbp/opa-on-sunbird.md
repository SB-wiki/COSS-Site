---
icon: elementor
---

# Opa on Sunbird

#### Introduction <a href="#introduction" id="introduction"></a>

* OPA is a short form for open policy agent
* OPA is a cncf graduated project that is generally used for evaluating policies
* We are using opa on sunbird to perform API checks such as role check, organisation check, user check etc
* For more details on opa, see here - [![](https://www.openpolicyagent.org/favicon.png)Introduction](https://www.openpolicyagent.org/docs/latest/)
* Envoy is a high perform proxy which receives the traffic in the pod and then makes an api call to opa to check if the request should be allowed or not
* The opa team has written an envoy-opa plugin which allows this authorization check possible in envoy
* For more details take a loo at this github repo - [![](https://github.com/fluidicon.png)GitHub - open-policy-agent/opa-envoy-plugin: A plugin to enforce OPA policies with Envoy](https://github.com/open-policy-agent/opa-envoy-plugin)
* For understanding envoy proxy and its configurations, refer to the envoy proxy docs - [![](https://www.envoyproxy.io/favicon.ico)Envoy proxy - home](https://www.envoyproxy.io/)

#### Opa Implementation Details <a href="#opa-implementation-details" id="opa-implementation-details"></a>

* For details and design doc on how opa is implemented, see this doc (check out the slide deck first that is mentioned on this page and then the contents of the page) - [RBAC on Sunbird](https://project-sunbird.atlassian.net/wiki/spaces/DevOps/pages/2849308673)
* For details on how to run opa locally, perform policy checks etc., see this video - [![](https://www.youtube.com/s/desktop/adbeefa1/img/favicon\_32x32.png)Opa on Sunbird](https://youtu.be/RwuRH-KRxic)

#### Opa Policy Files <a href="#opa-policy-files" id="opa-policy-files"></a>

* Opa polices are located here - [![](https://github.com/fluidicon.png)sunbird-devops/kubernetes/opa at master · project-sunbird/sunbird-devops](https://github.com/project-sunbird/sunbird-devops/tree/master/kubernetes/opa)
* The policies are segregated based on the service name (same as helm chart names)
* The `common` folder is where all the common files and checks reside that can be utilised by any other polices.
* The `main.rego` is the entry point for the code
* The `policies.rego` is the service specific policy file
* The `common.rego` is the common set of policy functions and checks
* The `policies_test.rego` is the test case file where every policy will have a corresponding test case

#### Opa Test Case and Coverage <a href="#opa-test-case-and-coverage" id="opa-test-case-and-coverage"></a>

* Every opa polciy should have a test case written
* A wrong policy can cause issues and can potentially block or allow requests that were not supposed to be blocked or allowed.
* Every test case should pass (be it allowed condition or deny condition)
* Code coverage should be 100% for both the service policies and common policies
* Without 100% code coverage and test case for every API, the deployment will fail
* Test case and code coverage should be implemented for both the type of policies
  * Common policies
  * Service policies
* Care should be taken when making changes to the common policies as that would affect all other service.
* Most issues will get identified during test case or code coverage phase, but its not guaranteed. A user must also self validate the policy to be 100% sure of the policy code
* The ansible role for opa test case and code coverage is located here - [![](https://github.com/fluidicon.png)sunbird-devops/kubernetes/ansible/roles/opa-test-coverage at master · project-sunbird/sunbird-devops](https://github.com/project-sunbird/sunbird-devops/tree/master/kubernetes/ansible/roles/opa-test-coverage)
* We can enable or disable the test case and code coverage mandate using these variables (not recommended as this can cause issues in case of a incorrect policy) - [![](https://github.com/fluidicon.png)sunbird-devops/ansible/roles/stack-sunbird/defaults/main.yml at master · project-sunbird/sunbird-devops](https://github.com/project-sunbird/sunbird-devops/blob/master/ansible/roles/stack-sunbird/defaults/main.yml#L1037)

#### OPA Enabled Services <a href="#opa-enabled-services" id="opa-enabled-services"></a>

* The following services have opa enabled
  * analytics
  * certregistry
  * content
  * knowledgemw
  * learner
  * lms
  * notification
  * registry
  * report
* To understand what all APIs are having opa check, take a look at the policy file
* For example, in the `knowledgemw` service, these are the APIs that have opa checks enabled - [![](https://github.com/fluidicon.png)sunbird-devops/kubernetes/opa/knowledgemw/policies.rego at master · project-sunbird/sunbird-devops](https://github.com/project-sunbird/sunbird-devops/blob/master/kubernetes/opa/knowledgemw/policies.rego#L9-L22)
* We can enable and disable opa for the services using these variables (not recommended as this will stop the API policy checks) - [![](https://github.com/fluidicon.png)sunbird-devops/ansible/roles/stack-sunbird/defaults/main.yml at master · project-sunbird/sunbird-devops](https://github.com/project-sunbird/sunbird-devops/blob/master/ansible/roles/stack-sunbird/defaults/main.yml#L1039-L1046)
* As desktop apps do not yet invoke the refresh token endpoint after login, the desktop keyclaok access tokens do not have the role injected into them. So desktop apps are skipped from opa checks.
* Desktop app policy checks are skipped using this block and variable
  * [![](https://github.com/fluidicon.png)sunbird-devops/kubernetes/opa/common/main.rego at master · project-sunbird/sunbird-devops](https://github.com/project-sunbird/sunbird-devops/blob/master/kubernetes/opa/common/main.rego#L65-L75)
  * [![](https://github.com/fluidicon.png)sunbird-devops/kubernetes/opa/common/main.rego at master · project-sunbird/sunbird-devops](https://github.com/project-sunbird/sunbird-devops/blob/master/kubernetes/opa/common/main.rego#L38)
  * [![](https://github.com/fluidicon.png)sunbird-devops/private\_repo/ansible/inventory/dev/Core/common.yml at release-5.1.0 · project-sunbird/sunbird-devops](https://github.com/project-sunbird/sunbird-devops/blob/release-5.1.0/private\_repo/ansible/inventory/dev/Core/common.yml#L471)
* We identify the kong consumer name and skip the check. All desktop apps are issued the desktop consumer key during the desktop register workflow.
* The checks for desktop app needs to be enabled once the dev team implements to refresh token api call in desktop login workflow.

#### Deployment Jobs, Ansible Roles, Helm Charts <a href="#deployment-jobs-ansible-roles-helm-charts" id="deployment-jobs-ansible-roles-helm-charts"></a>

* The existing helm charts are modified to include the opa and envoy side cars
* Take a look at this file to understand the side cars - [![](https://github.com/fluidicon.png)sunbird-devops/kubernetes/helm\_charts/core/analytics/templates/deployment.yaml at master · project-sunbird/sunbird-devops](https://github.com/project-sunbird/sunbird-devops/blob/master/kubernetes/helm\_charts/core/analytics/templates/deployment.yaml)
* There is also an init container section which routes all the inbound traffic to envoy by rewriting the iptable rules - [![](https://github.com/fluidicon.png)sunbird-devops/kubernetes/helm\_charts/core/analytics/templates/deployment.yaml at master · project-sunbird/sunbird-devops](https://github.com/project-sunbird/sunbird-devops/blob/master/kubernetes/helm\_charts/core/analytics/templates/deployment.yaml#L115-L134)
* Envoy configuration per service is located in the respective helm chart templates folder - [![](https://github.com/fluidicon.png)sunbird-devops/kubernetes/helm\_charts/core/analytics/templates/envoy-config.yaml at master · project-sunbird/sunbird-devops](https://github.com/project-sunbird/sunbird-devops/blob/master/kubernetes/helm\_charts/core/analytics/templates/envoy-config.yaml)
* Envoy will bypass opa check for prometheus metrics endpoints and health check urls. Rest all endpoints are sent to opa for check
* Deployment roles are modified to include opa as a side car. The deployment ansible role create a file named `bundle.tar.gz` as a configmap which gets injected as a volumen mount into the respective pods
* The deployment code is present here -
  * [![](https://github.com/fluidicon.png)sunbird-devops/kubernetes/ansible/roles/sunbird-deploy/tasks/main.yml at master · project-sunbird/sunbird-devops](https://github.com/project-sunbird/sunbird-devops/blob/master/kubernetes/ansible/roles/sunbird-deploy/tasks/main.yml#L21-L24)
  * [![](https://github.com/fluidicon.png)sunbird-devops/kubernetes/ansible/roles/sunbird-deploy/tasks/main.yml at master · project-sunbird/sunbird-devops](https://github.com/project-sunbird/sunbird-devops/blob/master/kubernetes/ansible/roles/sunbird-deploy/tasks/main.yml#L56-L70)
* The same jobs that deploy the service are used to deploy opa and envoy sidecars. There are no additional jobs for this. All these controlled using the one single opa enable / disable variable.

#### OPA and Envoy Metrics <a href="#opa-and-envoy-metrics" id="opa-and-envoy-metrics"></a>

* Opa and envoy directly expose prometheus metrics
* These are enabled using the service monitor file - [![](https://github.com/fluidicon.png)sunbird-devops/kubernetes/helm\_charts/core/analytics/templates/serviceMonitor.yaml at master · project-sunbird/sunbird-devops](https://github.com/project-sunbird/sunbird-devops/blob/master/kubernetes/helm\_charts/core/analytics/templates/serviceMonitor.yaml)
* The dashboards for opa and envoy are -
  * [![](https://github.com/fluidicon.png)sunbird-devops/kubernetes/helm\_charts/monitoring/dashboards/dashboards/envoy-global.json at master · project-sunbird/sunbird-devops](https://github.com/project-sunbird/sunbird-devops/blob/master/kubernetes/helm\_charts/monitoring/dashboards/dashboards/envoy-global.json)
  * [![](https://github.com/fluidicon.png)sunbird-devops/kubernetes/helm\_charts/monitoring/dashboards/dashboards/envoy-proxy.json at master · project-sunbird/sunbird-devops](https://github.com/project-sunbird/sunbird-devops/blob/master/kubernetes/helm\_charts/monitoring/dashboards/dashboards/envoy-proxy.json)
  * [![](https://github.com/fluidicon.png)sunbird-devops/kubernetes/helm\_charts/monitoring/dashboards/dashboards/opa-metrics.json at master · project-sunbird/sunbird-devops](https://github.com/project-sunbird/sunbird-devops/blob/master/kubernetes/helm\_charts/monitoring/dashboards/dashboards/opa-metrics.json)
* Alerts for opa and envoy errors are located here - [![](https://github.com/fluidicon.png)sunbird-devops/kubernetes/helm\_charts/monitoring/alertrules/templates/opa\_envoy\_403\_alerts.yaml at master · project-sunbird/sunbird-devops](https://github.com/project-sunbird/sunbird-devops/blob/master/kubernetes/helm\_charts/monitoring/alertrules/templates/opa\_envoy\_403\_alerts.yaml)

#### OPA Custom Logs Plugin <a href="#opa-custom-logs-plugin" id="opa-custom-logs-plugin"></a>

* We have written a custom opa plugin for enabling and disabling the logs from opa along with decoding token data and displaying it as text and removed the actual token from logs
* We can use the default opa logs plugin to enable or disable the logs. But it cannot mask certain fields so all the headers including bearer and access tokens are displayed in stdout and stored in graylog as logs.
* We added a new plugin to opa to decode the token data and send to stdout along with removing the actual tokens from logs
* The plugin code is located here - [![](https://github.com/fluidicon.png)sunbird-devops/kubernetes/opa-plugins at master · project-sunbird/sunbird-devops](https://github.com/project-sunbird/sunbird-devops/tree/master/kubernetes/opa-plugins)
* The instructions on how to build the opa image with this plugin is available in the readme file - [![](https://github.com/fluidicon.png)sunbird-devops/kubernetes/opa-plugins/README.md at master · project-sunbird/sunbird-devops](https://github.com/project-sunbird/sunbird-devops/blob/master/kubernetes/opa-plugins/README.md)
* The plugin when enabled sends the logs to stdout only for the failed / blocked API requests. It will not write any logs for successful API checks.
* If we want to disable logging even for failed api check, it can be done using this parameter - [![](https://github.com/fluidicon.png)sunbird-devops/kubernetes/helm\_charts/core/analytics/templates/deployment.yaml at master · project-sunbird/sunbird-devops](https://github.com/project-sunbird/sunbird-devops/blob/master/kubernetes/helm\_charts/core/analytics/templates/deployment.yaml#L97) and setting it to `false`

#### OPA Logs Searching <a href="#opa-logs-searching" id="opa-logs-searching"></a>

* In graylog all opa specific logs start with `opa_` keyword
* For example, in order to search all the logs that have been rejected by opa, we can use this query on graylog `opa_result_allowed: false` and then further drill down from there using other fields
* The log will also contain information about the API endpoint, roles of the user, userid of the user, other headers and payloads, token validity etc.,
* By using these information and cross check the policy definition, we can easily identify why a request was rejected.
