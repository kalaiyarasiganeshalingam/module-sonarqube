[![Build Status](https://travis-ci.org/wso2-ballerina/module-sonarqube.svg?branch=master)](https://travis-ci.org/wso2-ballerina/module-sonarqube)

# SonarQube Connector

SonarQube connector provides a Ballerina API to access the [SonarQube REST API](https://docs.sonarqube.org/display/DEV/Web+API)

## Compatibility

| Ballerina Language Version       | API Version     |
|:--------------------------------:|:---------------:|
| 0.991.0                          | 6.7.2           |

## Getting started

1.  Refer [Getting Strated Guide](https://stage.ballerina.io/learn/getting-started/) to download and install Ballerina.
2.  To use SonarQube endpoint, you need to provide the following:

       - SonarQube URL
       - SonarQube token
    
       Refer [SonarQube API docuementation](https://docs.sonarqube.org/display/SONAR/User+Token) to obtain the above credentials.

4. Create a new Ballerina project by executing the following command.

      ``<PROJECT_ROOT_DIRECTORY>$ ballerina init``

5. Import the sonarqube module to your Ballerina project as follows.

```ballerina
import ballerina/config;
import ballerina/http;
import ballerina/io;
import wso2/sonarqube6;

string token = "your token";
string sonarqubeURL = "your sonarqube url";

sonarqube6:SonarQubeConfiguration sonarqubeConfig = {
    baseUrl: sonarqubeURL,
    clientConfig: {
        auth: {
            scheme: http:BASIC_AUTH,
            config: {
                username: token,
                password: ""
            }
        }
    }
};
   
sonarqube6:Client sonarqubeClient = new(sonarqubeConfig);

public function main() {
   var projectDetails = sonarqubeClient->getProject(config:getAsString(PROJECT_NAME));
   if (projectDetails is sonarqube6:Project) {
       io:println("Project Details: ", projectDetails)
   } else {
       io:println("Error: ", projectDetails);
   }
}
```
