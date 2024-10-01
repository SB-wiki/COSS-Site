---
icon: elementor
---

# Setup Sonar Cloud

Adding new project for analysis.

Login to sonarcloud with Admin privileges. Click on new project.

![](../../../../../.gitbook/assets/1878982657.png)

Select the github repo and the programming language used and select the CI as CircleCI. Then it will give the sample config and token as below, copy the token and add in circleci env variables for the particular project.

![](../../../../../.gitbook/assets/1871970399.png)

### Sample sonarcloud config for JS/TS language: <a href="#sonarcloud-samplesonarcloudconfigforjs-tslanguage" id="sonarcloud-samplesonarcloudconfigforjs-tslanguage"></a>

Create a file by name **sonar-project.properties** in root of the repo and update the below info.

```
sonar.projectName=
sonar.language=
sonar.sources=.
sonar.typescript.lcov.reportPaths=
sonar.projectKey=
sonar.host.url=https://sonarcloud.io
sonar.organization=
sonar.projectVersion=1.0
```

Run sonar-scanner command in circleci config file, it will read all details from this file.

### Sample sonarcloud config for JAVA language: <a href="#sonarcloud-samplesonarcloudconfigforjavalanguage" id="sonarcloud-samplesonarcloudconfigforjavalanguage"></a>

Add this step in CircleCI by updating all the required parameters.

```
 name: sonar
 command: |
    mvn verify -Dlog4j.configuration=./logs sonar:sonar -Dsonar.projectKey=project-sunbird_sunbird-data-pipeline -Dsonar.organization=project-sunbird -Dsonar.host.url=https://sonarcloud.io -Dsonar.coverage.jacoco.xmlReportPaths=/home/circleci/dp/data-pipeline/assessment-aggregator/target/coverage-reports/jacoco-ut/jacoco.xml
```

Note: If you’re creating a token for `SONAR_TOKEN` env variable in circleci, please make sure, that you(sonar cloud user) has `execute analysis` in [roles](https://sonarcloud.io/organizations/sunbird-ed/permissions)

Ref: [https://community.sonarsource.com/t/error-youre-not-authorized-to-run-analysis-please-contact-the-project-administrator/11979](https://community.sonarsource.com/t/error-youre-not-authorized-to-run-analysis-please-contact-the-project-administrator/11979)



### Frequently Asked Questions

1. **What is the purpose of the `sonar` step in CircleCI?**
2. **How can I set the `SONAR_TOKEN` environment variable in CircleCI?**
3. **What permissions are required for the SonarCloud user to execute the analysis?**
4. **Where can I specify the project key and organization for SonarCloud analysis?**
5. **How do I ensure that the coverage report paths are correctly set for SonarQube analysis?**
6. **What should I do if I encounter authorization errors during analysis?**
