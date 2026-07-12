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

###### Important:

A provisioning package makes bulk setup faster, but the package normally still needs to be applied to each device.

For modern large-scale Windows deployment, Windows Autopilot is often a better option.
