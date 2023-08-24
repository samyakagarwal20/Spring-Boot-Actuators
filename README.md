# Spring-Boot-Actuators
It is a sample spring boot application to demonstrate the implementation and insights provided by actuators.

### Prerequisites for running the application:

---
Please make sure to have an active instance of MySQL DB running on your system before starting the application.

In case, if you don't have MySQL installed on your system then you could also simply run a container from the mysql image (taken from DockerHub) using the following command:

```docker run --name mysqldb -p 3306:3306 -e MYSQL_ROOT_PASSWORD=password -d mysql```

Once the container is in running state (which you could verify either using docker desktop app or using the command ```docker ps```), you can make use of MySQL Workbench to validate the connection with your running container on port **3306**.

The password specified for mysql DB **root** acoount is **password** :)

---
Once we are done with validating the connection, we need to create the target database as pracDB (the name of the database which I am using in my application).

We can do it either by using MySQL Workbench or by executing the following command in console

```docker exec -it mysqldb mysql -u root -p```

This command prompts for the root password which we specified at the time of running the container. After entering the correct credentials, we get the access to the mysql client where we can execute the SQL query as ```create database pracDB```

We could also create the database with some other name but make sure to change the **spring.datasource.url** property accordingly in application.yaml file.

---
In this method, we have explicitly defined a datasource and a corresponding JdbcTemplate object to perform the setup by referring to the properties defined in the application.yaml file.

The configuration are done within the file **JDBCConfig.java**

---

Before running the application, please locate the **USER.sql** file present in the root directory and execute the command either on your mysql client ar directly onto the MySQL workbench (the steps for accessing which are already present above)

---
### Overview of Actuators and HAL Explorer

Actuators can be thought of as monitoring and management endpoints embedded within Spring Boot applications. These endpoints provide valuable insights into the operational health of an application, allowing developers and administrators to gain real-time information about various aspects such as health, metrics, environment, configuration, and more. 

There are various actuator endpoints like 
* /actuator/health
* /actuator/metrics
* /actuator/env
* /actuator/configprops and so on

To enable all the actuator endpoints, we can add the following property in application.yaml
```
management:
  endpoints:
    web:
      exposure:
        include: '*'
```

In case of issue, the health status of the service might appear down. To gain additional info in this respect regarding the issue, we can add the following property in application.yaml
```
management:
  endpoint:
    health:
      show-details: ALWAYS
```

providing a user-friendly interface to navigate and interact with a RESTful API. It enables developers to explore the API's resources, their relationships, and available endpoints through a web-based UI.

To add the support for actuators in spring boot, we can add the following dependency
```
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-actuator</artifactId>
</dependency>
```

To add the support for HAL explorer, we can add the following dependency
```
<dependency>
    <groupId>org.springframework.data</groupId>
    <artifactId>spring-data-rest-hal-explorer</artifactId>
</dependency>
```
