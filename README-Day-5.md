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


## Windows Bulk Enrollment

During the **Set up device** process, you can define how device names are generated.

Example:

RAND:5 → Adds a random five-digit number to the device name.

Example:

LAPTOP-%RAND:5%
→ LAPTOP-48392

You can also use the device serial number as part of the device name.

The remaining sections, such as network configuration, are relatively straightforward.

At the end of the process, Windows Configuration Designer creates a provisioning package. You can copy this package to a USB drive and run it on new Windows devices to configure and enroll them.

![Windows provisioning package](Screenshots/day-5-01.png)


# Bulk Enrollment for Apple Devices

In Intune, go to:

Devices
→ Enrollment
→ Apple Enrollment
→ Apple Configurator

Apple Configurator can be used to manually prepare and enroll Apple devices that were not already added through Apple Business Manager or Apple School Manager.

Devices purchased through Apple or an authorized reseller can normally be added directly to Apple Business Manager and assigned to Intune for Automated Device Enrollment.

![Apple Configurator enrollment](Screenshots/day-5-02.png)


## User Affinity

Enroll with User Affinity
→ The device is associated with a specific user account.

Example:

A company iPhone assigned to one employee.

Enroll without User Affinity
→ The device is not associated with one specific user.

Example:

A shared iPad used by multiple Costco employees for scanning items outside the checkout line.

![Apple user affinity options](Screenshots/day-5-03.png)


## Setup Assistant

When an Apple device is registered in Apple Business Manager and assigned to Intune, the enrollment process starts automatically when the device is turned on and connected to the internet.

Apple Setup Assistant guides the user through the setup process while Intune applies the organization's enrollment settings.

For some other enrollment methods, the user may need to install and sign in to the Intune Company Portal app.

![Apple Setup Assistant](Screenshots/day-5-04.png)


## Apple Business Manager and Apple School Manager

Apple Business Manager, or ABM, is used by companies.

Apple School Manager, or ASM, is used by educational organizations.

The general process is:

Organization purchases devices
→ Devices are added to ABM or ASM
→ Devices are assigned to Intune
→ Intune connects through an enrollment token
→ The device is turned on
→ Automatic enrollment begins


# Bulk Enrollment for Android Devices

For corporate-owned Android devices, one enrollment option is Android Zero-touch Enrollment.

The general process is:

1. The organization purchases supported devices from an authorized reseller.
2. The reseller registers the devices in the organization's Zero-touch portal using identifiers such as IMEI or serial number.
3. The Zero-touch account is connected to Intune.
4. An enrollment profile is assigned.
5. When the device is turned on and connected to the internet, enrollment begins automatically.


## Android Enrollment Profiles

Fully Managed User Device
→ Assigned to one user and used only for work.

Dedicated Device
→ Used for a specific task and often shared among multiple users.

Example:

A warehouse scanner, kiosk, or check-in tablet.

Corporate-Owned Device with Work Profile
→ Assigned to one user and allows both work and limited personal use.

Work data is separated from personal data.

![Android Zero-touch enrollment](Screenshots/day-5-05.png)


# Configure Policy Sets

Intune can contain many different policies, applications, and configurations under sections such as Devices and Apps.

A Policy Set is a collection of related policies, applications, and configurations that can be assigned together.

Example:

A new employee is added to the Sales group.

The Sales Policy Set may include:

- Microsoft 365 Apps
- Wi-Fi configuration
- VPN configuration
- Compliance policy
- Security settings
- Required applications

When the Policy Set is assigned to the Sales group, its included settings and applications are delivered to members of that group.

The device may already have been enrolled in Intune through Windows Autopilot or another enrollment method.

![Intune Policy Sets](Screenshots/day-5-06.png)


# What Are Roles?

Roles define what users and administrators are allowed to do in Microsoft services.

Roles support the Principle of Least Privilege.

The Principle of Least Privilege means giving users only the minimum permissions required to perform their jobs.

RBAC stands for:

Role-Based Access Control

RBAC is used to determine:

- Who has access
- What actions they can perform
- Which resources they can perform those actions on


# Different Types of RBAC

## Microsoft Entra Roles

Microsoft Entra roles determine what administrators can manage in Microsoft Entra ID.

Examples include:

- Users
- Groups
- Enterprise applications
- Roles
- Licenses
- Identity and authentication settings

Examples of Microsoft Entra roles:

Global Administrator
→ Has broad administrative control.

User Administrator
→ Manages users and groups.

Security Reader
→ Can view security-related information.

Security Administrator
→ Can manage many security-related settings.

Cloud Application Administrator
→ Manages enterprise applications and app registrations.


## Application Roles

Application roles determine what a user, group, or service can do inside a specific application.

Example:

Admin
Editor
Viewer

These roles are created by the application developer or application owner.


## Azure RBAC

Azure RBAC controls access to Azure resources.

It can be assigned to:

- Users
- Groups
- Service Principals
- Managed Identities

Examples of Azure resources:

- Virtual Machines
- Storage Accounts
- Databases
- Resource Groups
- Subscriptions

Common Azure roles:

Owner
→ Can manage resources and assign access to other identities.

Contributor
→ Can create and manage resources but cannot normally assign roles to other identities.

Reader
→ Can view resources but cannot modify them.

Custom Role
→ A role created by the organization with a specific collection of permissions.


## Intune RBAC

Intune RBAC determines which administrators can manage:

- Devices
- Applications
- Configuration policies
- Compliance policies
- Enrollment settings
- Reports
- Intune roles


# What Is a Container?

Understanding a Virtual Machine helps explain a container.

## Virtual Machine

Multiple Virtual Machines can run on one physical server.

Each Virtual Machine includes:

- Its own operating system
- Its own applications
- Its own allocated resources

Virtual Machines provide strong isolation but require more resources.


## Container

Containers run isolated applications while sharing the host operating system kernel.

Because containers do not normally require a complete operating system for each application, they are:

- Lighter
- Faster to start
- Easier to deploy
- More resource-efficient

Container
→ Lighter, faster, and ideal for many application workloads.

Virtual Machine
→ Stronger isolation, full operating system, and more resource-intensive.


# What Is a Resource Group?

A Resource Group is a logical container used to organize related Azure resources.

Example:

Resource Group: Website-Project

Contains:

- Virtual Machine
- Storage Account
- Database
- Virtual Network

The Resource Group helps administrators manage, monitor, and apply access control to related resources together.


# What Is an Azure Subscription?

An Azure Subscription is a billing, management, and access-control boundary in Azure.

Azure resources are created inside a subscription.

Administrators can assign users, groups, Service Principals, or Managed Identities access to the subscription through Azure RBAC.

Example:

Owner
→ Can manage resources and access.

Contributor
→ Can create and manage resources.

Reader
→ Can only view resources.

A subscription is not the same as a user account. It is a boundary that contains Azure resources and tracks their usage and costs.


# Microsoft 365 Roles

Microsoft 365 contains administrative roles for services such as:

- Exchange Online
- SharePoint Online
- Microsoft Teams
- Microsoft Defender
- Microsoft Purview

It is not necessary to give someone the Global Administrator role when they only need to manage one service.

Examples:

Exchange Administrator
→ Manages Exchange Online.

SharePoint Administrator
→ Manages SharePoint Online.

Teams Administrator
→ Manages Microsoft Teams.

Security Administrator
→ Manages security-related settings.

Compliance Administrator
→ Manages compliance-related features.


# Principle of Least Privilege

The Principle of Least Privilege means giving users the minimum level of access they need to perform their jobs.

Correct sentence:

The Principle of Least Privilege means giving users only the minimum permissions they need to perform their jobs.


# PIM and JIT

PIM means:

Privileged Identity Management

JIT means:

Just-in-Time access

PIM
→ A Microsoft Entra service used to manage, monitor, and control privileged roles.

JIT
→ Temporary activation of a privileged role only when it is needed.

Example:

Junior Administrator requests the role
→ MFA or approval may be required
→ The role becomes active temporarily
→ The administrator completes the task
→ The activation period expires
→ The privileged access is removed


## Example of PIM and JIT

Imagine that the main administrator is going on vacation for one month.

The organization does not want to give the junior administrator permanent privileged access.

Instead, the junior administrator is assigned an eligible role through PIM.

Eligible means:

The user does not have the role active all the time, but can request and activate it when necessary.

The organization can configure requirements such as:

- MFA
- Approval
- Justification
- Maximum activation time
- Notification
- Access reviews

The role itself is not called a JIT role.

The user is eligible for a normal role, and that role is activated temporarily through Just-in-Time access.


# Summary of Role Types

Roles
→ Define permissions.

Microsoft Entra
→ Identity-focused.

Azure
→ Resource-focused.

Microsoft 365
→ Service and application-focused.

Intune
→ Device, application, and policy-management focused.


# RBAC Best Practices

Assign roles to groups rather than directly to individual users whenever practical.

Follow the Principle of Least Privilege.

Use PIM for privileged administrative roles.

Review role assignments regularly.

Remove permissions that are no longer required.

Use access reviews and reminders to periodically verify administrative access.


# Implementing RBAC in Microsoft Azure

## Security Principal

Security Principal
→ Any identity that can be assigned access or a role.

Examples of Security Principals:

User
→ Identity for an individual person.

Group
→ Identity for a collection of users.

Service Principal
→ Identity for an application or service; credentials are managed by the organization.

Managed Identity
→ Identity for an Azure resource; credentials are managed automatically by Azure.


## Service Principal

A Service Principal allows an application or service to authenticate and receive permissions.

Example:

A backup application needs access to an Azure Storage Account.

The organization creates a Service Principal and assigns it a role such as:

Storage Blob Data Contributor

The application uses its credentials to authenticate and access the Storage Account.


## Managed Identity

A Managed Identity is an identity automatically created and managed by Azure for an Azure resource.

Example:

A Virtual Machine needs to read files from an Azure Storage Account.

Without Managed Identity:

Application on the VM
→ Stores a secret, key, or connection string
→ Uses that credential to connect to Storage

With Managed Identity:

Azure creates an identity for the VM
→ A Storage role is assigned to that identity
→ The application uses the VM's identity
→ The VM connects to Storage without storing a password or secret

Example role:

Storage Blob Data Reader
→ Allows the VM to read blob data.

The main benefit is that Azure manages the underlying credentials automatically.


# Role Definitions

A Role Definition is a collection of permissions.

Azure role definitions are represented in JSON and describe:

- Allowed actions
- Denied actions
- Data actions
- Assignable scopes

A Role Assignment connects three elements:

Security Principal
+
Role Definition
+
Scope

Example:

User: Alex
+
Role: Reader
+
Scope: Resource Group A

Result:

Alex can view resources inside Resource Group A.


# Privileged Roles

In Microsoft Entra, some roles are considered privileged because they provide sensitive administrative access.

When reviewing a role, check its description to understand its permissions.

The Assignments section shows which users or groups have that role.

Through PIM role settings, an organization can configure requirements such as:

- MFA
- Approval
- Activation duration
- Justification
- Notifications

Examples of privileged roles include:

- Global Administrator
- Privileged Role Administrator
- Security Administrator
- Exchange Administrator
- SharePoint Administrator


# Managing Roles in Microsoft 365 Admin Center

Go to:

Microsoft 365 Admin Center
→ Show All
→ Roles
→ Role Assignments

From this section, you can:

- View available roles
- Read each role's permissions
- See current assignments
- Assign users or groups to roles


## Microsoft Defender Roles

To view permissions related to Microsoft Defender, go to the Microsoft Defender portal and open the Permissions section.

The exact navigation may vary depending on the portal version.

These roles are related specifically to security operations and Microsoft Defender.

Examples:

Security Reader
→ Can view security information.

Security Operator
→ Can investigate and respond to security alerts.

Security Administrator
→ Can manage many security settings and policies.


## Service-Specific Roles

Different Microsoft 365 services contain specialized roles.

Examples:

Microsoft Defender
→ Security roles

Microsoft Purview
→ Compliance and data-governance roles

Exchange Online
→ Exchange roles

SharePoint Online
→ SharePoint roles

Microsoft Teams
→ Teams roles

This supports least privilege because an administrator can receive access only to the service they manage instead of receiving Global Administrator access.


# Built-in and Custom Roles in Intune

In Intune, go to:

Tenant Administration
→ Roles

From this section, you can view built-in roles and create custom roles.

Built-in Role
→ A predefined role created by Microsoft.

Custom Role
→ A role created by the organization with selected permissions.

One important built-in role is:

Intune Role Administrator

This role can manage Intune roles, role assignments, and custom role definitions.


# What Is Windows 365?

Windows 365 is a Microsoft service that provides a complete Windows computer in the cloud.

This cloud-based computer is called a:

Cloud PC

The user can connect to the same:

- Desktop
- Applications
- Settings
- Files

from different devices.

Normal PC
→ Windows runs on the physical device.

Windows 365
→ Windows runs in the cloud, and the user connects to it remotely.


# Windows 365 Roles in Intune

Windows 365 roles in Intune control who can manage Cloud PCs.

Cloud PC Administrator
→ Can create, configure, provision, and manage Windows 365 Cloud PCs.

Cloud PC Reader
→ Can view Cloud PC information and settings but cannot make administrative changes.


# Windows Autopatch

Windows Autopatch is a Microsoft service that helps automate the management of updates for supported Windows devices and Microsoft applications.

It helps organizations deploy updates gradually and monitor update health.


# Windows Autopatch Roles

Windows Autopatch roles determine who can manage or view Autopatch operations.

Windows Autopatch Administrator
→ Can manage Autopatch settings, device groups, reports, messages, and support requests.

Windows Autopatch Reader
→ Can view Autopatch information and reports but cannot make administrative changes.


## Autopatch Device Groups

Autopatch device groups organize devices into deployment rings.

Updates can be installed gradually.

Example:

Test Group
→ A small number of devices receive the update first.

Early Group
→ A larger number of devices receive the update after initial testing.

Broad Group
→ Most organizational devices receive the update after the update appears stable.

The purpose is to avoid deploying a problematic update to every device at the same time.

If an update causes problems, the organization can pause or investigate deployment before it reaches the remaining devices.


# Scope Tags in Microsoft Intune

Scope Tags limit which Intune objects an administrator can see and manage.

Example:

A company has four branches across the country.

An IT Help Desk employee works at Branch A.

The administrator assigns:

Role
→ Defines what the Help Desk employee can do.

Scope
→ Defines which users or devices the employee can manage.

Scope Tag
→ Helps limit visibility to Intune objects associated with Branch A.

Example:

Role
→ Help Desk Operator

Scope
→ Branch A user and device groups

Scope Tag
→ Branch-A

Result:

The Help Desk employee can perform permitted support tasks only for the users, devices, and Intune objects within Branch A.

Role
→ What the administrator can do.

Scope
→ Which users or devices the role assignment applies to.

Scope Tag
→ Which tagged Intune objects the administrator can see and manage.
