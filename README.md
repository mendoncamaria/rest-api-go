# User Management 

This project provides RESTful API for user management, allowing you to create, retrieve, update, and delete users. This project is created as part of learning GoLang. 

Find the YouTube video I referred to learn API creation by <a href="https://github.com/DevProblems">DevProblems</a>(Sarang Kumar) <a href="https://www.youtube.com/watch?v=vDIAwtGU9LE">here</a>

## Tech Stack
Go-Gin + MongoDB



## API Endpoints
| HTTP Method | Endpoint                        | Description                                   |
|-------------|---------------------------------|-----------------------------------------------|
| POST        | /v1/user/create                 | Creates a new user in the database.           |
| GET         | /v1/user/get/:name              | Retrieves a user by name from the database.   |
| GET         | /v1/user/getall                 | Retrieves all users from the database.        |
| PATCH       | /v1/user/update                 | Updates an existing user in the database.     |
| DELETE      | /v1/user/delete/:name           | Deletes a user by name from the database.     |

## Installation and running
1. Clone the repository: `git clone https://github.com/mendoncamaria/rest-api-go`
2. Install dependencies: `go mod download`
3. Run the API: `go run main.go`
4. Start your MongoDB Database in Command Prompt/Terminal: `mongod`


## Detailed Documentation

### Create User
**Endpoint:** /v1/user/create <br />
**Type:** POST <br />
**Description:** This endpoint creates a new user in the database. If Database doesn't exist, it will create new and insert values in user collection. If already present, it will insert values in Database. It requires a JSON payload containing the user's information. Upon successful creation, it returns a success message.<br><br>
**Creating New User With all the Details Available:**
```
Request Payload:
{
  "name": "Maxie",
  "age": 25,
  "address": {
    "state": "karnataka",
    "city": "udupi",
    "pincode": 576101
  }
}

Response:
{
  "message": "success"
}
```

**Creating User with Blank Payload:**
```
Request Payload:
{}

Response:
{
  "message": "EOF"
}
```

**Payload with invalid address format:**
```
Request Payload:
{
  "name": "Maxie",
  "age": 25,
  "address": "karnataka"
}

Response:
{
  "message": "json: cannot unmarshal string into Go struct field User.address of type models.Address"
}
```

**Payload with missing name:**
```
Request Payload:
{
  "age": 25,
  "address": {
    "state": "karnataka",
    "city": "udupi",
    "pincode": 576101
  }
}

Response:
{
  "message": "Please Enter a name to add the user"
}
```

**Payload with missing age:**
```
Request Payload:
{
  "name": "Maxie",
  "address": {
    "state": "karnataka",
    "city": "udupi",
    "pincode": 576101
  }
}

Response:
{
  "message": "Please Enter valid age of the user"
}
```
**Payload with missing address:**
```
Request Payload:
{
  "name": "Maria",
  "age": 25,
  "address": {
    "city": "udupi",
    "pincode": 576101
  }
}

OR

{
  "name": "Maria",
  "age": 25,
  "address": {
    "state": "karnataka",
    "pincode": 576101
  }
}

OR

{
  "name": "Maria",
  "age": 25,
  "address": {
    "state": "karnataka",
    "city": "udupi",
  }
}

Response:
{
  "message": "Please Enter valid age of the user"
}
```
### Retrieve Specific User from Database 
**Endpoint:** /v1/user/get/:name <br />
**Type:** GET <br />
**Description:** This endpoint retrieves the user based on the name passed in the URL. The payload will always be blank<br><br>
**Payload:** `{}`<br />
**Retrieve existing User:**
```
URL: localhost:9090/v1/user/get/Maxie

Response:
{
  "name": "Maxie",
  "age": 25,
  "address": {
    "state": "karnataka",
    "city": "udupi",
    "pincode": 576101
  }
}
```

**Get User not available in the Database:**
```
URL: localhost:9090/v1/user/get/Maxei

Response:
{
  "message": "mongo: no documents in result"
}
```

**Incomplete URL to Retrieve User:**
```
URL: localhost:9090/v1/user/get

Response:
404 page not found
```

### Get All Users in Database
**Endpoint:** /v1/user/getall <br />
**Type:** GET <br />
**Description:** This endpoint retrieves all the users in the specific database. The request payload will always be blank<br><br>

**Payload:** `{}`<br />
**Get all details from API:**
```
[     
  {
    "name": "Maxie",
    "age": 25,
    "address": {
      "state": "karnataka",
      "city": "udupi",
      "pincode": 576101
    }
  }
]
```
**If no users are available in the database:**
```
{
  "message": "documents not found"
}
```

### Update user details 
**Endpoint:** /v1/user/update <br />
**Type:** PATCH <br />
**Description:** This endpoint updates the user based on the name passed in the payload. The payload should consist of all parameters<br><br>

**Update existing User:**
```
Payload:
{
  "name": "Maxie",
  "age": 55,
  "address": {
    "state": "karnataka",
    "city": "udupi",
    "pincode": 576101
  } 
}  

Response:
{
  "message": "success"
}
```

**Update User not available in the Database:**
```
Payload:
{
  "name": "Maxei",
  "age": 55,
  "address": {
    "state": "karnataka",
    "city": "udupi",
    "pincode": 576101
  } 
}  

Response:
{
  "message": "no matched document found for update"
}
```

**Incomplete URL to Delete User**
```
URL: localhost:9090/v1/user/delete

Response:
404 page not found
```

### Remove Specific User from Database 
**Endpoint:** /v1/user/delete/:name <br />
**Type:** DELETE <br />
**Description:** This endpoint deletes the user based on the name passed in the URL. The payload will always be blank<br><br>
**Payload:** `{}`<br />
**Delete existing User:**
```
URL: localhost:9090/v1/user/delete/Maxie

Response:
{
  "message": "success"
}
```

**Delete User not available in the Database:**
```
URL: localhost:9090/v1/user/delete/Maxei

Response:
{
  "message": "no matched document found for delete"
}
```

**Incomplete URL to Delete User:**
```
URL: localhost:9090/v1/user/delete

Response:
404 page not found
```
