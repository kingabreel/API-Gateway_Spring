# Products API

This microservice provides CRUD operations for managing product data in a modular Spring Boot microservices architecture. It exposes RESTful endpoints for listing, creating, retrieving, and deleting product entities.

## Technologies

- **Java 17+**
- **Spring Boot 3**
- **Spring Web**
- **Spring Data JPA**
- **H2 In-Memory Database**
- **Lombok**
- **Eureka Client (Spring Cloud Netflix)**

## Base URL

All endpoints are prefixed with: /v1/products

## Endpoints

### `GET /v1/products`

Returns a list of all products.

**Response Example:**
```json
{
  "responseObject": [
    {
      "id": "uuid",
      "name": "Product A",
      "price": 10.5,
      "description": "Example product",
      "stock": 100
    }
  ],
  "message": "products returned"
}
```
### `GET /v1/products/{id}`

Returns a product by its UUID.

**Response Example:**
```json
{
  "responseObject": {
    "id": "uuid",
    "name": "Product A",
    "price": 10.5,
    "description": "Example product",
    "stock": 100
  },
  "message": "product returned"
}
```
### `POST /v1/products`

Creates a new product.

**Request Body:**
```json
{
  "name": "Product B",
  "description": "New product",
  "stock": 50,
  "price": 19.99
}
```
**Response Example:**
```json
{
  "responseObject": {
    "id": "uuid",
    "name": "Product B",
    "price": 19.99,
    "description": "New product",
    "stock": 50
  },
  "message": "product created"
}
```

### `DELETE /v1/products/{id}`
Deletes a product by UUID.

Response:
Returns 204 No Content if successful.
Returns 404 Not Found if the product does not exist.


