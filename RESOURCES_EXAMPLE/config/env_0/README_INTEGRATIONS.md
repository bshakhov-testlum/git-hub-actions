# integration.xml
## Integration File Structure
`integration.xml` - is made to set up integrations with API, Database etc.

> Inside integration.xml file there is a set of integrations out-of-the-box:
```xml
<apis>
<websockets>
<clickhouse>
<dynamo>
<elasticsearch>
<kafka>
<mongo>
<mysql>
<oracle>
<postgres>
<rabbitmq>
<redis>
<s3>
<sendgrid>
<ses>
<sqs>
<graphQl>
<lambdaIntegration>
<smtpIntegration>
<twilioIntegration>
```
> When setting up a `integration.xml` file, for each integration tag in the structure there is a mandatory and unique `alias` parameter, with the help of which we get interaction with databases and APIs within the test scenario.

> Each service has a flag `enabled`: `true` & `false` which means whether the integration will be connected or not

### Available Integrations

* `apis`
    ```xml
    <apis> - is a command for API integration. It means, that you are able to integrate as much APIs for your test scenarios as you need
    ```

  * **Usage example:**
     ```xml
      <apis>
        <api alias="ALIAS_1" url="http://URL" enabled="true"/>
        <api alias="ALIAS_2" url="http://URL" enabled="false">
          <auth authStrategy="basic"/>
        </api>
      </apis>
     ```

  * **Contains attributes:**

     ```
     alias - unique Alias for the specific API. You can come up with your alias for your test scenarios to choose what API to use
     
     url - URL for the specific API
     ```
  * **Optional attributes:**
  
     `auth` - Authentication
     ```xml
      <apis>
        <api alias="ALIAS" url="http://URL" enabled="true">
          <auth authStrategy="basic" tokenName="token" autoLogout="true"/>
        </api>
      </apis>
     ```
    `authStrategy` - You can choose desired auth strategy, such as:
     * `basic`
     * `default`
     * `custom`
     * `jwt`

    **Optional attributes for Auth:**
    * `autoLogout` - When selected, Testlum will log out after test execution (default value - true)
    * `authCustomClassName` - attribute for custom auth strategy
    * `tokenName` - name for auth token (default value - token)


* `websockets`
    ```xml
    <websockets> - is a command for Websocket API integration
    ```

  * **Usage example:**
     ```xml
      <websockets>
        <api alias="ALIAS_1" url="ws://URL" protocol="stomp" enabled="true"/>
        <api alias="ALIAS_2" url="wss://URL" protocol="standard" enabled="false"/>
      </websockets>
     ```

  * **Contains attributes:**

     `alias` - unique Alias, that you can come up with and use in your test scenarios

     `url` - URL for Websocket API

     `protocol` - `standard/stomp` - choice of protocol for Websocket API.
  
     `enabled` -  `true/false` - indicator which shows whether specific websocket API integration enabled or not


* `clickhouse`
    ```xml
    <clickhouseIntegration> - is a command for ClickHouse integration
    ```

  * **Usage example:**
     ```xml
      <clickhouseIntegration>
    
        <clickhouse alias="ALIAS_1" enabled="true" truncate="true">
          <jdbcDriver>ru.yandex.clickhouse.ClickHouseDriver</jdbcDriver>
          <username>test</username>
          <password>test</password>
          <connectionUrl>jdbc:clickhouse://</connectionUrl>
        </clickhouse>
    
        <clickhouse alias="ALIAS_2" enabled="false" truncate="false">
          <jdbcDriver>ru.yandex.clickhouse.ClickHouseDriver</jdbcDriver>
          <username>test</username>
          <password>test</password>
          <connectionUrl>jdbc:clickhouse://</connectionUrl>
        </clickhouse>
    
      </clickhouseIntegration>
     ```

  * **Contains attributes:**

    `alias` - unique Alias, that you can come up with and use in your test scenarios

    `truncate="true"` - When selected, data will be cleared before each test run

    `truncate="false"` - When selected, data will not be cleared before each test run (default value)


* `dynamo`
    ```xml
    <dynamoIntegration> - is a command for DynamoDB integration
    ```

  * **Usage example:**
     ```xml
      <dynamoIntegration>
    
        <dynamo alias="ALIAS_1" enabled="true" truncate="true">
          <region>REGION</region>
          <endpoint>http://URL</endpoint>
          <accessKeyId>ACCESS_KEY</accessKeyId>
          <secretAccessKey>SECRET_KEY</secretAccessKey>
          <sessionToken>SESSION_TOKEN</sessionToken>
        </dynamo>
    
        <dynamo alias="ALIAS_2" enabled="false" truncate="false">
          <region>REGION</region>
          <endpoint>http://URL</endpoint>
          <accessKeyId>ACCESS_KEY</accessKeyId>
          <secretAccessKey>SECRET_KEY</secretAccessKey>
          <sessionToken>SESSION_TOKEN</sessionToken>
        </dynamo>
    
      </dynamoIntegration>
     ```

  * **Contains attributes:**

    `alias` - unique Alias, that you can come up with and use in your test scenarios

    `truncate="true"` - When selected, data will be cleared before each test run

    `truncate="false"` - When selected, data will not be cleared before each test run (default value)


* `elasticsearch`
    ```xml
    <elasticsearchIntegration> is a command for Elasticsearch integration
    ```

  * **Usage example:**
     ```xml
      <elasticsearchIntegration>
    
        <elasticsearch alias="ALIAS_1" enabled="true" truncate="true">
          <host>HOST</host>
          <port>PORT</port>
          <scheme>SCHEMA</scheme>
          <connectionTimeout>1000</connectionTimeout>
          <socketTimeout>1000</socketTimeout>
          <signer>SIGNER</signer>
          <serviceName>SEVICENAME</serviceName>
          <region>REGION</region>
          <username>USERNAME</username>
          <password>PASSWORD</password>
        </elasticsearch>
    
        <elasticsearch alias="ALIAS_2" enabled="false" truncate="false">
          <host>HOST</host>
          <port>PORT</port>
          <scheme>SCHEMA</scheme>
          <connectionTimeout>10000</connectionTimeout>
          <socketTimeout>10000</socketTimeout>
          <signer>SIGNER</signer>
          <serviceName>SEVICENAME</serviceName>
          <region>REGION</region>
          <username>USERNAME</username>
          <password>PASSWORD</password>
        </elasticsearch>
    
      </elasticsearchIntegration>
     ```

  * **Contains attributes:**

    `alias` - unique Alias, that you can come up with and use in your test scenarios

    `truncate="true"` - When selected, data will be cleared before each test run

    `truncate="false"` - When selected, data will not be cleared before each test run (default value)


* `kafka`
    ```xml
    <kafkaIntegration> - is a command for Kafka integration
    ```

  * **Usage example:**
     ```xml
     <kafkaIntegration>
    
       <kafka alias="ALIAS_1" enabled="false" truncate="true">
        <bootstrapAddress>HOST:PORT</bootstrapAddress>
        <autoOffsetReset>autoOffsetReset</autoOffsetReset>
        <maxPollRecords>1</maxPollRecords>
        <maxPollIntervalMs>1000</maxPollIntervalMs>
        <clientId>CLIENTID</clientId>
        <groupId>GROUPID</groupId>
      </kafka>
    
      <kafka alias="ALIAS_2" enabled="true" truncate="false">
        <bootstrapAddress>HOST:PORT</bootstrapAddress>
        <autoOffsetReset>autoOffsetReset</autoOffsetReset>
        <maxPollRecords>4</maxPollRecords>
        <maxPollIntervalMs>1000</maxPollIntervalMs>
        <clientId>CLIENTID</clientId>
        <groupId>GROUPID</groupId>
      </kafka>
    
    </kafkaIntegration>
     ```

  * **Contains attributes:**

    `alias` - unique Alias, that you can come up with and use in your test scenarios

    `truncate="true"` - When selected, data will be cleared before each test run

    `truncate="false"` - When selected, data will not be cleared before each test run (default value)



* `mongo`
    ```xml
    <mongoIntegration> - is a command for MongoDB integration
    ```

  * **Usage example:**
     ```xml
     <mongoIntegration>
     
       <mongo alias="ALIAS_1" enabled="true" truncate="true">
         <authenticationDatabase>authenticationDatabase</authenticationDatabase>
         <username>USERNAME</username>
         <password>PASSWORD</password>
         <host>HOST</host>
         <port>PORT</port>
       </mongo>
    
       <mongo alias="ALIAS_2" enabled="false" truncate="false">
         <authenticationDatabase>authenticationDatabase</authenticationDatabase>
         <username>USERNAME</username>
         <password>PASSWORD</password>
         <host>HOST</host>
         <port>PORT</port>
       </mongo>
    
     </mongoIntegration>
     ```

  * **Contains attributes:**

    `alias` - unique Alias, that you can come up with and use in your test scenarios

    `truncate="true"` - When selected, data will be cleared before each test run

    `truncate="false"` - When selected, data will not be cleared before each test run (default value)



* `mysql`
    ```xml
    <mysqlIntegration> - is a command for MySQL integration
    ```

  * **Usage example:**
     ```xml
     <mysqlIntegration>
       <mysql alias="ALIAS" enabled="true" truncate="true">
         <jdbcDriver>com.mysql.cj.jdbc.Driver</jdbcDriver>
         <username>USERNAME</username>
         <password>PASSWORD</password>
         <connectionUrl>jdbc:mysql://</connectionUrl>
         <schema>SCHEMA</schema>
         <hikari>
           <connectionTimeout>45000</connectionTimeout>
           <idleTimeout>60000</idleTimeout>
           <maxLifetime>180000</maxLifetime>
           <maximumPoolSize>50</maximumPoolSize>
           <minimumIdle>5</minimumIdle>
           <connectionInitSql>CONNECTION INIT SQL</connectionInitSql>
           <connectionTestQuery>CONNECTION TEST QUERY</connectionTestQuery>
           <poolName>POOL_NAME</poolName>
           <autoCommit>true</autoCommit>
         </hikari>
       </mysql>
     </mysqlIntegration>
     ```

  * **Contains attributes:**

    `alias` - unique Alias, that you can come up with and use in your test scenarios

    `truncate="true"` - When selected, data will be cleared before each test run

    `truncate="false"` - When selected, data will not be cleared before each test run (default value)



* `oracle`
    ```xml
    <oracleIntegration> - is a command for Oracle integration
    ```

  * **Usage example:**
     ```xml
     <oracleIntegration>
       <oracle alias="ALIAS" enabled="true" truncate="true">
         <jdbcDriver>oracle.jdbc.OracleDriver</jdbcDriver>
         <username>USERNAME</username>
         <password>PASSWORD</password>
         <connectionUrl>jdbc:oracle:thin:@</connectionUrl>
         <schema>SCHEMA</schema>
         <hikari>
           <connectionTimeout>45000</connectionTimeout>
           <idleTimeout>60000</idleTimeout>
           <maxLifetime>180000</maxLifetime>
           <maximumPoolSize>50</maximumPoolSize>
           <minimumIdle>5</minimumIdle>
           <connectionInitSql>CONNECTION INIT SQL</connectionInitSql>
           <connectionTestQuery>CONNECTION TEST QUERY</connectionTestQuery>
           <poolName>POOL_NAME</poolName>
           <autoCommit>true</autoCommit>
         </hikari>
       </oracle>
     </oracleIntegration>
     ```

  * **Contains attributes:**

    `alias` - unique Alias, that you can come up with and use in your test scenarios

    `truncate="true"` - When selected, data will be cleared before each test run

    `truncate="false"` - When selected, data will not be cleared before each test run (default value)


* `postgres`
    ```xml
    <postgresIntegration> - is a command for Postgres integration
    ```

  * **Usage example:**
     ```xml
     <postgresIntegration>
       <postgres alias="ALIAS" enabled="true" truncate="true">
         <jdbcDriver>org.postgresql.Driver</jdbcDriver>
         <username>USERNAME</username>
         <password>PASSWORD</password>
         <connectionUrl>jdbc:postgresql://</connectionUrl>
         <schema>SCHEMA</schema>
         <hikari>
           <connectionTimeout>45000</connectionTimeout>
           <idleTimeout>60000</idleTimeout>
           <maxLifetime>180000</maxLifetime>
           <maximumPoolSize>50</maximumPoolSize>
           <minimumIdle>5</minimumIdle>
           <connectionInitSql>CONNECTION INIT SQL</connectionInitSql>
           <connectionTestQuery>CONNECTION TEST QUERY</connectionTestQuery>
           <poolName>POOL_NAME</poolName>
           <autoCommit>true</autoCommit>
         </hikari>
       </postgres>
     </postgresIntegration>
     ```

  * **Contains attributes:**

    `alias` - unique Alias, that you can come up with and use in your test scenarios

    `truncate="true"` - When selected, data will be cleared before each test run

    `truncate="false"` - When selected, data will not be cleared before each test run (default value)



* `rabbitmq`
    ```xml
    <rabbitmqIntegration> - is a command for RabbitMQ integration
    ```

  * **Usage example:**
     ```xml
     <rabbitmqIntegration>
       <rabbitmq alias="ALIAS" enabled="true" truncate="true">
         <host>HOST</host>
         <port>PORT</port>
         <username>USERNAME</username>
         <password>PASSWORD</password>
         <apiPort>APIPORT</apiPort>
         <virtualHost>/</virtualHost>
         <enabledMetrics>true</enabledMetrics>
       </rabbitmq>
     </rabbitmqIntegration>
     ```

  * **Contains attributes:**

    `alias` - unique Alias, that you can come up with and use in your test scenarios

    `truncate="true"` - When selected, data will be cleared before each test run

    `truncate="false"` - When selected, data will not be cleared before each test run (default value)



* `redis`
    ```xml
    <redisIntegration> - is a command for Redis integration
    ```

  * **Usage example:**
     ```xml
     <redisIntegration>
       <redis alias="ALIAS_1" enabled="true" truncate="true">
         <host>HOST</host>
         <port>PORT</port>
       </redis>

       <redis alias="ALIAS_2" enabled="false">
         <host>HOST</host>
         <port>PORT</port>
       </redis>
     </redisIntegration>
     ```

  * **Contains attributes:**

    `alias` - unique Alias, that you can come up with and use in your test scenarios

    `truncate="true"` - When selected, data will be cleared before each test run

    `truncate="false"` - When selected, data will not be cleared before each test run (default value)



* `s3`
    ```xml
    <s3Integration> - is a command for S3 integration
    ```

  * **Usage example:**
     ```xml
     <s3Integration>
       <s3 alias="ALIAS_1" enabled="false" truncate="true">
         <region>REGION</region>
         <endpoint>http://URL</endpoint>
         <accessKeyId>ACCESS_KEY</accessKeyId>
         <secretAccessKey>SECRET_KEY</secretAccessKey>
       </s3>
       <s3 alias="ALIAS_2" enabled="false" truncate="false">
         <region>REGION</region>
         <endpoint>http://URL</endpoint>
         <accessKeyId>ACCESS_KEY</accessKeyId>
         <secretAccessKey>SECRET_KEY</secretAccessKey>
       </s3>
     </s3Integration>
     ```

  * **Contains attributes:**

    `alias` - unique Alias, that you can come up with and use in your test scenarios

    `truncate="true"` - When selected, data will be cleared before each test run

    `truncate="false"` - When selected, data will not be cleared before each test run (default value)


* `sendgrid`
    ```xml
    <sendgridIntegration> - is a command for SendGrid integration
    ```

  * **Usage example:**
     ```xml
     <sendgridIntegration>
       <sendgrid alias="ALIAS" enabled="true">
         <apiKey>APIKEY</apiKey>
       </sendgrid>
     </sendgridIntegration>
     ```

  * **Contains attributes:**

    `alias` - unique Alias, that you can come up with and use in your test scenarios



* `ses`
    ```xml
    <sesIntegration> - is a command for SES integration
    ```

  * **Usage example:**
     ```xml
     <sesIntegration>
       <ses alias="ALIAS" enabled="true">
         <region>REGION</region>
         <endpoint>http://URL</endpoint>
         <accessKeyId>ACCESS_KEY</accessKeyId>
         <secretAccessKey>SECRET_KEY</secretAccessKey>
       </ses>
     </sesIntegration>
     ```

  * **Contains attributes:**

    `alias` - unique Alias, that you can come up with and use in your test scenarios



* `sqs`
    ```xml
    <sqsIntegration> - is a command for SQS integration
    ```

  * **Usage example:**
     ```xml
     <sqsIntegration>
       <sqs alias="ALIAS" enabled="false" truncate="true">
         <region>REGION</region>
         <endpoint>http://URL</endpoint>
         <accessKeyId>ACCESS_KEY</accessKeyId>
         <secretAccessKey>SECRET_KEY</secretAccessKey>
       </sqs>
     </sqsIntegration>
     ```

  * **Contains attributes:**

    `alias` - unique Alias, that you can come up with and use in your test scenarios

    `truncate="true"` - When selected, data will be cleared before each test run

    `truncate="false"` - When selected, data will not be cleared before each test run (default value)



* `graphql`
    ```xml
    <graphqlIntegration> - is a command for GrapghQL integration
    ```

  * **Usage example:**
     ```xml
     <graphqlIntegration>
       <api alias="ALIAS_1" url="http://URL" enabled="true"/>
       <api alias="ALIAS_2" url="https://URL" enabled="true"/>
       <api alias="ALIAS_3" url="https://URL" enabled="true"/>
     </graphqlIntegration>
     ```

  * **Contains attributes:**

    `alias` - unique Alias, that you can come up with and use in your test scenarios

    `url` - URL for GraphQL API



* `lambda`
    ```xml
    <lambdaIntegration> - is a command for Lambda integration
    ```

  * **Usage example:**
     ```xml
     <lambdaIntegration>
       <lambda alias="ALIAS" enabled="true">
         <region>REGION</region>
         <endpoint>http://URL</endpoint>
         <accessKeyId>ACCESS_KEY</accessKeyId>
         <secretAccessKey>SECRET_KEY</secretAccessKey>
       </lambda>
     </lambdaIntegration>
     ```

  * **Contains attributes:**

    `alias` - unique Alias, that you can come up with and use in your test scenarios



* `smtp`
    ```xml
    <smtpIntegration> - is a command for SMTP integration
    ```

  * **Usage example:**
     ```xml
     <smtpIntegration>
       <smtp alias="ALIAS" enabled="false">
         <host>HOST</host>
         <port>PORT</port>
         <username>USERNAME</username>
         <password>PASSWORD</password>
         <smtpAuth>true</smtpAuth>
         <smtpStarttlsEnable>true</smtpStarttlsEnable>
       </smtp>
     </smtpIntegration>
     ```

  * **Contains attributes:**

    `alias` - unique Alias, that you can come up with and use in your test scenarios



* `twilio`
    ```xml
    <twilioIntegration> - is a command for Twilio integration
    ```

  * **Usage example:**
     ```xml
     <twilioIntegration>
       <twilio alias="ALIAS" enabled="false">
         <accountSid>accountSid</accountSid>
         <authToken>authToken</authToken>
         <twilioNumber>+NUMBER</twilioNumber>
       </twilio>
     </twilioIntegration>
     ```

  * **Contains attributes:**

    `alias` - unique Alias, that you can come up with and use in your test scenarios