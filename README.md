# Intel RealSense for Processing [![Build Status](https://travis-ci.org/cansik/realsense-processing.svg?branch=master)](https://travis-ci.org/cansik/realsense-processing) [![Build status](https://ci.appveyor.com/api/projects/status/nqmgr5d1pfcmco7u?svg=true)](https://ci.appveyor.com/project/cansik/realsense-processing) [![codebeat badge](https://codebeat.co/badges/9169f571-c486-4b1e-a34c-595e67cd9d93)](https://codebeat.co/projects/github-com-cansik-realsense-processing-master)
Intel RealSense 2 support for the [Processing](https://processing.org/) framework.

![Example](readme/example.jpg)

## Introduction

**Intel RealSense for Procesing** is a port of the **[Intel RealSense](https://github.com/IntelRealSense/librealsense)** library for processing. With this library it is possible to use the Intel RealSense D400 camera series within processing. The idea is **not** to expose the full API into Processing, however a simple and convenient way to work with RealSense devices. For full API support switching over to the underlying [java wrapper](https://github.com/cansik/librealsense-java) is recommended.

Supported Intel RealSense Version: [2.29.0](https://github.com/IntelRealSense/librealsense/releases/tag/v2.29.0)

#### ![#f03c15](https://placehold.it/12/f03c15/000000?text=+) Important

- Currently the library is still under development.
- `Linux`, `MacOS` and `Windows` binaries (x86 / x64) are already bundled into the Jar file.


#### Supported Configurations
Here are some configurations I have tested and which are working with the Intel RealSense D435. Please make sure you are using a USB 3.0 or 3.1 cable!

| width | height | fps                         | depth stream | color stream |
|-------|--------|-----------------------------|--------------|--------------|
| 424   | 240    | `6`, `15`, `30`, `60`       | ✅            | ✅            |
| 480   | 270    | `6`, `15`, `30`, `60`, `90` | ✅            | ❌            |
| 640   | 480    | `6`, `15`, `30`, `60`       | ✅            | ✅            |
| 640   | 480    | `90`                        | ✅            | ❌            |
| 848   | 480    | `6`, `15`, `30`, `60`       | ✅            | ✅            |
| 848   | 480    | `90`                        | ✅            | ❌            |
| 960   | 540    | `6`, `15`, `30`, `60`       | ❌            | ✅            |
| 1280  | 720    | `30`                        | ✅            | ✅            |
| 1280  | 800    | `6`, `15`, `30`, `60`, `90` | ❌            | ❌            |
| 1920  | 1080   | `6`, `15`, `30`             | ❌            | ✅            |

## Installation
There are multiple ways on how to install the library for this repository into your project.

### Contribution Manager
Use the contribution manager inside Processing to directly install the library into your local Processing instance.

![Contribution Manager](readme/contribution.png)

### Gradle / Maven
Include the library directly into your gradle / maven build by using [jitpack](https://jitpack.io/#cansik/realsense-processing/latest).

```groovy
repositories {
    maven { url 'https://jitpack.io' }
}

dependencies {
    implementation 'com.github.cansik:realsense-processing:latest'
}
```

### Manual

Download the [latest build](https://github.com/cansik/realsense-processing/releases/tag/contributed) and extract the files into your [processing library](https://github.com/processing/processing/wiki/How-to-Install-a-Contributed-Library) folder.

## Example

Here is an example which shows how to use the library. You find more [examples here](https://github.com/cansik/realsense-processing/tree/master/examples).

```java
import ch.bildspur.realsense.*;

RealSenseCamera camera = new RealSenseCamera(this);

void setup()
{
  size(640, 480);

  // width, height, fps, depth-stream, color-stream
  camera.start(640, 480, 30, true, true);
}

void draw()
{
  background(0);

  // read frames
  camera.readFrames();

  // show color image
  image(camera.getColorImage(), 0, 0);
  
  // -- or --
  
  // create grayscale image form depth buffer
  // min and max depth
  camera.createDepthImage(0, 3000);
  
  // show color image
  image(camera.getDepthImage(), 0, 0);
}
```

## About

The processing library is maintained by [@cansik](https://github.com/cansik) and based on the Intel RealSense [Java wrapper](https://github.com/cansik/librealsense-java).
