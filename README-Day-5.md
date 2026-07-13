# MD-102 Endpoint Administrator Notes - Day 5

## Yesterday, I did not finish the second scenario.So today I will start with a brief review of the second scenario, Bulk Enrollment in Non-Hybrid Environment, before continuing to finish it. 
### Should you have any questions, feel free to contact me: pouya.ecn@gmail.com 

---


## Scenario 2: Bulk Enrollment Without a Hybrid Environment

In a non-hybrid environment, Windows Configuration Designer can be used to create a provisioning package.

Provisioning packages use the `.ppkg` file format.

General process:

Windows Configuration Designer
> Provision desktop devices
> Create a provisioning package
> Configure the required settings
> Export the `.ppkg` file
> Run the package on each device

A provisioning package can be used to:

- Connect devices to Microsoft Entra ID
- Enroll devices in Intune
- Configure device settings
- Add certificates
- Configure Wi-Fi
- Install applications
- Apply organization-specific settings

Windows Configuration Designer can be installed from the Microsoft Store.

![Windows Configuration Designer](screenshots/windows-configuration-designer.png)

![Create Provisioning Package](screenshots/create-provisioning-package.png)

##### Important:

A provisioning package makes bulk setup faster, but the package normally still needs to be applied to each device.

For modern large-scale Windows deployment, Windows Autopilot is often a better option.

---



# Windows Bulk Enrollment

In Windows Configuration Designer, device names can include:

RAND:5 → Adds a random five-digit number.

Example:

LAPTOP-%RAND:5%
→ LAPTOP-48392

A device name can also include the serial number.

After the configuration is completed, a provisioning package is created. The package can be copied to a USB drive and run on new devices.

![Windows provisioning package](Screenshots/day-5-01.png)


# Bulk Enrollment for Apple Devices

Path:

Devices
→ Enrollment
→ Apple Enrollment
→ Apple Configurator

Apple Configurator can be used to prepare and enroll Apple devices manually.

Devices purchased through Apple or an authorized reseller are usually added to Apple Business Manager and assigned to Intune.

![Apple Configurator enrollment](Screenshots/day-5-02.png)


## User Affinity

Enroll with User Affinity
→ The device is assigned to one specific user.

Enroll without User Affinity
→ The device is shared or used for a specific task.

Example:

A shared iPad used by employees for scanning products.

![Apple user affinity](Screenshots/day-5-03.png)


## Setup Assistant

When an Apple device is registered and assigned to Intune, enrollment begins after the device is turned on and connected to the internet.

The Apple Setup Assistant guides the user through the enrollment process.

For some enrollment methods, the user may need to install the Company Portal app.

![Apple Setup Assistant](Screenshots/day-5-04.png)


## Apple Business Manager

General process:

Device purchased
→ Added to Apple Business Manager
→ Assigned to Intune
→ Intune syncs through a token
→ Device is turned on
→ Automatic enrollment begins


# Bulk Enrollment for Android Devices

Android Zero-touch Enrollment is used for corporate-owned Android devices.

General process:

Authorized reseller registers device identifiers
→ Devices appear in the Zero-touch portal
→ Zero-touch is connected to Intune
→ An enrollment profile is assigned
→ Enrollment begins when the device is turned on


## Android Enrollment Profiles

Fully Managed User Device
→ One user, work use only.

Dedicated Device
→ Shared device or device used for one specific task.

Corporate-Owned Device with Work Profile
→ One user, work and personal use are separated.

![Android Zero-touch enrollment](Screenshots/day-5-05.png)


# Policy Sets

A Policy Set is a collection of Intune policies, applications, and configurations.

Policy Sets are assigned to user or device groups.

Example:

A new Sales employee joins the Sales group
→ The employee receives the Sales apps, policies, Wi-Fi, VPN, and security settings.

![Intune Policy Sets](Screenshots/day-5-06.png)


# Roles and RBAC

Role
→ Defines what a user or administrator can do.

RBAC
→ Role-Based Access Control.

RBAC determines:

Who has access
→ What they can do
→ Which resources they can manage


# Types of Roles

## Microsoft Entra Roles

Microsoft Entra roles control identity-related administration.

Examples:

Global Administrator
→ Broad administrative control.

User Administrator
→ Manages users and groups.

Security Reader
→ Views security information.

Security Administrator
→ Manages security settings.

Cloud Application Administrator
→ Manages cloud applications.


## Application Roles

Application Roles control what users can do inside a specific application.

Examples:

Admin
Editor
Viewer


## Azure RBAC

Azure RBAC controls access to Azure resources.

Examples of Azure resources:

Virtual Machines
Storage Accounts
Databases
Resource Groups
Subscriptions

Common Azure roles:

Owner
→ Manages resources and access.

Contributor
→ Creates and manages resources.

Reader
→ Views resources only.

Custom Role
→ A role created with selected permissions.


## Intune RBAC

Intune RBAC controls who can manage:

Devices
Apps
Policies
Enrollment
Reports
Intune roles


# Container vs Virtual Machine

Virtual Machine
→ Has a complete operating system.
→ Stronger isolation.
→ Uses more resources.

Container
→ Shares the host operating system kernel.
→ Lighter and faster.
→ Commonly used for applications.


# Resource Group

A Resource Group is a logical container for related Azure resources.

Example:

Resource Group: Website-Project

Virtual Machine
Storage Account
Database
Virtual Network


# Azure Subscription

An Azure Subscription is a billing and management boundary that contains Azure resources.

Users and groups receive access through Azure RBAC.

Example:

Owner
→ Full management and access control.

Contributor
→ Resource management.

Reader
→ View-only access.


# Microsoft 365 Roles

Microsoft 365 services have specialized administrative roles.

Examples:

Exchange Administrator
→ Manages Exchange Online.

SharePoint Administrator
→ Manages SharePoint Online.

Teams Administrator
→ Manages Microsoft Teams.

Security Administrator
→ Manages security settings.

Compliance Administrator
→ Manages compliance features.

A user should receive a service-specific role instead of Global Administrator whenever possible.


# Principle of Least Privilege

The Principle of Least Privilege means giving users only the minimum permissions they need to perform their jobs.


# PIM and JIT

PIM
→ Privileged Identity Management.

PIM is used to manage and monitor privileged roles.

JIT
→ Just-in-Time access.

JIT activates a privileged role temporarily only when needed.

Example:

Junior administrator becomes eligible for a role
→ Requests activation
→ MFA or approval may be required
→ Role becomes active temporarily
→ Time expires
→ Access is removed

Eligible
→ The user can activate the role when necessary.

Active
→ The role is currently available to the user.


# RBAC Best Practices

Assign roles to groups instead of individuals.

Follow least privilege.

Use PIM for privileged roles.

Review role assignments regularly.

Remove unused permissions.


# Security Principals

Security Principal
→ Any identity that can receive a role or permission.

User
→ Identity for one person.

Group
→ Identity for multiple users.

Service Principal
→ Identity for an application or service; credentials are managed by the organization.

Managed Identity
→ Identity for an Azure resource; credentials are managed automatically by Azure.


# Service Principal

A Service Principal allows an application to authenticate and receive permissions.

Example:

Backup application
→ Receives Storage Blob Data Contributor
→ Can write backup files to Azure Storage


# Managed Identity

A Managed Identity allows an Azure resource to access another resource without storing a password or secret.

Example:

Virtual Machine
→ Receives a Managed Identity
→ Managed Identity receives Storage Blob Data Reader
→ VM can read Storage data without saving credentials


# Role Definitions and Role Assignments

Role Definition
→ Collection of permissions.

Role Assignment
→ Connects an identity, a role, and a scope.

Example:

User: Alex
+
Role: Reader
+
Scope: Resource Group A

Result:

Alex can view resources inside Resource Group A.


# Privileged Roles

Privileged roles provide sensitive administrative access.

Examples:

Global Administrator
Privileged Role Administrator
Security Administrator
Exchange Administrator
SharePoint Administrator

PIM settings may require:

MFA
Approval
Justification
Maximum activation time
Notifications


# Microsoft 365 Role Management

Path:

Microsoft 365 Admin Center
→ Show All
→ Roles
→ Role Assignments

From this section, administrators can:

View roles
Read permissions
View assignments
Assign users or groups


# Microsoft Defender Roles

Microsoft Defender has security-specific roles.

Examples:

Security Reader
→ Views security information.

Security Operator
→ Investigates and responds to alerts.

Security Administrator
→ Manages security settings and policies.


# Service-Specific Roles

Each Microsoft 365 service may have its own roles.

Microsoft Defender
→ Security roles.

Microsoft Purview
→ Compliance roles.

Exchange
→ Exchange roles.

SharePoint
→ SharePoint roles.

Teams
→ Teams roles.


# Intune Built-in and Custom Roles

Path:

Tenant Administration
→ Roles

Built-in Role
→ Predefined by Microsoft.

Custom Role
→ Created by the organization.

Intune Role Administrator
→ Can manage Intune roles and role assignments.


# Windows 365

Windows 365 provides a complete Windows computer in the cloud.

This computer is called a Cloud PC.

The user can connect to the same:

Desktop
Apps
Settings
Files

Normal PC
→ Windows runs on the physical device.

Windows 365
→ Windows runs in the cloud.


# Windows 365 Roles

Cloud PC Administrator
→ Manages Windows 365 Cloud PCs.

Cloud PC Reader
→ Views Cloud PC information only.


# Windows Autopatch

Windows Autopatch automatically manages supported Windows and Microsoft application updates.

Its purpose is to deploy updates gradually and reduce the risk of updating every device at the same time.


# Windows Autopatch Roles

Windows Autopatch Administrator
→ Manages Autopatch settings, groups, reports, and support requests.

Windows Autopatch Reader
→ Views Autopatch information and reports only.


# Autopatch Device Groups

Autopatch groups divide devices into deployment rings.

Example:

Test Group
→ Small number of devices.

Early Group
→ Larger number of devices.

Broad Group
→ Most company devices.

Updates are tested on smaller groups before reaching all devices.


