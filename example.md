# Proposal: Our current architecture / system design does not support multiple users

Author: [@vbrazo](https://github.com/vbrazo)

## Problem

The way the application is currently designed makes it impossible to appease the following user story from pilot scope: *"I want to add a second admin to give them equal access to their users' accounts".*


### Current Design
<pre>
+----------------------------------------------------------+
|  Authentication Engine                                   |
|                                                          |
|                                                          |
|  +-----------------------+                               |
|  |                       |                               |
|  |     Admin             |                               |
|  |                       |    +----------------------+   |
|  |                       |    |                      |   |
|  +-----------------------+    |   Admin Resources    |   |
|                               |                      |   |
|  +-----------------------+    |                      |   |
|  |                       |    +----------------------+   |
|  |      User             |                               |
|  |                       |                               |
|  |                       |                               |
|  +-----------------------+                               |
|                                                          |
+----------------------------------------------------------+
</pre>

Some of the characteristics of this design:

* Admins can have multiple users;
* User can have just one admin;
* All resources (accounts, handler, objects) are tied to the admin;

### Related Issues (if applicable)

[JIRA ticket](JIRA ticket)

## Solution

### Proposal

<pre>      
+---------------------------+  +-----------------------+   +-----------------------+
|                           |  |                       |   |                       |
|  Identity Engine          |  | Authentication Engine |   |Authorization Engine   |
|                           |  |                       |   |                       |
| +------------------+      |  | +-----------------+   |   | +-------------------+ |
| |                  |      |  | |                 |   |   | |                   | |
| | Admin            |      |  | | User            |   |   | | Permission        | |
| |                  |      |  | |                 |   |   | |                   | |
| +------------------+      |  | +-----------------+   |   | +-------------------+ |
|                           |  |                       |   |                       |
| +------------------+      |  |                       |   | +-------------------+ |
| |                  |      |  |                       |   | |                   | |
| | User             |      |  |                       |   | | Resource          | |
| |                  |      |  |                       |   | |                   | |
| +------------------+      |  |                       |   | +-------------------+ |
|                           |  |                       |   |                       |
| +------------------+      |  |                       |   |                       |
| |                  |      |  |                       |   |                       |
| |  Account         |      |  |                       |   |                       |
| |                  |      |  |                       |   |                       |
| +------------------+      |  |                       |   |                       |
+---------------------------+  +-----------------------+   +-----------------------+
</pre>

The solution consists of split the Authentication domain into three parts, also create three engines to separate these concerns:

### Identity

The Identity is responsible for representing the system's users and their relationship, exposing a public API to enable other components to interact with it.

The Identity contains three main entities: Admin, User, and Account.

The Account is the object responsible for hold information about admins and users and their connection. Differently from the current approach, all resources will be tied to the Account.

Additionally, the Account object must have an Owner, the Admin, with unlimited permissions and the only responsible for inviting other admins.

### Authentication

The Authentication is responsible for managing admin and user sessions, exposing public API to enable host application to create, expire, and verify the signature of JWTs, signup, sign-in, and recover the password.

### Authorization

The Authorization is responsible for managing which resources Admin and users can access. For instance, the Admin with an owner profile can invite another Admin and assign it the ability to sign up only.


### Goals

* Authentication and Authorization extensibility and reuse;
* The ability to have multiple admins in one account;
* A scalable design that satisfies not just alpha, but can evolve to more mature phases of the product;
* Avoid rework and delaying future product development;

### Technologies

* JWT;
* Rails Engines;
* Postgres Database;

### Business Rules

As a Admin, I want to add a second admin to give them equal access to my users' accounts.

### Compliance impact (if applicable)
NA

### Audit Trail - Is it necessary to audit this feature?
### Cogs
?

### Scale and Other Impacts
Is this proposal prepared to scale?
Yes, the only concern is about the tables, and for that, we can mitigate with sharding in the subsequent interactions. It will be easy because now we have a main Account object we can use as a namespace.

## Delivery Plan
### Waves, Deadline, Rollout And Communication plan
NA

### Fallback and Rollback plan
NA

### SRE, KPI's, Metrics and SL's Plan (if applicable)

Some metrics we can add in the future:

* Number of sign-ins;
* Number of sign-ups;

## Glossary (if applicable)
A list of important words and definitions to this project and its meanings.

[JWT - JSON WEB TOKEN](https://jwt.io/)

[Authentication vs Authorization](https://www.okta.com/identity-101/authentication-vs-authorization/#:~:text=Authentication%20and%20authorization%20might%20sound,permission%20to%20access%20a%20resource.)
