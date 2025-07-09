# Per-App Licensing Governance Flows

This repository contains four Power Automate flows that support a governance model for managing Per-App licenses in Power Platform. These flows help automate user access and license recycling using Entra security groups, Microsoft Forms and more.

For full context, including the licensing strategy and architectural decisions, see the accompanying blog post.

---

## Included Flows

### 1. `AssignUserstoSecurityGroup.json`
Triggered by a Microsoft Form submission. It:
- Retrieves the submitter’s email.
- Checks if the user is already in the `user-role1` group.
- Calls a child flow to add the user if not present.
- Sends confirmation to the user and a notification to the admin.

### 2. `ChildFlowAddUsertoSecurityGroup.json`
Adds a user to a specified Azure AD group using Microsoft Graph API. Skips if the user is already a member.

### 3. `ChildFlowRemoveUserFromSecurityGroup.json`
Removes a user from a specified Azure AD group. Used for license recycling.

### 4. `RemoveUsersFromSecurityGroupMonthly.json`
Scheduled flow that runs monthly to remove all users from the `user-role2` group.

---

## Placeholder Reference

Replace the following placeholders in the JSON files with values from your environment:

| Placeholder                        | Description                                 |
|------------------------------------|---------------------------------------------|
| `{{FormId}}`                       | Microsoft Form ID                           |
| `{{UserRole1GroupId}}`             | Azure AD group for user-role1               |
| `{{UserRole2GroupId}}`             | Azure AD group for user-role2               |
| `{{ClientId}}`, `{{ClientSecret}}`, `{{TenantId}}` | Azure AD app credentials        |
| `{{AdminEmail}}`, `{{FromEmail}}` | Email addresses used in notifications       |

---

## Setup Instructions

1. Replace all placeholders with actual values.
2. Import the flows into Power Automate.
3. Ensure your Azure AD app has Graph API permissions.
4. Configure the Microsoft Form and embed it in your documentation.
5. Test the flows with sample users.

---

## Blog Reference

For background, design decisions, and lessons learned, see the blog post:  

