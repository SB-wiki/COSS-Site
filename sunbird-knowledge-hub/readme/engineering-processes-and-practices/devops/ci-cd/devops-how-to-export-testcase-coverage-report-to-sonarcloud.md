---
icon: elementor
---

# DevOps : How to export Testcase coverage report to SonarCloud

We're using `jacoco.xml` to export code coverage report to sonarqube.

To check everything working fine, you can have a local sonarqube running and test against that.

### Steps to deploy a local sonarqube: <a href="#howtoexporttestcasecoveragereporttosonarcloud-stepstodeployalocalsonarqube" id="howtoexporttestcasecoveragereporttosonarcloud-stepstodeployalocalsonarqube"></a>

`docker run --rm -d --name sonarqube -p 9000:9000 sonarqube`

open browser → localhost:9000 → click on `login`

initial _username_ and _password_ will be **`admin`**

\


Click on the `create new project`



<figure><img src="../../../../../.gitbook/assets/image001.png" alt=""><figcaption></figcaption></figure>

Give a name for your project and click `setup`



<figure><img src="../../../../../.gitbook/assets/image003.png" alt=""><figcaption></figcaption></figure>

Generate a token

<figure><img src="../../../../../.gitbook/assets/image005.png" alt=""><figcaption></figcaption></figure>

Select your language



<figure><img src="../../../../../.gitbook/assets/image007.png" alt=""><figcaption></figcaption></figure>

copy the above command and run it in your project(above example is for maven projects)

After that you should see something like this, if your project is analysed properly

Note: you might have to refresh the page



<figure><img src="../../../../../.gitbook/assets/image011.png" alt=""><figcaption></figcaption></figure>

\


If you want to export a specific coverage report

```
mvn verify sonar:sonar \
-Dsonar.projectKey=data-pipeline \
-Dsonar.host.url=http://localhost:9000 \
-Dsonar.login=ed6b5431870626331d3c47e9f8240431d2843ade \
-Dsonar.coverage.jacoco.xmlReportPaths=/home/circleci/dp/data-pipeline/telemetry-location-updater/target/coverage-reports/jacoco-ut/jacoco.xml,/home/circleci/dp/data-pipeline/telemetry-validator/target/coverage-reports/jacoco-ut/jacoco.xml,/home/circleci/dp/data-pipeline/de-duplication/target/coverage-reports/jacoco-ut/jacoco.xml
```

**Adding SonarCloud Badge in the Github Repo:**



<figure><img src="../../../../../.gitbook/assets/image012.jpg" alt=""><figcaption></figcaption></figure>

Click on **Get project badges**



<figure><img src="../../../../../.gitbook/assets/image013.png" alt=""><figcaption></figcaption></figure>

Copy the URL and paste it in the Github repository README file.



<figure><img src="../../../../../.gitbook/assets/image016.jpg" alt=""><figcaption></figcaption></figure>
