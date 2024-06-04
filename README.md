# Search REST API Documentation

This is a Spring Boot application that provides a REST API for searching and creating products. The application uses JPA (Java Persistence API) and JPQL (Java Persistence Query Language) to interact with a MySQL database.

## Project Structure

The project follows the standard Maven project structure and is organized into the following packages:

- `net.javaguides.springboot.controller`: Contains the `ProductController` class for handling HTTP requests.
- `net.javaguides.springboot.entity`: Contains the `Product` entity class, which represents the product data stored in the database.
- `net.javaguides.springboot.repository`: Contains the `ProductRepository` interface, which extends `JpaRepository` and defines a custom JPQL query for searching products.
- `net.javaguides.springboot.service`: Contains the `ProductService` interface and its implementation `ProductServiceImpl` for managing product-related operations.

## Dependencies

The project relies on the following dependencies:

- `spring-boot-starter-data-jpa`: For integrating with JPA and Hibernate.
- `spring-boot-starter-web`: For building web applications and RESTful services.
- `mysql-connector-j`: For connecting to a MySQL database.
- `lombok`: For reducing boilerplate code.

## Configuration

The application configuration is specified in the `application.properties` file located in the project's root directory. This file contains the following properties:

- `spring.application.name`: The name of the application.
- `spring.datasource.url`, `spring.datasource.username`, and `spring.datasource.password`: The database connection details.
- `spring.jpa.properties.hibernate.dialect`: The Hibernate dialect for MySQL.
- `spring.jpa.hibernate.ddl-auto`: The strategy for automatically creating or updating database tables.
- `spring.jpa.hibernate.show_sql` and `spring.jpa.hibernate.format_sql`: Settings for logging SQL statements.

## API Endpoints

The application exposes the following REST endpoints:

### 1. Search Products

- **URL**: `/api/v1/products/search`
- **Method**: GET
- **Query Parameter**: `query` (string)
- **Description**: Searches for products based on the provided query string. The search is performed on the product name and description fields.
- **Response**: A list of `Product` objects matching the search query.

### 2. Create Product

- **URL**: `/api/v1/products`
- **Method**: POST
- **Request Body**: A `Product` object in JSON format.
- **Description**: Creates a new product in the database.
- **Response**: The created `Product` object.

## Classes

### 1. `ProductController`

This class handles the HTTP requests for searching and creating products. It has two methods:

- `searchProducts(@RequestParam("query") String query)`: Retrieves a list of products matching the provided search query by calling the `ProductService.searchProducts()` method.
- `createProduct(@RequestBody Product product)`: Creates a new product by calling the `ProductService.createProduct()` method.

### 2. `Product`

This class represents the product entity stored in the database. It has the following fields:

- `id`: The unique identifier for the product.
- `sku`: The stock keeping unit (SKU) of the product.
- `name`: The name of the product.
- `description`: The description of the product.
- `active`: A flag indicating whether the product is active or not.
- `imageUrl`: The URL of the product image.
- `dateCreated`: The date and time when the product was created.
- `dateUpdated`: The date and time when the product was last updated.

### 3. `ProductRepository`

This interface extends `JpaRepository` and defines a custom JPQL query for searching products. The `searchProducts(String query)` method performs a case-insensitive search on the product name and description fields using the provided query string.

### 4. `ProductService` and `ProductServiceImpl`

The `ProductService` interface defines the methods for managing product-related operations, and `ProductServiceImpl` implements these methods.

- `searchProducts(String query)`: Calls the `ProductRepository.searchProducts()` method to retrieve a list of products matching the search query.
- `createProduct(Product product)`: Saves a new product to the database by calling the `ProductRepository.save()` method.

## Build and Run

To build and run the application, follow these steps:

1. Ensure that you have MySQL installed and running on your system.
2. Create a new database named `search_api` or update the `spring.datasource.url` property in `application.properties` to match your database configuration.
3. Build the application using Maven: `mvn clean install`
4. Run the application: `mvn spring-boot:run`

The application will start, and you can access the REST API endpoints at `http://localhost:8080/api/v1/products`.