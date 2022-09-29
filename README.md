## REST CRUD API with Spring Data REST

**The Problem**

+ We have created a REST API for **Employee**
+ Need to create REST API for another entity?
    + Customer, Student, Product, Book ...

+ Do we have to repeat the same code again and again ????

**Spring Data REST - Solution**

+ **Spring Data RSET** is the solution
+ Leverages or existing **JpaRepository**

+ Spring will give us a REST CRUD implementation
    + Helps to minimize boiler-plate REST code
    + No new coding required


**REST API**

+ Spring Data REST will expose these endpoints

| HTTP Method | Endpoint                    | CRUD Action                 |
| ----------- | --------------------------- | --------------------------- |
| POST        | /api/employees              | Create a new employee       |
| GET         | /api/employees              | Read a list of employees    |
| GET         | /api/employees/{employeeId} | Read a single employee      |
| PUT         | /api/employees              | Update an existing employee |
| DELETE      | /api/employees/{employeeId} | Delete an existing employee |

**Spring Data REST - How Does It Work?**

+ Spring Data Rest will scan our project for **JpaRepository**
+ Expose REST APIs for each entity type of our **JpaRepository**


**REST Endpoints**

+ By default, Spring Data Rest will create endpoints based on entity type
+ Simple pluralized form
    + Fort character of Entity type is lowercase
    + Then just adds an "s" to entity

```JAVA
public interface EmployeeRepository extends JpaRepository<Employee, Interger> {
}
```
+ `Employee` will be `/employees`

**Development Process**

1. Add Spring Data Rest to our Maven POM file

Thats it , Absolutely NO CODING required

```XML
<dependency>
  <groupId>org.sprimgframework.boot</groupId>
  <artifactId>spring-boot-starter-data-rest</artifactId>
</dependency>
```

**In A Nutshell**

For Spring Data REST, we only need 3 items
1. Our entity: **Employee**
2. JpaRepository: **EmployeeRepository extends JpaRepository**
3. Maven POM dependency for: **spring-boot-starter-data-rest**


**Application Architecture**

_Before_
<img src="https://user-images.githubusercontent.com/80107049/193036903-a30ef3e4-6082-4bc0-b72a-794042c0b744.png" width="500"/>


_After_
<img src="https://user-images.githubusercontent.com/80107049/193037021-2233cfbc-f01c-4707-b2ae-2812c9bcd794.png" width="500"/>



**HATEOAS**

+ Spring Data Rest endpoints are HATEOAS compliant
    + **HATEOAS:** Hypermedia as the Engine of Application State

+ Hypermida-driven sites provides information to access REST interface
    + Think of it as meta-data for REST data

+ Spring Data REST response using HATEOAS
+ For example REST response from: **GET /employees/3**

```JSON
{
  "firstName": "Avani",
  "lastName": "Gupta",
  "email": "avani@gmail.com",
  "_links":{
    "self": {
      "href": "http://localhost:8080/employees/3"
    },
    "employee": {
      "href" : "http://localhost:8080/employees/3"
    }
  }
}
```
+ First we have employee data
+ Than response meta-data Links to data

+ For collection, meta-data includes page size, total elements, page etc
+ HATEOAS uses Hypertext Application Language(HAL) data format

**Advance Features**

+ Spring Data REST advanced features
    + Pagination, sorting and searching
    + Extending and adding custom queries with JPQL
    + Query Domain Specific Language (Query DSL)

