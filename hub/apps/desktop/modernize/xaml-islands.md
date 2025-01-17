---
description: This guide helps you to create Fluent-based UWP UIs directly in your WPF and Windows Forms applications
title: UWP controls in desktop apps
ms.date: 08/20/2019
ms.topic: article
keywords: windows 10, uwp, windows forms, wpf, xaml islands
ms.author: mcleans
author: mcleanbyron
ms.localizationpriority: medium
ms.custom: 19H1
---

# Host UWP XAML controls in desktop apps (XAML Islands)

Starting in Windows 10, version 1903, you can host UWP controls in non-UWP desktop applications using a feature called *XAML Islands*. This feature enables you to enhance the look, feel, and functionality of your existing WPF, Windows Forms, and C++ Win32 applications with the latest Windows 10 UI features that are only available via UWP controls. This means that you can use UWP features such as [Windows Ink](/windows/uwp/design/input/pen-and-stylus-interactions) and controls that support the [Fluent Design System](/windows/uwp/design/fluent-design-system/index) in your existing WPF, Windows Forms, and C++ Win32 applications.

You can host any UWP control that derives from [Windows.UI.Xaml.UIElement](https://docs.microsoft.com/uwp/api/windows.ui.xaml.uielement), including:

* Any first-party UWP control provided by the Windows SDK or WinUI library.
* Any custom UWP control (for example, a user control that consists of several UWP controls that work together). You must have the source code for the custom control so you can compile it with your application.

Fundamentally, XAML Islands are created by using the *UWP XAML hosting API*. This API consists of several Windows Runtime classes and COM interfaces that were introduced in the Windows 10, version 1903 SDK. We also provide a set of XAML Island .NET controls in the [Windows Community Toolkit](https://docs.microsoft.com/windows/uwpcommunitytoolkit/) that use the UWP XAML hosting API internally and provide a more convenient development experience for WPF and Windows Forms apps.

The way you use XAML Islands depends on your application type and the types of UWP controls you want to host.

> [!NOTE]
> If you have feedback about XAML Islands, create a new issue in the [Microsoft.Toolkit.Win32 repo](https://github.com/windows-toolkit/Microsoft.Toolkit.Win32/issues) and leave your comments there. If you prefer to submit your feedback privately, you can send it to XamlIslandsFeedback@microsoft.com. Your insights and scenarios are critically important to us.

## WPF and Windows Forms applications

We recommend that WPF and Windows Forms applications use the XAML Island .NET controls that are available in the Windows Community Toolkit. These controls provide an object model that mimics (or provides access to) the properties, methods, and events of the corresponding UWP controls. They also handle behavior such as keyboard navigation and layout changes.

There are two sets of XAML Island controls for WPF and Windows Forms applications: *wrapped controls* and *host controls*. As of Windows 10, version 1903, these controls are [available as a developer preview](#feature-roadmap).

### Wrapped controls

WPF and Windows Forms applications can use a selection of XAML Island controls that wrap the interface and functionality of a specific UWP control. You can add these controls directly to the design surface of your WPF or Windows Forms project and then use them like any other WPF or Windows Forms control in the designer.

The following wrapped UWP controls are currently available in the Windows Community Toolkit. 

| Control | Minimum supported OS | Description |
|-----------------|-------------------------------|-------------|
| [InkCanvas](https://docs.microsoft.com/windows/communitytoolkit/controls/wpf-winforms/inkcanvas)<br>[InkToolbar](https://docs.microsoft.com/windows/communitytoolkit/controls/wpf-winforms/inktoolbar) | Windows 10, version 1903 | Provide a surface and related toolbars for Windows Ink-based user interaction in your Windows Forms or WPF desktop application. |
| [MediaPlayerElement](https://docs.microsoft.com/windows/communitytoolkit/controls/wpf-winforms/mediaplayerelement) | Windows 10, version 1903 | Embeds a view that streams and renders media content such as video in your Windows Forms or WPF desktop application. |
| [MapControl](https://docs.microsoft.com/windows/communitytoolkit/controls/wpf-winforms/mapcontrol) | Windows 10, version 1903 | Enables you to display a symbolic or photorealistic map in your Windows Forms or WPF desktop application. |

For a walkthrough that demonstrates how to use the wrapped UWP controls, see [Host a standard UWP control in a WPF app](host-standard-control-with-xaml-islands.md).

### Host controls

For scenarios beyond those covered by the available wrapped controls, WPF and Windows Forms applications can also use the [WindowsXamlHost](https://docs.microsoft.com/windows/communitytoolkit/controls/wpf-winforms/windowsxamlhost) control that is available in the Windows Community Toolkit.

| Control | Minimum supported OS | Description |
|-----------------|-------------------------------|-------------|
| [WindowsXamlHost](https://docs.microsoft.com/windows/communitytoolkit/controls/wpf-winforms/windowsxamlhost) | Windows 10, version 1903 | Can host any UWP control that derives from [Windows.UI.Xaml.UIElement](https://docs.microsoft.com/uwp/api/windows.ui.xaml.uielement), including any first-party UWP control provided by the Windows SDK as well as custom controls. |

For walkthroughs that demonstrate how to use the **WindowsXamlHost** control, see [Host a standard UWP control in a WPF app](host-standard-control-with-xaml-islands.md) and [Host a custom UWP control in a WPF app using XAML Islands](host-custom-control-with-xaml-islands.md).

> [!NOTE]
> Using the **WindowsXamlHost** control to host custom UWP controls is supported only in WPF and Windows Forms apps that target .NET Core 3. Hosting first-party UWP controls provided by the Windows SDK is supported in apps that target either the .NET Framework or .NET Core 3.

<span id="requirements" />

### Configure your project to use the XAML Island .NET controls

The XAML Island .NET controls require Windows 10, version 1903, or a later version. To use these controls, install one of the NuGet packages listed below. These packages provide everything you need to use the XAML Island wrapped controls and host controls, and they include other related NuGet packages that are also required.

| Type of control | NuGet package  | Related articles |
|-----------------|----------------|---------------------|
| [Wrapped controls](#wrapped-controls) | Version 6.0.0-preview7 or later of these packages: <ul><li>WPF: [Microsoft.Toolkit.Wpf.UI.Controls](https://www.nuget.org/packages/Microsoft.Toolkit.Wpf.UI.Controls)</li><li>Windows Forms: [Microsoft.Toolkit.Forms.UI.Controls](https://www.nuget.org/packages/Microsoft.Toolkit.Forms.UI.Controls)</li></ul>  | [Host a standard UWP control in a WPF app](host-standard-control-with-xaml-islands.md)  |
| [Host control](#host-controls) | Version 6.0.0-preview7 or later of these packages: <ul><li>WPF: [Microsoft.Toolkit.Wpf.UI.XamlHost](https://www.nuget.org/packages/Microsoft.Toolkit.Wpf.UI.XamlHost)</li><li>Windows Forms: [Microsoft.Toolkit.Forms.UI.XamlHost](https://www.nuget.org/packages/Microsoft.Toolkit.Forms.UI.XamlHost)</li></ul>  | [Host a standard UWP control in a WPF app](host-standard-control-with-xaml-islands.md)<br/>[Host a custom UWP control in a WPF app](host-custom-control-with-xaml-islands.md)  |

Be aware of the following details:

* The host control packages are also included in the wrapped control packages. You can install the wrapped control packages if you want to use both sets of controls.

* If you're hosting a custom UWP control, your WPF or Windows Forms project must target .NET Core 3. Hosting custom UWP controls is not supported in apps that target the .NET Framework. You'll also need to perform some additional steps to reference the custom control. For more info, see [Host a custom UWP control in a WPF app using XAML Islands](host-custom-control-with-xaml-islands.md).

* Earlier versions of these instructions had you add the `maxversiontested` element to an application manifest in your WPF or Windows Forms project. As long as you're using the latest preview versions of the NuGet packages listed above, you no longer need to add this element to your manifest.

### Architecture of XAML Island .NET controls

Here's a quick look at how the different types of XAML Island controls are organized architecturally on top of the UWP XAML hosting API.

![Host control Architecture](images/xaml-islands/host-controls.png)

The APIs that appear at the bottom of this diagram ship with the Windows SDK. The wrapped controls and host controls are available via NuGet packages in the Windows Community Toolkit.

### Web view controls

The Windows Community Toolkit also provides the following .NET controls for hosting web content in WPF and Windows Forms applications. These controls are often used in similar desktop app modernization scenarios as the XAML Island controls, and they are maintained in the same [Microsoft.Toolkit.Win32 repo](https://github.com/windows-toolkit/Microsoft.Toolkit.Win32) repo as the XAML Island controls.

| Control | Minimum supported OS | Description |
|-----------------|-------------------------------|-------------|
| [WebView](https://docs.microsoft.com/windows/communitytoolkit/controls/wpf-winforms/webview) | Windows 10, version 1803 | Uses the Microsoft Edge rendering engine to show web content. |
| [WebViewCompatible](https://docs.microsoft.com/windows/communitytoolkit/controls/wpf-winforms/webviewcompatible) | Windows 7 | Provides a version of **WebView** that is compatible with more OS versions. This control uses the Microsoft Edge rendering engine to show web content on Windows 10 version 1803 and later, and the Internet Explorer rendering engine to show web content on earlier versions of Windows 10, Windows 8.x, and Windows 7. |

To use these controls, install one of these NuGet packages:

* WPF: [Microsoft.Toolkit.Wpf.UI.Controls.WebView](https://www.nuget.org/packages/Microsoft.Toolkit.Wpf.UI.Controls.WebView)
* Windows Forms: [Microsoft.Toolkit.Forms.UI.Controls.WebView](https://www.nuget.org/packages/Microsoft.Toolkit.Forms.UI.Controls.WebView)

## C++ Win32 applications

The XAML Island .NET controls are not supported in C++ Win32 applications. These applications must instead use the *UWP XAML hosting API* provided by the Windows 10 SDK (version 1903 and later).

The UWP XAML hosting API consists of several Windows Runtime classes and COM interfaces that your C++ Win32 application can use to host any UWP control that derives from [Windows.UI.Xaml.UIElement](https://docs.microsoft.com/uwp/api/windows.ui.xaml.uielement). You can host UWP controls in any UI element in your application that has an associated window handle (HWND). For more information about this API, including prerequisites, see [Using the UWP XAML hosting API in a C++ Win32 app](using-the-xaml-hosting-api.md).

> [!NOTE]
> The wrapped controls and host controls in the Windows Community Toolkit use the UWP XAML hosting API internally and implement all of the behavior you would otherwise need to handle yourself if you used the UWP XAML hosting API directly, including keyboard navigation and layout changes. For WPF and Windows Forms applications, we strongly recommend that you use these controls instead of the UWP XAML hosting API directly because they abstract away many of the implementation details of using the API.

## Feature roadmap

As of the release of Windows 10, version 1903, the XAML Island .NET controls in the Windows Community Toolkit are still in developer preview until the version 1.0 release of the controls is available.

* Version 1.0 of the controls for the .NET Framework 4.6.2 and later are planned to be released in the [6.0 release of the toolkit](https://github.com/windows-toolkit/WindowsCommunityToolkit/milestones).
* Version 1.0 of the controls for .NET Core 3 are planned for a later release of the toolkit.
* If you want to try the latest previews of the version 1.0 releases of these controls for the .NET Framework and .NET Core 3, see the version 6.0.0-preview7 (or later) NuGet packages in the [UWP Community Toolkit](https://dotnet.myget.org/gallery/uwpcommunitytoolkit) gallery.

For more details, see [this blog post](https://blogs.windows.com/windowsdeveloper/2019/06/13/xaml-islands-v1-updates-and-roadmap).

## Additional resources

For more background information and tutorials about using XAML Islands, see the following articles and resources:

* [Modernize a WPF app tutorial](modernize-wpf-tutorial.md): This tutorial provides step-by-step instructions for using the wrapped controls and host controls in the Windows Community Toolkit to add UWP controls to an existing WPF line-of-business application. This tutorial includes the complete code for the WPF application as well as detailed instructions for each step in the process.
* [XAML Islands v1 - Updates and Roadmap](https://blogs.windows.com/windowsdeveloper/2019/06/13/xaml-islands-v1-updates-and-roadmap): This blog post discusses many common questions about XAML Islands and provides a detailed development roadmap.
