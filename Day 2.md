Spring Framework Notes – Day 2

Overview

These notes cover the basics of Spring Framework, including:

- Spring Framework Introduction
- Spring Core
- Spring IoC (Inversion of Control)
- Spring MVC
- Spring Boot Architecture
- Example Product Management API using Spring Boot
- MySQL Database Integration
- API Testing using Postman

---

1. What is Spring Framework

Spring is a Java Framework used to build enterprise-level applications.

Features

- Lightweight framework
- Dependency Injection
- Aspect-Oriented Programming
- MVC architecture
- Easy integration with databases
- Simplifies Java development

---

2. Spring Core

Spring Core is the foundation module of the Spring Framework.

Responsibilities

- Dependency Injection
- Bean Management
- IoC Container

Important Concepts

Concept| Description
Bean| Object managed by Spring
Dependency Injection| Injecting objects automatically
IoC Container| Manages object lifecycle

---

3. Spring IoC (Inversion of Control)

Definition

Inversion of Control means Spring container creates and manages objects instead of the developer.

Example

Without Spring

Product product = new Product();

With Spring

Spring automatically creates objects using annotations.

Benefits

- Loose coupling
- Easy testing
- Better modular design
- Automatic dependency management

---

4. Spring MVC

Spring MVC is used to build web applications and REST APIs.

MVC Architecture
```
Layer| Responsibility
Model| Data and business logic
View| UI
Controller| Handles requests
```
Flow of Spring MVC
```
Client Request
     ↓
Controller
     ↓
Service Layer
     ↓
DAO / Repository
     ↓
Database
```
---

5. Spring Boot Architecture

Spring Boot simplifies Spring development.

Main Layers
```
Controller
   ↓
Service
   ↓
DAO
   ↓
Repository
   ↓
Database
```

---

6. Spring Boot Application

Main Class
```
@SpringBootApplication
public class PmsApplication {

    public static void main(String[] args) {
        SpringApplication.run(PmsApplication.class, args);
    }

}
```
Annotation

"@SpringBootApplication"

Purpose:

- Starts Spring Boot application
- Enables auto configuration

It combines:

@Configuration
@EnableAutoConfiguration
@ComponentScan

---

7. Creating Model Class

Product.java
```
@Entity
public class Product {

@Id
@GeneratedValue(strategy = GenerationType.IDENTITY)
private long id;

private String name;
private String description;
private String category;
private int price;
private int stockQuantity;
private boolean inStock;

}
```
Annotations Used

Annotation| Purpose
"@Entity"| Converts class into database table
"@Id"| Primary key
"@GeneratedValue"| Auto increment ID

---

8. Generate Getters and Setters

In Eclipse:
```
Right Click
   ↓
Source
   ↓
Generate Getters and Setters
```
Select all fields and click Generate.

---

9. Repository Layer

ProductRepository.java
```
@Repository
public interface ProductRepository extends JpaRepository<Product, Long> {

}
```
Purpose

- Connects Java code with database
- Provides CRUD operations automatically

---

10. DAO Layer

ProductDao.java
```
@Repository
public class ProductDao {

@Autowired
ProductRepository repo;

public List<Product> getProduct(){
return repo.findAll();
}

}
```
Purpose

Handles database logic.

---

11. Service Layer

ProductService.java
```
@Service
public class ProductService {

@Autowired
ProductDao dao;

public List<Product> getProduct(){
return dao.getProduct();
}

}
```
Purpose

Contains business logic.

---

12. Controller Layer

ProductController.java
```
@RestController
public class ProductController {

@Autowired
ProductService service;

@GetMapping("/getProduct")
public List<Product> getProduct(){
return service.getProduct();
}

}
```
Purpose

Handles HTTP requests and returns API responses.

---

13. Database (MySQL)

Create Database
```
create database ProductManagementSystem;
```
```
use ProductManagementSystem;
```
```
Insert Data

INSERT INTO product (name, description, category, price, stock_quantity, in_stock)
VALUES
('Laptop','High performance laptop','Electronics',65000,10,true),
('Smartphone','Android smartphone with 128GB storage','Electronics',25000,25,true),
('Office Chair','Ergonomic office chair','Furniture',5000,15,true);
```
Retrieve Data
```
select * from product;
```

---

14. API Testing (Postman)

Run the Spring Boot application.

Use GET request:
```
http://localhost:8080/getProduct
```

Example Response
```
[
{
"id":1,
"name":"Laptop",
"category":"Electronics"
}
]
```
---

15. Tools Used

- Java
- Spring Boot
- Spring Data JPA
- MySQL
- Postman
- Eclipse / IntelliJ
- Maven

---

Conclusion

This project demonstrates:

- Spring Boot application structure
- MVC architecture
- REST API development
- Database integration using JPA
- API testing with Postman
