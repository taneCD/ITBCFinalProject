## Client

1. Register
    - HTTP Method: `POST`
    - Endpoint URL: `/api/clients/register`
    - Request body:
        ```json
        {
            "username": "string",
            "password": "string",
            "email": "string"
        }
        ```
    - Responses:
        - 201 - Registered
        - 400 - Bad Request
            - email must be valid
            - username at least 3 characters
            - password at least 8 characters and one letter and one number
        - 409 - Conflict
            - username already exists
            - email already exists

2. Login 
    - HTTP Method: `POST`
    - Endpoint URL: `/api/clients/login`
    - Request body:
        ```json
        {
            "account": "string", // email or username
            "password": "string"
        }
        ```
    - Responses:
        - 200 - OK
            ```json
            {
                "token": "string" // uuid* || JWT || username
            }
            ```
        - 400 - Bad Request
            - Email/Username or password incorrect

3. Create log
    - HTTP Method: `POST`
    - Endpoint URL: `/api/logs/create`
    - Request body:
        ```json
        {
            "message": "string",
            "logType": 0
        }
        ```
    - Request headers:
        - `Authorization` - token
    - Responses:
        - 201 - Created
        - 400 - Bad Request
            - Incorrect logType
        - 401 - Unauthorized
            - Incorrect token
        - 413 - Payload too large
            - Message should be less than 1024

4. Search logs
    - HTTP Method: `GET`
    - Endpoint URL: `/api/logs/search`
    - Request params:
        - `dateFrom` - date
        - `dateTo` - date
        - `message` - string
        - `logType` - int
    - Request headers:
        - `Authorization` - token
    - Responses:
        - 200 - OK
            ```json
            [
              {
                "message": "string",
                "logType": 0,
                "createdDate": "date"
              }  
            ]
            ```
        - 400 - Bad request
            - Invalid dates
            - Invalid logType
        - 401 - Unauthorized
            - Incorrect token

<div style="page-break-after: always;"></div>

## Admin

1. Get all clients
    - HTTP Method: `GET`
    - Endpoint URL: `/api/clients`
    - Request headers:
        - `Authorization` - token (Admin token)
    - Responses:
        - 200 - OK
            ```json
            [
              {
                "id": "uuid",
                "username": "string",
                "email": "string",
                "logCount": 0
              }  
            ]
            ```
        - 401 - Unauthorized
            - Correct token, but not admin
        - 403 - Forbidden
            - Incorrect token

2. Change client password
    - HTTP Method: `PATCH`
    - Endpoint URL: `/api/clients/{clientId}/reset-password`
    - Request body:
        ```json
        {
            "password": "string"
        }
        ```
    - Request headers:
        - `Authorization` - token (Admin token)
    - Responses:
        - 204 - No content
        - 401 - Unauthorized
            - Correct token, but not admin
        - 403 - Forbidden
            - Incorrect token
            
   ______________________________________________________________________________         
            
Technologies:

IntelliJ IDEA 2022.1.4

Java oracle 19,

Microsoft SQL Server Managment studio 18,

Spring Boot (2.7.5),

API testing: Postman v10

Code by: Nebojša Tanasković
