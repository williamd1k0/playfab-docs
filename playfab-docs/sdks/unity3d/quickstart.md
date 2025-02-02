---
title: Unity3D quickstart
author: v-thopra
description: This guide will help you make your first PlayFab API call in the Unity3d engine.
ms.author: v-thopra
ms.date: 06/11/2018
ms.topic: article
ms.prod: playfab
keywords: playfab, unity3d, playfab unity sdk, csharp
ms.localizationpriority: medium
---

# Unity3D quickstart

This quickstart helps you make your first PlayFab API call in the Unity3d engine. Before continuing, make sure you have completed [Getting started for developers](../../personas/developer.md), which ensures you have a PlayFab account and are familiar with the PlayFab Game Manager.

Before you can call any PlayFab API, you must have a [PlayFab developer account](https://developer.playfab.com/en-us/sign-up). 

OS: This guide is written for Windows 10, however it should also work well with a Mac.

## Download Unity

If you don't have Unity installed, then you will need to install it and create a project.

1. [Download Unity3D](https://store.unity.com/download)  
    We support all recent versions of Unity including 2019 versions. Most features work better with 5.3 or higher.

2. Pick a personal or professional license based on your preferences.

3. Keep going until you can start a new project.

![Create Unity project](media/unity-create-project.png)

4. Finish creating a new empty project with a name and location of your choice.

## Download PlayFab SDK

The best way to acquire our Unity SDK is via the Unity editor extensions right within the Unity project window. Alternatively, you can directly download the Unity 3D SDK from our GitHub page. 

### Download the SDK only 

1. Log into your Unity project.

2. Click on this link to download the [PlayFab Unity3D SDK](https://api.playfab.com/downloads/unity-v2ap) from our GitHub page.

![Unity 3D SDK](media/unity-sdk.png)

3. Choose **Import** to install the selected components to your project. 

### Install the editor extensions

1. Download and Import the [PlayFab Unity Editor Extensions package](https://github.com/PlayFab/UnityEditorExtensions/raw/master/Packages/PlayFabEditorExtensions.unitypackage).

2. To import the the Unity Editor Extensions package, navigate to where the file was downloaded, and double-click on the .UnityPackage file. This will bring up the following window.

   ![Import Unity package](media/import-uedex.png)

3. Select **Import**, which will import the PlayFab Unity Editor Extensions into your project.

> [!NOTE]
> Before you can download the SDK make sure you are logged into your PlayFab account. Select the **Log In** link to take you to the login pane, and log in with your PlayFab username and password.  

   ![Log in to PlayFab](media/login-register-uedex.png)  

   - Once you have logged in, your screen should change to the one shown in the following example.
   - Select **Install PlayFab SDK**, and it will automatically import the SDK into your project, or upgrade the version you currently have.

   ![Install PlayFab SDK](media/install-sdk.png)

## Set title settings

Now that you have installed the PlayFab SDK, you will need to set your title in **Title Settings**. If you are not using editor extensions, you can do this directly in the PlayFab Settings Scriptable Object located in the folder shown below.

![PlayFab setting scriptable object](media/playfab-settings-so.png)

Otherwise, you can see the **Title Settings** in the **Editor Extensions** UI.

- Select the **Settings** tab in the **Editor Extensions**.
- The **Title ID** and **Developer Secret Key** are set automatically.

![PlayFab Settings tab](media/playfab-settings-tab.png)

Title Settings are applied when you select your studio and title name. Title ID and Developer Secret Key are applied automatically.

![PlayFab Title Settings](media/save-title-settings-uedex.png)

## Making your first API call

Now that you have installed the SDK and set your Title Settings, you are ready to make your first API call with the Unity SDK.

This part of the guide will provide the minimum steps to make your first PlayFab API call, without any GUI or on-screen feedback. Confirmation will be done with the Console log.

- Find the Project panel.

- Create a new C# script named "PlayFabLogin".

![Create a new C# script](media/first-script.png)

- In Unity, double-click this file to open it in a code-editor.
  - Depending on your settings/installed-programs, this will likely be Visual Studio or MonoDevelop.

- Next, create a new `GameObject`, and attach the script (`PlayFabLogin.cs`) to it.
- Replace the contents of `PlayFabLogin.cs` with the code shown below.

```csharp
using PlayFab;
using PlayFab.ClientModels;
using UnityEngine;

public class PlayFabLogin : MonoBehaviour
{
    public void Start()
    {
        // Note: Setting title Id here can be skipped if you have set the value in Editor Extensions already.
        if (string.IsNullOrEmpty(PlayFabSettings.staticSettings.TitleId)){
            PlayFabSettings.staticSettings.TitleId = "144"; // Please change this value to your own titleId from PlayFab Game Manager
        }
        var request = new LoginWithCustomIDRequest { CustomId = "GettingStartedGuide", CreateAccount = true};
        PlayFabClientAPI.LoginWithCustomID(request, OnLoginSuccess, OnLoginFailure);
    }

    private void OnLoginSuccess(LoginResult result)
    {
        Debug.Log("Congratulations, you made your first successful API call!");
    }

    private void OnLoginFailure(PlayFabError error)
    {
        Debug.LogWarning("Something went wrong with your first API call.  :(");
        Debug.LogError("Here's some debug information:");
        Debug.LogError(error.GenerateErrorReport());
    }
}
```  

> [!IMPORTANT]
> Please note that the code shown above is not for use with Mobile. This is only an example, and shows how to log in with a CustomID. Mobile games should use either
[LoginWithAndroidDeviceID](xref:titleid.playfabapi.com.client.authentication.loginwithandroiddeviceid), [LoginWithIOSDeviceID](xref:titleid.playfabapi.com.client.authentication.loginwithiosdeviceid), or some form of social login like [LoginWithFacebook](xref:titleid.playfabapi.com.client.authentication.loginwithfacebook).

## Finish and execute

You are now ready to test out this sample.

- Be sure to Save all files, and return to the Unity Editor.

- Press the Play button at the top of the editor.

- Be sure to **Save** all files, and return to the Unity Editor.

- Press the **Play** button at the top of the editor.

Ideally, you should see the following in your Unity Console Panel.

![Console log of first API call](media/first-call-log.png)  

> [!TIP]
>Alternatively, you can also log into the game in the PlayFab Game Manager, and select the **PlayStream Monitor** tab. Each time you **Alt+ TAB** focus away from the actively running Unity game, the game passes an event which you can see and confirm in the PlayStream Monitor.

For a list of all available client API calls, see our [PlayFab API References](../../api-references/index.md) documentation.

Happy Coding!

## Deconstruct the code

This optional last section describes each part of `PlayFabLogin.cs` in detail.

- There are 3 functions in PlayFabLogin:

  - `Start`, `OnLoginSuccess`, `OnLoginFailure`
  - `Start` is a Unity function which is automatically called for every `MonoBehaviour` object.
    - See the [Unity MonoBehaviour Guide](https://docs.unity3d.com/ScriptReference/MonoBehaviour.html) for more information.

Inside of Start():

- `PlayFabSettings.staticSettings.TitleId = "xxxx"`;
  - Every PlayFab developer creates a title in Game Manager. When you publish your game, you must code that titleId into your game. This lets the client know how to access the correct data within PlayFab. For most users, just consider it a mandatory step that makes PlayFab work.

- `var request = new LoginWithCustomIDRequest { CustomId = "GettingStartedGuide", CreateAccount = true};`
  - Most PlayFab API methods require input parameters, and those input parameters are packed into a request object.
  - Every API method requires a unique request object, with a mix of optional and mandatory parameters.
    - For `LoginWithCustomIDRequest`, there is a mandatory parameter of `CustomId`, which uniquely identifies a player and `CreateAccount`, which allows the creation of a new account with this call.

  - For login, most developers will want to use a more appropriate login method.
    - See the PlayFab Login Documentation for:
    - [LoginWithAndroidDeviceID](xref:titleid.playfabapi.com.client.authentication.loginwithandroiddeviceid)
    - [LoginWithIOSDeviceID](xref:titleid.playfabapi.com.client.authentication.loginwithiosdeviceid)
    - [LoginWithEmailAddress](xref:titleid.playfabapi.com.client.authentication.loginwithemailaddress)
    - [LoginWithFacebook](xref:titleid.playfabapi.com.client.authentication.loginwithfacebook)

Inside of `OnLoginSuccess`

- The result object of many API success callbacks will contain the requested information.
- `LoginResult` contains some basic information about the player, but for most users, login is simply a mandatory step before calling other APIs.

Inside of OnLoginFailure

- API calls can fail for many reasons, and you should always attempt to handle failure.
  - You can find error codes shared by all API methods in our [Global API Method Error Codes](../../features/automation/cloudscript/global-api-method-error-codes.md) tutorial, or specific codes at the bottom of each API method documentation.

- Why API calls fail (In order of likelihood).
  - `PlayFabSettings.staticSettings.TitleId` is not set. If you forget to set titleId to your title, then nothing will work.
  - Request parameters. If you have not provided the correct or required information for a particular API call, then it will fail. See `error.errorMessage`, `error.errorDetails`, or `error.GenerateErrorReport()` for more info.
  - Device connectivity issue. Cell-phones lose/regain connectivity constantly, and so any API call at any time can fail randomly, and then work immediately after. Going into a tunnel can disconnect you completely.
  - The PlayFab Unity SDK currently expects API calls from the main Unity thread. Calling the SDK on a background thread will likely cause exceptions with coroutines and other Unity methods not being invoked on the main Unity thread.
  - PlayFab server issue. As with all software, there can be issues. See our [forums](https://community.playfab.com/index.html) to look for issue reports similar to yours, or post your own question. You can also review our [release notes](../../release-notes/index.md).
