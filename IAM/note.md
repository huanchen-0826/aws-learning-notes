# IAM (Identity and Access Management) Notes

# IAM: Identity and Access Management

## Summary
IAM manages access to AWS resources. It is a **Global Service**.

## Essential Security Checklist
1. **Root Account**: Only use for initial setup. Enable MFA immediately.
2. **Users**: One person = One IAM user. No sharing passwords.
3. **Roles**: Use roles for AWS services (e.g., EC2) instead of hardcoding credentials.
4. **MFA**: Multi-Factor Authentication should be on for everyone, especially Admins.

## Terminology
- **Policy**: A JSON document defining permissions.
- **Principle of Least Privilege**: Give only the access required, nothing more.
