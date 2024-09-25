---
icon: elementor
---

# Nginx on Sunbird

#### Introduction <a href="#introduction" id="introduction"></a>

* Nginx is a very popular reverse proxy that can scale well and requires minimum amount of resources
* On sunbird, we are using as an ingress endpoint. All traffic flows into the cluster via nginx proxy
* Nginx runs on the Kubernetes cluster
* We have two nginx service running within the Kubernetes cluster
  * Public facing nginx which serves on the domain name
  * Private facing nginx which is used to reach the kubernetes services from services which are running outside the kubernetes cluster
* The public facing nginx uses a public load balancer and the private facing nginx uses a internal load balancer
* The public facing nginx runs as a daemonset and the private facing nginx runs as a deployment on kubernetes

#### Jenkins Jobs <a href="#jenkins-jobs" id="jenkins-jobs"></a>

* The related jenkins jobs for nginx public and private are listed below
  * Build/Core/Proxy
  * ArtifactUpload/Core/Proxy
  * Deploy/Kubernetes/nginx-public-ingress
  * Deploy/Kubernetes/nginx-private-ingress

#### Ansible Roles and Helm Charts <a href="#ansible-roles-and-helm-charts" id="ansible-roles-and-helm-charts"></a>

* The related ansible roles and helm charts for nginx public and private are listed below
  * [![](https://github.com/fluidicon.png)sunbird-devops/kubernetes/helm\_charts/core/nginx-public-ingress at master · project-sunbird/sunbird-devops](https://github.com/project-sunbird/sunbird-devops/tree/master/kubernetes/helm\_charts/core/nginx-public-ingress)
  * [![](https://github.com/fluidicon.png)sunbird-devops/kubernetes/helm\_charts/core/nginx-private-ingress at master · project-sunbird/sunbird-devops](https://github.com/project-sunbird/sunbird-devops/tree/master/kubernetes/helm\_charts/core/nginx-private-ingress)
  * [![](https://github.com/fluidicon.png)sunbird-devops/kubernetes/ansible/roles/helm-deploy at master · project-sunbird/sunbird-devops](https://github.com/project-sunbird/sunbird-devops/tree/master/kubernetes/ansible/roles/helm-deploy)

#### SSL Renewal <a href="#ssl-renewal" id="ssl-renewal"></a>

* Nginx public ingress uses SSL to serve https traffic. The SSL details is stored in private repo. Below are the variables related to SSL
  * Nginx public ingress uses SSL to serve https traffic. The SSL details is stored in private repo. Below are the variables related to SSL
  * [![](https://github.com/fluidicon.png)sunbird-devops/private\_repo/ansible/inventory/dev/Core/secrets.yml at master · project-sunbird/sunbird-devops](https://github.com/project-sunbird/sunbird-devops/blob/master/private\_repo/ansible/inventory/dev/Core/secrets.yml#L37-L47)
  * Merge domain site key and certificate are missing in private repo templates as it is not required for adopters (required only if running a state SSO system)
  * Below are the variables that need to be defined for merge domain
  * `merge_proxy_server_name: # Example merge.dev.sunbird.org sunbird_subdomain_keycloak_base_url: "{{proto}}://{{merge_proxy_server_name}}/auth" merge_domain_status: true proxymerge_site_key: |+ -----BEGIN PRIVATE KEY----- proxymerge_site_crt: |+ -----BEGIN CERTIFICATE-----`
  * Merge domain workflow is used to to merge a state account and a personal account into one
  * For more information on the merge domain workflow, reach out to the [Sunbird-Ed](https://github.com/orgs/Sunbird-Ed/discussions) community
* SSL can be renewed in two ways - Manual and Automated
* Manual SSL procurement
  * You can purchase an SSL manually and update the certificate and key in private repo and deploy the below jenkins job to update the kubernetes secrets
  * Deploy/Kubernetes/BootstrapMinimal
  * After this, restart the nginx daemonset (it will auto restart, in case it doesn’t, please restart manually)
  * SSL procurement is a standard process and can be procured from many poplar sites such as [![](https://www.namecheap.com/assets/img/nc-icon/favicon.ico)Buy a domain name - Register cheap domain names from $0.99 - Namecheap](https://www.namecheap.com/) and [![](https://letsencrypt.org/favicon.ico)Let's Encrypt](https://letsencrypt.org/)
* Automated SSL procurement
  * We have created a kuberntes job which will automatically renew the SSL from Letsencrypt every 85 days once for both the regular domain and merge domain
  * The details of this can be found here - [![](https://github.com/fluidicon.png)LetsEncrypt SSL Auto Renewal · project-sunbird sunbird-devops · Discussion #3439](https://github.com/project-sunbird/sunbird-devops/discussions/3439)

#### Nginx Public and Private Location Blocks <a href="#nginx-public-and-private-location-blocks" id="nginx-public-and-private-location-blocks"></a>

* There are various location blocks in both nginx public and private
* The location blocks can be found here
  * Nginx Public - [![](https://github.com/fluidicon.png)sunbird-devops/kubernetes/helm\_charts/core/nginx-public-ingress/values.j2 at master · project-sunbird/sunbird-devops](https://github.com/project-sunbird/sunbird-devops/blob/master/kubernetes/helm\_charts/core/nginx-public-ingress/values.j2)
  * Nginx Private - [![](https://github.com/fluidicon.png)sunbird-devops/kubernetes/helm\_charts/core/nginx-private-ingress/templates/configmap.yaml at master · project-sunbird/sunbird-devops](https://github.com/project-sunbird/sunbird-devops/blob/master/kubernetes/helm\_charts/core/nginx-private-ingress/templates/configmap.yaml)
* Refer to the nginx documentation to understand all the parameters of a location blocks - [![](https://nginx.org/favicon.ico)nginx documentation](https://nginx.org/en/docs/)

#### Nginx Build Process <a href="#nginx-build-process" id="nginx-build-process"></a>

* The default nginx image does not expose prometheus metrics
* We build nginx from source to include the prometheus lua module in order to enable prometheus metrics
* The build files are located here - [![](https://github.com/fluidicon.png)sunbird-devops/images/proxy at master · project-sunbird/sunbird-devops](https://github.com/project-sunbird/sunbird-devops/tree/master/images/proxy)
* Refer to the Jenkinsfile and Jenkinsjob to understand the build process

#### Nginx Public Prometheus Metrics and Dashboards <a href="#nginx-public-prometheus-metrics-and-dashboards" id="nginx-public-prometheus-metrics-and-dashboards"></a>

* We get various metrics from nginx such as request per second, error codes etc.
* All these are made available using the prometheus lua module which is injected during the build process
* Here is a sample metrics block defined in the nginx configuration - [![](https://github.com/fluidicon.png)sunbird-devops/kubernetes/helm\_charts/core/nginx-public-ingress/values.j2 at master · project-sunbird/sunbird-devops](https://github.com/project-sunbird/sunbird-devops/blob/master/kubernetes/helm\_charts/core/nginx-public-ingress/values.j2#L1051-L1064)
* Here are some of the grafana dashboards that use the nginx metrics
  * [![](https://github.com/fluidicon.png)sunbird-devops/kubernetes/helm\_charts/monitoring/dashboards/dashboards/nginx-detailed.json at master · project-sunbird/sunbird-devops](https://github.com/project-sunbird/sunbird-devops/blob/master/kubernetes/helm\_charts/monitoring/dashboards/dashboards/nginx-detailed.json)
  * [![](https://github.com/fluidicon.png)sunbird-devops/kubernetes/helm\_charts/monitoring/dashboards/dashboards/nginx.json at master · project-sunbird/sunbird-devops](https://github.com/project-sunbird/sunbird-devops/blob/master/kubernetes/helm\_charts/monitoring/dashboards/dashboards/nginx.json)
  * [![](https://github.com/fluidicon.png)sunbird-devops/kubernetes/helm\_charts/monitoring/dashboards/dashboards/dashboard-all.json at master · project-sunbird/sunbird-devops](https://github.com/project-sunbird/sunbird-devops/blob/master/kubernetes/helm\_charts/monitoring/dashboards/dashboards/dashboard-all.json)
* The metrics are also recorded on a regular basis using the prometheus recording rules. The recording rule file is located here - [![](https://github.com/fluidicon.png)sunbird-devops/kubernetes/helm\_charts/core/nginx-public-ingress/templates/recordingRules.yaml at master · project-sunbird/sunbird-devops](https://github.com/project-sunbird/sunbird-devops/blob/master/kubernetes/helm\_charts/core/nginx-public-ingress/templates/recordingRules.yaml)

#### Nginx Caching <a href="#nginx-caching" id="nginx-caching"></a>

* We have enabled caching of various assets in nginx
* The caching block is defined here - [![](https://github.com/fluidicon.png)sunbird-devops/kubernetes/helm\_charts/core/nginx-public-ingress/values.j2 at master · project-sunbird/sunbird-devops](https://github.com/project-sunbird/sunbird-devops/blob/master/kubernetes/helm\_charts/core/nginx-public-ingress/values.j2#L1094-L1110)
* Here is a sample API that uses the cache - [![](https://github.com/fluidicon.png)sunbird-devops/kubernetes/helm\_charts/core/nginx-public-ingress/values.j2 at master · project-sunbird/sunbird-devops](https://github.com/project-sunbird/sunbird-devops/blob/master/kubernetes/helm\_charts/core/nginx-public-ingress/values.j2#L221-L232)
* To know more about how nginx caching works, refer to these docs -
  * [![](https://nginxblog-8de1046ff5a84f2c-endpoint.azureedge.net/blobnginxbloga72cde487e/wp-content/uploads/2024/05/cropped-NGINX-product-square-2-32x32.png)A Guide to Caching with NGINX and NGINX Plus](https://www.nginx.com/blog/nginx-caching-guide/)
  * [![](https://docs.nginx.com/images/favicon-48x48.ico)NGINX Content Caching](https://docs.nginx.com/nginx/admin-guide/content-cache/content-caching/)
* The cache validity can be customized using this dictionary - [![](https://github.com/fluidicon.png)sunbird-devops/kubernetes/ansible/roles/helm-deploy/defaults/main.yml at master · project-sunbird/sunbird-devops](https://github.com/project-sunbird/sunbird-devops/blob/master/kubernetes/ansible/roles/helm-deploy/defaults/main.yml#L40-L63)

#### Nginx Mirroring <a href="#nginx-mirroring" id="nginx-mirroring"></a>

* We can use nginx mirroring feature in case we want to monitor what request headers, payload etc are being sent by a client
* Nginx mirror block is defined here - [![](https://github.com/fluidicon.png)sunbird-devops/kubernetes/helm\_charts/core/nginx-public-ingress/values.j2 at master · project-sunbird/sunbird-devops](https://github.com/project-sunbird/sunbird-devops/blob/master/kubernetes/helm\_charts/core/nginx-public-ingress/values.j2#L1217-L1236)
* For details on how mirroring works, refer this docs - [![](https://nginx.org/favicon.ico)Module ngx\_http\_mirror\_module](https://nginx.org/en/docs/http/ngx\_http\_mirror\_module.html)
* Usually we will deploy an echo service as the backend for the mirroring block
* The echo service will dump all the data such as headers, payload etc on the stdout. These can be then analysed using Graylog as these logs also will be pushed to the log stack
* Mirroring should be enabled with utmost care as this will cause the below
  * Access and Bearer tokens will also be displayed in stdout logs. These need to be masked before ingesting into Log ES using Graylog pipelines or it should be disabled from emitting in the echo service itself. If someone gets hold onto these tokens, they will be able to spoof as that user
  * There would be too much data from the echo service stdout logs. This will cause huge load on the graylog and Log ES cluster in terms of CPU and disk. Based on the load, the clusters may need to be scaled up

#### Nginx GeoIP <a href="#nginx-geoip" id="nginx-geoip"></a>

* Using a combination of geoip module and maxmind geoip database, traffic from certain countries can be blocked
* The GeoIP module is also an external lua module that get injected during the build phase. The code for this located here - [![](https://github.com/fluidicon.png)sunbird-devops/images/proxy at master · project-sunbird/sunbird-devops](https://github.com/project-sunbird/sunbird-devops/tree/master/images/proxy)
* The relevant configuration blocks for these are located here
  * [![](https://github.com/fluidicon.png)sunbird-devops/kubernetes/helm\_charts/core/nginx-public-ingress/values.j2 at master · project-sunbird/sunbird-devops](https://github.com/project-sunbird/sunbird-devops/blob/master/kubernetes/helm\_charts/core/nginx-public-ingress/values.j2#L1010-L1024)
  * [![](https://github.com/fluidicon.png)sunbird-devops/kubernetes/helm\_charts/core/nginx-public-ingress/values.j2 at master · project-sunbird/sunbird-devops](https://github.com/project-sunbird/sunbird-devops/blob/master/kubernetes/helm\_charts/core/nginx-public-ingress/values.j2#L73-L80)
  * [![](https://github.com/fluidicon.png)sunbird-devops/kubernetes/helm\_charts/core/nginx-public-ingress/values.j2 at master · project-sunbird/sunbird-devops](https://github.com/project-sunbird/sunbird-devops/blob/master/kubernetes/helm\_charts/core/nginx-public-ingress/values.j2#L101-L108)
* We will return the response code as 444 for requests that get originated from the countries which are blocked
* The deployment Jenkinsfile along with the ansible roles for the GeoIP module injection into nginx pubic is not available in to public repo yet. These need to be sourced and published from the Diksha’s private repo.
* Providing the file names here so that these can be published at a later date
  * `ansible/nginx-k8s-custom.yml pipelines/proxy/Jenkinsfile.k8s ansible/roles/nginx-k8s-custom`
* This will also require the maxmind geoip db to present in artifact storage bucket. The name of the artifact should be `GeoIP2-City.mmdb` or can be changed as per the inventory or Jenkinsfile variable

#### Nginx Private <a href="#nginx-private" id="nginx-private"></a>

* The nginx private ingress is used by services outside of the Kubernetes so that they can connect to services within the kubernetes cluster
* As an example of this workflow
  * Keycloak → Nginx Private → Learner
  * Flink Job → Nginx Private → Content Service
* The dev teams also use the nginx private to directly reach their service to test the API’s during development phase
* The nginx private is made available using a private loadbalancer ip and is accessible when connected to VPN
* This service should be never exposed to public as it will allow anyone to directly reach any service without any authentication
* The private load balancer configuration is defined using this variable
  * [![](https://github.com/fluidicon.png)sunbird-devops/kubernetes/helm\_charts/core/nginx-private-ingress/values.j2 at master · project-sunbird/sunbird-devops](https://github.com/project-sunbird/sunbird-devops/blob/master/kubernetes/helm\_charts/core/nginx-private-ingress/values.j2#L21)
  * [![](https://github.com/fluidicon.png)sunbird-devops/private\_repo/ansible/inventory/dev/Core/common.yml at master · project-sunbird/sunbird-devops](https://github.com/project-sunbird/sunbird-devops/blob/master/private\_repo/ansible/inventory/dev/Core/common.yml#L39-L53)
* There are no prometheus metrics configured for nginx private. But these can be enabled if required as the docker image is same as the nginx public. So the docker image already has all the required lua modules for prometheus and Geoip
