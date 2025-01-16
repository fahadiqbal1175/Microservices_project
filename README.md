# Node.js Microservice Project

This project demonstrates a Node.js-based microservices architecture for an e-commerce platform. It is composed of multiple microservices including customer, products, shopping, and a gateway service that serves as an API gateway. Below is a comprehensive guide to understanding the project structure, architecture, and how to run it.

## **Microservices Architecture Overview**
Microservices architecture is an architectural style that structures an application as a collection of small, independent services. Each service runs in its own process, communicates with other services through lightweight mechanisms (usually HTTP or messaging), and is independently deployable.

### **Key Advantages of Microservices Architecture:**
1. **Scalability**: Each service can scale independently based on its load.
2. **Flexibility in Technology**: Each service can be developed using different technologies or programming languages.
3. **Fault Isolation**: A failure in one service does not directly impact other services.
4. **Ease of Deployment**: Services can be deployed independently without affecting the entire system.

### **Microservices in this Project:**
- **Customer Service**: Manages customer data, including account creation and authentication.
- **Product Service**: Handles product details such as listings, prices, and descriptions.
- **Shopping Service**: Manages the shopping cart and order processing.
- **API Gateway**: Acts as a single entry point for client requests, forwarding them to appropriate services and handling authentication.

## **API Gateway**
The API Gateway is a critical component in this microservices architecture. It simplifies the client’s interaction with the system by acting as an intermediary between the client and the services.

### **Responsibilities of the API Gateway:**
- **Routing**: Forwards incoming client requests to the appropriate microservice.
- **Load Balancing**: Distributes incoming requests evenly across instances of a microservice.
- **Authentication and Authorization**: Verifies user credentials and permissions before forwarding requests.
- **Aggregation**: Combines data from multiple services into a single response when necessary.

## **Project Structure**
```
nodejs_microservice/
|-- customer/
|   |-- src/
|   |-- db/
|   |-- .env.dev
|   |-- Dockerfile
|-- products/
|   |-- src/
|   |-- db/
|   |-- .env.dev
|   |-- Dockerfile
|-- shopping/
|   |-- src/
|   |-- db/
|   |-- .env.dev
|   |-- Dockerfile
|-- gateway/
|   |-- index.js
|   |-- package.json
|-- proxy/
|   |-- nginx.conf
|   |-- Dockerfile
|-- docker-compose.yml
```

## **Prerequisites**
Ensure the following software is installed on your system:
- [Node.js](https://nodejs.org/)
- [Docker](https://www.docker.com/)
- [Docker Compose](https://docs.docker.com/compose/)

## **Steps to Run the Project**

### **1. Set Up Environment Variables**
Each service has a `.env.example` file. Copy it and rename it to `.env.dev` in the respective service directories. Set the following values:

#### **Example: `/customer/.env.dev`**
```env
MONGODB_AUTH_URI=mongodb://mongo:27017/customerDB
JWT_SECRET=your_jwt_secret
```

### **2. Build and Run the Services**
1. Navigate to the project’s root directory in your terminal.
2. Run the following command to build the Docker containers:
   ```bash
   docker-compose build
   ```
3. Start all services using:
   ```bash
   docker-compose up
   ```
   This will start the containers for all microservices, MongoDB, and the API gateway.

### **3. Access the Services**
- The API Gateway will be available at: `http://localhost:3000`
- Each service can be accessed through the gateway or directly (if needed):
  - Customer Service: `http://localhost:3001`
  - Product Service: `http://localhost:3002`
  - Shopping Service: `http://localhost:3003`

### **4. Testing the APIs**
Use a tool like [Postman](https://www.postman.com/) or [cURL](https://curl.se/) to test the APIs. You can send requests to the API Gateway at `http://localhost:3000` and specify the desired endpoint (e.g., `/customers`, `/products`, `/cart`).

## **Service Details**

### **Customer Service**
- **Description**: Handles customer-related operations such as registration, login, and profile management.
- **Endpoints**:
  - `POST /customers/register`: Register a new customer.
  - `POST /customers/login`: Authenticate a customer and return a JWT token.

### **Product Service**
- **Description**: Manages product-related operations such as listing products, retrieving product details, and managing inventory.
- **Endpoints**:
  - `GET /products`: Retrieve a list of all products.
  - `GET /products/:id`: Retrieve details of a specific product.

### **Shopping Service**
- **Description**: Handles shopping cart and order processing.
- **Endpoints**:
  - `POST /cart`: Add items to the cart.
  - `POST /checkout`: Process an order.

## **Development Notes**
- Use `npm install` inside each service directory to install dependencies if running locally.
- Logs for each service can be viewed using Docker logs:
  ```bash
  docker logs <container_name>
  ```
- To stop all services:
  ```bash
  docker-compose down
  ```

