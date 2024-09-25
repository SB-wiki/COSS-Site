---
icon: elementor
---

# Jenkins Configuration as code

Jenkins is the CI/CD tool that we use today.

**Problem statement**:

Jenkins maintainabliltiy:

* Jenkins Installation/upgradation
* Plugin installation/upgradation

Job Configuration:

* Jobs are getting created manually in dev
* Variable updates happen release on release
* Every release we’ve to copy the job created/changed to the staging jenkins
* Every GA release we’ve to cleanup entire jobs and publish to adopters

**Proposed solution:**

Run jenkins as a container in the machine, and mount the host volume (simplest)

Run jenkins in kubernetes cluster (so that automatically we can bring up clients for specific jobs, like for backup one set, deployment one set). This we’ll take as second step.

Keep Jenkins configuration in github, and use jenkins to update self ( via poll for change )

**Tools / Methods available for CaC:**

1. Jenkins Configuration as Code\
   [https://www.jenkins.io/projects/jcasc/](https://www.jenkins.io/projects/jcasc/)\
   https://github.com/jenkinsci/configuration-as-code-plugin
2. Use Ansible Module to update jenkins\
   https://docs.ansible.com/ansible/latest/collections/community/general/jenkins\_job\_module.html
