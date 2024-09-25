# My Awesome CRUD API 

This is a backend focussed project mainly used to learn CRUD (create, read, update, delete), retrieve from Database(using mongodb) by using the api

<a href="https://www.youtube.com/watch?v=vDIAwtGU9LE">ref</a>


run: 
`go run main.go`

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
