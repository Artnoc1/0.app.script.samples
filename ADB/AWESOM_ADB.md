-----------------------------

# Awesome-adb
---

## Basic Usage
---

### Command syntax
---

#### adb basic syntax of the command is as follows:

```
adb [-d|-e|-s <serialNumber>] <command>
```

If only one device / emulator connection, you can omit the

[-d | -e | -s <serialNumber>] 

this part, the direct use 
```
adb <command>.
```
Targeting equipment for command

If you have more than one device / emulator connection, you need to specify the target device for the command.

Parameter    Meaning

-d    

Specifies currently the only Android device USB connector as the command target

-e    

Specify currently the only goal for the command to run the simulator

-s <SerialNumber>    

Specifies the device number corresponding serialNumber / simulator command target
In the case of multiple devices / simulators are connected to the more common

-s <serialNumber> 

parameters, serialNumber can be obtained through adb devices command.

Such as:
```
$ adb devices
```

List of devices attached cf264b8f    device
emulator-5554    device

Output in the cf264b8f
and emulator-5554 is 
serialNumber. 

For example, this time I want to specify cf264b8f this equipment to run the adb command to take a screen resolution:
```
adb -s cf264b8f shell wm size
```

Encountered multiple devices / simulators use the case of these parameters for the command to specify the target device, hereinafter to simplify the description will not be repeated.

###S tart/Stop

#### Start adb server command:
```
adb start-server
```

(Generally no need to manually execute this command, when you run the command adb adb server if found does not start automatically from the transfer.)

#### Stop adb server command:
```
adb kill-server
```

View adb version command:
```
adb version
```

Sample output:

Android Debug Bridge version 1.0.36
Revision 8f855a3d9b35-android

Run adbd as root

The operating principle is adb adb server daemon and the phone side PC side adbd establish a connection, then the PC side adb client via adb server forward command parsing after running adbd receive commands.
So if adbd ordinary rights to perform some require root privileges to execute the command can not be directly used adb xxx execution. Then you can then execute the command adb shell after su, but also allows adbd root privileges to perform this high privilege can execute arbitrary commands.
command:
```
adb root
```

Normal output:

restarting adbd as root
Now run adb shell, take a look at the command line prompt is not turned into a #?
After some phone root can not let adbd by adb root execute commands with root privileges, some models such as Samsung, will be prompted to adbd can not run as root in production builds, then you can install adbd 
Insecure, then adb root try.
Accordingly, if you want to restore adbd non-root privileges, you can use adb unroot command.
Designated adb server network port command:
```
adb -P <port> start-server
```

The default port is 5037.
Device connection management
Inquiries connected device / simulator command:
```
adb devices
```

Example output:
---
List of devices attached
cf264b8f    device
emulator-5554    device
---
Output format is 
---
[serialNumber] [state], 
---
serialNumber that is, we often say that the SN, state the following categories:
---
Offline 
---
indicates that the device is not connected to the success or unresponsive.
---
Device 
---
device is connected. Note that this state does not identify the Android system has been fully activated and operational in the device during startup device instance can be connected to the adb, but after boot the system before it becomes operational.
---
No device 
---
no device / emulator connection.
The output shows the current connected the two devices / simulators, cf264b8f and emulator-5554 are they SN. 
As can be seen from the emulator-5554 name it is an Android emulator.

Common alarm output:

No device / emulator connection is successful.
---
List of devices attached
---
The device / emulator is not connected to adb or unresponsive.
---
List of devices attached
cf264b8f    offline
---
USB connection
USB connection normal use adb by the need to ensure that:
---
Hardware status is normal.
---
Including Android devices in the normal power state, USB cable and interface intact.

Developer Options 2. 

Android devices and USB debugging mode is on.

You can go to the "Settings" 
  
"Developer options" 
"Android Debug" view.

If you can not find the developer options in the settings, it needs to make it through an egg is displayed: In the "Settings" - "About phone" continuous click "version number" 7 times.
The device driver is normal.
It seems to worry about the Linux and Mac OS X, the Windows likely to be encountered in the case of the need to install drivers, this can be confirmed right "Computer" - "Properties", the "Device Manager" in view on related equipment Is there a yellow exclamation point or question mark, if not explain the driving state has been good. Otherwise, you can download a mobile assistant class program to install the driver first.

Status after confirmation via USB cable connected computers and devices.
---
adb devices
If you can see
xxxxxx device

Description Connection successful.
Wireless connection (need to use the USB cable)
In addition to the USB connection to the computer to use adb, can also be a wireless connection - although the connection process is also step using USB needs, but after a successful connection to your device can get rid of the limit of the USB cable within a certain range it !

Steps:

Connect Android device to run adb computer connected to the same local area network, such as connected to the same WiFi.
The device connected to the computer via a USB cable.
Make sure the connection is successful (you can run adb devices see if you can list the device).
Allow the device listens on port 5555 TCP / IP connections:
```
adb tcpip 5555
```
Disconnect the USB connection.
Find the IP address of the device.
Generally the 'Settings' in - "About phone" - "state information" - "IP address" is found, you can also use the following in the View device information - IP address a Lane method adb command.
Connect the device via IP address.
---
adb connect <device-ip-address>
---
Here <device-ip-address> is the IP address of the device found in the previous step.
Confirm the connection status.

adb devices
If you can see
<device-ip-address>:5555 device

Description Connection successful.
If you can not connect, verify that Android devices and the computer is connected to the same WiFi, then execute adb connect <device-ip-address> that step again;
If that does not work, by adb kill-server restart the adb and then try it all over again.
The wireless connection command:
```
adb disconnect <device-ip-address>
```

Wireless connection (without using the USB cable)
Note: You need root privileges.

On a "wireless connection (need to use USB cable)" method is described in official documents, need the help of a USB cable to enable the wireless connection.
Since we want to achieve a wireless connection, it can all step down are wireless it? 
The answer is energy.
Install a terminal emulator on the Android device.
Equipment already installed you can skip this step. 
Terminal emulator download address I use is: Terminal Emulator for Android Downloads
To run the Android device and computer adb is connected to the same local area network, such as connected to the same WiFi.
Open a terminal emulator on your Android device, in which run the command sequence:
```
su
setprop service.adb.tcp.port 5555
```

Find the IP address of the Android device.
Generally the 'Settings' in - "About phone" - "state information" - "IP address" is found, you can also use the following in the View device information - IP address a Lane method adb command.
Connect Android device on a computer via adb and IP addresses.
```
adb connect <device-ip-address>
```

Here <device-ip-address> is the IP address of the device found in the previous step.
If you can see connected to <device-ip-address>: 5555 such output indicates a successful connection.
Notice: 
* Some device may not working unless you restart adbd service, so you need to run command on the device's terminal as below restart adbd if restart is not working, try following command:
```
stop adbd
start adbd
```

Application Management
Check the list of
Check the list of basic commands format
```
adb shell pm list packages [-f] [-d] [-e] [-s] [-3] [-i] [-u] [--user USER_ID] [FILTER]
```

That is the basis of adb shell pm list packages can add some parameters on the filter to view different lists, supports filtering parameters are as follows:
Parameter    display list
No    all applications
-f    Display apk file application association
-d    Show only applications disabled
-e    Show only enabled applications
-s    Display only System
-3    Show only third-party application
-i    Display applications installer
-u    Contains uninstall applications
<FILTER>    package name contains <FILTER> strings
All applications
command:
adb shell pm list packages
Example output:
package:com.android.smoketest
package:com.example.android.livecubes
package:com.android.providers.telephony
package:com.google.android.googlequicksearchbox
package:com.android.providers.calendar
package:com.android.providers.media
package:com.android.protips
package:com.android.documentsui
package:com.android.gallery
package:com.android.externalstorage
...
// other packages here
...
system applications
command:
adb shell pm list packages -s
third-party usage
command:
adb shell pm list packages -3
Application package name contains a string
For example, to view a list of package names that contain the string mazhuang applications, order:
adb shell pm list packages mazhuang
Of course, you can also use grep to filter:
adb shell pm list packages | grep mazhuang
Install APK Format:
---
adb install [-lrtsdg] <path_to_apk>
---
parameter:
Adb install may be followed by some optional parameters to control the behavior of the installation APK, available parameters and their meanings are as follows:

Parameter    Meaning
---
 -l    Will be applied to protect the installation directory / mnt / asec
 -r    Allowed to cover the installation
 -t    Allowed to install application specified in AndroidManifest.xml android: testOnly =" true " Application
 -s    Install apps to sdcard
 -d    Downgrade coverage allows installation
 -g    Grant all runtime permissions
---
After you run the command to see if similar to the following output (status is Success) represents the installation was successful:
---
[100%] /data/local/tmp/1.apk
    pkg: /data/local/tmp/1.apk
Success
---
The above is the output of adb current latest version v1.0.36, it will push apk file to display the progress of the percentage of mobile phones.
Using older versions of adb output is this:
---
12040 KB/s (22205609 bytes in 1.801s)
        pkg: /data/local/tmp/SogouInput_android_v8.3_sweb.apk
Success
---
If the status is Failure said installation failure, such as:
---
[100%] /data/local/tmp/map-20160831.apk
        pkg: /data/local/tmp/map-20160831.apk
---
Failure [INSTALL_FAILED_ALREADY_EXISTS]
---
Common Installation failed output code, the meaning and possible solutions are as follows:
---
Output    Meaning    solutions
---
INSTALL_FAILED_ALREADY_EXISTS    application already exists    use -r parameters
INSTALL_FAILED_INVALID_APK    invalid APK file    
INSTALL_FAILED_INVALID_URI    invalid filename APK    APK file names to ensure no Chinese
INSTALL_FAILED_INSUFFICIENT_STORAGE    lack of space    cleanup space
INSTALL_FAILED_DUPLICATE_PACKAGE    program of the same name already exists    
INSTALL_FAILED_NO_SHARED_USER    shared user requested does not exist    
INSTALL_FAILED_UPDATE_INCOMPATIBLE    already installed the app, but signature is not the same; or uninstalled, but data is not removed.    
INSTALL_FAILED_SHARED_USER_INCOMPATIBLE    shared user request exists but the signatures do not match    
INSTALL_FAILED_MISSING_SHARED_LIBRARY    installation package used on the device unusable shared library    
INSTALL_FAILED_REPLACE_COULDNT_DELETE    can not be deleted when replacing    
INSTALL_FAILED_DEXOPT    dex optimization validation failure or lack of space    
INSTALL_FAILED_OLDER_SDK    equipment system version is lower than the application requirements    
INSTALL_FAILED_CONFLICTING_PROVIDER    equipment already exists with the same name in application content provider    
INSTALL_FAILED_NEWER_SDK    equipment system version higher than the application requirements    
INSTALL_FAILED_TEST_ONLY    test-only applications, but when you install -t parameter is not specified    
INSTALL_FAILED_CPU_ABI_INCOMPATIBLE    contains incompatible device CPU Application Binary Interface for native code    
INSTALL_FAILED_MISSING_FEATURE    application uses device features that are unavailable    
INSTALL_FAILED_CONTAINER_ERROR    sdcard access failure    confirm sdcard is available, or to install built-in storage
INSTALL_FAILED_INVALID_INSTALL_LOCATION    can not be installed to the specified location    switch mounting position, add or delete -s parameters
INSTALL_FAILED_MEDIA_UNAVAILABLE    installation location is unavailable    generally sdcard, confirm sdcard is available or to install built-in storage
INSTALL_FAILED_VERIFICATION_TIMEOUT    Installation Timeout verify    
INSTALL_FAILED_VERIFICATION_FAILURE    verify the installation package fails    
INSTALL_FAILED_PACKAGE_CHANGED    calling application program expects inconsistent    
INSTALL_FAILED_UID_CHANGED    previously installed the app, and this assignment UID inconsistent    remove residual files previously installed
INSTALL_FAILED_VERSION_DOWNGRADE    already installed the application later    use -d parameters
INSTALL_FAILED_PERMISSION_MODEL_DOWNGRADE    installed target SDK runtime support for application permissions of the same name, to install the runtime version does not support permission    
INSTALL_PARSE_FAILED_NOT_APK    specified path is not a file or not to .apk end    
INSTALL_PARSE_FAILED_BAD_MANIFEST    unresolved AndroidManifest.xml file    
INSTALL_PARSE_FAILED_UNEXPECTED_EXCEPTION    parser encounters an exception    
INSTALL_PARSE_FAILED_NO_CERTIFICATES    installation package is not signed    
INSTALL_PARSE_FAILED_INCONSISTENT_CERTIFICATES    already installed the app, and signed with the APK files are inconsistent    first uninstall the application on the device, then install
INSTALL_PARSE_FAILED_CERTIFICATE_ENCODING    encountered while parsing APK file CertificateEncodingException    
INSTALL_PARSE_FAILED_BAD_PACKAGE_NAME    manifest file no or an invalid package name    
INSTALL_PARSE_FAILED_BAD_SHARED_USER_ID    manifest file specifies an invalid shared user ID    
INSTALL_PARSE_FAILED_MANIFEST_MALFORMED    encountered while parsing file manifest error structural    
INSTALL_PARSE_FAILED_MANIFEST_EMPTY    in the manifest file can not be found to find operable label (instrumentation or application)    
INSTALL_FAILED_INTERNAL_ERROR    installation fails because of system problems    
INSTALL_FAILED_USER_RESTRICTED    Users are limited to installing applications    open options 'install app via USB' in developer options, if it was opened, close and reopen it
INSTALL_FAILED_DUPLICATE_PERMISSION    application attempts to define an existing permission name    
INSTALL_FAILED_NO_MATCHING_ABIS    applications include device application binary interface does not support the native code    
INSTALL_CANCELED_BY_USER    applications installed on the device needs confirmation, but not operate the device or the point of cancellation    agree to install on the device
INSTALL_FAILED_ACWF_INCOMPATIBLE    applications are not compatible with the device    
INSTALL_FAILED_TEST_ONLY    APK file is build via Android Studio 'RUN'    Rebuild via Gradle assembleDebug or assembleRelease, or Generate Signed APK
Does not contain AndroidManifest.xml    invalid APK file    
Is not a valid zip file    invalid APK file    
Offline    device is not connected successfully    first device with adb successful connection
Unauthorized    unauthorized device allows debugging    
Error: device not found    not successfully connected equipment    equipment and adb first successful connection
Protocol failure    device is disconnected    first device with adb successful connection
Unknown option: -s    Android 2.2 does not support the following installation to sdcard    do not use -s parameters
No space left on device    lack of space    cleanup space
Permission denied ... sdcard ...    sdcard unavailable    
signatures do not match the previously installed version; ignoring!    already installed this app, but signatures do not match    uninstall previous installed, then install this one
Reference: PackageManager.java
Adb install internal principle Introduction
Adb install actually three steps:

push apk files to / data / local / tmp.
Call pm install installation.
Delete the corresponding apk file / data / local / tmp under.
Therefore, when necessary, according to this step, manually step through the installation process.
Uninstalling command:

adb uninstall [-k] <packagename>
<Packagename> represents the application package name, -k optional parameter indicates uninstall the application but keep the data and cache directories.
Command Example:
```
adb uninstall com.qihoo360.mobilesafe
Uninstall represents 360 mobile guards.
```

Clear app cache data
command:
```
adb shell pm clear <packagename>
<Packagename> represents the name of the application package, the effect of this command is equivalent to the application information in the settings screen, click the "Clear Cache" and "Clear data."
Command Example:

adb shell pm clear com.qihoo360.mobilesafe
360 mobile guards to clear the data and cache.
View Reception Activity
command:

adb shell dumpsys activity activities | grep mFocusedActivity
Example output:

mFocusedActivity: ActivityRecord{8079d7e u0 com.cyanogenmod.trebuchet/com.android.launcher3.Launcher t42}
Where com.cyanogenmod.trebuchet / com.android.launcher3.Launcher is currently in the foreground Activity.
View Running Services
command:

adb shell dumpsys activity services [<packagename>]
<packagename> parameter is optional, command with <packagename> will output services related with that packagename, and command without <packagename> will output all services.
Complete packagename is unnecessary. For example, adb shell dumpsys activity services org.mazhuang will output services related with org.mazhuang.demo1, org.mazhuang.demo2 and org.mazhuang123, etc.
Query package detail information
command:

adb shell dumpsys package <packagename>
There are many infos in output, include Activity Resolver Table, Registered ContentProviders, package name, userId, files/resources/codes path after install, version name and code, permissions info and their granted status, signing version, etc.
<packagename> is package name of an application.
Example output:

Activity Resolver Table:
  Non-Data Actions:
      android.intent.action.MAIN:
        5b4cba8 org.mazhuang.guanggoo/.SplashActivity filter 5ec9dcc
          Action: "android.intent.action.MAIN"
          Category: "android.intent.category.LAUNCHER"
          AutoVerify=false
Registered ContentProviders:
  org.mazhuang.guanggoo/com.tencent.bugly.beta.utils.BuglyFileProvider:
    Provider{7a3c394 org.mazhuang.guanggoo/com.tencent.bugly.beta.utils.BuglyFileProvider}
ContentProvider Authorities:
  [org.mazhuang.guanggoo.fileProvider]:
    Provider{7a3c394 org.mazhuang.guanggoo/com.tencent.bugly.beta.utils.BuglyFileProvider}
      applicationInfo=ApplicationInfo{7754242 org.mazhuang.guanggoo}
Key Set Manager:
  [org.mazhuang.guanggoo]
      Signing KeySets: 501
Packages:
  Package [org.mazhuang.guanggoo] (c1d7f):
    userId=10394
    pkg=Package{55f714c org.mazhuang.guanggoo}
    codePath=/data/app/org.mazhuang.guanggoo-2
    resourcePath=/data/app/org.mazhuang.guanggoo-2
    legacyNativeLibraryDir=/data/app/org.mazhuang.guanggoo-2/lib
    primaryCpuAbi=null
    secondaryCpuAbi=null
    versionCode=74 minSdk=15 targetSdk=25
    versionName=1.1.74
    splits=[base]
    apkSigningVersion=2
    applicationInfo=ApplicationInfo{7754242 org.mazhuang.guanggoo}
    flags=[ HAS_CODE ALLOW_CLEAR_USER_DATA ALLOW_BACKUP ]
    privateFlags=[ RESIZEABLE_ACTIVITIES ]
    dataDir=/data/user/0/org.mazhuang.guanggoo
    supportsScreens=[small, medium, large, xlarge, resizeable, anyDensity]
    timeStamp=2017-10-22 23:50:53
    firstInstallTime=2017-10-22 23:50:25
    lastUpdateTime=2017-10-22 23:50:55
    installerPackageName=com.miui.packageinstaller
    signatures=PackageSignatures{af09595 [53c7caa2]}
    installPermissionsFixed=true installStatus=1
    pkgFlags=[ HAS_CODE ALLOW_CLEAR_USER_DATA ALLOW_BACKUP ]
    requested permissions:
      android.permission.READ_PHONE_STATE
      android.permission.INTERNET
      android.permission.ACCESS_NETWORK_STATE
      android.permission.ACCESS_WIFI_STATE
      android.permission.READ_LOGS
      android.permission.WRITE_EXTERNAL_STORAGE
      android.permission.READ_EXTERNAL_STORAGE
    install permissions:
      android.permission.INTERNET: granted=true
      android.permission.ACCESS_NETWORK_STATE: granted=true
      android.permission.ACCESS_WIFI_STATE: granted=true
    User 0: ceDataInode=1155675 installed=true hidden=false suspended=false stopped=true notLaunched=false enabled=0
      gids=[3003]
      runtime permissions:
        android.permission.READ_EXTERNAL_STORAGE: granted=true
        android.permission.READ_PHONE_STATE: granted=true
        android.permission.WRITE_EXTERNAL_STORAGE: granted=true
    User 999: ceDataInode=0 installed=false hidden=false suspended=false stopped=true notLaunched=true enabled=0
      gids=[3003]
      runtime permissions:
Dexopt state:
  [org.mazhuang.guanggoo]
    Instruction Set: arm64
      path: /data/app/org.mazhuang.guanggoo-2/base.apk
      status: /data/app/org.mazhuang.guanggoo-2/oat/arm64/base.odex [compilation_filter=speed-profile, status=kOatUpToDa
      te]
Query application installation path
command:
adb shell pm path <PACKAGE>
Output shows application installation path.
Example output:
adb shell pm path ecarx.weather
package:/data/app/ecarx.weather-1.apk
Interact with Applications
The most used syntax for interacting with applications is :
am <command>
The common commands for <command> are as follow:
Command    Use
start [options] <INTENT>    Start an Activity specified by <INTENT>
startservice [options] <INTENT>    Start the Service specified by <INTENT>
broadcast [options] <INTENT>    Send a broadcast <INTENT>
force-stop <packagename>    Force stop everything associated with <packagename>
The <INTENT> is a flexible parameter which is corresponding to the Intent writing in the application.
The options for <INTENT> are as follows:
Parameter    Meaning
-a <ACTION>    Specify the intent action, such as android.intent.action.VIEW. You can declare this only once.
-c <CATEGORY>    Specify an intent category, such as android.intent.category.APP_CONTACTS
-n <COMPONENT>    Specify the component name with package name prefix to create an explicit intent, such as com.example.app/.ExampleActivity
There are some options addting data for <INTENT>, similar to extra for Bundle:
Parameter    Meaning
--esn <EXTRA_KEY>    null value (only key name)
`-e    --es <EXTRA_KEY> <EXTRA_STRING_VALUE>`
--ez <EXTRA_KEY> <EXTRA_BOOLEAN_VALUE>    boolean value
--ei <EXTRA_KEY> <EXTRA_INT_VALUE>    integer value
--el <EXTRA_KEY> <EXTRA_LONG_VALUE>    long value
--ef <EXTRA_KEY> <EXTRA_FLOAT_VALUE>    float value
--eu <EXTRA_KEY> <EXTRA_URI_VALUE>    URI
--ecn <EXTRA_KEY> <EXTRA_COMPONENT_NAME_VALUE>    component name
--eia <EXTRA_KEY> <EXTRA_INT_VALUE> [, <EXTRA_INT_VALUE ...]    integer array
--ela <EXTRA_KEY> <EXTRA_LONG_VALUE> [, <EXTRA_LONG_VALUE ...]    long array
Launch app / Start an Activity
The syntax is:
adb shell am start [options] <INTENT>
For example:
adb shell am start -n com.tencent.mm/.ui.LauncherUI
The command above means starting the launch activity of WeChat.
adb shell am start -n org.mazhuang.boottimemeasure/.MainActivity --es "toast" "hello, world"
The command above means starting MainActivity of the application with the package name org.mazhuang.boottimemeasure with an extra string information (key is 'toast' and value is 'hello, world').
Start a Service
The syntax is:
adb shell am startservice [options] <INTENT>
For example:
adb shell am startservice -n com.tencent.mm/.plugin.accountsync.model.AccountAuthenticatorService
The command above means starting a service from WeChat.
Another typical useage is that if devices has bottom virtual keys but not show, you can try this:
adb shell am startservice -n com.android.systemui/.SystemUIService
Stop service
The syntax is:
adb shell am stopservice [options] <INTENT>
Send a broadcast
The syntax is:
adb shell am broadcast [options] <INTENT>
Broadcast intent can be sent to all components or a specified component.
For example, the command of issuing a broadcast intent with BOOT_COMPLETED to all of the components is as following:
adb shell am broadcast -a android.intent.action.BOOT_COMPLETED
As another example of issuing a broadcast intent with BOOT_COMPLETED only to org.mazhuang.boottimemeasure / .BootCompletedReceiver is as following:
adb shell am broadcast -a android.intent.action.BOOT_COMPLETED -n org.mazhuang.boottimemeasure/.BootCompletedReceiver
The command of issuing a broadcast intent is very useful in the test, especially when a broatcast intent is hard to generate normally, it would be of great use to send the broadcast intent by the command.
Both system predefined and custom broadcast intent are able to be sent. The following is part of the system predefined broadcast intents and the triggers:
Action    Trigger
android.net.conn.CONNECTIVITY_CHANGE    network connectivity changes
android.intent.action.SCREEN_ON    screen on
android.intent.action.SCREEN_OFF    screen off
android.intent.action.BATTERY_LOW    low battery, corresponding to the "Low battery warning" system dialog
android.intent.action.BATTERY_OKAY    the battery is now okay after being low
android.intent.action.BOOT_COMPLETED    device boot finished
android.intent.action.DEVICE_STORAGE_LOW    low memory condition on the device
android.intent.action.DEVICE_STORAGE_OK    low memory condition on the device no longer exists
android.intent.action.PACKAGE_ADDED    a new application has been installed
android.net.wifi.STATE_CHANGE    WiFi connection status changed
android.net.wifi.WIFI_STATE_CHANGED    Wi-Fi has been enabled, disabled, enabling, disabling, or unknown
android.intent.action.BATTERY_CHANGED    battery level changed
android.intent.action.INPUT_METHOD_CHANGED    system input method changed
android.intent.action.ACTION_POWER_CONNECTED    external power connected to the device
android.intent.action.ACTION_POWER_DISCONNECTED    external power removed from the device
android.intent.action.DREAMING_STARTED    system starts dreaming
android.intent.action.DREAMING_STOPPED    system stops dreaming
android.intent.action.WALLPAPER_CHANGED    wallpaper changeed
android.intent.action.HEADSET_PLUG    wired headset plugged in or unplugged
android.intent.action.MEDIA_UNMOUNTED    external media is present, but not mounted at its mount point
android.intent.action.MEDIA_MOUNTED    external media is present and mounted at its mount point
android.os.action.POWER_SAVE_MODE_CHANGED    power-saving mode changed
(Above broadcast intents are all available to be sent via adb commands)
Force stop an application
The syntax is:
adb shell am force-stop <packagename>
For example:
adb shell am force-stop com.qihoo360.mobilesafe
The command above means stopping all processes and services related to the package name com.qihoo360.mobilesafe.
Trim memory
command:
adb shell am send-trim-memory  <pid> <level>
pid: process id level: HIDDENãRUNNING_MODERATEãBACKGROUNDãRUNNING_LOWãMODERATEãRUNNING_CRITICALãCOMPLETE
For example:
adb shell am send-trim-memory 12345 RUNNING_LOW
means send command to process 12345, notify it to set level to RUNNING.
File Management
Copy files from a device to a computer
command:
adb pull <remote> [local]
remote: file path on device
local: directory on computer
The local parameter is optional, the default value is current directory.
For example:
adb pull /sdcard/sr.mp4 ~/tmp/
Tips: The file from device may be not readable without root permission, you need to make sure your device is rooted and then use adb shell and su commands to gain the root permission in the adb shell environment, after that you can use cp /path/on/device /sdcard/filename to copy the target file from those directories which require root permission to a public directory, and finaly you can use adb pull /sdcard/filename /path/on/pc normally as mentioned above after exiting the adb shell environment.
Copy files from a computer to a device
command:
adb push <local> <remote>
local: file path on computer
remote: directory on device
For example:
adb push ~/sr.mp4 /sdcard/
Tips: The directory on device may be not writable without root permission, you need to make sure your device is rooted and then use adb push /path/on/pc /sdcard/filename firstly, and use adb shell and su to gain the root permission in the adb shell environment, and finaly use cp /sdcard/filename /path/on/device to copy the file to the target directory.
Analog Keys / inputs
In adb shell there is a very useful command called input, through which you can do some interesting things.
Complete help information input command is as follows:
Usage: input [<source>] <command> [<arg>...]
The sources are:
      mouse
      keyboard
      joystick
      touchnavigation
      touchpad
      trackball
      stylus
      dpad
      gesture
      touchscreen
      gamepad
The commands and default sources are:
      text <string> (Default: touchscreen)
      keyevent [--longpress] <key code number or name> ... (Default: keyboard)
      tap <x> <y> (Default: touchscreen)
      swipe <x1> <y1> <x2> <y2> [duration(ms)] (Default: touchscreen)
      press (Default: trackball)
      roll <dx> <dy> (Default: trackball)
Such as using adb shell input keyevent <keycode> command, different keycode to achieve different functions, keycode complete list see KeyEvent, I think the interesting part of the quote is as follows:
Keycode    Meaning
3    HOME button
4    return key
5    open dialing application
6    hang up
24    increase volume
25    Volume Down
26    Power button
27    taking pictures (in the camera application needs in)
64    Open Browser
82    menu button
85    Play / Pause
86    stop playing
87    play the next
88    played on a
122    Move the cursor to the beginning or top of the list
123    Move the cursor to the end of the line or bottom of the list
126    resume playing
127    pause play
164    Mute
176    Open the System Setup
187    switching applications
207    Open Contacts
208    Open calendar
209    Open Music
210    Open Calculator
220    Decrease screen brightness
221    Increase screen brightness
223    System Sleep
224    light up the screen
231    Open the voice assistant
276    If no wakelock allow the system to sleep
Here are some examples of the use of input command.
Power button
command:
adb shell input keyevent 26
Executive effect equivalent to pressing the power button.
menu
command:
adb shell input keyevent 82
HOME key
command:
adb shell input keyevent 3
return key
command:
adb shell input keyevent 4
volume control
Increase the volume:
adb shell input keyevent 24
lower the volume:
adb shell input keyevent 25
Mute:
adb shell input keyevent 164
Media Control
play / Pause:
adb shell input keyevent 85
Stop play:
adb shell input keyevent 86
Play the next song:
adb shell input keyevent 87
Played on one:
adb shell input keyevent 88
Resume playback:
adb shell input keyevent 126
Pause playback:
adb shell input keyevent 127
On / Off screen
It can be switched on and off by telling off the screen above the analog power button, but if you want to light up or clear off the screen, then you can use the following method.
Light up the screen:
adb shell input keyevent 224
Off screen:
adb shell input keyevent 223
Slide to unlock
If no password lock screen is unlocked by sliding gestures, so you can input swipe to unlock.
Command (parameter models Nexus 5, swipe up to unlock, for example):
adb shell input swipe 300 1000 300 500
3001000300 parameters represent 500` starting x coordinate of the start point y coordinate of the end point x coordinate y coordinate of the end point '.
Enter text
When the focus is in a text box, you can enter text by input command.
command:
adb shell input text hello
Hello now appear in the text box.
View Log
Log Android system is divided into two parts, the underlying Linux kernel log output to / proc / kmsg, Android's log output to / dev / log.
Android log
Format:
[adb] logcat [<option>] ... [<filter-spec>] ...
Common usage are listed below:
Filter the log by level
Android log divided into the following levels:
V - Verbose (lowest output most)
D - Debug
I - Info
W - Warning
E - Error
F - Fatal
S - Silent (highest, what is not output)
Press a grade level and above filter log is the log output.
For example, the command:
adb logcat *:W
Will Warning, Error, Fatal and Silent log output.
(Notice: tag * must surrounded with double quotation, like adb logcat "*:W", otherwise an error no matches found *:W would throws.)
Filter by tag and log level
filterspecs are a series of <tag>[:priority].
For example, the command:
adb logcat ActivityManager:I MyApp:D *:S
Represents an output tag ActivityManager above the level of Info logs, Debug log output above the level of the tag MyApp, and other tag Silent level of log (ie, shield other tag logging).
Log format
You can use adb logcat -v <format> option specifies log output format.
Log supported by the following <format>:
brief
The default format. The format is:
<priority>/<tag>(<pid>): <message>
Example:
D/HeadsetStateMachine( 1785): Disconnected process message: 10, size: 0
process
The format is:
<priority>(<pid>) <message>
Example:
D( 1785) Disconnected process message: 10, size: 0  (HeadsetStateMachine)
tag
The format is:
<priority>/<tag>: <message>
Example:
D/HeadsetStateMachine: Disconnected process message: 10, size: 0
raw
The format is:
<message>
Example:
Disconnected process message: 10, size: 0
time
The format is:
<datetime> <priority>/<tag>(<pid>): <message>
Example:
08-28 22:39:39.974 D/HeadsetStateMachine( 1785): Disconnected process message: 10, size: 0
threadtime
The format is:
<datetime> <pid> <tid> <priority> <tag>: <message>
Example:
08-28 22:39:39.974  1785  1832 D HeadsetStateMachine: Disconnected process message: 10, size: 0
long
The format is:
[ <datetime> <pid>:<tid> <priority>/<tag> ]
<message>
Example:
[ 08-28 22:39:39.974  1785: 1832 D/HeadsetStateMachine ]
Disconnected process message: 10, size: 0
Specified format can be used simultaneously with the above filter. such as:
adb logcat -v long ActivityManager:I *:S
Clear log
adb logcat -c
Kernel log
command:
adb shell dmesg
Example output:
<6>[14201.684016] PM: noirq resume of devices complete after 0.982 msecs
<6>[14201.685525] PM: early resume of devices complete after 0.838 msecs
<6>[14201.753642] PM: resume of devices complete after 68.106 msecs
<4>[14201.755954] Restarting tasks ... done.
<6>[14201.771229] PM: suspend exit 2016-08-28 13:31:32.679217193 UTC
<6>[14201.872373] PM: suspend entry 2016-08-28 13:31:32.780363596 UTC
<6>[14201.872498] PM: Syncing filesystems ... done.
In brackets [14201.684016] time represents the core begins to start in seconds.
By kernel log, we can do some things, such as a measure of the kernel boot time, Freeing init memory find that time is in front of the line after system startup, the kernel log.
View device information
Model
Command:
adb shell getprop ro.product.model
Sample output:
Nexus 5
Battery Status
Command:
adb shell dumpsys battery
Sample output:
Current Battery Service state:
  AC powered: false
  USB powered: true
  Wireless powered: false
  status: 2
  health: 2
  present: true
  level: 44
  scale: 100
  voltage: 3872
  temperature: 280
  technology: Li-poly
Scale means the maximum value of level, and level means the current battery level. The output above means there is 44% of battery left of the device.
Screen Resolution
Command:
adb shell wm size
Sample output:
Physical size: 1080x1920
The above output means the device's screen resolution is 1080px * 1920px.
If resolution has been changed by command, the output would be like this:
Physical size: 1080x1920
Override size: 480x1024
It means the original resolution of the screen is 1080px * 1920px, and currently it is 480px * 1024px.
Screen density
Command:
adb shell wm density
Sample output:
Physical density: 420
The output shows the density of the device is 420dpi.
If screen density has been changed by command, the output would be like this:
Physical density: 480
Override density: 160
It means the original density of the screen is 480dpi, and currently it is 160dpi.
Display Parameters
Command:
adb shell dumpsys window displays
Sample output:
WINDOW MANAGER DISPLAY CONTENTS (dumpsys window displays)
  Display: mDisplayId=0
    init=1080x1920 420dpi cur=1080x1920 app=1080x1794 rng=1080x1017-1810x1731
    deferred=false layoutNeeded=false
The mDisplayId stands for the number of the display screen, init shows the initial resolution and density of the screen, the height in app is smaller than that in init, which means the device has a virtual navigation bar with a height: 1920 - 1794 = 126px (42dp).
android_id
Command:
adb shell settings get secure android_id
Sample output:
51b6be48bac8c569
IMEI
For Android 4.4 and the belows, the IMEI viewing command is like this:
adb  shell  dumpsys  iphonesubinfo
Sample output:
Phone Subscriber Info:
  Phone Type = GSM
  Device ID = 860955027785041
Device ID stands for IMEI.
For Android 5.0 and the aboves, the command used to view IMEI above is not working which always comes out nothing, the alternative is like this(requires root privileges):
adb shell
su
service call iphonesubinfo 1
Sample output:
Result: Parcel(
  0x00000000: 00000000 0000000f 00360038 00390030 '........8.6.0.9.'
  0x00000010: 00350035 00320030 00370037 00350038 '5.5.0.2.7.7.8.5.'
  0x00000020: 00340030 00000031                   '0.4.1...        ')
After extracting the data the normal IMEI will show, such as the IMEI above is 860955027785041.
Android system version
Command:
adb shell getprop ro.build.version.release
Sample output:
5.0.2
IP address
Are you getting bored for pressing "Setting" - "About phone" - "state information" - "IP address" to get the IP address of the device? You can make it easily via adb command:
Command:
adb shell ifconfig | grep Mask
Sample output:
inet addr:10.130.245.230  Mask:255.255.255.252
inet addr:127.0.0.1  Mask:255.0.0.0
The IP address of the device is 10.130.245.230.
The above command may result in an empty result on some devices if they are connected via WIFI, then you can use the following command to view the LAN IP:
adb shell ifconfig wlan0
Sample output:
wlan0: ip 10.129.160.99 mask 255.255.240.0 flags [up broadcast running multicast]
or
wlan0     Link encap:UNSPEC
          inet addr:10.129.168.57  Bcast:10.129.175.255  Mask:255.255.240.0
          inet6 addr: fe80::66cc:2eff:fe68:b6b6/64 Scope: Link
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:496520 errors:0 dropped:0 overruns:0 frame:0
          TX packets:68215 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:3000
          RX bytes:116266821 TX bytes:8311736
If the two commands above still don't get the desired information, then you can try the following command (available in some system):
adb shell netcfg
Sample output:
wlan0    UP                               10.129.160.99/20  0x00001043 f8:a9:d0:17:42:4d
lo       UP                                   127.0.0.1/8   0x00000049 00:00:00:00:00:00
p2p0     UP                                     0.0.0.0/0   0x00001003 fa:a9:d0:17:42:4d
sit0     DOWN                                   0.0.0.0/0   0x00000080 00:00:00:00:00:00
rmnet0   DOWN                                   0.0.0.0/0   0x00000000 00:00:00:00:00:00
rmnet1   DOWN                                   0.0.0.0/0   0x00000000 00:00:00:00:00:00
rmnet3   DOWN                                   0.0.0.0/0   0x00000000 00:00:00:00:00:00
rmnet2   DOWN                                   0.0.0.0/0   0x00000000 00:00:00:00:00:00
rmnet4   DOWN                                   0.0.0.0/0   0x00000000 00:00:00:00:00:00
rmnet6   DOWN                                   0.0.0.0/0   0x00000000 00:00:00:00:00:00
rmnet5   DOWN                                   0.0.0.0/0   0x00000000 00:00:00:00:00:00
rmnet7   DOWN                                   0.0.0.0/0   0x00000000 00:00:00:00:00:00
rev_rmnet3 DOWN                                   0.0.0.0/0   0x00001002 4e:b7:e4:2e:17:58
rev_rmnet2 DOWN                                   0.0.0.0/0   0x00001002 4e:f0:c8:bf:7a:cf
rev_rmnet4 DOWN                                   0.0.0.0/0   0x00001002 a6:c0:3b:6b:c4:1f
rev_rmnet6 DOWN                                   0.0.0.0/0   0x00001002 66:bb:5d:64:2e:e9
rev_rmnet5 DOWN                                   0.0.0.0/0   0x00001002 0e:1b:eb:b9:23:a0
rev_rmnet7 DOWN                                   0.0.0.0/0   0x00001002 7a:d9:f6:81:40:5a
rev_rmnet8 DOWN                                   0.0.0.0/0   0x00001002 4e:e2:a9:bb:d0:1b
rev_rmnet0 DOWN                                   0.0.0.0/0   0x00001002 fe:65:d0:ca:82:a9
rev_rmnet1 DOWN                                   0.0.0.0/0   0x00001002 da:d8:e8:4f:2e:fe
It shows the network connection name, connection enable status, IP address, Mac address and etc.
Mac Address
Command:
adb shell cat /sys/class/net/wlan0/address
Sample output:
f8:a9:d0:17:42:4d
The output above is the Mac address of LAN, if you want other infomation of connection, the command adb shell netcfg mentioned in the section IP address would be helpful.
CPU Information
Command:
adb shell cat /proc/cpuinfo
Sample output:
Processor       : ARMv7 Processor rev 0 (v7l)
processor       : 0
BogoMIPS        : 38.40
processor       : 1
BogoMIPS        : 38.40
processor       : 2
BogoMIPS        : 38.40
processor       : 3
BogoMIPS        : 38.40
Features        : swp half thumb fastmult vfp edsp neon vfpv3 tls vfpv4 idiva idivt
CPU implementer : 0x51
CPU architecture: 7
CPU variant     : 0x2
CPU part        : 0x06f
CPU revision    : 0
Hardware        : Qualcomm MSM 8974 HAMMERHEAD (Flattened Device Tree)
Revision        : 000b
Serial          : 0000000000000000
This is the CPU information of Nexus 5, we can find from the output that the hardware is Qualcomm MSM 8974, and the processor number is from 0 to 3, which means the cpu is a quad-core, then from the Processor we can find the architecture of the cpu isARMv7 Processor rev 0 ( v71).
Memory Information
Command:
adb shell cat /proc/meminfo
Sample output:
MemTotal:        1027424 kB
MemFree:          486564 kB
Buffers:           15224 kB
Cached:            72464 kB
SwapCached:        24152 kB
Active:           110572 kB
Inactive:         259060 kB
Active(anon):      79176 kB
Inactive(anon):   207736 kB
Active(file):      31396 kB
Inactive(file):    51324 kB
Unevictable:        3948 kB
Mlocked:               0 kB
HighTotal:        409600 kB
HighFree:         132612 kB
LowTotal:         617824 kB
LowFree:          353952 kB
SwapTotal:        262140 kB
SwapFree:         207572 kB
Dirty:                 0 kB
Writeback:             0 kB
AnonPages:        265324 kB
Mapped:            47072 kB
Shmem:              1020 kB
Slab:              57372 kB
SReclaimable:       7692 kB
SUnreclaim:        49680 kB
KernelStack:        4512 kB
PageTables:         5912 kB
NFS_Unstable:          0 kB
Bounce:                0 kB
WritebackTmp:          0 kB
CommitLimit:      775852 kB
Committed_AS:   13520632 kB
VmallocTotal:     385024 kB
VmallocUsed:       61004 kB
VmallocChunk:     209668 kB
MemTotal means the total memory of the device, and MemFree means the current free memory.
More hardware and system properties
More hardware devices and system properties can be obtained by the following command:
adb shell cat /system/build.prop
This will output a lot of information, including "model" and "Android system version" and other infomation which are mentioned in previous several sections.
In output also includes some other useful information, which can also be obtained individually via the command adb shell getprop <attribute name>:
Attribute name    Meaning
ro.build.version.sdk    SDK version
ro.build.version.release    Android system version
ro.build.version.security_patch    Android security patch level
ro.product.model    Type
ro.product.brand    Brands
ro.product.name    device name
ro.product.board    Processor Model
ro.product.cpu.abilist    CPU supported abi list[Ref 1]
persist.sys.isUsbOtgEnabled    OTG supports
dalvik.vm.heapsize    limit on heap size for each app
ro.sf.lcd_density    screen density
Ref 1: The property of abi list may be changed in some custom ROMs, if it can't be obtained via ro.product.cpu.abilist, you can try this command:
adb shell cat /system/build.prop | grep ro.product.cpu.abi
Sample output:
ro.product.cpu.abi=armeabi-v7a
ro.product.cpu.abi2=armeabi
Modify Settings
Notice: Display may not normal after reset settings, you can use command adb reboot to reboot device, or reboot it maually.
Resolution
command:
adb shell wm size 480x1024
It means change the resolution to 480px * 1024px.
Reset to original resolution:
adb shell wm size reset
Screen density
command:
adb shell wm density 160
It means change the screen density to 160dpi.
Reset to original screen density:
adb shell wm density reset
Overscan
command:
adb shell wm overscan 0,0,0,200
Four parameters are left, top, right and bottom margin pixels to the edge, command above means leave 200px in screen bottom clean.
Reset to original overscan:
adb shell wm overscan reset
Turn off Android Debug
command:
adb shell settings put global adb_enabled 0
To reset:
We can't do this via command now, because without "Android Debug" on, adb cannot communicate with Devices.
So just do it on device manually:
"Settings" - "Developer options" - "Android Debug".
allow/forbidden access non SDK API
allow access non SDK API:
adb shell settings put global hidden_api_policy_pre_p_apps 1
adb shell settings put global hidden_api_policy_p_apps 1
forbidden access non SDK API:
adb shell settings delete global hidden_api_policy_pre_p_apps
adb shell settings delete global hidden_api_policy_p_apps
Note: Commands above don't need root privileges.
meaning for number in command tail:
value    meaning
0    disable detect for non SDK API call. In this situation, there is no call log in logcat, and make strict mode API, detectNonSdkApiUsage() invalid. Not recommended.
1    Just warning -- allow access all non SDK API, but retain warning in logcat. You can continue to use strick mode API.
2    It is forbidden to invoke interfaces in dark grey lists and black lists.
3    It is forbidden to invoke the interface in the black list, but it is allowed to call the interface in the dark grey list.
Show/hide status bar or navigation bar
Settings in this section correspond with "Expanded desktop" in Cyanogenmod.
command:
adb shell settings put global policy_control <key-values>
<key-values> composite by keys and their values below, format is <key1>=<value1>:<key2>=<value2>.
key    meaning
immersive.full    Hide both
immersive.status    Hide status bar
immersive.navigation    Hide navigation bar
immersive.preconfirms    ?
Values for these keys are comma-delimited list of tokens, where tokens:
value    å«ä¹
apps    All applications
*    Everywhere
packagename    Include package
-packagename    Exclude package
For example:
adb shell settings put global policy_control immersive.full=*
Means set hide both status bar and navigation bar everywhere.
adb shell settings put global policy_control immersive.status=com.package1,com.package2:immersive.navigation=apps,-com.package3
Means set hide status bar in applications whoes package name is com.package1 or com.package2, hide navigation bar in all applications, exclude whoes package name is com.package3.
Utility functions
Screenshots
Take screenshot and save to computer:
adb exec-out screencap -p > sc.png
If your adb is old version, doesn't have exec-out command, then your can take screenshot like below:
First, take screenshot and save to device:
adb shell screencap -p /sdcard/sc.png
And then export the png file to your computer:
adb pull /sdcard/sc.png
You can use the adb shell screencap -h See help screencap command, here are two significant parameters and their meanings:
Parameter    Meaning
-p    Save the file in png format specified
-d Display-id    screenshots display the specified number (multiple screen display case next)
Found If you specify a file name can be omitted when the -p parameter to .png ending; otherwise you need to use the -p parameter. If you do not specify a file name, file contents screenshot will be directly output to stdout.
Another method to save screenshot file to computer with a single line command:
adb shell screencap -p | sed "s/\r$//" > sc.png
This depends on sed command, it's avaliable in Linux and Mac OS X by default. In Windows, you may find it in bin directory in Git installation place. Otherwise, you may need to download sed for Windows and add the directory where sed.exe is to PATH environment variable.
Recording Screen
Record screen are saved in mp4 format to / sdcard:
adb shell screenrecord /sdcard/filename.mp4
When you need to stop press Ctrl-C </ kbd>, the default recording time and maximum recording time is 180 seconds.
If you need to export to your computer:
adb pull /sdcard/filename.mp4
You can use the adb shell screenrecord --help See help screenrecord command, the following are common parameters and their meanings:
Parameter    Meaning
--size WIDTHxHEIGHT    dimensions of the video, such as 1280x720, default screen resolution.
--bit-Rate RATE    bit-rate video, the default is 4Mbps.
--time-Limit TIME    recording length, in seconds.
--verbose    Print more information.
Remount system partition as writable
Note: You need root privileges.
/system partitions are mounted read-only, but some operating systems such as Android to add commands to remove the need to bring their own application / system write operation, it is necessary to remount it read-write.
step:
Enter the shell and switch to the root user privileges.
command:
adb shell
su
View the current partition mounted case.
command:
mount
Example output:
rootfs / rootfs ro,relatime 0 0
tmpfs /dev tmpfs rw,seclabel,nosuid,relatime,mode=755 0 0
devpts /dev/pts devpts rw,seclabel,relatime,mode=600 0 0
proc /proc proc rw,relatime 0 0
sysfs /sys sysfs rw,seclabel,relatime 0 0
selinuxfs /sys/fs/selinux selinuxfs rw,relatime 0 0
debugfs /sys/kernel/debug debugfs rw,relatime 0 0
none /var tmpfs rw,seclabel,relatime,mode=770,gid=1000 0 0
none /acct cgroup rw,relatime,cpuacct 0 0
none /sys/fs/cgroup tmpfs rw,seclabel,relatime,mode=750,gid=1000 0 0
none /sys/fs/cgroup/memory cgroup rw,relatime,memory 0 0
tmpfs /mnt/asec tmpfs rw,seclabel,relatime,mode=755,gid=1000 0 0
tmpfs /mnt/obb tmpfs rw,seclabel,relatime,mode=755,gid=1000 0 0
none /dev/memcg cgroup rw,relatime,memory 0 0
none /dev/cpuctl cgroup rw,relatime,cpu 0 0
none /sys/fs/cgroup tmpfs rw,seclabel,relatime,mode=750,gid=1000 0 0
none /sys/fs/cgroup/memory cgroup rw,relatime,memory 0 0
none /sys/fs/cgroup/freezer cgroup rw,relatime,freezer 0 0
/dev/block/platform/msm_sdcc.1/by-name/system /system ext4 ro,seclabel,relatime,data=ordered 0 0
/dev/block/platform/msm_sdcc.1/by-name/userdata /data ext4 rw,seclabel,nosuid,nodev,relatime,noauto_da_alloc,data=ordered 0 0
/dev/block/platform/msm_sdcc.1/by-name/cache /cache ext4 rw,seclabel,nosuid,nodev,relatime,data=ordered 0 0
/dev/block/platform/msm_sdcc.1/by-name/persist /persist ext4 rw,seclabel,nosuid,nodev,relatime,data=ordered 0 0
/dev/block/platform/msm_sdcc.1/by-name/modem /firmware vfat ro,context=u:object_r:firmware_file:s0,relatime,uid=1000,gid=1000,fmask=0337,dmask=0227,codepage=cp437,iocharset=iso8859-1,shortname=lower,errors=remount-ro 0 0
/dev/fuse /mnt/shell/emulated fuse rw,nosuid,nodev,relatime,user_id=1023,group_id=1023,default_permissions,allow_other 0 0
/dev/fuse /mnt/shell/emulated/0 fuse rw,nosuid,nodev,relatime,user_id=1023,group_id=1023,default_permissions,allow_other 0 0
Find one of our concerns with the / system of the line:
/dev/block/platform/msm_sdcc.1/by-name/system /system ext4 ro,seclabel,relatime,data=ordered 0 0
remount.
command:
mount -o remount,rw -t yaffs2 /dev/block/platform/msm_sdcc.1/by-name/system /system
Here / dev / block / platform / msm_sdcc.1 / by-name / system is we get the file path from the output in the previous step.
If the output is not an error, then the operation is successful, you can file / system under wanted.
Check connection over WiFi password
Note: You need root privileges.
command:
adb shell
su
cat /data/misc/wifi/*.conf
Example output:
network={
    ssid="TP-LINK_9DFC"
    scan_ssid=1
    psk="123456789"
    key_mgmt=WPA-PSK
    group=CCMP TKIP
    auth_alg=OPEN
    sim_num=1
    priority=13893
}
network={
    ssid="TP-LINK_F11E"
    psk="987654321"
    key_mgmt=WPA-PSK
    sim_num=1
    priority=17293
}
Ssid we shall see in the WLAN settings in the name, psk the password, key_mgmt security encryption.
To set the system date and time
** Note: You need root privileges. **
command:
adb shell
su
date -s 20160823.131500
It said it would change the system date and time at 13:15:00 on August 23, 2016.
restart cellphone
command:
adb reboot
Detect whether the device is root
command:
adb shell
su
In this case the command line prompt is $ indicates no root privileges, is the # indicates root.
Monkey use stress testing
Monkey can generate pseudo-random event to simulate a user click, touch, gesture and other operations, you can program being developed random stress test.
Usage is simple:
adb shell monkey -p <packagename> -v 500
He told <packagename> specific application to send 500 pseudo-random events.
Monkey in detail with reference to the use of official document.
On / off WiFi
** Note: You need root privileges. **
Sometimes the need to control the device WiFi mode, you can use the following command to complete.
Open WiFi:
adb root
adb shell svc wifi enable
Close WiFi:
adb root
adb shell svc wifi disable
If successfully implemented, the output is empty; if not get root privileges to execute this command will fail, output Killed.
Flashing-Phone related commands
Restart to Recovery mode
command:
adb reboot recovery
To restart from the Recovery Android
command:
adb reboot
Restart to Fastboot mode
command:
adb reboot bootloader
Through sideload system update
If we downloaded the Android system update package corresponds to the device to your computer, you can also adb to complete the update.
Case in Recovery Mode Update:
Restart to Recovery mode.
command:
adb reboot recovery
Recovery operations on the interface device into the Apply update-Apply from ADB.
Note: Different Recovery menu may differ from this, there is some level menu Apply update from ADB.
adb upload and update the system.
command:
adb sideload <path-to-update.zip>
Security-related commands
Enable / Disable SELinux
Enable SELinux
adb root
adb shell setenforce 1
Disable SELinux
adb root
adb shell setenforce 0
Enable / Disable dm_verity
Enable dm_verity
adb root
adb enable-verity
Disable dm_verity
adb root
adb disable-verity
More adb shell command
Android system is based on Linux kernel, so Linux where many commands in Android also has the same or similar implement, in adb shell where you can call. Part earlier in this document have been used in the adb shell command.
See process
command:
adb shell ps
Example output:
USER     PID   PPID  VSIZE  RSS     WCHAN    PC        NAME
root      1     0     8904   788   ffffffff 00000000 S /init
root      2     0     0      0     ffffffff 00000000 S kthreadd
...
u0_a71    7779  5926  1538748 48896 ffffffff 00000000 S com.sohu.inputmethod.sogou:classic
u0_a58    7963  5926  1561916 59568 ffffffff 00000000 S org.mazhuang.boottimemeasure
...
shell     8750  217   10640  740   00000000 b6f28340 R ps
Meaning of each column:
Listing    Meaning
USER    their user
PID    Process ID
PPID    parent process ID
NAME    process name
View real-time resource consumption
command:
adb shell top
Example output:
User 0%, System 6%, IOW 0%, IRQ 0%
User 3 + Nice 0 + Sys 21 + Idle 280 + IOW 0 + IRQ 0 + SIRQ 3 = 307
  PID PR CPU% S  #THR     VSS     RSS PCY UID      Name
 8763  0   3% R     1  10640K   1064K  fg shell    top
  131  0   3% S     1      0K      0K  fg root     dhd_dpc
 6144  0   0% S   115 1682004K 115916K  fg system   system_server
  132  0   0% S     1      0K      0K  fg root     dhd_rxf
 1731  0   0% S     6  20288K    788K  fg root     /system/bin/mpdecision
  217  0   0% S     6  18008K    356K  fg shell    /sbin/adbd
 ...
 7779  2   0% S    19 1538748K  48896K  bg u0_a71   com.sohu.inputmethod.sogou:classic
 7963  0   0% S    18 1561916K  59568K  fg u0_a58   org.mazhuang.boottimemeasure
 ...
Meaning of each column:
Listing    Meaning
PID    Process ID
PR    Priority
CPU%    instantaneous current occupancy percentage of CPU
S    process state (R = run, S = sleep, T = trace / stop, Z = zombie process)
#THR    Threads
VSS    Virtual Set Size of virtual memory consumption (including shared libraries occupy memory)
RSS    Resident Set Size actual physical memory (including shared libraries occupy memory)
PCY    scheduling policy priority, SP_BACKGROUND / SPFOREGROUND
UID    process owner user ID
NAME    process name
Top command also supports a number of command-line parameters, detailed usage is as follows:
Usage: top [ -m max_procs ] [ -n iterations ] [ -d delay ] [ -s sort_column ] [ -t ] [ -h ]
    -m num  How many processes displays up
    -n num refresh how many times
    -d num refresh interval (in seconds, default value of 5)
    -s col sorted by a column (available col value: cpu, vss, rss, thr)
    -t display thread information
    -h displays help documentation
query process uid
There are two methods:
adb shell dumpsys package <packagename> | grep userId=
For example:
$ adb shell dumpsys package org.mazhuang.guanggoo | grep userId=
   userId=10394
Get pid by ps first, then adb shell cat /proc/<pid>/status | grep Uid
For example:
$ adb shell
gemini:/ $ ps | grep org.mazhuang.guanggoo
u0_a394   28635 770   1795812 78736 SyS_epoll_ 0000000000 S org.mazhuang.guanggoo
gemini:/ $ cat /proc/28635/status | grep Uid
Uid:    10394   10394   10394   10394
gemini:/ $
Other
The following is a brief description of other commonly used commands, has previously spoken commands no special additional explanation:
Command    function
cat    display file contents
cd    change directory
chmod    change file access mode / access
df    view disk space usage
grep    output filter
kill    kill the specified process PID
ls    list directory contents
mount    Mount View and manage directory
mv    move or rename a file
ps    view running processes
rm    delete files
top    Check process resource consumption
common problem
Start adb server failure
Error message
error: protocol fault (couldn't read status): No error
Possible Causes
adb server process wants to use 5037 port is occupied.
solution
Found consumes process 5037 port, and then terminate it. In Windows, for example:
netstat -ano | findstr LISTENING
...
TCP    0.0.0.0:5037           0.0.0.0:0              LISTENING       1548
...
1548 Here is the process ID, the process ends with the command:
taskkill /PID 1548
Then start adb no problem.
com.android.ddmlib.AdbCommandRejectedException
Create a new emulator in Android Studio, but cannot connect with adb, output is:
com.android.ddmlib.AdbCommandRejectedException: device unauthorized.
This adb server's $ADB_VENDOR_KEYS is not set
Try 'adb kill-server' if that seems wrong.
Otherwise check for a confirmation dialog on your device.
After install a terminal app in emulator and run su command, it shows no su program, that is not normal.
So just delete the emulator and re-download, reinstall, all is well now.
Acknowledgements
Thanks friends for theirs selfless sharing and supplement. Names listed in no particular order.
