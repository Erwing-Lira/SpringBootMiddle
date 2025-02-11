﻿# Microservices Spring Boot Example

Architecture  
![Microservice Architecture drawio](https://github.com/user-attachments/assets/e92e5f13-a4d1-431c-95f4-a67b552fbe2c)


Process to run:
1. Run ```docker compose up``` in the directory of this repository
2. Run [Config Server Microservice](https://github.com/Erwing-Lira/MicroserviceConfigServer/tree/master)
3. Run [Eureka Server Microservice](https://github.com/Erwing-Lira/MicroserviceEureka/tree/master)
4. Run [Gateway Microservice](https://github.com/Erwing-Lira/MicroserviceGateway/tree/master)
5. Run [Course Microservice](https://github.com/Erwing-Lira/MicroserviceCourse/tree/master) and [Student Microservice](https://github.com/Erwing-Lira/MicroserviceStudent/tree/master)

## How did I create the microservices?
Common configuration to create with Spring Initializer
![spring boot config](https://github.com/user-attachments/assets/fb1568c6-585e-44d1-86a4-4d44dfc250a3)

## Eureka Server
Link to see:
```http://localhost:8761```

![Eureka-1](https://github.com/user-attachments/assets/bff6018c-4b3e-4733-b1f2-3b8deb19bc5b)

## Gateway
All the request will be re-directed to the corresponding port and microservice.

## DataBases
The following configurations depends on the docker-compose.yml to create a container with the databases.
Import some dummy data with the ```import.sql``` in the ```courseDb``` and ```studentDb``` databases.

### PostgresSQL
Export port: ```5432```
#### PgAdmin
To be able to see the PostgreSQL Database:
```http://localhost:9090```

Server: **postgres_database**  
User: **postgres**  
Password: **root**

### MySQL
Export port: ```3306```
#### PhpMyAdmin
To be able to see the MySQL Database:
```http://localhost:9091```

Server: **mysql_db**  
User: **root**  
Password: **root**

## Postman
The following curls allows test the endpoints about students and courses.
### Students
port: ```8090```
##### Save student
```
curl --location 'http://localhost:8080/api/student/create' \
--header 'Content-Type: application/json' \
--data-raw '{
"name":"Erwing",
"lastName": "Martínez",
"email":"erwing.martinez@example.com",
"courseId":2
}'
```

##### Get All students
```
curl --location 'http://localhost:8080/api/student/all'
```

##### Get student by id
```
curl --location 'http://localhost:8080/api/student/search/1'
```

##### Get students by id course
```
curl --location 'http://localhost:8080/api/student/search-by-course/1'
```

### Courses
port: ```8091```
###### Create Course
```
curl --location 'http://localhost:8080/api/course/create' \
--header 'Content-Type: application/json' \
--data '{
"name":"Física",
"teacher":"Profesor F"
}'
```

##### Get All courses
```
curl --location 'http://localhost:8080/api/course/all'
```

##### Get course by id
```
curl --location 'http://localhost:8080/api/course/search/1'
```

##### Get all students by id course
This endpoint interact with the student microservice
```
curl --location 'http://localhost:8080/api/course/search-students-by-course/1'
```
