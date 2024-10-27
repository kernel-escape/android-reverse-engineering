# Reversing Android `0x00`

Hello all! I'm Hai Nguyen, and today I'll post my very first reversing Android tutorial. In this blog, I'll write about the preparation of setup tools related to Android.

## Setup (Windows)

First, you need to install these things:
* [Android Studio](https://developer.android.com/studio)
* `frida-tools` (`pip install frida-tools`)

### Android Installation

* In Android Studio installation, you just follow the setup wizard and install any recommended SDK packages.
* After finishing the installation, you should go to `Virtual Device Manager` and create a new device.
* In the `Select Hardware` window, you can choose your device as you want: in that case, you should choose the smallest size of device to display all the screens easily.
* Then click `Next` to go to the `System Image` window. You **must** select a device that supports root permission. I prefer to select `Google APIs` for the new device, and it will support root permission.
* Note: You should look at the `Play Store` column and select a device with no `Play Store` icon, that device should have `Google APIs`. Click on the `Next` button to verify your new device and finish the installation.

### Frida Server Setup

* First, you should set the environment path for `adb.exe` in system variables (make sure file `adb.exe` is located in the `platform-tools` folder).
* Download the latest [`frida-server`](https://github.com/frida/frida/releases) on this GitHub release.
* Note that you have to select a `frida-server` that matches your device architecture. The format is the following: `frida-server-xx.xx.xx-android-your_arch.xz`
* Then make sure your version of `frida-server` is the same as your `frida-tools`: `frida --version`
* If you were successful in the previous step, you can start your Android emulator and try this command to see your connected devices: `adb devices`
* Next, type `adb root` to promote your current permission to root. If it does not show anything, it means your `adb` has been run with root.
* Then use the commands below:

```
$ adb push <frida-server-file-path> /data/local/tmp
$ adb shell "chmod 755 /data/local/tmp/frida-server"
$ adb shell "/data/local/tmp/frida-server &"
```

* Now you can verify the `frida-server` file is running by using this command in another terminal: `adb shell "ps -A | grep frida"`
* You should see your `frida-server` running as root. So that is the final step in setting up `frida-server` in your Android emulator. Thanks for reading!