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
