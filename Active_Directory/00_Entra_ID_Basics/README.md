# Day 1 – Microsoft Entra ID & Microsoft 365 Admin Center

## Overview
This lab documents my initial hands-on experience with **Microsoft Entra ID**
(formerly Azure Active Directory) and **Microsoft 365 Admin Center**.
The focus was on understanding tenant structure, domain configuration, and
basic user and group provisioning.

---

## 1. Active Directory vs Azure AD (Entra ID)

**Active Directory Domain Services (AD DS)** is an on-premises directory service
used to manage Windows domain environments, including user authentication,
computer accounts, and Group Policy.

**Azure Active Directory**, now known as **Microsoft Entra ID**, is a cloud-based
identity and access management service designed for modern applications and
cloud services such as Microsoft 365.

While both manage identities, they serve different purposes and are often used
together in **hybrid environments**, rather than acting as direct replacements
for one another.

---

## 2. Environment Setup

- Microsoft Azure
- Microsoft Entra ID (formerly Azure AD)
- Microsoft 365 Admin Center

### What I did
- Created a Microsoft Azure account
- Confirmed the rebranding of Azure Active Directory to **Microsoft Entra ID**
- Reviewed Entra ID tenant structure and default domain behavior

---

## 3. Microsoft 365 Admin Center Access

### What I practiced
- Logged into Microsoft 365 Admin Center using the **Entra ID Global Administrator account**
- Identified that access requires an Entra ID admin account,
  not just an Azure subscription account

### Key takeaway
Microsoft 365 Admin Center is tightly coupled with **Entra ID roles and permissions**,
not Azure subscription ownership.

---

## 4. Domain Configuration (`onmicrosoft.com`)

### What I practiced
- Reviewed the default tenant domain (`*.onmicrosoft.com`)
- Attempted to create a new `onmicrosoft.com` domain to simplify the default domain name
- Initially tried using the **Add domain** feature
- Encountered repeated prompts to verify domain ownership

### Issue encountered
- `onmicrosoft.com` domains cannot be verified using the standard custom domain workflow
- This caused confusion during initial setup

### How I resolved it
- Researched Microsoft Learn documentation
- Learned that `onmicrosoft.com` domains must be created or replaced through a
  **dedicated tenant domain workflow**, not the custom domain process
- Understood the correct procedure for managing additional `onmicrosoft.com` domains

Reference:
- https://learn.microsoft.com/en-us/microsoft-365/admin/setup/add-or-replace-your-onmicrosoftcom-domain

---

## 5. User & Group Management (Basic)

### What I practiced
- Created one test user account
- Created one security group
- Added the test user to the group
- Reviewed how group-based access is applied in Entra ID

---

## 6. Key Concepts Practiced

- Understanding the structure and role of the default `.onmicrosoft.com` domain
- Managing **User Principal Name (UPN)** formats during user provisioning
- Using Microsoft 365 Admin Center to manage users and groups
- Differentiating between administrator accounts and standard user accounts

---

## 7. Administrative Design Considerations

- Practiced separating the **initial administrator (root) account domain**
  from standard user account domains
- Learned how this separation clarifies:
  - Administrative responsibility
  - Service and user account ownership
- Reviewed the concept of a **fallback domain** in Microsoft Entra ID tenant management

---

## Key Takeaways
- Microsoft Entra ID is the central identity service for Microsoft 365 and cloud environments
- Proper domain and UPN management is critical for scalable tenant administration
- Clear separation of admin and user accounts improves security and operational clarity





---

# Day 2 – Bulk User & Group Management

## 1. Bulk User Creation (CSV Upload)

Reference:
- https://learn.microsoft.com/en-ca/entra/identity/users/users-bulk-add

### What I practiced
- Created multiple users using CSV bulk upload
- Auto-generated user names
- Used Excel **Flash Fill** to generate email addresses with a consistent format
- Generated passwords using Excel formulas

### Issues encountered & lessons learned
- Initial password generation failed due to **password complexity requirements**
  (less than 8 characters)
- Updated the formula to generate passwords with 8+ characters, which succeeded
- Attempted to add a `forceChangePasswordNextSignIn` column to the CSV
  - Result: upload failed
  - Learned that this header is **not supported** in CSV bulk upload

### Unexpected issue
- Login failed using the password provided in the CSV
- Resolved by performing a password reset
- Possible cause: Excel formulas regenerated passwords when the file recalculated

### Key takeaway
CSV bulk upload is for **account creation only**.  
Advanced user properties and password management should be handled **after creation**
(e.g., via admin portal, PowerShell, or Microsoft Graph).

---

## 2. Group Management

### What I practiced
- Created multiple groups
- Assigned members during group creation
- Added users to existing groups
- Renamed groups (e.g., `Sales` → `Sales_Team`)
- Deleted a group and confirmed:
  - Users remain intact
  - Only group membership is removed

---

## 3. User Deletion & Restore

### What I practiced
- Deleted a user
- Confirmed users can be restored within **30 days**
- Restored a deleted user

### Interesting discovery
- Deleted a user who belonged to a group
- After restoring the user, **group membership was automatically restored**

### Key takeaway
Entra ID preserves group membership information during the soft-delete period.

---

## 4. Password Reset Scenario

### What I practiced
- Simulated a “Forgot password” scenario
- Used the **Reset password** feature
- Confirmed:
  - Temporary password is issued
  - User must change password at first sign-in
  - No additional configuration was required

### Next step
- Simulate an MFA recovery scenario:
  - “User lost or changed their phone and needs to reconfigure MFA”

---

## Overall Reflection
Through these labs, I learned that while Entra ID’s UI makes basic identity tasks
simple, understanding **platform limitations, default behaviors, and recovery
mechanisms** is critical for real-world administration.
