---
author: jdeweyMSFT
title: "PartyDevice::GetCustomContext"
description: Retrieves the app's private, custom pointer-sized context value previously associated with this device object.
ms.author: jdewey
ms.topic: reference
ms.prod: playfab
ms.date: 09/25/2019
ROBOTS: NOINDEX,NOFOLLOW
---

# PartyDevice::GetCustomContext  

Retrieves the app's private, custom pointer-sized context value previously associated with this device object.  

## Syntax  
  
```cpp
PartyError GetCustomContext(  
    void** customContext  
)  
```  
  
### Parameters  
  
**`customContext`** &nbsp; void**  
*output, may return nullptr*  
  
The output custom context.  
  
  
### Return value  
PartyError
  
```c_partyErrorSuccess``` if retrieving the custom context succeeded or an error code otherwise. The human-readable form of the error code can be retrieved via [PartyManager::GetErrorMessage()](../../PartyManager/methods/partymanager_geterrormessage.md).
  
## Remarks  
  
If no custom context has been set yet, the value pointed to by `customContext` is set to nullptr.
  
## Requirements  
  
**Header:** Party.h
  
## See also  
[PartyDevice](../partydevice.md)  
[PartyDevice::SetCustomContext](partydevice_setcustomcontext.md)
  
  
