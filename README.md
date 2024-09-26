# Go User Management 

This project provides a Go-based RESTful API for user management, allowing you to create, retrieve, update, and delete users.

<a href="https://www.youtube.com/watch?v=vDIAwtGU9LE">ref</a>

## API Endpoints
| HTTP Method | Endpoint                       | Description                                   |
|-------------|---------------------------------|-----------------------------------------------|
| POST        | /v1/user/create                 | Creates a new user in the database.           |
| GET         | /v1/user/get/:name              | Retrieves a user by name from the database.  |
| GET         | /v1/user/getall                | Retrieves all users from the database.      |
| PATCH        | /v1/user/update                  | Updates an existing user in the database.     |
| DELETE      | /v1/user/delete/:name              | Deletes a user by name from the database.      |

# Installation and running
1. Clone the repository: `git clone https://github.com/mendoncamaria/rest-api-go`
2. Install dependencies: `go mod download`
3. Run the API: `go run main.go`
4. Start your MongoDB Database in Command Prompt/Terminal: `mongod`


open thunderclient extension in vscode

create:      
url: http://localhost:9090/v1/user/create     
type: POST     
payload: {
  "name": "Maxie",
  "age": 25,
  "address": {
    "state": "karnataka",
    "city": "udupi",
    "pincode": 576101
  }
}          
response: {
  "message": "success"
}
-x-
payload: blank
response: {
  "message": "EOF"
}
-x-
invalid address format
payload: {
  "name": "Maxie",
  "age": 25,
  "address": "karnataka"
}
response: {
  "message": "json: cannot unmarshal string into Go struct field User.address of type models.Address"
}
-x-
missing name

payload: {
  "age": 25,
  "address": {
    "state": "karnataka",
    "city": "udupi",
    "pincode": 576101
  }
}
response: {
  "message": "Please Enter a name to add the user"
}
-x-
missing age

payload: {
  "name": "Maria",
  "address": {
    "state": "karnataka",
    "city": "udupi",
    "pincode": 576101
  }
} 
response: {
  "message": "Please Enter valid age of the user"
}
-x-
missing address

payload: {
  "name": "Maria",
  "age": 25,
  "address": {
    "city": "udupi",
    "pincode": 576101
  }
} 
{
  "name": "Maria",
  "age": 25,
  "address": {
    "state": "karnataka",
    "pincode": 576101
  }
} 
{
  "name": "Maria",
  "age": 25,
  "address": {
    "state": "karnataka",
    "city": "udupi",
  }
} 
response: {
  "message": "Please Enter valid age of the user"
}
----------------------------------------------------------------------------
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
