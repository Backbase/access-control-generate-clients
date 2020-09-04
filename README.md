# How to create a client for Access Control
## Create a client for Access Control.

[Example: How to create a client for Access Control](https://community.backbase.com/documentation/entitlements/latest/how_to_create_clients)

## Description
When you have a custom service, such as an integration service, that needs to call Access Control endpoints, then you need to have a generated client in that service. The custom service does not directly call Access Control endpoints, but calls the corresponding method in the generated client, which will call the Access Control endpoint.

## How to use
Follow these steps to generate a client from a specification:

##### 1. Go to the Maven project folder of your custom service and open the POM file.

##### 2. Select the RAML file that you want to generate a client from:

- accessgroup-presentation-spec
    * Client API
    * Service API
- legalentity-presentation-spec
    * Client API
    * Service API
- accesscontrol-pandp-query-spec
    * Service API

##### 3. Add an execution for the raml-api-maven-plugin-1-0 to the POM file. See examples below:

- accessgroup-presentation-spec

```
    <execution>
      <id>accessgroup-presentation-spec</id>
      <phase>generate-sources</phase>
      <goals>
        <goal>raml-api-generator</goal>
      </goals>
      <configuration>
        <includeBindingResult>false</includeBindingResult>
        <inputSpec>
          <groupId>com.backbase.dbs.accesscontrol</groupId>
          <artifactId>access-control-spec</artifactId>
          <version>${access-control-spec.version}</version>
          <inputFiles>
            <inputFile>accessgroup-presentation-spec/api.raml</inputFile>
            <inputFile>accessgroup-presentation-spec/service-api.raml</inputFile>
          </inputFiles>
        </inputSpec>
        <outputFile>target/generated-sources</outputFile>
        <serviceId>access-control</serviceId>
        <packageName>presentation.accessgroup</packageName>
        <basePackageName>com.backbase</basePackageName>
        <generateApi>false</generateApi>
        <generateClients>true</generateClients>
      </configuration>
    </execution>
```
    
- legalentity-presentation-spec

```
    <execution>
      <id>legalentity-presentation-spec</id>
      <phase>generate-sources</phase>
      <goals>
        <goal>raml-api-generator</goal>
      </goals>
      <configuration>
        <inputSpec>
          <groupId>com.backbase.dbs.accesscontrol</groupId>
          <artifactId>access-control-spec</artifactId>
          <version>${access-control-spec.version}</version>
          <inputFiles>
            <inputFile>legalentity-presentation-spec/api.raml</inputFile>
            <inputFile>legalentity-presentation-spec/service-api.raml</inputFile>
          </inputFiles>
        </inputSpec>
        <outputFile>target/generated-sources</outputFile>
        <serviceId>access-control</serviceId>
        <packageName>presentation.legalentity</packageName>
        <basePackageName>com.backbase</basePackageName>
        <generateApi>false</generateApi>
        <generateClients>true</generateClients>
      </configuration>
    </execution>
```

- accesscontrol-pandp-query-spec

```
    <execution>
      <id>accesscontrol-pandp-query-spec</id>
      <phase>generate-sources</phase>
      <goals>
        <goal>raml-api-generator</goal>
      </goals>
      <configuration>
        <includeBindingResult>false</includeBindingResult>
        <inputSpec>
          <groupId>com.backbase.dbs.accesscontrol</groupId>
          <artifactId>access-control-spec</artifactId>
          <version>${access-control-spec.version}</version>
          <inputFiles>
            <inputFile>accesscontrol-pandp-query-spec/service-api.raml</inputFile>
          </inputFiles>
        </inputSpec>
        <outputFile>target/generated-sources</outputFile>
        <serviceId>access-control</serviceId>
        <packageName>pandp.accesscontrol.query</packageName>
        <basePackageName>com.backbase</basePackageName>
        <generateApi>false</generateApi>
        <generateClients>true</generateClients>
      </configuration>
    </execution>
```
    
##### 4. Build the specification
Build the project to generate the client:

    mvn clean install