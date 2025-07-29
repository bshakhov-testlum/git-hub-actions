# global-config.xml
## Global Config File Structure
`global-config.xml` - is a file which will contain the main configuration settings of your project. You have the ability to create multiple configuration files and divide the testing environment.

> **Does the global-config.xml file have a strict name structure?**
> 
> No, you can give it any name you like. But we provide an example of how to name this file for convenience!

For example:
```
global-config-local.xml
global-config-dev.xml
global-config-jenkins.xml
```

### Available Commands
`global-config.xml` - is a XSD schema of which has an optional set of commands out-of-the-box, which extremely simplifies the settings configuration process.
The set of basic commands for configuration global-config.xml:
```xml
  <parallelExecution>
  <stopScenarioOnFailure>
  <stopIfInvalidScenario>
  <delayBetweenScenarioRuns>
  <runScenariosByTag>
  <report>
  <environments>
```

* `parallelExecution` 
    ```xml
    <parallelExecution> - is a command for enabling or disabling parallel execution of test scenarios.
    ```
      
  * **Usage example:** 
     ```xml
     <parallelExecution>false</parallelExecution>
     ```

  * **Contains flags:**

     ```
     true - Enables parallel execution of test scenarios, if environments are set up
     
     false - Disables parallel execution of test scenarios
     ```

* `stopScenarioOnFailure`
    ```xml
    <stopScenarioOnFailure> - is a command that controls the passage of your test scenarios.
    ```
  * **Usage example:** 
     ```xml
     <stopScenarioOnFailure>false</stopScenarioOnFailure>
     ```

  * **Contains flags:**

     ```
     true - When starting several or one test scenario, and detecting invalid test scenario in test resources, start will be terminated with an error output, which will show path to invalid scenario

     false - when running several or one test scenario, and an exception is detected, the starter will not be stopped, all the scenarios and steps will be executed until the starter finishes working, with a further output of an exception for all the scenarios that have been passed and received an exception
     ```

* `delayBetweenScenariosRuns`
    ```xml
    <delayBetweenScenariosRuns> - is a command, that adds a timeout between script executions
    ```
  * **Usage example:** 
      ```xml 
      <delayBetweenScenariosRuns seconds="3" enabled="true"/>
     ```

  * **Contains attributes:**

     ```
     seconds - Sets the time counter between the script timeout

     enabled="true" - When selected, the ability to perform a timeout between scenarios is enabled

     enabled="false" - When selected, the ability to perform a timeout between scenarios is disabled
     ```

* `runScenariosByTag`
    ```xml
    <runScenariosByTag> - allows you to be able to implement a global launch of test scenarios for a specific command. It is designed to separate the launch of test scenarios.
    ```
  `Create your own FilterTag for your convenience`

  `Set a unique tag for each scenario`
  * **Usage example:** 
     ```xml
     <runScenariosByTag enable="true">
        <tag name="WEB" enable="true"/>
        <tag name="API" enable="false"/>
     </runScenariosByTag>
     ```

  * **Contains attributes:**
     ```
     enable="true" - When selected, the ability to run scenarios by all or specific tags is enabled

     enable="false" - When selected, the ability to run scenarios by all or specific tags is disabled

     name - allows to come up with and specify, which exactly tag user wants to run
     ```

* `report`
    ```xml
    <report> - configuring local and server reporting  
    ```
  * **Usage example:**
       ```xml
       <report>
          <extentReports projectName="shop">
            <htmlReportGenerator enable="true"/>
            <klovServerReportGenerator enable="true">
                <mongoDB host="localhost" port="27017"/>
            </klovServerReportGenerator>
          </extentReports>
       </report>
       ```
    * **Contains attributes:**
         ```
          <extentReports projectName="shop"> - is to specify project name for reports

          <htmlReportGenerator enable="true"/> - enables or disables creating of local reports, that will be saved in report folder inside your test resources

          <klovServerReportGenerator enable="true"> - enables or disables creating of remote reports, that will be saved on remote server

          <mongoDB host="localhost" port="27017"/> - allows to specify host and port for storing remote reports
         ```

* `environments`
    ```xml
    <environments> - is a command, that allows to set up several environments for parallel test execution  
    ```
  * **Usage example:**
       ```xml
       <environments>
          <env folder="env0" enabled="true"/>
          <env folder="disabled_env" enabled="false" threads="2"/>
       </environments>
       ```
  * **Contains attributes:**
       ```
        folder - is to specify folder name with integration.xml and ui.xml files for specific environment

        enabled - is used to enable or disable specific environment

        threads - (optional): execution allow to run tests concurrently, however, in the case of tests that affect each other, the tests will fail because the same environment (default value - 1)
       ```

* `vault`
    ```xml
    <vault> - is a command, for interaction with the Vault service, and creation of variables for configurations. It offers features for secret storage, dynamic secret generation, authentication.  
    ```
  * **Usage example:**
       ```xml
       <vault>
          <host>HOST</host>
          <port>PORT</port>
          <scheme>SCHEME</scheme>
          <token>TOKEN</token>
       </vault>
       ```
  * **Contains attributes:**
       ```
        host - host for vault URL

        port - port for vault URL

        scheme - scheme for vault URL (For example - http, https)

        token - token for vault account
       ```

  > **_NOTE:_**  Data for variables from vault, you can write in ui and integration files to any field with the format - {{path_to_vault_variable}}
  * **Example with vault variable:**
     ```xml
       <rabbitmqIntegration>
         <rabbitmq alias="ALIAS" enabled="true" truncate="true">
           <host>HOST</host>
           <port>PORT</port>
           <username>{{secret/data/rabbit/user.username}}</username>
           <password>{{secret/data/rabbit/password.password}}</password>
           <apiPort>API_PORT</apiPort>
           <virtualHost>/</virtualHost>
           <enabledMetrics>true</enabledMetrics>
         </rabbitmq>
     </rabbitmqIntegration> 
     ```

* `system env variable`

  > **_NOTE:_** It is also possible to write a variable in the config from personal computer, in ui and integration files to any field with the format - ${PC_variable_name}

  * **Example with personal computer variable:**
    ```xml
      <rabbitmqIntegration>
        <rabbitmq alias="ALIAS" enabled="true" truncate="true">
          <host>HOST</host>
          <port>PORT</port>
          <username>${rabbit_username}</username>
          <password>${rabbit_password}</password>
          <apiPort>API_PORT</apiPort>
          <virtualHost>/</virtualHost>
          <enabledMetrics>true</enabledMetrics>
        </rabbitmq>
      </rabbitmqIntegration>
    ```