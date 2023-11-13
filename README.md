# **OakWood**

## **Table of Contents**

- [Team](#team)
- [Description](#project-description)
- [Architecture](#architecture)
- [Concurrency patterns usage](#concurrency-patterns-usage)
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
| Table reservation aprove| In the list of items that the user will get after choosing the needed table, he will need to set the date of the reservation, choose hours, book them and get aprove from restaurant                                                                                                            |  
| Table reservation canncel | When a user change his plan he can cancel reservation of his table in restaurants                

**Use case diagram**

<img src="use-case-diagram.png">
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

## **Identity Management**

Identity Management in our restaurant reservation web application is a key aspect that ensures user security and personalization. Below is a description of the functionality and features associated with the identity management system:

Registration and Login:
The application allows users to create accounts by entering basic information (name, email, password). Upon registration, each user will be assigned a unique identifier. Password must be at least 8 characters long, including at least one uppercase and lowercase letter and one number. Email verification when registering with an email address that is already in use.

User profile:
After registration, users can add and modify information in their profile, such as contact information, food preferences, or other personalized information.

Password Recovery:
Enable users to recover forgotten passwords via email with a secure verification mechanism.

## **Functional requirements**

**Role: Client**
Registration and Login:
- Ability to register a new account.
- Authorization by e-mail.

User profile:
- Changing and updating personal data in the profile.
- Add and change preferences for type of cuisine, allergies, etc.

Reservation of Tables:
- Choice of restaurant, date and time for booking.
- Selection of the number of guests.
- View the history of your reservations and their cancellations.
- Receipt of booking confirmation via e-mail.

Ratings and Reviews:
- Leave reviews and ratings for restaurants visited by the user.

Notification:
- Receiving notifications about promotions and news from the selected restaurant.


**Role: Administrator**
Management of Restaurants:
- Adding new restaurants and editing them.
- Indication of working hours, type of cuisine and other information.

Management of Reservations:
- View and manage all bookings.
- Confirmation or cancellation of reservations.

Statistics and Analytics:
- View statistics on the popularity of restaurants.
- Analysis of user reviews and ratings.

Management of Promotions and Discounts:
- Adding and editing promotions and discounts for restaurants.

User Management System:
- Providing the ability to block or edit user accounts in cases of violations.

Reporting:
- Preparation of reports on the operation of restaurants and the effectiveness of the application.


## **Architecture**

| Part of project | Description                                               | Technologies                  |
| --------------- | --------------------------------------------------------- | ----------------------------- |
| Back end        | API based on CQRS                                         | .NET 5, ASP.Net Core          |
| Fron end        | SPA                                                       | React, Type Script, AntDesign |
| DB              | SQL database for user management and NoSQL for user reservations | Azure SQL Database, MongoDB   |

<br/>
<img src="architecture-diagram.png">
<br/>
<br/>

**ER diagram**

<img src="./Documentation/Go & See ER-diagram.png">
<br/>
<br/>

## **Concurrency patterns usage**

Optimistic Concurrency Control:

**Database Schema:**
Include a version or timestamp field in the reservation table.

**Reservation Retrieval (Client Side):**
Fetch both the reservation details and the current version or timestamp value when displaying reservation information.

**User Edits (Client Side):**
When a user wants to modify a reservation, include the original version or timestamp value along with the updated reservation details.

**Server-Side Update:**
Compare the version or timestamp from the client with the one in the database.
If they match, proceed with the update; if not, handle the conflict by notifying the user.

**Conflict Resolution (Server Side and User Interface):**
Notify the user of a conflict and provide options to reload data, reapply changes, or merge changes with the updated reservation details.

**Client Notification:**
Use user-friendly messages and interface components to inform users of successful updates or conflicts.

**Concurrency Logging:**
Log concurrency conflicts and resolutions for auditing and analysis.

Pessimistic Concurrency Control:

**Database Schema:**
Include a lock_status field in the reservation table to indicate whether a reservation is currently locked by a user.

**Reservation Locking (Server Side):**
When a user starts editing a reservation, set the lock_status to "locked" in the database to prevent other users from editing the same reservation concurrently.
If the reservation is already locked, notify the user attempting to edit that the reservation is currently being edited by another user.

**Reservation Unlocking (Server Side):**
When the user finishes editing or cancels the reservation update, unlock the reservation by setting the lock_status to "unlocked."

**Timeouts and Release Mechanism:**
Implement a mechanism to release locks automatically after a certain period to handle cases where a user might close the browser or navigate away without explicitly unlocking.

**User Interface Feedback:**
Provide clear indications in the user interface when a reservation is locked by another user to avoid confusion.

Detecting Concurrency Conflicts:

**Database Schema:**
Ensure that each record in the relevant tables has a version or timestamp field.

**Reservation Retrieval (Client Side):**
When a user retrieves data for editing or viewing, fetch not only the reservation details but also the current value of the version or timestamp field.

**User Edits (Client Side):**
When the user makes changes to a reservation and submits them for an update, include the original version or timestamp value along with the updated reservation details.
**Server-Side Update:**
Upon receiving an update request, compare the version or timestamp from the client with the one in the database.
If they match, it means no other user has modified the record since the user loaded the data. Proceed with the update.
If there's a mismatch, handle the conflict by notifying the user.

**Conflict Handling (Server Side):**
Notify the user about the conflict and provide options for resolution.
Options may include reloading the data and reapplying their changes or merging their changes with the updated data.

## **Telemetry**

## **Storage**

## **Resiliency Model**

## **Security Model**

## **Hosted Service**

## **Telemetry**

Local application insights

## **Monitoring**
