# Strong Password Policy
This section of the documentation defines the password security requirements for system architecture to ensure account protection and compliance with security standards.

## Password Expiration
- **Expiration Period.** Passwords must be changed every **30 days**.
- **Minimum Period.** Users must wait at least **2 days** before changing a password again.
- **Warning Period.** Users receive a notification **7 days** before password expiration.

## Password Complexity
Passwords must meet all of the following criteria:
- **Minimum Length:** 10 characters
- **Character Requirements:**
  - At least one uppercase letter (A-Z)
  - At least one lowercase letter (a-z)
  - At least one number (0-9)
- **Repetition Limit:** No more than 3 consecutive identical characters (e.g., "aaa" is not allowed)
- **Username Restriction:** Password must not contain the username
