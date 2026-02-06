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
