
# Spring Boot Todo App with MySQL

This project is a **Spring Boot Todo Application** with a **MySQL** database. The application allows users to manage tasks in a simple to-do list.

### Prerequisites

Before running the application, make sure you have the following installed on your system:

- **Docker** (for containerization)
- **Docker Compose** (to orchestrate multi-container applications)
- **Java 8 or above** (for building the Spring Boot application)
- **Maven** (for building the application, if not using Docker)
- **MySQL** (will be set up via Docker)

### Project Structure

The project follows a standard **Spring Boot** structure:

```
├── README.md          # This file with setup instructions
├── mvnw               # Maven Wrapper for building the application
├── pom.xml            # Maven configuration file for dependencies
├── src/
│   ├── main/
│   │   ├── java/      # Java code for the application
│   │   └── resources/ # Configuration files and templates
│   └── test/          # Test files for the application
├── target/            # Compiled application files (including the .jar or .war)
├── Dockerfile         # Dockerfile for containerizing the app
└── docker-compose.yml # Docker Compose file to run the app with MySQL
```

### Setup Instructions

1. **Clone the Repository**:
   Clone the project to your local machine:

   ```bash
   git clone https://github.com/Madhan152004/todo-app-springboot-mysql.git
   ```

2. **Build the Application**:
   If you're not using Docker, you need to build the Spring Boot application manually. You can build the application using **Maven**:

   ```bash
   ./mvnw clean package
   ```

   This will create the `todo-0.0.1-SNAPSHOT.jar` file in the `target/` folder.

3. **Dockerize the Application**:
   If you're using Docker, follow these steps:

   - The **Dockerfile** is configured to build and run the application in a container.
   - **Docker Compose** will run both the application and the MySQL container together.

4. **Start the Application with Docker Compose**:
   Use Docker Compose to start the application along with the MySQL database:

   ```bash
   docker-compose up --build
   ```

   This command will:
   - Build the Docker images.
   - Start both the Spring Boot application and MySQL containers.

5. **Access the Application**:
   - **Locally (on your machine)**: Once the containers are running, you can access the application at:

     ```
     http://localhost:8080
     ```

   - **On an EC2 instance**: If you're running the application on an EC2 instance, you need to access the application using the EC2 instance's public IP or domain name, followed by port 8080. For example:

     ```
     http://<your-ec2-public-ip>:8080
     ```

     - Ensure that port `8080` is open in your EC2 instance's security group to allow inbound traffic on this port.
     - Replace `<your-ec2-public-ip>` with the actual public IP of your EC2 instance.

6. **Access MySQL Database**:
   The MySQL database will be available on port `3306`. You can access it using MySQL client tools (like MySQL Workbench or `mysql` CLI) with the following credentials:

   - **Host**: `localhost` (for local setups) or `<your-ec2-public-ip>` (for EC2 setups)
   - **Port**: `3306`
   - **Username**: `todo`
   - **Password**: `todo`
   - **Database**: `tododb`

### Files to Be Added

- **`application.properties`**: You need to configure your database connection in the `src/main/resources/application.properties` file:
   - `spring.datasource.url=jdbc:mysql://localhost:3306/tododb`
   - `spring.datasource.username=todo`
   - `spring.datasource.password=todo`

### Notes

- The database schema is automatically created via Hibernate (JPA) when the application starts.
- **Docker Compose** manages both the Spring Boot application and the MySQL database, so you don't need to manually set up MySQL.

### Troubleshooting

- If you encounter any issues with Docker containers, check the container logs with:
  
  ```bash
  docker-compose logs
  ```

