---
icon: elementor
---

# Setup and Configure CircleCI

**Setup and Configure Circleci**

1. Signin to circleci [https://circleci.com/gh/Sunbird-Ed](https://circleci.com/gh/Sunbird-Ed)
2. Setup new Project in Circleci (user should have admin access for repos to add project)

Select ADD PROJETS → Select Repo → Set Up Project

![](../../../../../.gitbook/assets/0%20\(1\).png)

1. Add Circleci config file in github Repo

Create a folder named .circleci and add a file config.yml (so that the filepath be in .circleci/config.yml).

1. Edit Config.yml file (sample config file [https://github.com/Sunbird-Ed/SunbirdEd-portal/blob/release-1.13/.circleci/config.yml](https://github.com/Sunbird-Ed/SunbirdEd-portal/blob/release-1.13/.circleci/config.yml))

(Configuration refference [https://circleci.com/docs/2.0/configuration-reference/](https://circleci.com/docs/2.0/configuration-reference/) )

1. Go to SETTINGS → Projects (Under Organization) select your project from the Followed Projects lists → settings → Advanced Settings (under Build Setting) mark enable(on) for below option

**Build forked pull requests**

**Pass secrets to builds from forked pull requests**

**Only build pull requests**

![](../../../../../.gitbook/assets/1.png)

1. Add Environment variables. Environment Variable(under Build Setting) → Add new variable (eg: CODACY\_PROJECT\_TOKEN)
2. Start Building (Add Projects → Set Up Project → Start Building)



**Questions to Consider:**

* How can you configure environment variables in the CI platform?
* What is the purpose of passing secrets to builds from forked pull requests?
* Which setting should be used to build only pull requests?
* What steps are involved in starting the build process for a new project?
* Why is it important to manage secrets when building forked pull requests?
