Exo is a lightweight background service bundled with a nice modern Windows UI, that will manage the features of your devices without sacrificing your memory or CPU.

With Exo, you can get rid of many inefficient apps on your computer, and reduce the RAM and CPU consumption.

You can check the [Supported Devices](devices.md) page to see if your device(s) are supported.

Download a [recent build](https://github.com/hexawyz/Exo/actions), or [a release](https://github.com/hexawyz/Exo/releases) on GitHub.

# Prerequisites

* [.NET 8.0.8 runtime](https://dotnet.microsoft.com/en-us/download/dotnet/8.0)
* [Windows App SDK 1.6 Runtime](https://aka.ms/windowsappsdk/1.6/1.6.240829007/windowsappruntimeinstall-x64.exe)

# Features

## Quick Battery Summary on the Home Page

![Screenshot of the Home Page](images/Screenshot-Exo-Home.png)

Something that you may miss is the ability to quickly check the battery state of your devices.
Exo provides that on its home page, so that this is the first thing you see when opening the app.

## Notifications

Overlay notifications will be shown for changes in your devices, for devices supporting it.

<img alt="Screenshot of a Battery Charging notification" src="images/Screenshot-Exo-Notification-BatteryCharging.png" width="150" />
<img alt="Screenshot of a Caps Lock notification" src="images/Screenshot-Exo-Notification-CapsLock.png" width="150" />
<img alt="Screenshot of a Keyboard Backlighting Up notification" src="images/Screenshot-Exo-Notification-KeyboardBacklighting.png" width="150" />
<img alt="Screenshot of a Mouse DPI Up notification" src="images/Screenshot-Exo-Notification-MouseDpi.png" width="150" />

Shown above are examples of the notifications that Exo can show.

## List of recognized devices

![Screenshot of the Devices Page](images/Screenshot-Exo-Devices.png)

On this page, you will quickly know which devices are currently recognized by Exo, and which ones are currently connected.

It will allow you to access device-specific informations and settings.

## Wireless USB dongles support

When you connect one or more device through a custom USB dongle, such as Logitech and Razer ones, Windows won't be able to tell what devices are behing the Dongle.

The ability to see which real devices are connected through a dongle is a very important one for proper support of your devices, and Windows cannot do this out of the box.

## Identify devices by serial number

While not all devices are able to expose their serial number to software, most of them actually do.

Exo will strictly identify devices by their serial numbers, even in cases where Windows wouldn't be able to, and display that information to you in the UI.

## Mouse settings

![Screenshot of the settings for a Razer Mouse](images/Screenshot-Exo-Mouse-Razer.png)
![Screenshot of the settings for a Logitech Mouse](images/Screenshot-Exo-Mouse-Logitech.png)

Capability to configure DPI presets and change the active preset are implemented in Exo, as well as ability to support 

## Battery and Power settings

![Screenshot of the Devices Page](images/Screenshot-Exo-Mouse-PowerManagement.png)

For the devices where it is applicable, Exo will display detailed battery informations and allow to configure some power saving settings.

## Monitor settings

![Screenshot of the settings for a ViewSonic Monitor](images/Screenshot-Exo-Monitor-ViewSonic-1.png)
![Screenshot of the settings for a ViewSonic Monitor](images/Screenshot-Exo-Monitor-ViewSonic-2.png)
![Screenshot of the settings for a ViewSonic Monitor](images/Screenshot-Exo-Monitor-ViewSonic-3.png)

Exo has built-in support for various monitor settings, based on what the monitor reports.

⚠️ Some monitors will lie about the feature they support, so you should be careful when playing with monitor settings.

A specific configuration may need to be written for your particular monitor(s) to inform Exo about how to work with it.
This can also be done to enable non-standard Monitor features supported by Exo.

![Screenshot of the settings for a LG Monitor](images/Screenshot-Exo-Monitor-Lg-1.png)
![Screenshot of the settings for a LG Monitor](images/Screenshot-Exo-Monitor-Lg-2.png)

As you can see in the screenshots above, some monitors support less features than others.

## RGB Lighting

![Screenshot of the Lighting page, showing RGB RAM settings](images/Screenshot-Exo-Lighting-1.png)

Exo will manage the RGB lighting of devices, as long as they are supported, of course.

Only hardware effects are supported at the moment (no custom/dynamic lighting effects), which is the best choice to reduce CPU usage anyway.

The option to persist lighting settings to non-volatile memory of the device is also provided, if the device supports it.

![Screenshot of the Lighting page, showing a motherboard with multiple lighting zones](images/Screenshot-Exo-Lighting-2.png)
![Screenshot of the Lighting page, showing a motherboard with unified lighting](images/Screenshot-Exo-Lighting-3.png)

Support for unified lighting effects can also be toggled for mlti-zone devices that support it.

## Embedded Monitors

![Screenshot of a Device page, showing Embedded Monitor settings](images/Screenshot-Exo-Embedded-Monitor.png)

Exo will manage the embedded monitors on your devices. While relatively niche, these external displays are becoming more common, as many AIOs will have them.
Buttons of the StreamDeck devices will also be exposed as embedded monitors.

Embedded monitors can be assigned an image from the image library managed by Exo, with support for animated GIFs, and automatic conversion of images to the correct format for the device.

As on-device memory may be limited, and Exo's image processing capabilities are not perfect, you may sometimes want to preprocess images with a tool such as gifsicle to produce an optimized output.

If you provide an image in the correct format and with the correct characteristics, it will be passed through to the device without any processing.

It is also worth noting that, at the expense of more disk usage, image transformations are cached to save on processing time.
This is especially important for large animated GIFs, which may require multiple seconds to be processed.

## Image library

![Screenshot of a the Images page, showing the image library](images/Screenshot-Exo-Image-Library.png)

To support the embedded monitors feature, an image library has been added to Exo.
Here, you'll be able to add images to the service, which will then be useable for display on embedded monitors.

Naming of image is for user convenience, and Exo will never use the name to reference images.

⚠️ There is currently no check on the use of an image before deletion. Deleting images should not break the service, though.

ℹ️ This image library is alays present in Exo, but it is pointless if you don't have any (supported) embedded monitor.

## Sensors

![Screenshot of the Sensors page](images/Screenshot-Exo-Sensors-1.png)
![Screenshot of the Sensors page](images/Screenshot-Exo-Sensors-2.png)

Exo has support for listening to hardware device sensors.

This is mainly used for low-level devices such as a GPU or a PSU, but being able to take a quick look of the status of your devices should be useful.

More importantly, having a wide source of sensors is necessary to support software cooling curves.

## Cooling

![Screenshot of the Cooling page](images/Screenshot-Exo-Cooling.png)

Exo is able to change cooling settings of devices. (Fan power, Pump power)

Cooling curves can be applied based on other sensors.
Support for hardware cooling curves is available for devices that are capable of it.
Otherwise, Exo will manage software cooling curves, which are more flexible and can be more efficient but will consume some CPU.

# How

Exo is implemented as a Windows service. This means that it will start early and outside of any graphical user session, which is something that you absolutely want.

This background service will only consume a few dozens of MB, which is far from the hundreds of MB that many of manufacturer apps would typically consume.
Many of those apps would also be unable to run outside of graphical user session because of their design.

Obviously, we still want some nice UI to configure everything.
In the case of Exo, the UI is kept as a separate application, that you can start only when needed.
This allow preserving previous system resources, while not depriving of the comfort of a UI.

Exo is also supported by a lighter UI helper component that will be in charge of displaying overlay notifications and providing some support to the service for some features that require UI access.
Notably, this component is strictly required to be running in order to support monitor devices on most Intel GPUs. (Because on "old" devices, Intel does not provide an API allowing to access DDC features unlike NVIDIA or AMD)

![Screenshot from Task Manager running Exo](images/Screenshot-TaskManager-Exo-Resources.png)

As you can see on the screenshot above, Exo memory consumption is pretty reasonable, topping at about 43 MB of exclusive memory for the background service.
This is all while handling more devices and combined features than the software you would typically use for a single device.
