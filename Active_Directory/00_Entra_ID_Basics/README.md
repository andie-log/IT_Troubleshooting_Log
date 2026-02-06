# Day 1 – Microsoft Entra ID & Microsoft 365 Admin Center

## Overview
This lab documents my initial hands-on experience with Microsoft Entra ID (formerly Azure Active Directory) and Microsoft 365 Admin Center.
The focus was on understanding tenant structure, domain configuration, and basic user and group provisioning.

---

## Active Directory vs Azure AD (Entra ID)

Active Directory Domain Services (AD DS) is an on-premises directory service primarily used to manage Windows domain environments, including user authentication, computer accounts, and Group Policy.

Azure Active Directory, now known as Microsoft Entra ID, is a cloud-based identity and access management service designed for modern applications and cloud services such as Microsoft 365.

While both manage identities, they serve different purposes and are often used together in hybrid environments rather than as replacements.

---

## Environment
- Microsoft Azure
- Microsoft Entra ID (formerly Azure AD)
- Microsoft 365 Admin Center

---

## Tasks Completed

### Azure & Entra ID
- Created a Microsoft Azure account
- Confirmed that Azure Active Directory has been rebranded as **Microsoft Entra ID**
- Reviewed the Entra ID tenant structure and default domain behavior

---

### Microsoft 365 Admin Center Access
- Successfully logged in using the **Entra ID Global Administrator account**
- Identified that Microsoft 365 Admin Center access requires the Entra ID admin account, not just the Azure subscription account

---

### Domain Configuration
- Reviewed the default tenant domain (`*.onmicrosoft.com`)
- Attempted to create a new `onmicrosoft.com` domain to simplify the default domain name
- Initially tried using the **Add domain** feature, which repeatedly required domain verification
- Identified that `onmicrosoft.com` domains cannot be verified through the standard custom domain process
- Researched Microsoft documentation and learned that creating or replacing an `onmicrosoft.com` domain must be done through the dedicated tenant domain workflow
- Successfully understood the correct procedure for creating and managing an additional `onmicrosoft.com` domain

---

### User & Group Management
- Created one test user account
- Created one security group
- Added the test user to the group
- Reviewed how group-based access is applied in Entra ID

---

## Key Concepts Practiced

- Understanding the structure and role of the default `.onmicrosoft.com` domain
- Managing **User Principal Name (UPN)** formats during user provisioning
- Using Microsoft 365 Admin Center to manage users and groups
- Differentiating between administrator accounts and standard user accounts

---

## Administrative Design Considerations

- Practiced separating the **initial administrator (root) account domain** from standard user account domains
- Learned how this separation helps clarify administrative responsibility versus service user responsibility
- Reviewed the concept of a **fallback domain** in Microsoft Entra ID tenant management

---

## Key Takeaways
- Microsoft Entra ID is the central identity service for Microsoft 365 and cloud-based environments
- Proper domain and UPN management is critical for scalable tenant administration
- Clear separation of admin and user accounts improves security and operational clarity

---

## Issues Encountered
- Attempted to create a new `onmicrosoft.com` domain using the **Add domain** feature
- Was repeatedly prompted to verify domain ownership, which caused confusion since `onmicrosoft.com` domains are managed by Microsoft


## How I Resolved It
- Reviewed [Microsoft Learn documentation related to `onmicrosoft.com` domains](https://learn.microsoft.com/en-us/microsoft-365/admin/setup/add-or-replace-your-onmicrosoftcom-domain?view=o365-worldwide&WT.mc_id=365AdminCSH_inproduct)
- Learned that `onmicrosoft.com` domains cannot be added or verified as custom domains
- Identified the correct process for creating or replacing the default `onmicrosoft.com` domain using Microsoft’s recommended tenant domain configuration method






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
