# Go User Management 

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

**Creating User with Blank Payload**
```
Request Payload:
{}

Response:
{
  "message": "EOF"
}
```

**invalid address format**
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

**missing name**
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

**missing age**
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
**missing address**
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

get specific user:      
url: http://localhost:9090/v1/user/get/Maxie     
type: GET     
payload: blank     
response 1 (no user found): {
  "message": "mongo: no documents in result"
}     
response 2 : {
  "name": "Maxie",
  "age": 25,
  "address": {
    "state": "karnataka",
    "city": "udupi",
    "pincode": 576101
  }
}

-------------------------
get all users:      
url: http://localhost:9090/v1/user/getall     
type: GET     
payload: blank     
response: [     
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

-------------------------
update user details:      
url: http://localhost:9090/v1/user/update     
type: PATCH     
payload: {
  "name": "Maxie",
  "age": 55,
  "address": {
    "state": "karnataka",
    "city": "udupi",
    "pincode": 576101
  }
  
}     
response: {
  "message": "success"
}

-------------------------
delete user:      
url: http://localhost:9090/v1/user/delete/Maxie     
type: DELETE      
payload: blank     
response: {
  "message": "success"
}
