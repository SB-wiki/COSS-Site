---
icon: elementor
---

# Adminutils on Sunbird

#### Introduction <a href="#introduction" id="introduction"></a>

* Adminutils service is used to issues two types of tokens -
  * Kong consumer tokens
  * Keycloak access token
* The source code of adminutils repo is located here - [![](https://github.com/fluidicon.png)GitHub - Sunbird-Lern/sunbird-apimanager-util: Wrapper for Kong admin util](https://github.com/Sunbird-Lern/sunbird-apimanager-util)
* For more information about the service, reach out to the [Sunbird-Lern](https://github.com/orgs/Sunbird-Lern/discussions) community forum.

#### Kong consumer tokens <a href="#kong-consumer-tokens" id="kong-consumer-tokens"></a>

* These tokens are issued in the mobile device register, desktop device register, portal anonymous and logged in user workflows. For an understanding on how this works, refer to this design doc -
  * [Kong JWT Tokens Design Proposal](https://project-sunbird.atlassian.net/wiki/spaces/DevOps/pages/1463746630)
  * [RBAC on Sunbird](https://project-sunbird.atlassian.net/wiki/spaces/DevOps/pages/2849308673)

#### Keycloak access token <a href="#keycloak-access-token" id="keycloak-access-token"></a>

* These tokens are issued when a user logs in on the mobile or portal. Desktop app login does not follow this workflow as of now and is yet to be implemented. For more details on how this works, refer to this design doc
  * [RBAC on Sunbird](https://project-sunbird.atlassian.net/wiki/spaces/DevOps/pages/2849308673)

#### Deployment Files / Process <a href="#deployment-files-process" id="deployment-files-process"></a>

* The deployment helm chart is present here - [![](https://github.com/fluidicon.png)sunbird-devops/kubernetes/helm\_charts/core/adminutils at master · project-sunbird/sunbird-devops](https://github.com/project-sunbird/sunbird-devops/tree/master/kubernetes/helm\_charts/core/adminutils)
* The related jenkins jobs are
  * Build/Core/Adminutils
  * ArtifcatUpload/Core/Adminutils
  * Deploy/Kubernetes/Adminutils
  * Deploy/Kubernetes/KongJWTAdminUtil

#### Token issue and signing process <a href="#token-issue-and-signing-process" id="token-issue-and-signing-process"></a>

* The service is injected with private keys. The key generation script can be found here - [![](https://github.com/fluidicon.png)sunbird-devops/private\_repo/ansible/inventory/dev/key-generate.sh at release-5.1.0 · project-sunbird/sunbird-devops](https://github.com/project-sunbird/sunbird-devops/blob/release-5.1.0/private\_repo/ansible/inventory/dev/key-generate.sh)
* During deployment these keys are injected into the pod as volume mounts. Refer to these ansible roles to understand how its being done -
  * [![](https://github.com/fluidicon.png)sunbird-devops/kubernetes/ansible/roles/mount-keys at master · project-sunbird/sunbird-devops](https://github.com/project-sunbird/sunbird-devops/tree/master/kubernetes/ansible/roles/mount-keys)
  * [![](https://github.com/fluidicon.png)sunbird-devops/kubernetes/ansible/roles/helm-deploy at master · project-sunbird/sunbird-devops](https://github.com/project-sunbird/sunbird-devops/tree/master/kubernetes/ansible/roles/helm-deploy)
  * [![](https://github.com/fluidicon.png)sunbird-devops/kubernetes/ansible/roles/sunbird-deploy at master · project-sunbird/sunbird-devops](https://github.com/project-sunbird/sunbird-devops/tree/master/kubernetes/ansible/roles/sunbird-deploy)
  * [![](https://github.com/fluidicon.png)sunbird-devops/kubernetes/ansible/roles/kong-jwt-create-adminutil at master · project-sunbird/sunbird-devops](https://github.com/project-sunbird/sunbird-devops/tree/master/kubernetes/ansible/roles/kong-jwt-create-adminutil)
* When an API request arrives, the adminutils services creates the token and issues to the users. Refer to the adminutils source code and the key generation process
* In case of kong consumer api, a HS256 kong token is issued which gets created using the respective private keys -
  * For mobile - a random key is picked with the name mobile\_device
  * For desktop - a random key is picked with the name desktop\_device
  * For portal anonymous sessions - a random key is picked with the name portal\_anonymous
  * For portal logged in sessions - a random key is picked with the name portal\_loggedin
* In case of Keycloak token, a RS256 token is issues which gets created using the respective private keys -
  * For keycloak token - a random key is picked with the name access\_v1
* The private file names, number of keys, portal session variables etc are all controlled using these variables - [![](https://github.com/fluidicon.png)sunbird-devops/private\_repo/ansible/inventory/dev/Core/common.yml at release-5.1.0 · project-sunbird/sunbird-devops](https://github.com/project-sunbird/sunbird-devops/blob/release-5.1.0/private\_repo/ansible/inventory/dev/Core/common.yml#L446-L477)
* The consumers are controlled using these variables - [![](https://github.com/fluidicon.png)sunbird-devops/private\_repo/ansible/inventory/dev/Core/common.yml at release-5.1.0 · project-sunbird/sunbird-devops](https://github.com/project-sunbird/sunbird-devops/blob/release-5.1.0/private\_repo/ansible/inventory/dev/Core/common.yml#L366-L403)
* The mobile and portal invoke the refresh token api immediately after a user logs in and get a token issued by the adminutils service
  * This token would have a kid of the form access\_v1\_key\*
* The mobile, desktop and portal invoke the register api when the app is installed and opened for the first time or a browser session is opened. This token will have appropriate kid based on the type of device
  * portal\_anonymous\_key\* for portal anonymous sessions
  * portal\_loggedin\_key\* for portal loggedin sessions
  * desktop\_devicev2\_key\* for desktop register
  * mobile\_devicev2\_key\* for mobile device register
* All the services that require keycloak token verification are injected with the public keys. The public keys correspond to the private keys which have the file names of the form access\_v1\*
* The services will check the kid field in the token and use the appropriate public key file to validate the token.
* The public keys are created on the fly using the private key and are injected using this anisble role - [![](https://github.com/fluidicon.png)sunbird-devops/kubernetes/ansible/roles/mount-keys at master · project-sunbird/sunbird-devops](https://github.com/project-sunbird/sunbird-devops/tree/master/kubernetes/ansible/roles/mount-keys)
* Similarly the the kong consumer keys issued by the adminutils (desktop, mobile, portal anonymous and loggedin) are validated on the kong api gateway. The public key for these are created on the fly and onboarded to the kong as consumers.
* You can refer to the KongJWTAdminUtil job to understand how the public keys are created and onboarded. The ansible role that does this is located here - [![](https://github.com/fluidicon.png)sunbird-devops/kubernetes/ansible/roles/kong-jwt-create-adminutil at master · project-sunbird/sunbird-devops](https://github.com/project-sunbird/sunbird-devops/tree/master/kubernetes/ansible/roles/kong-jwt-create-adminutil)

#### Adminutils connections <a href="#adminutils-connections" id="adminutils-connections"></a>

* Mobile / Desktop → Nginx → Kong → Adminutils - For the mobile / desktop register API kong consumer token and refresh token API (Desktop doesn’t yet invoke the refresh token endpoint)
* Portal → Kong → Adminutils - For portal anonymous and loggedin kong consumer token and refresh token API
* Adminutils → Kong → Learner Service - For fetching user roles

#### Rotating the keys <a href="#rotating-the-keys" id="rotating-the-keys"></a>

* In order to rotate the keys, you can just run the key generate script to create a new set of keys and then commit to github and inject them to the pod.
* The key generate script is located here - [![](https://github.com/fluidicon.png)sunbird-devops/private\_repo/ansible/inventory/dev/key-generate.sh at release-5.1.0 · project-sunbird/sunbird-devops](https://github.com/project-sunbird/sunbird-devops/blob/release-5.1.0/private\_repo/ansible/inventory/dev/key-generate.sh)
* If old keys are replaced, all the user sessions will be invalidated and users will be logged out
* Another way is to generate new set of keys by incrementing the key number. We can still retain the old keys for only verification purpose. We should configure adminutils to issue tokens using only the new set of keys. Eventually, all the tokens will be signed only using the new keys. After this point, the old keys can be removed even from verification flows. But this would be a manual activity and has not been tested. It can be automated if required.
