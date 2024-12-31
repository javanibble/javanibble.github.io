---
layout: post
title: "How to Access H2 Database with Spring JDBC"
date: 2019-08-12 00:00:00 +0200
tags: spring_boot jdbc h2
categories: [Spring Boot]
author: "andre_mare"
post_image: "/assets/img/my_images/feature-images/feature-image-spring.png"
---

In this guide, I will show you how to create a Spring Boot application and use Spring JDBC to access an in-memory H2 database. The guide describes in a step-by-step manner how to create a Data Access Object (DAO), and use the JDBCTemplate to perform CRUD operations on the "mammal" table. Finally I will show you how to compile and run the application from the command line and view the H2 database via the console. 

<h3>Getting Started</h3>
The following list defines the technologies and libraries I used to implement the sample code:
<ul>
<li>Maven 3.2+. <a href="https://maven.apache.org/download.cgi">(Download)</a></li>
<li>JDK 1.8 <a href="http://www.oracle.com/technetwork/java/javase/downloads/index.html">(Download)</a></li>
<li>Spring Tool Suite <a href="https://spring.io/tools/sts/all">(Download)</a> </li>
</ul>

<h3>Introduction</h3>
This guide explains how to create a Spring Boot application that makes use of Spring JDBC to connect to a H2 in-memory database. Like most guides, you can read through the complete guide and complete each step or you can bypass all of this and download the code from Github. In the end, you should have working code on your machine that performs CRUD functions on a H2 in-memory database.

<h3>Code Example</h3>
The code example can be downloaded from Github from the button below. After you have downloaded the code onto your machine, you can either work through the guide step-by-step to understand the example, or jump to the "<em>Compile & Run The Example</em>" section to get the example up and running.

<a href="https://github.com/Code2Bits/Spring-Boot-Data-Examples/tree/master/JDBC/Example_01" class="btn">Download Code</a>

<h4>Step 1: Define Maven Dependencies</h4>
The following dependencies should be included in the pom.xml file:
<ul>
<li><strong>spring-boot-starter-jdbc</strong>: The Spring Boot starter dependency descriptor for using JDBC with the HikariCP connection pool.</li>
<li><strong>spring-boot-starter-web</strong>: The Spring Boot starter dependency descriptor for building web, including RESTful, applications using Spring MVC. Uses Tomcat as the default embedded container. Used to run the H2 Console in this example.</li>
<li><strong>spring-boot-starter-test</strong>: The Spring Boot starter dependency descriptor for testing Spring Boot applications with libraries including JUnit, Hamcrest and Mockito.</li>
<li><strong>spring-boot-devtools</strong>: The spring-boot-devtools module is included to provide additional development-time features like automatic restart, live reload, global settings and remote applications.</li>
<li><strong>h2</strong>: The H2 module is included to provide the in-memory database.</li>
</ul>

```xml
<dependency>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-starter-jdbc</artifactId>
</dependency>
<dependency>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-starter-web</artifactId>
</dependency>
<dependency>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-starter-test</artifactId>
  <scope>test</scope>
</dependency>
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-devtools</artifactId>
    <scope>runtime</scope>
</dependency>
<dependency>
  <groupId>com.h2database</groupId>
  <artifactId>h2</artifactId>
  <scope>runtime</scope>
</dependency>
```

<h4>Step 2: Define Schema and Sample Data</h4>
The example contains a database table called mammal. The schema.sql file within the resources directory is used to define the database table.

<strong>Resources: schema.sql</strong>
```sql
CREATE TABLE mammal (
    id                      integer            NOT NULL,
    english_name            varchar(50)        NOT NULL,
    afrikaans_name          varchar(50)        NOT NULL,
    binomial_name           varchar(50)        NOT NULL,
    conservation_status     varchar(10)        NOT NULL,
    gestation_period        varchar(10)        NOT NULL,
    young                   varchar(20)        NOT NULL,
    mass_male               varchar(10)        NOT NULL,
    mass_female             varchar(10)        NOT NULL,
    life_expectancy         varchar(10)        NOT NULL,
 PRIMARY KEY (id)
);
```

To populate the database table, the following insert scripts within the data.sql file will be executed as part of the startup process.

<strong>Resources: data.sql</strong>
```sql
insert into mammal (id, english_name, afrikaans_name, binomial_name, conservation_status, gestation_period, young, mass_male, mass_female, life_expectancy) 
values (1, 'Southern African Hedgehog','Krimpvarkie','Atelerix frontalis','LC','35','one - nine','0.4','0.4','3');

insert into mammal (id, english_name, afrikaans_name, binomial_name, conservation_status, gestation_period, young, mass_male, mass_female, life_expectancy) 
values (2, 'Thick-tailed bushbaby','Bosnagaap','Otolemur crassicaudatus','LC','130','one - three','1.2','0.8','14');
```

<h4>Step 3: Enable H2 Console</h4>
The H2 in-memory database contains a web console which enables you to access the database via your browser. To enable the H2 Console, you should set the <em>spring.h2.console.enabled</em> property to <em>true</em>.

<strong>Resources: application.properties</strong>
```properties
# Enabling H2 Console
spring.h2.console.enabled=true
```

Once the application is running you can access the console via your browser from at the following url: 

<a href="http://localhost:8080/h2-console" class="btn">http://localhost:8080/h2-console</a>

<h4>Step 4: Define the Mammal POJO</h4>
The Mammal class is a simple Java POJO that define the properties that align to columns in the database table. The class follows the Java Bean convention in that it follows getter/setter naming convention, has a public default constructor and is also serialisable.

```java
public class Mammal {
    private int id;
    private String englishName;
    private String afrikaansName;
    private String binomialName;
    private String conservationStatus;
    private String gestationPeriod;
    private String young;
    private String massMale;
    private String massFemale;
    private String lifeExpectancy;

    // Add Constructors
    // Add Getter & Setter methods
    // Add toString method
}
```

The full class is not displayed here due to space and readability reasons.

<h4>Step 5: Define the Mammal Data Access Object (DAO)</h4>
The Mammal Data Access Object (DAO) class is an object that provides an abstraction to the H2 in-memory database. The DAO provides specific CRUD operations without exposing the details of the database by mapping the table columns to the Mammal object. 

```java
@Repository
public class MammalDAO {
    @Autowired
    private JdbcTemplate jdbcTemplate;
    
    public List<Mammal> findAllMammals() {
        return jdbcTemplate.query("select * from mammal", new MammalRowMapper());
    }
    
    class MammalRowMapper implements RowMapper<Mammal>{
        @Override
        public Mammal mapRow(ResultSet rs, int rowNum) throws SQLException {
            Mammal mammal = new Mammal();
            mammal.setId(rs.getInt("id"));
            mammal.setEnglishName(rs.getString("english_name"));
            mammal.setAfrikaansName(rs.getString("afrikaans_name"));
            mammal.setBinomialName(rs.getString("binomial_name"));
            mammal.setConservationStatus(rs.getString("conservation_status"));
            mammal.setGestationPeriod(rs.getString("gestation_period"));
            mammal.setYoung(rs.getString("young"));
            mammal.setMassMale(rs.getString("mass_male"));
            mammal.setMassFemale(rs.getString("mass_female"));
            mammal.setLifeExpectancy(rs.getString("life_expectancy"));
            
            return mammal;
        }
    }
}
```

<h4>Step 6: Define the Spring Boot Application</h4>
The Spring Boot application's main class define the @SpringBootAnnotation. The @SpringBootApplication annotation enables three features namely auto-configuration, component scan and the ability to define extra configuration on the "application class". The application also contains a public static void main() method that starts up the Spring ApplicationContext. 

The CommandLineRunner interface provides an option to run a specific piece of code when the application is fully started. The run method executes 8 commands on the MammalDAO class to perform the CRUD operations on the in-memory H2 database.
<ol>
<li>Retrieve All Mammals -> {}", mammalDAO.findAllMammals());</li>
<li>Retrieve Mammal with ID: 1 -> {}", mammalDAO.findMammalById(1));</li>
<li>Delete Mammal with ID: 1 -> {}", mammalDAO.deleteMammalById(1));</li>
<li>Retrieve All Mammals -> {}", mammalDAO.findAllMammals());</li>
<li>Insert Mammal -> {}", mammalDAO.insertMammal(...);</li>
<li>Retrieve Mammal with ID: 1 -> {}", mammalDAO.findMammalById(1));</li>
<li>Update Mammal with ID 1 -> {}", mammalDAO.updateMammal(...);</li>
<li>Retrieve Mammal with ID: 1 -> {}", mammalDAO.findMammalById(1));</li>
</ol>

```java
@SpringBootApplication
public class Application implements CommandLineRunner {

    private Logger logger = LoggerFactory.getLogger(this.getClass());
    
    @Autowired
    private MammalDAO mammalDAO;

    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }

    @Override
    public void run(String... args) throws Exception {
        logger.info("\n 1. Retrieve All Mammals -> {}", mammalDAO.findAllMammals());
        logger.info("\n 2. Retrieve Mammal with ID: 1 -> {}", mammalDAO.findMammalById(1));
        
        logger.info("\n 3. Delete Mammal with ID: 1 -> {}", mammalDAO.deleteMammalById(1));
        logger.info("\n 4. Retrieve All Mammals -> {}", mammalDAO.findAllMammals());
        
        logger.info("\n 5. Insert Mammal -> {}", mammalDAO.insertMammal(new Mammal(1, "Southern African Hedgehog","Krimpvarkie","Atelerix frontalis","LC","35","one - nine","0.4","0.4","3")));
        logger.info("\n 6. Retrieve Mammal with ID: 1 -> {}", mammalDAO.findMammalById(1));
        
        logger.info("\n 7. Update Mammal with ID 1 -> {}", mammalDAO.updateMammal(new Mammal(1, "Southern African Hedgehog","Krimpvarkie","Atelerix frontalis","LC","10","one - ten","10.0","10.0","10")));
        logger.info("\n 8. Retrieve Mammal with ID: 1 -> {}", mammalDAO.findMammalById(1));
    }
}
```

<h3>Compile & Run The Example</h3>

<h4>1. Compile & Run the application</h4>
The following commands show you how to compile and run the Spring Boot application:

```shell
$ mvn clean install
$ mvn spring-boot:run
```

This is the commands and result of the commands. The eight commands within the main Application prints the eight commands out to the console. These are vissible as just before the application is terminated.
 
<img src="{{site.baseurl}}/assets/img/my_images/springboot_h2_jdbc/terminal_h2_database_spring_jdbc.gif" width="100%"/>

<h4>2. View the H2 Console</h4>
To view the H2 Console, type the following url in your browser while the application is running. You will be prompted with the login screen.

<pre style="background-color:black;color:white;padding:10px;">
http://localhost:8080/h2-console
</pre>

After you have typed the above URL in a browser while the application is running, you will be prompted with the login screen. The image display the default settings for the H2 console and will allow you to login withou a password.

<img src="{{site.baseurl}}/assets/img/my_images/springboot_h2_jdbc/h2_console_login.png"/>

The image display the values within the H2 in-memory database while the application is running. The moment the application terminates, the in-memory H2 database will be destroyed.
<img src="{{site.baseurl}}/assets/img/my_images/springboot_h2_jdbc/h2_console_mammal_table.png" width="100%"/>

<h3>Summary</h3>
Congratulations! You have successfully created a Spring Boot application and used Spring JDBC to connect to an H2 in-memory database.