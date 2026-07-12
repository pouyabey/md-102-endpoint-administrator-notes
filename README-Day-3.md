# MD-102 Endpoint Administrator Notes - Day 3

## Microsoft Intune Device Enrollment and Management


Today’s topic is Microsoft Intune and how organizations add and manage devices.

Microsoft Intune is a cloud-based endpoint management platform. It can be used to manage different types of devices, including:

- Windows computers
- macOS devices
- Android devices
- iPhones and iPads

Microsoft previously used the name Microsoft Endpoint Manager for the combined management platform that included Intune and Configuration Manager. The current cloud management portal is called the Microsoft Intune admin center.

## Devices Overview

When you sign in to:

https://intune.microsoft.com

you can select **Devices** from the navigation menu.

This section shows the devices that are connected to and managed by Intune.

Under **By platform**, devices can be viewed based on their operating system, such as Windows, Android, iOS/iPadOS, and macOS.

One important thing to remember is that Microsoft frequently changes the layout and navigation of its admin portals. The location or name of some options may be different in the future.

The more experience you gain with the platform, the easier it becomes to adapt to these interface changes.

## Device Onboarding

Inside the Devices section, there is an area called **Device onboarding**.

In the current interface, this area includes options such as:

- Enrollment
- Windows 365

These options are used for different purposes.

## Enrollment

Enrollment determines how devices are registered with Intune so that the organization can manage them.

There are several possible enrollment methods.

### Automatic Intune Enrollment

An organization can configure Windows devices to automatically enroll in Intune when they are joined to Microsoft Entra ID.

The basic process is:

Microsoft Entra ID Join
→ Automatic Intune Enrollment
→ Device management through Intune

Automatic enrollment can be enabled for all users or only selected groups of users.

### Windows Autopilot Enrollment

Devices prepared through Windows Autopilot can also be automatically enrolled in Intune.

Windows Autopilot is commonly used for new company-owned devices.

The organization registers the device with Windows Autopilot and assigns an Autopilot deployment profile to it.

When the employee turns on the device and connects it to the internet, the device can:

- Display the organization’s sign-in experience
- Join Microsoft Entra ID
- Enroll in Intune
- Receive company applications
- Receive configuration and security policies

The basic process is:

Windows Autopilot
→ Microsoft Entra ID Join
→ Intune Enrollment
→ Applications and policies are applied

### BYOD Enrollment

BYOD stands for Bring Your Own Device.

This means that an employee uses a personally owned device to access company resources.

A personal device may be enrolled through methods such as:

- Adding a work or school account
- Using the Company Portal application

If the organization allows personal device enrollment, the device can be registered with Intune and receive the required management or security settings.

Organizations can also configure enrollment restrictions to control:

- Which users are allowed to enroll devices
- Which operating systems are allowed
- Whether personally owned devices are allowed
- How many devices each user can enroll

## Windows 365

The Windows 365 section is related to creating and managing Cloud PCs.

A Cloud PC is a Windows computer that runs in Microsoft’s cloud instead of directly on the employee’s physical device.

The employee connects to the Cloud PC through the internet and sees a separate Windows desktop environment.

It is similar to opening a virtual machine in a window, but the Windows environment is running in Microsoft’s cloud rather than on the employee’s local computer.

Organizations may use Windows 365 to provide employees with secure and centrally managed work environments.

## Windows 365 Provisioning Policies

A Windows 365 provisioning policy defines how Cloud PCs should be created.

For example, the administrator can configure:

- Which Windows image should be used
- How the Cloud PC should join Microsoft Entra ID
- Which network connection should be used
- Which users should receive a Cloud PC
- How the Cloud PC should be configured during deployment

The provisioning policy is then assigned to a user group.

Users generally need both:

- Membership in the assigned group
- An appropriate Windows 365 license

When both conditions are met, a Cloud PC can be provisioned for that user.

The basic process is:

Create a Windows 365 provisioning policy
→ Assign the policy to a user group
→ Confirm that users have Windows 365 licenses
→ A dedicated Cloud PC is created for each eligible user

After the Cloud PC is created, it appears as a Windows device in Intune.

The administrator can then manage it by deploying:

- Applications
- Configuration policies
- Compliance policies
- Security settings
- Updates

## Screenshot

![Microsoft Intune Device Onboarding Overview](screenshots/Day3-01.png)

# Microsoft Intune: Apps, Devices, and Enrollment Settings

## Apps in Microsoft Intune

Microsoft Intune includes an Apps section that administrators can use to deploy, configure, protect, and manage applications.

Main capabilities include:

- Installing applications on managed devices
- Making application installation mandatory
- Making applications available through Company Portal
- Configuring application settings
- Assigning applications to specific users or device groups
- Applying application security and data-protection policies
- Removing company data from managed applications without wiping the entire device
- Monitoring application installation status and deployment failures


---

## Devices in Microsoft Intune

The Devices section is used to enroll, configure, secure, monitor, and manage devices.

Main capabilities include:

- Creating and deploying device configuration policies
- Applying security settings to devices
- Deploying PowerShell scripts
- Creating compliance policies
- Checking whether devices are compliant
- Viewing device inventory and hardware information
- Performing remote actions such as restart, sync, retire, and wipe
- Monitoring device configuration and enrollment status

Intune configuration profiles are somewhat similar to traditional Group Policy. However, Intune is cloud-based and is not an exact replacement for every Group Policy setting.


---

## Other Important Intune Sections

The Intune admin center contains several other important sections.

Examples:

- Reports: View information about device compliance, firewall status, configuration profiles, applications, and security policies.
- Users: View users and information related to their managed devices and applications.
- Groups: Assign policies, applications, and configurations to selected users or devices.
- Endpoint security: Configure antivirus, firewall, disk encryption, account protection, and attack-surface reduction settings.

I will explore these sections in more detail through practical labs later.

---

## Intune Licensing

Users who enroll devices, receive Intune policies, or access managed company resources generally need an appropriate Intune license.

Intune is included in several Microsoft licensing packages, such as:

- Microsoft Intune Plan 1
- Microsoft 365 E3
- Microsoft 365 E5
- Enterprise Mobility + Security E3
- Enterprise Mobility + Security E5
- Microsoft 365 Business Premium

The exact licensing requirement depends on the organization's environment and the features being used.

---

## Intune and Microsoft Configuration Manager

Microsoft Intune is increasingly used for cloud-based endpoint management.

SCCM has had several names:

- System Center Configuration Manager
- Microsoft Endpoint Configuration Manager
- Microsoft Configuration Manager

Its current name is Microsoft Configuration Manager.

Configuration Manager is still supported and commonly used in on-premises and hybrid environments. It can also work together with Intune through co-management.

Therefore, Intune has not completely replaced Configuration Manager, but many organizations are gradually moving more workloads to Intune.

Microsoft frequently changes product names, so it is useful to recognize both the old and current names.

---

# Configuring Enrollment Settings

To configure device enrollment, go to:

```
Intune admin center
└── Devices
    └── Device onboarding
        └── Enrollment
```

Enrollment options are organized by operating system because Windows, Apple, and Android devices use different enrollment methods.

---

# Windows Enrollment

## Automatic Enrollment

Automatic enrollment allows eligible Windows devices to enroll in Intune when they are joined or registered with Microsoft Entra ID.

This can happen when:

- A corporate device joins Microsoft Entra ID
- A user adds a work or school account to a device
- A supported provisioning or enrollment method is used

The administrator configures the MDM user scope to determine which users can automatically enroll devices.

The MDM user scope can normally be configured as:

- None
- Some
- All

Important:

Joining or registering a device in Microsoft Entra ID and enrolling it in Intune are two separate processes.

Automatic enrollment connects these processes when it is correctly configured.

---

## Windows Hello for Business

Windows Hello for Business is not an enrollment method.

It is an authentication feature that can be configured during or after device provisioning.

It allows users to sign in using stronger authentication methods, such as:

- A device-specific PIN
- Fingerprint recognition
- Facial recognition
- Security keys

Windows Hello for Business helps reduce dependence on traditional passwords.

---

## CNAME Validation

A DNS CNAME record helps Windows devices automatically find the correct Intune enrollment server.

For example:

EnterpriseEnrollment.companydomain.com

The CNAME Validation option checks whether the required DNS record has been configured correctly.

Without the correct CNAME record, users performing some manual enrollment methods may need to enter the enrollment server address manually.

CNAME configuration is especially useful when:

- The organization uses manual Windows enrollment
- Automatic enrollment is not being used
- The organization uses custom domain names
- Devices cannot automatically find the enrollment endpoint

CNAME is not specifically based on whether the organization uses an on-premises network or Microsoft Entra ID Premium.

Its importance mainly depends on the enrollment method.


---

# Enrollment Status Page

The Enrollment Status Page, also called ESP, controls what users see while a Windows device is being prepared and configured.

It is not only a reporting page. Administrators create and configure Enrollment Status Page profiles.

An ESP profile can control:

- Whether enrollment progress is displayed
- Which setup stages are shown
- Whether users can access the desktop before setup finishes
- Whether the device remains blocked until required applications are installed
- Whether the device remains blocked until required security policies are applied
- What happens when setup exceeds the configured time limit
- Whether users can collect logs after a failure
- Whether users can reset the device after a failure

The purpose of ESP is to prevent users from accessing a partially configured device before required applications and policies are ready.

---

# Apple Device Enrollment

## Apple MDM Push Certificate

Before Intune can manage Apple devices, an Apple MDM Push Certificate must be configured.

This certificate allows Intune to communicate with Apple devices through the Apple Push Notification service, also called APNs.

Intune uses this communication channel to notify Apple devices that new commands or policies are available.

Examples include:

- Installing applications
- Applying configuration profiles
- Applying security settings
- Locking a device
- Sending remote management commands
- Requesting updated device information

The Apple MDM Push Certificate normally needs to be renewed every year.

Important:

The certificate should always be renewed using the same organizational Apple Account that was originally used to create it.

Creating a completely new certificate instead of renewing the existing one may require Apple devices to be enrolled again.

---

## Certificate Signing Request

CSR stands for Certificate Signing Request.

The CSR file is downloaded from Intune and uploaded to the Apple Push Certificates Portal.

Apple uses the CSR to create the Apple MDM Push Certificate.

The general process is:

1. Open the Apple MDM Push Certificate settings in Intune.
2. Download the CSR file from Intune.
3. Open the Apple Push Certificates Portal.
4. Sign in using an organizational Apple Account.
5. Select Create a Certificate.
6. Accept Apple's terms and conditions.
7. Upload the CSR file downloaded from Intune.
8. Download the Apple MDM Push Certificate.
9. Return to the Intune admin center.
10. Enter the Apple Account used to create the certificate.
11. Upload the certificate file.
12. Save the configuration.

After completing these steps, supported Apple devices can enroll in Intune.


---

# Android Enrollment

Before managing Android Enterprise devices, Intune must be connected to Managed Google Play.

The general process is:

1. Open Android enrollment settings in Intune.
2. Select the option to connect Managed Google Play.
3. Sign in using the Google account used by the organization.
4. Enter the required organization information.
5. Accept the Android Enterprise agreement.
6. Complete the registration.
7. Return to Intune and confirm that the Managed Google Play connection is active.

After the connection is complete, administrators can:

- Enroll Android Enterprise devices
- Approve and deploy Managed Google Play applications
- Create Android configuration profiles
- Apply compliance and security policies
- Configure personally owned and corporate-owned enrollment methods


---

# Enrollment Device Limit Restrictions

Enrollment device limit restrictions control how many devices a user is allowed to enroll in Intune.

The limit can be configured from 1 to 15 devices per user.

The default Intune restriction is commonly set to five devices, but administrators should verify the current setting in their tenant.

To view or create a device limit restriction, go to:

```
Devices
└── Device onboarding
    └── Enrollment
        └── Device platform restrictions
            └── Device limit restrictions
```

Administrators can create multiple restriction policies and assign them to different user groups.

When creating a restriction, the administrator can configure:

- Policy name
- Description
- Maximum number of devices
- Priority
- Assigned user groups

For example:

- Regular employees may be allowed to enroll five devices.
- Contractors may be allowed to enroll only one device.
- IT personnel may receive a different enrollment limit.

The restriction must be assigned to a user group before it applies.


---

# Summary

Microsoft Intune provides centralized cloud-based management for applications and devices.

The Apps section is mainly used to:

- Deploy applications
- Configure applications
- Protect organizational data
- Monitor application installations

The Devices section is mainly used to:

- Enroll devices
- Apply configuration and security policies
- Deploy scripts
- Check compliance
- Perform remote actions

Enrollment settings determine how Windows, Apple, and Android devices connect to Intune.

Each operating system has its own requirements and enrollment methods, which I will explore through practical labs.
