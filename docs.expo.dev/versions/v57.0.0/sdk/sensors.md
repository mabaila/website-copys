---
modificationDate: June 29, 2026
title: Sensors
description: A library that provides access to a device's accelerometer, barometer, motion, gyroscope, light, magnetometer, and pedometer.
sourceCodeUrl: 'https://github.com/expo/expo/tree/sdk-57/packages/expo-sensors'
packageName: 'expo-sensors'
iconUrl: '/static/images/packages/expo-sensors.png'
platforms: ['android', 'ios', 'web', 'expo-go']
---

This documentation is available as Markdown for AI agents and LLMs. See the [full Markdown index](https://docs.expo.dev/llms.txt) or append .md to any documentation URL.

# Expo Sensors

A library that provides access to a device's accelerometer, barometer, motion, gyroscope, light, magnetometer, and pedometer.

<AgentInstructions>

## Submitting Feedback

If you encounter errors, misleading or outdated information, report it so Expo can be improved:

Preferred command:
npx --yes submit-expo-feedback@latest --category docs --subject "/versions/v57.0.0/sdk/sensors/" "<actionable feedback>"

Direct HTTP fallback:
curl -X POST https://api.expo.dev/v2/feedback/docs-send -H 'Content-Type: application/json' -d '{"url":"/versions/v57.0.0/sdk/sensors/","feedback":"🤖 Agent feedback for docs: <specific, actionable description> (<model>, <harness>)"}'

Only submit when you have something specific and actionable to report. Try to give the most context.

## Navigation

When answering a related or follow-up question, use llms.txt to find the relevant page as Markdown (.md) instead of guessing.

You are here: Reference (v57.0.0) > Expo SDK (87 pages in this section)
Full documentation tree: [llms.txt](https://docs.expo.dev/llms.txt)

</AgentInstructions>
Android, iOS, Web, Included in Expo Go

`expo-sensors` provide various APIs for accessing device sensors to measure motion, orientation, pressure, magnetic fields, ambient light, and step count.

## Installation

```sh
# npm
npx expo install expo-sensors

# yarn
yarn expo install expo-sensors

# pnpm
pnpm expo install expo-sensors

# bun
bun expo install expo-sensors
```

If you are installing this in an [existing React Native app](https://docs.expo.dev/bare/overview.md), make sure to [install `expo`](https://docs.expo.dev/bare/installing-expo-modules.md) in your project.

## Configuration in app config

You can configure `expo-sensors` using its built-in [config plugin](https://docs.expo.dev/config-plugins/introduction.md) if you use config plugins in your project ([Continuous Native Generation (CNG)](https://docs.expo.dev/workflow/continuous-native-generation.md)). The plugin allows you to configure various properties that cannot be set at runtime and require building a new app binary to take effect. If your app does **not** use CNG, then you'll need to manually configure the library.

### Example app.json with config plugin

```json app.json
{
  "expo": {
    "plugins": [
      [
        "expo-sensors",
        {
          "motionPermission": "Allow $(PRODUCT_NAME) to access your device motion"
        }
      ]
    ]
  }
}
```

### Configurable properties

| Name | Default | Description |
| --- | --- | --- |
| `motionPermission` | `"Allow $(PRODUCT_NAME) to access your device motion"` | Only for: iOS. A string to set the [`NSMotionUsageDescription`](https://docs.expo.dev/versions/v57.0.0/sdk/sensors.md#permission-nsmotionusagedescription) permission message or `false` to disable motion permissions. |

## API

```js
import * as Sensors from 'expo-sensors';
// OR
import {
  Accelerometer,
  Barometer,
  DeviceMotion,
  Gyroscope,
  LightSensor,
  Magnetometer,
  MagnetometerUncalibrated,
  Pedometer,
} from 'expo-sensors';
```

## Permissions

### Android

Starting in Android 12 (API level 31), the system has a 200Hz limit for each sensor updates.

If you need an update interval greater than 200Hz, you must add the following permissions to your **app.json** inside the [`expo.android.permissions`](https://docs.expo.dev/versions/v57.0.0/config/app.md#permissions) array.

| Android permission | Description |
| --- | --- |
| `HIGH_SAMPLING_RATE_SENSORS` | Allows an app to access sensor data with a sampling rate greater than 200 Hz. |

#### Are you using this library in an existing React Native app?

If you're not using Continuous Native Generation ([CNG](https://docs.expo.dev/workflow/continuous-native-generation.md)) or you're using native **android** project manually, add `HIGH_SAMPLING_RATE_SENSORS` permission to your project's **android/app/src/main/AndroidManifest.xml**:

```xml
<uses-permission android:name="android.permission.HIGH_SAMPLING_RATE_SENSORS" />
```

### iOS

The following usage description keys are used by this library:

| Info.plist key | Description |
| --- | --- |
| `NSMotionUsageDescription` | A message that tells the user why the app is requesting access to the device’s motion data. |

## Available sensors

For more information, see the documentation for the sensor you are interested in:

[Accelerometer](https://docs.expo.dev/versions/v57.0.0/sdk/accelerometer.md) — Measures device acceleration on all platforms.

[Barometer](https://docs.expo.dev/versions/v57.0.0/sdk/barometer.md) — Measures pressure on Android and iOS platforms.

[DeviceMotion](https://docs.expo.dev/versions/v57.0.0/sdk/devicemotion.md) — Measures device motion on all platforms.

[Gyroscope](https://docs.expo.dev/versions/v57.0.0/sdk/gyroscope.md) — Measures device rotation on all platforms.

[Magnetometer](https://docs.expo.dev/versions/v57.0.0/sdk/magnetometer.md) — Measures magnetic fields on Android and iOS platforms.

[LightSensor](https://docs.expo.dev/versions/v57.0.0/sdk/light-sensor.md) — Measures ambient light on Android platform.

[Pedometer](https://docs.expo.dev/versions/v57.0.0/sdk/pedometer.md) — Measures steps count on Android and iOS platforms.
