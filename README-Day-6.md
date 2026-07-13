# MD-102 Endpoint Administrator Notes - Day 6

### Should you have any questions, feel free to contact me : pouya.ecn@gmail.com 

---


# Scope Tags in Intune

Role
→ Defines what an administrator can do.

Scope Group
→ Defines which users and devices the administrator can manage.

Scope Tag
→ Defines which Intune objects the administrator can see and manage.

Example:

A company has four branches.

A Help Desk administrator receives:

Role
→ Help Desk Operator.

Scope Group
→ Users and devices from Branch A.

Scope Tag
→ Branch-A.

Result:

The administrator can manage only the devices, users, and Intune objects related to Branch A.
The administrator can manage only the devices, users, and Intune objects related to Branch A.


# Microsoft Intune RBAC

## Main Concepts

Role
→ Defines what an administrator can do.

Admin Group
→ Defines which administrators receive the Role.

Scope Group
→ Defines which Users and Devices the administrators can manage.

Scope Tag
→ Defines which Intune objects the administrators can see and manage.

Intune objects include:

- Apps
- Policies
- Configuration profiles
- Scripts
- Managed devices

---

## Example

Assume the company has two branches:

- United States
- Turkey

Each branch has its own administrators, users, devices, apps, and policies.

For the Turkey branch:

Admin Group:
Turkey-Intune-Admins

Scope Groups:
Turkey-Users
Turkey-Devices

Scope Tag:
Turkey

Result:

Turkey administrators can perform only the actions allowed by their Role, only on Turkey users and devices, and only on Intune objects tagged with Turkey.

---

## Role Assignment Steps

1. Create the Role and define its permissions.
2. Create a Role Assignment.
3. Select the Admin Group.
4. Select the Scope Groups.
5. Select the Scope Tag.

---

## Scope Tag Process

1. Create a Scope Tag, such as Turkey.
2. Add the Turkey tag to Turkey policies, apps, profiles, and devices.
3. Select the Turkey Scope Tag in the Role Assignment.

The Scope Tag is only a label until it is added to Intune objects.

---

## Security Groups

Administrator Security Group
→ Contains administrators who receive a Role.

Device Security Group
→ Contains devices that receive apps and policies or are selected as a Scope Group.

User Security Group
→ Contains users who receive apps and policies or are selected as a Scope Group.

A Security Group does not automatically become a Scope Group.

It becomes a Scope Group when you select it under Scope Groups in the Role Assignment.

---

## Summary

Role
→ What can the administrator do?

Admin Group
→ Who receives the Role?

Scope Group
→ Which Users and Devices can they manage?

Scope Tag
→ Which Intune objects can they manage?
