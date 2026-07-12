# Microsoft Intune Automatic and Bulk Enrollment

## 1. Windows Automatic Enrollment

Automatic enrollment allows Windows devices to enroll in Intune when they connect to Microsoft Entra ID.

Path:

Devices > Enrollment > Windows Enrollment > Automatic Enrollment

MDM User Scope options:

- None: Automatic enrollment is disabled
- Some: Only selected user groups can enroll
- All: All eligible users can enroll

Important:

- MDM is used for device enrollment and management.
- MAM is mainly used to protect company data inside applications.

---

# 2. Windows Enrollment in a Hybrid Environment

This method is used when devices are:

- Joined to on-premises Active Directory
- Synchronized with Microsoft Entra ID
- Hybrid Microsoft Entra joined

A Group Policy can automatically enroll domain-joined devices in Intune.

GPO path:

Computer Configuration
> Policies
> Administrative Templates
> Windows Components
> MDM

Enable this policy:

Enable automatic MDM enrollment using default Microsoft Entra credentials

Then link the GPO to the correct domain or Organizational Unit.

Result:

Eligible domain-joined devices automatically attempt to enroll in Intune.

---

# 3. Windows Bulk Enrollment with a Provisioning Package

For devices that are not part of a hybrid environment, Windows Configuration Designer can be used.

It creates a provisioning package with the following file extension:

.ppkg

A provisioning package can:

- Rename the computer
- Join the device to Microsoft Entra ID
- Enroll the device in Intune
- Configure Wi-Fi
- Install applications
- Add certificates
- Create a local administrator account
- Remove some preinstalled applications

A Bulk Microsoft Entra Enrollment Token can also be added to the package.

Important facts about the token:

- It has an expiration date.
- It allows multiple devices to use the same package.
- The package should be protected because it contains enrollment information.

The `.ppkg` file can be applied through:

- USB drive
- Network share
- Local storage

Important:

The package usually still needs to be applied to each device.

---

# 4. Windows Autopilot

Windows Autopilot is the modern method for deploying large numbers of Windows devices.

The device hardware information is registered with Autopilot.

When the device starts and connects to the internet, it can:

- Receive the organization’s deployment profile
- Join Microsoft Entra ID
- Enroll in Intune
- Install required applications
- Apply security and configuration policies

Autopilot is usually more scalable than manually applying provisioning packages.

---

# 5. Apple Bulk Enrollment

Before managing Apple devices, the Apple MDM Push Certificate must be configured.

Two important Apple enrollment methods are:

- Apple Configurator
- Apple Business Manager

---

## Apple Configurator

Apple Configurator can be used to prepare and enroll Apple devices.

Administrators can import device serial numbers and assign enrollment profiles.

Enrollment profiles can use:

### With User Affinity

- The device is associated with a specific user.
- Best for a company phone assigned to one employee.

### Without User Affinity

- The device is not associated with one specific user.
- Best for shared, kiosk, or task-based devices.

Users may authenticate through:

- Company Portal
- Apple Setup Assistant

---

# 6. Apple Business Manager

Apple Business Manager is used by organizations to automate Apple device enrollment.

Apple School Manager provides a similar service for educational institutions.

With Apple Business Manager:

- Devices are purchased from Apple or an authorized reseller.
- The devices are assigned to the organization.
- The devices are connected to Intune.
- Enrollment starts when the device is turned on and connected to the internet.

This process is similar to Windows Autopilot.

---

# 7. Android Zero-Touch Enrollment

Android Zero-Touch Enrollment is used for automatic enrollment of supported corporate devices.

Requirements may include:

- A supported Android device
- Android 9 or later
- Purchase from an authorized reseller
- An Android Zero-Touch account
- A Managed Google Play connection in Intune

After configuration, an enrollment profile can be assigned to the devices.

When a device starts and connects to the internet, it receives the organization’s enrollment settings.

---

# 8. Android Enrollment Types

## Personally Owned with Work Profile

Used for BYOD devices.

- Work and personal data are separated.
- Intune manages only the work profile.
- Personal data remains private.

## Corporate-Owned with Work Profile

The device belongs to the company, but limited personal use is allowed.

- Work and personal areas are separated.
- The organization has more control than in a BYOD scenario.

## Dedicated Device

Used for a specific purpose, such as:

- Kiosk
- Digital signage
- Ticket printing
- Inventory management

These devices usually do not have one assigned user.

## Fully Managed Device

The device is company-owned and intended only for work.

The organization has the highest level of control, including:

- Restricting application installation
- Preventing application removal
- Blocking factory reset
- Applying full security policies

---

# Quick Review

## Windows

- Hybrid environment: Group Policy
- Non-hybrid bulk enrollment: Provisioning Package
- Modern large-scale deployment: Windows Autopilot

## Apple

- Apple Configurator
- Apple Business Manager
- User Affinity for assigned devices
- No User Affinity for shared devices

## Android

- Zero-Touch Enrollment
- Personally Owned Work Profile
- Corporate-Owned Work Profile
- Dedicated Device
- Fully Managed Device
