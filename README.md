# Firefly Luciferin
**Luciferin** is a generic term for the light-emitting compound found in organisms that generate bioluminescence like Fireflies and Glow Worms. `Firefly Luciferin is a Java Fast Screen Capture` PC software designed for the  
[Glow Worm Luciferin](https://github.com/sblantipodi/glow_worm_luciferin) firmware,  
the combination of these software create the perfect `Bias Lighting and Ambient Light system for PC`.  
_Written in Java with a native flavour for Windows and Linux._  
  
  
<img align="right" width="100" height="100" src="https://github.com/sblantipodi/firefly_luciferin/blob/master/data/img/java_fast_screen_capture_logo.png">


[![Java CI with Maven](https://github.com/sblantipodi/firefly_luciferin/workflows/Java%20CI%20with%20Maven/badge.svg)](https://github.com/sblantipodi/firefly_luciferin/actions)
[![GitHub version](https://img.shields.io/github/v/release/sblantipodi/firefly_luciferin.svg)](https://github.com/sblantipodi/firefly_luciferin/releases)
[![License: GPL v3](https://img.shields.io/badge/License-GPLv3-yellow.svg)](https://www.gnu.org/licenses/gpl-3.0)
[![Maintenance](https://img.shields.io/badge/Maintained%3F-yes-green.svg)](https://GitHub.com/sblantipodi/firefly_luciferin/graphs/commit-activity)
[![DPsoftware](https://img.shields.io/static/v1?label=DP&message=Software&color=orange)](https://www.dpsoftware.org)
[![Discord](https://img.shields.io/discord/747247942074892328.svg?label=&logo=discord&logoColor=ffffff&color=7389D8&labelColor=6A7EC2)](https://discord.gg/aXf9jeN)


If you like **Firefly Luciferin**, give it a star, or fork it and contribute!

[![GitHub stars](https://img.shields.io/github/stars/sblantipodi/firefly_luciferin.svg?style=social&label=Star)](https://github.com/sblantipodi/firefly_luciferin/stargazers)
[![GitHub forks](https://img.shields.io/github/forks/sblantipodi/firefly_luciferin.svg?style=social&label=Fork)](https://github.com/sblantipodi/firefly_luciferin/network)

## Quick start
You can build the software from the source or if you prefer you can **download the installer from [here](https://github.com/sblantipodi/firefly_luciferin/releases)**.  
`Firefly Luciferin` uses `Java 14` to create the native installer, this means that you don't have to install Java or other libraries separately.
  
This software can run on any Desktop PC using **Windows or Linux**. MacOS support will be added later. 
To get the full `Bias Lighting` experience you need a microcontroller (ex. ESP8266, ESP32) running [Glow Worm Luciferin](https://github.com/sblantipodi/glow_worm_luciferin) firmware. You can connect the microcontroller to the PC via USB or via wirelss using an MQTT server. 

Why don't you build your own `Luciferin`?  
Here's a [**Quick Start guide**](https://github.com/sblantipodi/firefly_luciferin/wiki/Quick-start)  

## Glow Worm Luciferin + Firefly Luciferin (click to watch it on YouTube)
[![Luciferin YouTube Video #1](https://github.com/sblantipodi/glow_worm_luciferin/blob/master/assets/img/ambilight_viddeo.jpg)](https://youtu.be/Hd6BtPp40I0)

## Configuration
As soon as you start the software it creates a `FireflyLuciferin.yaml` file in your documents folder, you can configure it manually or via the user interface.
`If you don't know how to configure it, just use the default settings`. 

![IMAGE ALT TEXT HERE](https://github.com/sblantipodi/firefly_luciferin/blob/master/data/img/settings_screen.png)

```yaml
---
numberOfCPUThreads: 3     // more threads more performance but more CPU usage
captureMethod: "DDUPL"    // WinAPI and DDUPL enables GPU Hardware Acceleration, CPU uses CPU brute force only
serialPort: "AUTO"        // use "AUTO" to autodetect Serial Port, "COM7" for COM7 
dataRate: 500000          // faster data rate helps when using more LEDs or higher framerate
timeout: 2000             // timeout in serial port detection
screenResX: 3840          // screen resolution width
screenResY: 2160          // screen resolution height
osScaling: 150            // OS scaling feature
gamma: 2.2                // gamma correction for the LED strip
mqttServer: "OPTIONAL"    // MQTT Server protocol://host:port (E.g. "tcp://192.168.1.3:1883")
mqttTopic: "OPTIONAL"     // MQTT Server Topic used to start/stop screen capture on the microcontroller
mqttUsername: "OPTIONAL"  // MQTT Server username
mqttPwd: "OPTIONAL"       // MQTT Server pwd
ledMatrix:                // Auto generated LED Matrix
  Letterbox:
    1:
      x: 2596
      y: 1590
    2:
      x: 2694
      y: 1590
  ...
```

## What is the Performance Impact on your System?
Firefly Luciferin is a very optimized software and it has **nearly no impact on your system performance**.  
By default Firefly Luciferin captures at 30FPS, if you want you can unlock the framerate.  
  
If you are using a slow microcontroller, capturing at a very high framerate will not help. If you right click the tray icon and then click `FPS`,
you can see the output as shown in the image below. In that output you can see how fast the software is capturing the screen (producing)
and how fast your microcontroller is able to process (consume) this data.  

<p align="center">
  <img width="700" src="https://raw.githubusercontent.com/sblantipodi/firefly_luciferin/master/data/img/framerate_counter_javafx_menu.png">
</p>

Increase `dataRate` accordingly to your microcontroller's serial speed, 115200 is generally more than enough for 30FPS and 100 LEDs. Producers framerate should not exceed the consuming one, all data that is not consumed in time, is lost.

## GPU Hardware Acceleration using Java Native Access 
Screen capturing is pretty slow and very CPU intensive in Windows systems (Linux is much more efficient in this regard),
for this reason I wrapped the Windows GDI32 C class using [Java Native Access](https://github.com/java-native-access/jna) to access Windows hardware acceleration.  

This API captures and delivers captured frames in GPU memory. 

If you are running Windows 8 or Windows 10 you can use `Desktop Duplication API (DDUPL)`, it's the fastest implementation yet, no lag, 
no stutter, very small usage of resources. DDUPL is accessed via [JNA](https://github.com/java-native-access/jna) using the [GStreamer bindings for Java](https://gstreamer.freedesktop.org/bindings/java.html).  

## Credits
- Davide Perini

## Thanks To 
|  Thanks              |  For                           |
|----------------------|--------------------------------|
|<a href="https://www.jetbrains.com/"><img width="200" src="https://raw.githubusercontent.com/sblantipodi/arduino_bootstrapper/master/data/img/jetbrains.png"></a>| For the <a href="https://www.jetbrains.com/idea">IntelliJ IDEA</a> licenses.|
