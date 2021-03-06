---
title: Sample Registry Entry for UVC Extension Units
author: windows-driver-content
description: Sample Registry Entry for UVC Extension Units
ms.assetid: a34e00e2-90f0-4073-8740-7f3e04d68639
keywords:
- registry WDK USB Video Class
- extension units WDK USB Video Class , samples, registry entry
- sample code WDK USB Video Class , registry entry for UVC extension units
ms.author: windowsdriverdev
ms.date: 04/20/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
ms.localizationpriority: medium
---

# Sample Registry Entry for UVC Extension Units


This topic contains a sample registry entry that you can use to support Extension Units.

The entries must be added to the **HKLM\\System\\CurrentControlSet\\Control\\NodeInterfaces** registry subkey. This registry subkey contains property set GUID values and the IID and CLSID values for the interfaces that correspond to that property set.

Verify that:

-   The property set GUID matches the GUID in the [Extension Unit descriptor](sample-extension-unit-descriptor.md).

-   The IID and CLSID values in the **NodeInterfaces** subkey are stored in binary, little-endian form.

     

    Thus, an IID value of {12345678-1234-5678-0123456789abcdef}

     

    would be stored as 78 56 34 12 34 12 78 56 01 23 45 67 89 ab cd ef.

-   The GUIDs must be unique and should be generated by using *Guidgen.exe*, a tool that is included in the Microsoft Windows SDK.

Include the following code in the registry script, arbitrarily named *Xusample.rgs*:

```cpp
HKLM
{
    NoRemove SYSTEM
    {
        NoRemove CurrentControlSet
        {
            NoRemove Control
            {
                NoRemove NodeInterfaces
                {
                    ForceRemove {xxxxxxxx-xxxx-xxxx-xxxx-
                       xxxxxxxxxxxx} = s &#39;Extension Unit 
                       Property Set&#39;
                    {
                        val IID = b &#39;yyyyyyyyyyyyyyyyyyy
                           yyyyyyyyyyyyy&#39;
                        val CLSID = b &#39;zzzzzzzzzzzzzzzzz
                           zzzzzzzzzzzzzzz&#39;
                    }             
                }
            }
        }
    }
}
```

To support installation by registering the plug-in DLL, add the following code to your registry script:

```cpp
HKCR
{
    NoRemove CLSID
    {
         ForceRemove {zzzzzzzz-zzzz-zzzz-zzzz-zzzzzzzzzzzz} = s &#39;CompanyName Extension Unit Interface&#39;
        {
            InprocServer32 = s &#39;%MODULE%&#39;
                                                {
                                val ThreadingModel = s &#39;Both&#39;
                                                }
        }
 
    }
}
```
