# IAM (Identity and Access Management) Notes

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

## IAM Permissions
- Users or Groups can be assigned JSON docluments calleld **policies**
```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": "ec2:Describe*",
            "Resource": "*"},
        {},
        {}
    ],
}
```
- Don't give more permissions than a user needs.



# IAM Core Concepts: User, Role, and Policy

## 1. High-Level Conclusion
**Users** and **Roles** are identities (authentication entities), while **Policies** are documents that define permissions (authorization rules).

* **User:** A permanent identity with long-term credentials, representing a specific person or service.
* **Role:** A temporary identity with short-term credentials, intended to be "assumed" by a User, a Service, or an external identity.
* **Policy:** A ruleset attached to Users or Roles that explicitly allows or denies actions on specific resources.

---

## 2. Detailed Breakdown

### IAM User (The "Who" - Permanent)
An **IAM User** represents a unique identity within your cloud account. It corresponds to a specific human or workload that requires long-term access.

* **Credentials:** Long-term (Passwords for console access, Access Keys for programmatic access).
* **Use Case:** An admin logging into the console; a service account running on a local server.
* **First Principle:** Identity persistence. The entity exists until explicitly deleted.

### IAM Role (The "Who" - Temporary)
An **IAM Role** is an identity that has specific permissions but is not associated with a specific person. It does not have standard long-term credentials (passwords or access keys).

* **Credentials:** Temporary security tokens provided by the Security Token Service (STS) upon assumption.
* **Use Case:** An EC2 instance needing to access S3; a Lambda function writing to DynamoDB; a user from a different account needing temporary access.
* **First Principle:** Identity delegation. An entity temporarily adopts this identity to gain specific privileges.

### IAM Policy (The "What" - Rules)
An **IAM Policy** is an object (typically a JSON document) that defines permissions. It does not perform actions itself. It dictates what the identities (Users and Roles) are allowed to do.

* **Structure:** Contains `Effect` (Allow/Deny), `Action` (e.g., `s3:ListBucket`), and `Resource` (e.g., `arn:aws:s3:::my-bucket`).
* **Use Case:** "Allow Read-Only access to S3" or "Deny deletion of production databases."
* **First Principle:** Governance. It separates the logic of *access control* from the *identity* itself.

---

## 3. Comparison Summary

| Feature | IAM User | IAM Role | IAM Policy |
| :--- | :--- | :--- | :--- |
| **Nature** | Identity | Identity | Configuration / Rule |
| **Credentials** | Long-term (Password/Keys) | Short-term (Tokens) | None |
| **Association** | 1:1 (One Person/App) | 1:Many (Assumed by many) | Attached to Users/Roles |
| **Primary Goal** | Authentication (Log in) | Delegation (Assume access) | Authorization (Permissions) |
