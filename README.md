[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

# Dynamic Wallpaper
Turn your Cisco video device wallpaper from a static image to a rolling video. 

* [Introduction](https://github.com/dhenwood/Dynamic-Wallpaper#introduction)
* [Video](https://github.com/dhenwood/Dynamic-Wallpaper#video)
* [Setup](https://github.com/dhenwood/Dynamic-Wallpaper#setup)
* [Examples](https://github.com/dhenwood/Dynamic-Wallpaper#examples)

![example](https://github.com/dhenwood/Dynamic-Wallpaper/blob/main/DynamicWallpaperExample.gif)

## Introduction
The capability to display a looped video is not a native RoomOS feature, but rather leverages the embedded Chromium browser in the current Cisco video device portfolio. Note: whilst this capability will work on all Cisco video devices, it is better suited to the room series as the touch devices (Desk and Board series) require interactions on the screen.

## Video
A short video of this in action can be found on [Vidcast](https://app.vidcast.io/share/23e1360f-2ef6-4fc5-a89c-9f4b5514f3e3)

## Setup
In order to have the browser communicate to the video device, the [jsxapi library](https://github.com/cisco-ce/jsxapi) is used to establish a websocket connection through which, the device name, airplay/miracast support and calendar information is passed. In order establish this connection, the following steps are required on the video device. 

I will use the xAPI commands to set this up, however the same can be achived via the devices WebGUI or Control Hub.
1. A local user account needs to be created with only the User permissions required. ```xCommand UserManagement User Add Role: Integrator Role: User Username: "dynamicWallpaper" Passphrase: "C!sco123"```
2. The video devices webview needs to trust the video device's self-signed certificate. This requires the AllowDeviceCertificate value to be set to True. ```xConfiguration WebEngine Features AllowDeviceCertificate: True``` Once this command has been applied, a **reboot of the device** is needed.

## Examples
After applying the two commands in the previous section, perform the following xapi command to launch the dynamic wallpaper. Ensure you replace the username, password and IP address fields to reflect your video device details ```xcommand UserInterface WebView Display url: https://www.employees.org/~dhenwood/video/obtp.html?username=dynamicWallpaper&password=C!sco123&ipAddress=192.168.0.10&video=Oregon```

Their are currently a few videos to select from, so by replacing the above command from video=Oregon, to one of the following, you will get different videos.
* Oregon
* Utah
* LakeFire
* Fluid

To stop the Dynamic Wallpaper, you can perform the following xapi command ```xcommand WebEngine DeleteStorage ```
