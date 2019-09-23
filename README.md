# KazanExpres test for Java/Kotlin backend developer
Here lies the description of the test task for Java/Kotlin backend position applicants.
## Task goal
There is a microservice architecture which contains 3 microservices. Each service has external REST endpoints to support several types of clients (web, android, ios). To display the page with orders for a certain customers the information should be obtained from all three microservices: customer-service to display name of the customer, order-service to display all orders, product-service to display product information in orders. In this case, requests can be made asynchronously:

`1 Thread) getting order -> getting products for orders`

`2 Thread) getting customer info`

Such requests potentially slow down clients. But there is a solution to this problem: API gateway. API gateway accepts a single request to display information and obtain information from all other repositories. 

The task is to write a simple gateway which will resolve one request:

`GET /api/v1/orders/?client_id={{id}}` - where id is the identifier in the customer-service. The request should return all orders for the customer in the format described below:
```
{
	customerName: [[string]],
	orders: [
		{
			id: [[number]],
			productId: [[number]],
			productTitle: [[string]]
		}
	]
}
```

Gateway should use these requests from three different microservices:

### Order-service

`GET /api/v1/orders/?client_id={{id}}` - getting all order for the customer with `id`

Response format: 
```
[
	{
		id: [[number]],
		productId: [[number]]
	}
]
```

### Product-service

`GET /api/v1/products/{{id}}` - getting product info for the product with `id`

Response format:
```
{
	id: [[number]],
	title: [[string]]
}
```

### Customer-service

`GET /api/v1/users/{{id}}` - getting information about customer with `id`

Response format:
```
{
	id: [[number]],
	name: [[string]],
}
```

## Requirements

API gateway should support asynchronous execution of requests as it was explained above. The solution also should be extendable to support new endpoints and new microservices.

The main goal of the test task is to asses your ability to think and write clean code. The main criteria are software architecture and clean code. Working code is welcome. Tests for the solution are not mandatory but desired (better with testcontainers).

The solution should be built with one of the build automation tool (Maven/Gradle).

### Stack techonologies:
* Java/Kotlin
* Spring Boot 5+
* Annotation driven configuration
* JDK[8-10]
* Maven-3.5+/Gradle-5+

### Optional part
Add activity logging through Kafka. All requests should be sent to Apache Kafka. Records have to contain information about the incoming request and the outgoing response.

## Submission
Zip archive with repository to hr@kazanexpress.ru with subject `test-java-backend`. The archive shouldn't contain any binaries except mvn/gradle wrappers.
## Good luck!
