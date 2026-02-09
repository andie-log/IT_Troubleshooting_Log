# Troubleshooting Cases – Microsoft Entra ID

## Case 1 – User Forgot Password

### Scenario
A user reported that they forgot their password and were unable to sign in.

### Investigation
- **Account Status Verification:**
  - Confirmed the account was not disabled.
  - **Insight**: Verified that 'Block sign-in' (Microsoft 365 admin center) and 'Account Enabled: No' (Microsoft Entra admin center) are the same state reflected in different portals.

- **Sign-in Risk Assessment:**
  - Checked Entra ID **Sign-in logs** to ensure no security-related blocks were present.

### Resolution
- Action: Used the Reset password feature in the Entra admin center.
- Process:
  - A **temporary password** was automatically issued by the system.
  - The system enforced **"User must change password at first sign-in"** by default (this is mandatory and not an optional setting during this process).
- Configuration: Confirmed that no additional configuration was required to perform this administrative reset.

### Result
- The user successfully signed in with the temporary password.
- The user was immediately prompted to set a new password as expected.
- The user regained access with their new credentials.

### Key Takeaway
1. Portal Integration: Admin actions in either the Microsoft 365 admin center or the Entra admin center sync perfectly as they share the same identity backend.
2. Built-in Security: The reset process inherently protects user privacy by forcing a password change, ensuring the administrator's temporary access is revoked.

---

## Case 2 – User Changed Phone and Needs MFA Re-Setup

### Scenario
A user reported that they changed their mobile phone and were unable to complete multi-factor authentication (MFA).


### Investigation
- **Account Status Verification:**
  - Confirmed that the user account was enabled.
  - Verified that Block sign-in was not applied.
  - **Insight**: Blocking sign-in in Microsoft 365 Admin Center is reflected as Account Enabled: No in Microsoft Entra ID.

- **Authentication Method Review:**
  - Checked existing authentication methods assigned to the user.
  - Identified that the previously registered MFA method was no longer accessible due to the device change.

### Resolution
### Option 1: Force MFA Re-Registration

Microsoft Entra admin center
→ Users
→ Select user
→ Authentication methods
→ **Require re-register multifactor authentication**


- Action: Selected **Require re-register multifactor authentication**
- Result:
  - All previously registered authentication methods were removed
  - MFA configuration was reset for the user

**User Experience After Reset**
- When the user attempted to sign in:
  - The system prompted the user to complete MFA setup again
  - The user was guided through re-registering authentication methods

### Additional Investigation: MFA Method Options
- Discovered the Add authentication methods option:
  - Available methods included:
    - Email
    - Phone number
    - Temporary Access Pass (TAP)
    - QR code

- **Observation:**
  - The system strongly encourages the use of the Microsoft Authenticator App, as it provides:
    - Higher security
    - Support for passwordless authentication
    - Better integration with Conditional Access policies

### Option 2: Temporary Access Pass (TAP)
- Created a Temporary Access Pass for the user
- Provided the user with:
  - A one-time Temporary Access Pass
  - A secure link
- User Process:
  - Accessed the link
  - Entered the Temporary Access Pass
  - Successfully accessed **My Sign-Ins**
  - Registered new authentication methods

**Reference:**
- [Microsoft Learn – Temporary Access Pass](https://learn.microsoft.com/en-us/entra/identity/authentication/howto-authentication-temporary-access-pass)

### Result
- The user successfully re-registered MFA using a new device
- Old authentication methods were invalidated

### Key Takeaway

1. MFA Reset vs Account Lock: Resetting MFA does not disable the user account; it only forces re-enrollment at the next sign-in.
2. Security by Design: Microsoft prioritizes the Authenticator App due to its stronger security and broader feature support.
3. Temporary Access Pass: TAP is an effective and secure method for onboarding or recovering users who have lost access to all MFA methods.

