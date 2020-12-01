# Proposal: [Add accounts for Users]

## Metadata
|Tag |Value |
|---- | ---------------- |
|Proposal| |
|Authors| |
|Status| |
|Issues| |
|Deadline Feedback||

## Problem
Users can't create accounts.

### Related Issues (if applicable)

JIRA ticket

## Solution
### Proposal

### Implementation
To implement this solution would be necessary to execute the following steps:

1. Make sure that the `library X` is integrated and initialized in the application.
2. Create a seed file that sets up the accounts when booting up the docker instance.
3. Create an endpoint to handle the account creation: POST `api/mobile/accounts`.
4. Add a `UserResource` for the new record that was just created
5. Add swagger docs
6. Include tests for valid and invalid scenarios

### Goals
1. Integrate the library X to allow the application to communicate with our third-party service.
2. Allow users to create accounts.

### Technologies
- Library X: url link

## QA
To QA this solution would be necessary to execute the following steps:

1. Clone/pull the [Insomnia_testsuite repo](Insomnia_testsuite repository url).
2. Run tests against the POST request `api/mobile/accounts` using the following params structure:
    ```
    {
      code: "123456789",
      user_id: user.id,
    }
    ```
3. Ask someone to review and test the files.

### Business Rules
Are there business rules that influence the problem/solution?
No.

### Diagrams and Screens (if applicable)
?

### Load and Performance tests - Application Limits (if applicable)
?

### Compliance impact (if applicable)
No.

### Audit Trail - Is it necessary to audit this feature?
### Cogs
N/A

### Scale and Other Impacts
Yes.

## Delivery Plan
### Waves, Deadline, Rollout And Communication plan
N/A

### Fallback and Rollback plan
The application will be tested on Staging via Insomnia.

### SRE, KPI's, Metrics and SL's Plan (if applicable)
?

## Glossary (if applicable)
N/A
