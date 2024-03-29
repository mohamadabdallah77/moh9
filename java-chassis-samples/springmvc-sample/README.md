# Spring MVC Sample

`RestTemplate` is a RESTful API provide by the Spring framework. ServiceComb provides the API for service calling. Users can call microservices using customized URL and `RestTemplate` instance provided by ServiceComb regardless of the specific address of the service.

* The URL must be in format of ServiceComb: `cse://microserviceName/path?querystring`.
* During use of this URL format, the ServiceComb framework will perform internal microservice discovery, fallback, and fault tolerance and send the requests to the microservice providers.

## Precondition
see [Precondition](../../README.md)

## Sample Quick Start

1. Start the ServiceComb/Service Center

   - [how to start the service center](http://servicecomb.apache.org/docs/products/service-center/install/)
   - make sure service center address is configured correctly in `microservice.yaml` file

```yaml
servicecomb:
 service:
   registry:
     address: http://127.0.0.1:30100		#service center address
```

2. Start the springmvc-provider service

   * Start provider service by maven

     Compile the source code, and use `mvn exec` to execute the main class `SpringmvcProviderMain`.

     ```bash
     mvn clean install 
     cd springmvc-sample/springmvc-provider/
     mvn exec:java -Dexec.mainClass="org.apache.servicecomb.samples.springmvc.provider.SpringmvcProviderMain"
     ```

   * Start provider service by IDE

     Import the project by InteliJ IDEA or Eclipse, then find `main` function of provider service and `RUN` it like any other Java Program.

3. Start the springmvc-consumer service

   Just like how to start springmvc-provider service. But the main class of springmvc-consumer service is `SpringmvcConsumerMain`. 

   ```bash
   cd springmvc-sample/springmvc-consumer/
   mvn exec:java -Dexec.mainClass="org.apache.servicecomb.samples.springmvc.consumer.SpringmvcConsumerMain"
   ```

4. How to verify
   On the producer side, the output should contain the following stuffs if the producer starts up successfully:
   1. *'swagger: 2.0 info: version: 1.0.0 ...'* means the producer generated swagger contracts
   2. *'rest listen success. address=0.0.0.0:8080'* means the rest endpoint is listening on port 8080
   
   On the consumer side, you can see the following outputs if the consumer can invoke the producer:
   1. *'RestTemplate consumer sayhi services: Hello Java Chassis'* means the consumer calls sayhi by RestTemplate successfully
   2. *'RestTemplate consumer sayhello services: Hello person ServiceComb/Java Chassis'* means the consumer calls sayhello by RestTemplate successfully
   3. *'POJO consumer sayhi services: Hello Java Chassis'* means the consumer calls sayhi by RpcReference successfully
   4. *'POJO consumer sayhello services: Hello person ServiceComb/Java Chassis'* means the consumer calls sayhello by RpcReference successfully
   ​
## More

[Develop with SpringMVC](https://docs.servicecomb.io/java-chassis/zh_CN/build-provider/springmvc/)
