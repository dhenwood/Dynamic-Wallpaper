[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

# Dynamic Wallpaper
Turn your Cisco video device wallpaper from a static image to a rolling video. 

* [Introduction](https://github.com/dhenwood/Dynamic-Wallpaper#introduction)
* [Video](https://github.com/dhenwood/Dynamic-Wallpaper#video)
* [Setup](https://github.com/dhenwood/Dynamic-Wallpaper#setup)

![example](https://github.com/dhenwood/Dynamic-Wallpaper/blob/main/DynamicWallpaperExample.gif)

## Introduction
The capability to display a looped video is not a native RoomOS feature, but rather leverages the embedded Chromium browser in the current Cisco video device portfolio. Note: whilst this capability will work on all Cisco video devices, it is better suited to the room series as the touch devices (Desk and Board series) require interactions on the screen.

## Video
A short video of this in action can be found on [Vidcast](https://app.vidcast.io/share/23e1360f-2ef6-4fc5-a89c-9f4b5514f3e3)

## Setup
In order to have the browser communicate to the video device, the [jsxapi library](https://github.com/cisco-ce/jsxapi) is used to establish a websocket connection through which, the device name, airplay/miracast support and calendar information is passed. In order establish this connection, the following steps are required on the video device. 

### Option 1 (simple macro)
The following article contains the steps to install a macro to allow a user to turn on or off as well as different video options. https://github.com/dhenwood/Dynamic-Wallpaper-Simple-Setup

### Option 2 (command line)
I will use the xAPI commands to set this up, however the same can be achived via the devices WebGUI or Control Hub.
1. A local user account needs to be created with only the User permissions required. You will likely want to replace the username and password to something else for security reasons. ```xCommand UserManagement User Add Role: User Username: "dynamicWallpaper" Passphrase: "C!sco123"```
2. The video devices webview needs to trust the video device's self-signed certificate. This requires the AllowDeviceCertificate value to be set to True. ```xConfiguration WebEngine Features AllowDeviceCertificate: True```
3. After applying the two commands above, perform the following xapi command to launch the dynamic wallpaper. Ensure you **replace the username, password** (to what you set in step 1) and **IP address** fields to reflect your video device details. ```xcommand UserInterface WebView Display url: https://www.employees.org/~dhenwood/video/obtp.html?username=dynamicWallpaper&password=C!sco123&ipAddress=192.168.0.10&video=Oregon```

Their are currently a few videos to select from so from the above command simply replace the "video" variable (at the end) from Oregon, to one of the following:
* Oregon
* Utah
* LakeFire
* Magic
* Rollercoaster
* Any MP4 file online - remove the .mp4 extension in the URL (eg, http://commondatastorage.googleapis.com/gtv-videos-bucket/sample/BigBuckBunny)

To stop the Dynamic Wallpaper, you can perform the following xapi command ```xcommand WebEngine DeleteStorage ```

### Option 3 (customized videos)
Download the obtp.html file and run it on a web server. Ensure the video files you wish to use are available. You will still need to perform Option 2 above to have the video device launch the web page, but with your own web servers address.
