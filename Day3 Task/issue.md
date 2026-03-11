# Day 3 – Common Errors in Spring Boot CRUD (Notes)

## 1. Application Not Running Error

**Problem:**
Spring Boot application not started.

**Error Example**

```
Connection refused: localhost:8080
```

**Reason**

* Spring Boot server not running.

**Solution**

* Run `PmsApplication.java`
* Check console logs.

---

## 2. Wrong URL Error

**Problem:**
Incorrect API URL in Postman.

**Correct URL**

```
http://localhost:8080/Product/addProduct
```

**Error Example**

```
404 Not Found
```

**Reason**

* Wrong endpoint
* Wrong mapping

**Check**

```java
@RequestMapping("/Product")
@PostMapping("/addProduct")
```

---

## 3. JSON Format Error

**Problem:**
Wrong JSON format in Postman Body.

**Correct Format**

```json
[
  {
    "Category": "hello",
    "Description": "123",
    "inStock": true,
    "name": "Laptop",
    "price": 55000,
    "stockQuantity": 10
  }
]
```

**Error Example**

```
400 Bad Request
```

**Reason**

* Missing brackets
* Wrong key names

---

## 4. Field Name Mismatch Error

**Problem:**
JSON field names not matching `Product.java` fields.

**Example Mismatch**

```
JSON → Category
Java → category
```

**Error**

```
HttpMessageNotReadableException
```

**Solution**

* Ensure JSON keys match Java entity fields.

---

## 5. Database Connection Error

**Error Example**

```
Cannot connect to database
```

**Reason**

* MySQL not running
* Wrong username/password

**Check Configuration**

```
spring.datasource.url
spring.datasource.username
spring.datasource.password
```

---

## 6. Table Not Found Error

**Error Example**

```
Table 'Product' doesn't exist
```

**Reason**

* Table not created
* Wrong database selected

**Run in MySQL**

```sql
use ProductManagementSystem;
select * from Product;
```

---

## 7. Repository Bean Error

**Error Example**

```
No qualifying bean of type ProductRepository
```

**Reason**

* Repository not extending `JpaRepository`.

**Correct Example**

```java
public interface ProductRepository
        extends JpaRepository<Product, Integer>
```

---

## 8. Dependency Injection Error

If `@Autowired` not working.

**Error Example**

```
NullPointerException
```

**Reason**

```
ProductService service = null
```

**Check Annotations**

```java
@RestController
@Service
@Repository
@Autowired
```

---

## 9. HTTP Method Error

If using the wrong HTTP method.

**Error Example**

```
405 Method Not Allowed
```

**Reason**

* Using **GET instead of POST**

**Correct**

```
POST /Product/addProduct
```

---

## 10. Data Not Inserting in Database

**Possible Reasons**

* Entity mapping wrong
* Database not connected
* Transaction error

---
