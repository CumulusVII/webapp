# :cloud: cirrus-webapp [![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](./LICENSE) [![Build AMI Test](https://github.com/cloud-cirrus/webapp/actions/workflows/amibuild.yml/badge.svg)](https://github.com/cloud-cirrus/webapp/actions/workflows/amibuild.yml)

## :wrench: Prerequisites

This project requires NodeJS, NPM, local Postgresql server set up.
## :hammer: Build Instructions

Start with cloning this repo on your local machine:

1. Clone this repo to local.
```
git@github.com:jeeltpatel/webapp.git
```

2. Start Development
```
$cd webapp
npm install
```
3. To Start the application, run
```   
npm start   
``` 
4. Run your development Server

The site is now running at `http://localhost:3000`
## :busstop: API Endpoints

This cloud-native web appilcation RESTful API mirror the API mentioned in the [Swagger Docs here](https://app.swaggerhub.com/apis-docs/fall2022-csye6225/cloud-native-webapp/assignment-02#/Account).

### :lock: Authenticated Users

- **GET** _/v1/account/{accountID}_ : Get the user account information
  - **AccountID:** String (Required)
  - **Response:** 200 _OK_, **Media Type:** Application/JSON
  - **Response:** 401 _Unauthorized_
  - **Response:** 403 _Forbidden_

- **PUT** _/v1/account/{accountID}_ : Update the user's account information
  - **AccountID:** String (Required)
  - **Request Body:** Application/JSON (Required)

    ```json
      {
        "first_name": "Julia",
        "last_name": "Summer",
        "password": "somepassword"
      }
    ```

  - **Response:** 204 _No Content_
  - **Response:** 400 _Bad Request_
  - **Response:** 401 _Unauthorized_
  - **Response:** 403 _Forbidden_

### :unlock: Unauthenticated Users

- `**POST** _/v1/account_ : Create a user account
  - **Request Body:** Application/JSON (Required)

    ```json
      {
        "first_name": "Julia",
        "last_name": "Summer",
        "password": "somepassword",
        "username": "julia.summer@example.com"
      }
    ```

  - **Response:** 201 _User Created_
  - **Response** 400 _Bad Request_

### :lotus_position: Schemas For Users

```text
  {
    id: string($uuid)
      example: d290f1ee-6c54-4b01-90e6-d701748f0851
      readOnly: true
    first_name*: string
      example: Julia
    last_name*: string
      example: Summer
    password*: string($password)
      example: somepassword
      writeOnly: true
    username*: string($email)
      example: jane.doe@example.com
    account_created: string($date-time)
      example: 2017-02-02T04:11:23.001Z
      readOnly: true
    account_updated: string($date-time)
      example: 2017-02-02T04:12:33.001Z
      readOnly: true
  }
```
### :lock: Authenticated Users

- **POST** _/v1/documents/_ : Post user document 
  - **DocumentID:** String (Required)
  - **Payload Body:** Form-Data/File (Required)

    ```shell
      Key:document
      Value:Select File
    ```
  - **Response:** 201 _OK_, **Media Type:** Application/JSON
  - **Response:** 400 _Bad Request_
  - **Response:** 401 _Unauthorized_

- **GET** _/v1/documents/{doc_id}/_ : Get user particular document  
  - **DocumentID:** String (Required)
  - **Response:** 200 _OK_, **Media Type:** Application/JSON
  - **Response:** 401 _Unauthorized_
  - **Response:** 403 _BadRequest_
- **DELETE** _/v1/documents/{doc_id}/_ : Delete user particular document  
  - **DocumentID:** String (Required)
  - **Response:** 204 _NoContent_
  - **Response:** 401 _Unauthorized_
  - **Response:** 404 _NotFound_

### :lotus_position: Schemas For Document

```text
  {
    doc_id: string($uuid)
      example: d290f1ee-6c54-4b01-90e6-d701748f0851
      readOnly: true
    user_id*: string
      example: d290f1ee-6c54-4b01-90e6-d701748f0851
    name*: string
      example: Summer
    date_created*: string($date-time)
      example: 2016-08-29T09:12:33.001Z
      writeOnly: true
    s3_bucket_path*: string($s3Path)
      example: (https://summer-bucket.s3.amazonaws.com/Screen%20Shot%202022-10-17%20at%2012.42.43%20PM.png)
    account_created: string($date-time)
      example: 2017-02-02T04:11:23.001Z
      readOnly: true
    account_updated: string($date-time)
      example: 2017-02-02T04:12:33.001Z
      readOnly: true
  }
```

### :key: Verify Users

- **GET** _/v1/verifyUserEmail/email=user@example.com&token=sometoken : Get user verified   
 
  - **Response:** 200 _OK_, **Media Type:** Application/JSON
  - **Response:** 401 _Unauthorized_
  - **Response:** 403 _BadRequest_

## :test_tube: Testing

To run the test suite, use the following commands:

- To run the test suite in interactive mode:

```shell
  #for yarn users
  yarn test
  #for npm users
  npm run test
```

- To run the test suite without interactive mode:

```shell
  #for yarn users
  yarn test
  #for npm users
  npm run test
```
## 👨🏻‍💻 Author 
 Jeel Patel