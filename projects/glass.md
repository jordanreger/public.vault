A guide on how to get started with Google Glass in 202X.

## Installing XE24
This is a bit confusing as the instructions have changed over the years, and practically every revision recently doesn't really work. The instructions on [this page](https://support.google.com/glass/answer/9649198?hl=en) are a great starter, but some things don’t work. Here’s a (hopefully) decent walkthrough.

## Android Studio + Google USB Driver
1. Make sure to have Android Studio installed
2. In the `tools` menu of Studio, go to the SDK manager and select the **SDK Tools** tab.
3. Select the checkbox next to **Google USB Driver** and then click **Apply** and finally **OK**.
4. Reboot the computer to make sure that it's installed.

## Allow Unsigned Drivers
This will allow us to temporarily disable driver signature enforcement. This only works in Windows.
1. Click the **Start** button, hold `Shift` and click `Restart`
2. Once it reboots, go to **Troubleshoot > Advanced options > Startup settings > Restart**
3. Press `F7` to disable driver signature enforcement
4. Open CMD as an administrator
5. Type `bcdedit /set testsigning on` and press **Enter**

## Editing the Driver
I would recommend following [this tutorial](https://jeffzzq.medium.com/using-google-glass-in-2020-5f0a01188e6e) for the rest of the process.

> [!FAQ]
> You must edit the driver in *both* regular mode and fastboot; otherwise `adb` will not recognize the device.

## Successful Installation of XE24
Now that you've successfully installed the final update, here's a couple things I wish I knew while I was getting started.

## Entering Fastboot
To enter fastboot, you must enter Recovery Mode by holding down the **camera button**, tapping the **power button** *once*, and then continuing to hold down the **camera button** for 10 seconds. Once you do this, you will see a menu with 4 options, but we want to choose **Reboot into fastboot**.

## Copying Files via ADB
To copy files from your Glass to your computer via `adb`, you're going to need two terminal windows. One will run `adb shell` and then `cd sdcard` and the other will run `cd { /Downloads or wherever you want your files }`  and then `adb pull { file name } . `; Make sure to add the dot at the end to pull the file to the current directory.

## Listing All Installed Packages
The below script will allow you to see all user-installed packages, in case you want to uninstall one:

```sh
pm list packages -3|cut -f 2 -d ":"
```

## Development
Go to the page about [Glassware development](/projects/glassware).