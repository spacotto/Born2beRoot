# Strong Password Policy
This section of the documentation defines the password security requirements for system architecture to ensure account protection and compliance with security standards.

## Password Expiration
- **Expiration Period.** Passwords must be changed every **30 days**.
- **Minimum Period.** Users must wait at least **2 days** before changing a password again.
- **Warning Period.** Users receive a notification **7 days** before password expiration.

## Password Complexity
Passwords must meet all of the following criteria:
- **Minimum Length:** 10 characters (recommended: **16+** characters for enhanced security)
- **Character Requirements:**
  - At least one uppercase letter (A-Z)
  - At least one lowercase letter (a-z)
  - At least one number (0-9)
- **Repetition Limit:** No more than 3 consecutive identical characters (e.g., "aaa" is not allowed)
- **Username Restriction:** Password must not contain the username

### Password Generator: urandom
>[!TIP]
>If you want to simulate a random password generator, you can use `urandom`.

Run this command in the terminal
```
< /dev/urandom tr -dc "[:alnum:]" | fold -w 16 | head -n 1 > password.txt
```

| Parameter      | Description                                                                                                                                        |
| :------------- | :------------------------------------------------------------------------------------------------------------------------------------------------- |
| `/dev/urandom` | A special file in Unix-like operating systems that provides random numbers from a cryptographically secure pseudorandom number generator (CSPRNG). |
| `tr -dc`       | Deletes all the characters not belonging to the set.                                                                                               |
| `"[:alnum:]"`  | The ASCII set of characters you want to use (in the example, digits, uppercase letters, and lowercase letters).                                    |
| `fold -w 16`   | Fills lines with `n` characters (16 in the example).                                                                                               |
| `head -n 1`    | Outputs `n` amount of lines (1 in the example). You can create several passwords at once by increasing the number of lines.                        |

## Password Reuse
- **Standard Users:** New password must have at least **7 characters different from the previous password**
- **Root Account:** This reuse restriction does not apply to the root password

## Login Attempts
- **Maximum Attempts:** 3 failed login attempts before account lockout

>[!WARNING]
>Users must contact system administration to unlock the account after exceeding the attempt limit.

## Best Practices
- Choose passwords that combine letters, numbers, and varied character patterns.
- Avoid using personal information, dictionary words, or predictable sequences.
- Store passwords securely using a password manager.
- Never share passwords or write them down in accessible locations.
- Respond promptly to expiration warnings to avoid account disruption.
- Never provide your password to anyone, including system administrators or IT staff: **legitimate administrators never need your password and will never ask for it**.

## Policy Ratio
These policies protect against the following threats.
- **Brute force attacks.** Limited login attempts and complexity requirements.
- **Password cracking.** Length and complexity standards increase cracking difficulty.
- **Credential reuse.** Expiration and difference requirements prevent long-term compromise.
- **Social engineering.** Username restriction reduces predictability.
