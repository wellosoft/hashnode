---
title: "How to Install Unity and Visual Studio on Mac without Admin Rights"
datePublished: Thu Mar 02 2023 12:40:08 GMT+0000 (Coordinated Universal Time)
cuid: cler3gspp00010ajqe7g2e0bj
slug: how-to-install-unity-and-visual-studio-on-mac-without-admin-rights
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1677805419287/b5bf6f3b-d3db-4e49-b90f-409430becc01.png
tags: macos, unity3d

---

I came across a situation where I was stuck with a work laptop that didn't allow me to install apps with system privileges... So I went with a workaround.

This assumes you still have `sudo` access needed to grant a Unity license and additional Visual Studio packages.

## Installing Unity

Start with downloading [Unity Hub for Mac](https://unity.com/download#how-get-started). After opening the `.dmg` file, copy the "Unity Hub" App and paste it to `~/Applications` (Use `⌘⇧G` to access this folder). Don't drag it directly to Applications as it will ask you for a system password.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1677756867682/4af3f849-b373-4d52-86b2-d6fe0e8e1e69.png align="center")

Continue following the installation as usual, but skip the granting license part.

When installing Unity, change the installation target directory to `~/Applications/Unity` (create the `Unity` folder in `~/Applications` first)

Now, we'll try to activate the Unity license. Use manual activation by using the "Activate with license request" as we can't use the "automatic" way without asking for a system password.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1677757232786/3c1ec6c9-becc-4448-aa2e-770efff0dd01.png align="center")

It will generate a `.alf` file, upload it to [the unity site](https://license.unity3d.com/manual), download the `.ulf`, or licensed file. Then we activate it using Terminal.

```bash
# replace "2021.3.19f1" with your Unity version
~/Applications/2021.3.19f1/Unity.app/Contents/MacOS/Unity -batchmode -manualLicenseFile ~/Downloads/Unity_v2017.x.ulf -logfile
```

It should be activated and you can open Unity from now.

## Installing Visual Studio

Download Visual Studio for Mac. Follow the usual installation steps.

Without the knowledge of the system password, we'll be stuck on this installation progress, and had to cancel:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1677758338826/dac0a709-eb51-408b-8a85-f174b2e17c09.png align="center")

Fornatunely, the download has just been cached. Open this folder in Finder using `⌘⇧G`:

```bash
~/Library/Caches/VisualStudioInstaller/downloads/
```

Find the `.dmg` file contains Visual Studio, copy the "Visual Studio" app to `~/Applications`.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1677758733574/e1d38407-e1a3-41da-8080-c184ab7309d5.png align="center")

Next, open a project with Unity. We will integrate Unity with Visual Studio.

## Additional Setup for Unity + Visual Studio

Configure your Unity to Open External Script Editor with Visual Studio for Mac: (browse and locate the editor in `~/Applications/Visual Studio.app`)

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1677759039958/e7884d1d-d02d-467d-a868-a6f491e15374.png align="center")

Next, open the C# Project. It should be opened with Visual Studio.

At first open, you will be asked to Install Mono, which is required so your project compiles:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1677759411346/db65abb9-a104-4d20-8a3c-685247e2b220.png align="center")

Clicking Restart will not work as it will ask system password. We'll use Terminal to install it.

```bash
# go to temporary downloads. Change "17.0" with your version
cd ~/Library/Caches/VisualStudio/17.0/TempDownload/ 
# install all .pkgs there
sudo installer -pkg monoframework-mdk-6.12.0.188.macos10.xamarin.universal.pkg -target /
sudo installer -pkg microsoft-jdk-11.0.16.1-macos-aarch64.pkg -target /
sudo installer -pkg OpenJDK8U-jdk_x64_mac_hotspot_8u302b08.pkg  -target /
```

Things should works now. Enjoy!

References:

* [Submit a license request from a command line and browser](https://docs.unity3d.com/2023.1/Documentation/Manual/ManualActivationCmdMac.html)
    
* [Visual Studio installation failed in MAC OS X](https://stackoverflow.com/questions/61094646/visual-studio-installation-failed-in-mac-os-x)
    
* [Installing .pkg with Terminal](https://apple.stackexchange.com/questions/72226/installing-pkg-with-terminal)