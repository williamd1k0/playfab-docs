---
author: jdeweyMSFT
title: "PartyNetwork::SetCustomContext"
description: Configures an optional, custom pointer-sized context value with this network object.
ms.author: jdewey
ms.topic: reference
ms.prod: playfab
ms.date: 09/25/2019
ROBOTS: NOINDEX,NOFOLLOW
---

# PartyNetwork::SetCustomContext  

Configures an optional, custom pointer-sized context value with this network object.  

## Syntax  
  
```cpp
PartyError SetCustomContext(  
    void* customContext  
)  
```  
  
### Parameters  
  
**`customContext`** &nbsp; void*  
*optional*  
  
An arbitrary, pointer-sized value to store with the network object.  
  
  
### Return value  
PartyError
  
```c_partyErrorSuccess``` if configuring the custom context succeeded or an error code otherwise. The human-readable form of the error code can be retrieved via [PartyManager::GetErrorMessage()](../../PartyManager/methods/partymanager_geterrormessage.md).
  
## Remarks  
  
The custom context is typically used as a "shortcut" that simplifies accessing local, title-specific memory associated with the network without requiring a mapping lookup. The value is retrieved using the [GetCustomContext()](partynetwork_getcustomcontext.md) method. <br /><br /> Any configured value is treated as opaque by the library, and is only valid on the local device; it is not transmitted over the network.
  
## Requirements  
  
**Header:** Party.h
  
## See also  
[PartyNetwork](../partynetwork.md)  
[PartyNetwork::GetCustomContext](partynetwork_getcustomcontext.md)
  
  
