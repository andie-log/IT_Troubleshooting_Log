# Admin Account Setup & Microsoft Teams Messaging Test

## Overview
This lab focuses on creating a dedicated IT administrator account, assigning appropriate administrative roles, and validating real-time communication between end users and administrators using Microsoft Teams.
The goal was to simulate a realistic helpdesk environment while applying basic security best practices for administrative accounts.

## Environment
- Microsoft Entra ID
- Microsoft 365 Admin Center
- Microsoft Teams (Web)
- Microsoft 365 Business Trial

## 1. Administrator Account Creation
### Account Design Consideration
- Initially considered creating an account named:
  - Administrator@domain
- Re-evaluated this approach due to security concerns:
  - Highly predictable account name
  - Common target for brute-force and credential-stuffing attacks

### Final Decision
- Created a dedicated admin account with a less predictable naming convention:
  - IT_Admin_Name@domain
- This approach:
  - Reduces exposure to common attack patterns
  - Clearly separates IT administrative users from standard user accounts

## 2. Assigning Administrative Roles
### Procedure
- Logged into Microsoft 365 Admin Center using an existing admin account
- Navigated to:
  - Users → Active users → ITAdmin_<Name> → Account → Roles
- Selected Manage roles
- Enabled Admin center access
- Assigned the Global Administrator role
  - Chosen for full-feature testing and lab purposes
  - Noted that in real-world environments, a Helpdesk Administrator role would be more appropriate for day-to-day support tasks
- Saved the changes and confirmed role assignment

## 3. Microsoft Teams Admin–User Communication Test
### Objective
- Verify that messages sent by a standard user are delivered in real time to an administrator via Microsoft Teams.

### Test Scenario
- Logged in as a standard test user
- Sent a message to the IT administrator account via Teams:
- “Hi, something popped up on my computer and I’m not sure what it is. Could you please check it for me?”

### Result
- The message was delivered instantly to the administrator’s Teams web app
- Confirmed that:
  - User-to-admin communication works as expected
  - Teams can be effectively used as a primary helpdesk communication channel

## 4. Key Takeaways

### 1. Dedicated Admin Accounts
- Administrator accounts should be separate from regular user accounts
- Predictable account names (e.g., Administrator@domain) introduce unnecessary risk

### 2. Role-Based Access Control
- Global Administrator provides full visibility and control, but should be used sparingly
- Least-privilege roles (e.g., Helpdesk Administrator) are preferred in production environments

### 3. Teams as a Helpdesk Tool
- Microsoft Teams enables real-time communication between users and IT staff
- This setup closely mirrors real-world internal IT support workflows
