---
author: jdeweyMSFT
title: "PartyManager::Initialize"
description: Initializes the PartyManager object instance.
ms.author: jdewey
ms.topic: reference
ms.prod: playfab
ms.date: 09/26/2019
ROBOTS: NOINDEX,NOFOLLOW
---

# PartyManager::Initialize  

Initializes the PartyManager object instance.  

## Syntax  
  
```cpp
PartyError Initialize(  
    PartyString titleId  
)  
```  
  
### Parameters  
  
**`titleId`** &nbsp; [PartyString](../../../typedefs.md)  
  
The title's PlayFab Title ID.  
  
  
### Return value  
PartyError
  
```c_partyErrorSuccess``` if the call succeeded or an error code otherwise. The human-readable form of the error code can be retrieved via [GetErrorMessage()](partymanager_geterrormessage.md).
  
## Remarks  
  
This must be called before any other method, aside from the static methods [GetSingleton()](partymanager_getsingleton.md), [SetMemoryCallbacks()](partymanager_setmemorycallbacks.md), [GetMemoryCallbacks()](partymanager_getmemorycallbacks.md), [SetThreadAffinityMask()](partymanager_setthreadaffinitymask.md), [GetThreadAffinityMask()](partymanager_getthreadaffinitymask.md), [SerializeNetworkDescriptor()](partymanager_serializenetworkdescriptor.md), and [DeserializeNetworkDescriptor()](partymanager_deserializenetworkdescriptor.md). Initialize() cannot be called again without a subsequent [Cleanup()](partymanager_cleanup.md) call. <br /><br /> Every call to Initialize() should have a corresponding Cleanup() call.   <br /><br /> The provided `titleId` must be the same Title ID used to acquire the PlayFab Entity IDs and Entity Tokens that will be passed to [CreateLocalUser()](partymanager_createlocaluser.md).
  
## Requirements  
  
**Header:** Party.h
  
## See also  
[PartyManager](../partymanager.md)  
[PartyManager::CreateLocalUser](partymanager_createlocaluser.md)  
[PartyManager::Cleanup](partymanager_cleanup.md)  
[PartyManager::GetSingleton](partymanager_getsingleton.md)  
[PartyManager::SetMemoryCallbacks](partymanager_setmemorycallbacks.md)  
[PartyManager::GetMemoryCallbacks](partymanager_getmemorycallbacks.md)  
[PartyManager::SetThreadAffinityMask](partymanager_setthreadaffinitymask.md)  
[PartyManager::GetThreadAffinityMask](partymanager_getthreadaffinitymask.md)  
[PartyManager::SerializeNetworkDescriptor](partymanager_serializenetworkdescriptor.md)  
[PartyManager::DeserializeNetworkDescriptor](partymanager_deserializenetworkdescriptor.md)
  
  
