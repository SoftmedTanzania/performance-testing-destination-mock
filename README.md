# Performance Testing Destination System Mock

[![Java CI Badge](https://github.com/SoftmedTanzania/performance-testing-destination-mock/workflows/Java%20CI%20with%20Maven/badge.svg)](https://github.com/SoftmedTanzania/performance-testing-destination-mock/actions?query=workflow%3A%22Java+CI+with+Maven%22)
[![Coverage Status](https://coveralls.io/repos/github/SoftmedTanzania/performance-testing-destination-mock/badge.svg?branch=main)](https://coveralls.io/github/SoftmedTanzania/performance-testing-destination-mock?branch=main)

An [OpenHIM](http://openhim.org/) mediator used as a destination system mock while performing TanzaniaHIM performance testing using [Performance Testing Framework](https://github.com/SoftmedTanzania/performance-testing-framework)

## 1. Dev Requirements

1. Java 1.8
2. IntelliJ or Visual Studio Code
3. Maven 3.6.3

### 2 Configuration Parameters

The configuration parameters specific to the mediator and destination system can be found at

`src/main/resources/mediator.properties`

```
# Mediator Properties
mediator.name=Sample-Performance-Testing-Destination
mediator.host=localhost
mediator.port=4000
mediator.timeout=60000
mediator.heartbeats=true

core.host=localhost
core.api.port=8080
core.api.user=root@openhim.org
core.api.password=openhim-password

```

The configuration parameters specific to the mediator and the mediator's metadata can be found at

`src/main/resources/mediator-registration-info.json`

```
{
  "urn": "urn:uuid:70691430-4e69-11ec-83f8-cbbb49e93173",
  "version": "0.1.0",
  "name": "Sample Performance Testing Destination",
  "description": "This mediator mocks a sample destination and returns success messages after receiving requests. It used while perfoming perfomance testing",
  "endpoints": [
    {
      "name": "Sample Performance Testing Destination Route",
      "host": "localhost",
      "port": "4000",
      "path": "/destination",
      "type": "http"
    }
  ],
  "defaultChannelConfig": [
    {
      "name": "Sample Performance Testing Destination",
      "urlPattern": "^/destination$",
      "type": "http",
      "allow": ["sampleperformancetestingdestination"],
      "routes": [
        {
          "name": "Sample Performance Testing Destination Route",
          "host": "localhost",
          "port": "4000",
          "path": "/destination",
          "type": "http",
          "primary": "true"
        }
      ]
    }
  ]
}
```

## 4. Deployment

To build and run the mediator after performing the above configurations, run the following

```
  mvn clean package -DskipTests=true -e source:jar javadoc:jar
  java -jar target/performance-testing-destination-<version>-jar-with-dependencies.jar
```
