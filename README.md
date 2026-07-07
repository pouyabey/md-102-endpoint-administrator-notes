# Microsoft Entra ID Device Notes

### I  started to study for md-102 certification exam yesterday. I will keep updating this readme file as long as I'm preparing for exam.
### The PowerShell repository I made yesterday is also useful for md-102 exam.
### Should you have any questions, feel free to contact me pouya.ecn@gmail.com

---


## Why do we add devices to Microsoft Entra ID?

Devices are added or registered in Microsoft Entra ID so organizations can control and secure access to company resources.

Example:

If an employee uses a personal laptop for work, this is called BYOD, or Bring Your Own Device.

The employee can still sign in to the laptop with a local account or personal account. However, when they want to access company resources like Microsoft 365, Teams, SharePoint, OneDrive, or work apps, they must use their Microsoft Entra ID work account.

This helps the company apply security rules and protect company data.

Examples of what Entra ID can help with:

- Single Sign-On (SSO)
- Conditional Access
- Passwordless sign-in with Microsoft Authenticator
- Controlling access to company apps and resources
- Working with Intune to check whether a device is compliant

Important:

Microsoft Entra ID is mainly for identity and access management.

Microsoft Intune is mainly for device management, app management, and compliance.

## Main device types

There are two important device types:

1. Microsoft Entra Registered
2. Microsoft Entra Joined

## Microsoft Entra Registered

Microsoft Entra Registered devices are usually personal devices.

This is common in BYOD scenarios.

The user signs in to the device with a personal or local account, but signs in to company resources with their Entra ID work account.

Examples:

- Personal laptop
- Personal phone
- Personal tablet

This gives the company some control over access to company data, but the device is still personal.

## Microsoft Entra Joined

Microsoft Entra Joined devices are usually company-owned devices.

In this case, the user signs in to Windows itself using their Microsoft Entra ID work account.

Example:

The company gives a laptop to an employee. The employee turns it on and signs in with their work email and password.

This type gives the company more control over the device.

Important:

Microsoft Entra Join is mainly for Windows 10 and Windows 11, except Home editions.

Windows Home edition does not support Entra Join.

## Entra Registered vs Entra Joined

Entra Registered:

- Usually BYOD
- Usually personal device
- User signs in to the device with a personal/local account
- User signs in to company resources with Entra ID
- Less company control

Entra Joined:

- Usually company-owned device
- User signs in to Windows with Entra ID
- Usually managed by Intune
- More company control

## How to configure devices

Windows 10/11:

Settings > Accounts > Access work or school

iOS and Android:

- Microsoft Intune Company Portal
- Microsoft Authenticator

macOS:

- Microsoft Intune Company Portal

Linux:

- Microsoft Intune-supported enrollment method or Intune agent, depending on support

## MDM and MAM

There are two important concepts:

1. MDM
2. MAM

## MDM: Mobile Device Management

MDM means managing the whole device.

Microsoft Intune is an example of MDM.

With MDM, the company can:

- Configure device settings
- Require password or PIN
- Require encryption
- Install apps
- Check compliance
- Manage updates
- Wipe company data or the whole device if needed

## MAM: Mobile Application Management

MAM means managing apps, not the whole device.

This is useful for BYOD.

With MAM, the company can:

- Protect company data inside apps
- Block copy/paste from work apps to personal apps
- Require PIN for work apps
- Remove company data from apps without wiping the whole device

## Conditional Access and Intune

Conditional Access is configured in Microsoft Entra ID.

Intune can report whether a device is compliant.

Example:

A company can create a rule that says:

Only allow access to company resources if the device is compliant.

A compliant device may mean:

- Enrolled in Intune
- Password or PIN enabled
- Encryption enabled
- Not rooted or jailbroken
- Meets company security requirements

## Provisioning Entra Joined Devices

Provisioning means preparing a device for work use.

For Entra Joined devices, this can happen in different ways.

## OOBE

OOBE means Out-of-Box Experience.

This is the setup screen when a new Windows device is turned on for the first time.

During setup, the user can sign in with a work account, and the device can join Microsoft Entra ID.

## Join from Settings

If Windows is already installed, the device can be joined later from:

Settings > Accounts > Access work or school

## Bulk Enrollment and Windows Autopilot

Bulk enrollment is useful when a company has many devices.

Example:

A company buys 50 laptops.

Instead of setting up each laptop manually, IT can use Windows Autopilot.

Autopilot uses the device hardware hash to identify the device.

The hardware hash is uploaded to Intune/Autopilot.

When the employee turns on the laptop and connects to the internet, Windows recognizes that the device belongs to the company.

Then the employee signs in with a work account, and the device can automatically:

- Join Microsoft Entra ID
- Enroll in Intune
- Receive company policies
- Install required apps

## Summary

Microsoft Entra Registered is mostly for personal/BYOD devices.

Microsoft Entra Joined is mostly for company-owned Windows devices.

Entra ID manages identity and access.

Intune manages devices, apps, and compliance.

Conditional Access uses Entra ID policies and can use Intune compliance status to decide whether access should be allowed or blocked.

Windows Autopilot helps companies deploy many Windows devices automatically.
