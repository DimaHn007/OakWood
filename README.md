# **OakWood**

## **Table of Contents**

- [Team](#team)
- [Description](#project-description)
- [Architecture](#architecture)
- [Storage](#storage)
- [Resiliency model](#resiliency-model)
- [Security model](#security-model)
- [Hosted Service](#hosted-service)
- [Telemetry](#telemetry)
- [Monitoring](#monitoring)

## **Team**

- Malets Bohdan
- Hnativ Dmytro 

## **Project Description**

### **Book a table**

This web application is for reserving tables in restaurants in advance and right before the trip.

### **Functional description**

The user can create an account and manage it. There will be the next pages for logged-in users: _My profile_ and _Reservations_ and the _Restaurants_ page :

- reserved
- restaurants
- profile

**Use cases**

| Use case                | Description                                                                                                                                                                                                                                                                                                |
| ----------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Sign up                 | Guest of web system can sign up by filling in next fields: <ul><li>Username</li><li>Email</li><li>Password</li></ul>                                                                                                                                                                                       |
| Log in                  | If the user has created an account he is able to log in to the system, by entering Email and Password that were filled in sign in the form before                                                                                                                                                          |
| Password recovery       | If a user forgot his password he can recover it by entering his email address. Then he will get a letter with the next instructions about password recovery                                                                                                                                                |
| Profile editing         | The user that is logged in the system can edit his personal information, such as Username, Email address and password                                                                                                                                                                                      |
| Table reservation       | The user is able to reserve a table using templates that are suggested by the web system. He needs to choose a table and based on his choice he will get a list of restaurans needed to be done                                                                                                            |
| Table reservation aprove| In the list of items that the user will get after choosing the needed table, he will need to set the date of the reservation, choose hours, book them and get aprove from restaurant
                                                                         |
| Table reservation canncel| When a user change his plan he can cancel reservation of his table in restaurants 
|


**Use case diagram**

<img src="./Documentation/use-case-diagram.png">
<br/>
<br/>

**Guest sequence diagram**

<img src="./Documentation/guest-sequence-diagram.png">
<br/>
<br/>

**User sequence diagram**

<img src="./Documentation/user-sequence-diagram.png">
<br/>
<br/>

## **Architecture**

| Part of project | Description                                               | Technologies                  |
| --------------- | --------------------------------------------------------- | ----------------------------- |
| Back end        | API based on CQRS                                         | .NET 5, ASP.Net Core          |
| Fron end        | SPA                                                       | React, Type Script, AntDesign |
| DB              | SQL database for user management and NoSQL for user trips | Azure SQL Database, MongoDB   |

<br/>
<img src="./Documentation/architecture-diagram.png">
<br/>
<br/>

Example of _Trip_ document for MongoDB:

```json
{
  "id": "00000000-0000-0000-0000-000000000000",
  "status": 1,
  "userId": "00000000-0000-0000-0000-000000000000",
  "name": "string",
  "description": "string",
  "startDate": "2021-10-23T17:36:04.432Z",
  "endDate": "2021-10-23T17:36:04.432Z",
  "itemsToTake": [
    {
      "id": "00000000-0000-0000-0000-000000000000",
      "name": "string",
      "isTaken": true
    }
  ],
  "toDoNodes": [
    {
      "id": "00000000-0000-0000-0000-000000000000",
      "name": "string",
      "description": "string",
      "type": 1,
      "date": "2021-10-23T17:36:04.432Z",
      "status": 1
    }
  ]
}
```

Example of _TripTemplate_ document for MongoDB:

```json
{
  "id": "00000000-0000-0000-0000-000000000000",
  "name": "string",
  "itemsToTake": [
    {
      "id": "00000000-0000-0000-0000-000000000000",
      "name": "string",
      "isTaken": true
    }
  ],
  "toDoNodes": [
    {
      "id": "00000000-0000-0000-0000-000000000000",
      "name": "string",
      "description": "string",
      "type": 1,
      "date": "2021-10-23T17:36:04.432Z",
      "status": 1
    }
  ]
}
```

**ER diagram**

<img src="./Documentation/Go & See ER-diagram.png">
<br/>
<br/>

## **Storage**

## **Resiliency Model**

## **Security Model**

## **Hosted Service**

## **Telemetry**

Local application insights

## **Monitoring**
