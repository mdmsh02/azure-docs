---
title: Automatic device registration FAQ | Microsoft Docs
description: Automatic device registration with Azure Active Directory FAQ.
services: active-directory
documentationcenter: ''
author: MarkusVi
manager: femila

ms.assetid: cdc25576-37f2-4afb-a786-f59ba4c284c2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/30/2017
ms.author: markvi

---
# Automatic device registration FAQ

**Q: I registered the device recently. Why can’t I see the device under my user info in the Azure portal?**

**A:** Windows 10 devices that are domain-joined with automatic device registration do not show up under the USER info.
You need to use PowerShell to see all devices. 

Only the following devices are listed under the USER info:

- All personal devices that are not enterprise joined 
- All non-Windows 10 / Windows Server 2016 
- All non-Windows devices 

---

**Q: Why can I not see all the devices registered in Azure Active Directory in the Azure portal?** 

**A:** Currently, there is no way to see all registered devices in the Azure portal. 
You can use Azure PowerShell to find all devices. 
For more details, see the [Get-MsolDevice](https://docs.microsoft.com/en-us/powershell/msonline/v1/get-msoldevice) cmdlet.

--- 

**Q: How do I know what the device registration state of the client is?**

**A:** The device registration state depends on:

- What the device is
- How it was registered 
- Any details related to it. 
 

---

**Q: Why is a device I have deleted in the Azure portal or using Windows PowerShell still listed as registered?**

**A:** This is by design. The device will not have access to resources in the cloud. 
If you want to re-register the device, a manual action needs to be taken on the device. 

For Windows 10 and Windows Server 2016 that are on-premises AD domain-joined:

1.	Open the command prompt as an administrator.

2.	Type **dsregcmd.exe /leave**.

3.	Type **dsregcmd.exe**.

For other Windows platforms that are on-premises AD domain-joined:

1.	Open the command prompt as an administrator.
2.	Type `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /l"`.
3.	Type `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /j"`.

---

**Q: Why do I see duplicate device entries in Azure portal?**

**A:**

-	For Windows 10 and Windows Server 2016, if they are repeated attempts to unjoin and re-join the same device, there might be duplicate entries. 

-	If you have used Add Work or School Account, each windows user who uses Add Work or School Account will create a new device record with the same device name.

-	Other Windows platforms that are on-premises AD domain-joined using automatic registration will create a new device record with the same device name for each domain user who logs into the device. 

-	An AADJ machine that has been wiped, re-installed and re-joined with the same name, will show up as another record with the same device name.

---

**Q: Why can a user still access resources from a device I have disabled in the Azure portal?**

**A:** It can take up to an hour for a revoke to be applied.

>[!Note] 
>For lost devices, we recommend wiping the device to ensure that users cannot access the device. For more details, see [Enroll devices for management in Intune](https://docs.microsoft.com/intune/deploy-use/enroll-devices-in-microsoft-intune). 


---

**Q: Why do my users see “You can’t get there from here”?**

**A:** If you have configured certain conditional access rules to require a specific device state and the device does not meet the criteria, users are blocked and see this message. 
Please evaluate the rules and ensure that the device is able to meet the criteria to avoid this message.

---


**Q: I see the device record under the USER info in the Azure portal and can see the state as registered on the client. Am I setup correctly for using conditional access?**

**A:** The device record (deviceID) and state on the Azure portal must match the client and meet any evaluation criteria for conditional access. 
For more details, see [Get started with Azure Active Directory Device Registration](active-directory-conditional-access-device-registration-overview.md).

---

**Q: Why do I get a "username or password is incorrect" message for a device I have just joined to Azure AD?**

**A:** Common reasons for this scenario are:

1.	Your user credentials are no longer valid.

2.	Your computer is unable to communicate with Azure Active Directory. Check for any network connectivity issues.

3.	The Azure AD Join pre-requisites were not met. Please ensure that you have followed the steps for [Extending cloud capabilities to Windows 10 devices through Azure Active Directory Join](active-directory-azureadjoin-overview.md).  

4.	Federated logins requires your federation server to support a WS-Trust active endpoint. 

---

**Q: Why do I see the “Oops… an error occurred!" dialog when I try do join my PC?**

**A:** This is a result of setting up Azure Active Directory enrollment with Intune. For more details, see [Set up Windows device management](https://docs.microsoft.com/intune/deploy-use/set-up-windows-device-management-with-microsoft-intune#azure-active-directory-enrollment).  

---

**Q: Why did my attempt to join a PC fail although I didn't get any error information?**

**A:** A likely cause is that the user is logged in to the device using the built-in administrator account. 
Please create a different local account before using Azure Active Directory Join to complete the setup. 

---

**Q: Where can I find troubleshooting information about the automatic device registration?**

**A:** For troubleshooting information, see:

1. [Troubleshooting the auto-registration of Azure AD domain joined computers for Windows 10 and Windows Server 2016](active-directory-conditional-access-automatic-device-registration-troubleshoot-windows.md)

2. [Troubleshooting the auto-registration of Azure AD domain joined computers for Windows down-level clients](active-directory-conditional-access-automatic-device-registration-troubleshoot-windows-legacy.md)
 
---

