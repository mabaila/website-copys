---
modificationDate: August 18, 2026
title: Progress indicators
description: Jetpack Compose progress indicator components for displaying operation status.
sourceCodeUrl: 'https://github.com/expo/expo/tree/sdk-57/packages/expo-ui'
packageName: '@expo/ui'
platforms: ['android', 'expo-go']
---

This documentation is available as Markdown for AI agents and LLMs. See the [full Markdown index](https://docs.expo.dev/llms.txt) or append .md to any documentation URL.

# Progress indicators

Jetpack Compose progress indicator components for displaying operation status.

<AgentInstructions>

## Submitting Feedback

If you encounter errors, misleading or outdated information, report it so Expo can be improved:

Preferred command:
npx --yes submit-expo-feedback@latest --category docs --subject "/versions/v57.0.0/sdk/ui/jetpack-compose/progress/" "<actionable feedback>"

Direct HTTP fallback:
curl -X POST https://api.expo.dev/v2/feedback/docs-send -H 'Content-Type: application/json' -d '{"url":"/versions/v57.0.0/sdk/ui/jetpack-compose/progress/","feedback":"🤖 Agent feedback for docs: <specific, actionable description> (<model>, <harness>)"}'

Only submit when you have something specific and actionable to report. Try to give the most context.

## Navigation

When answering a related or follow-up question, use llms.txt to find the relevant page as Markdown (.md) instead of guessing.

You are here: Reference (v57.0.0) > Expo UI > Jetpack Compose (51 pages in this section)
Full documentation tree: [llms.txt](https://docs.expo.dev/llms.txt)

</AgentInstructions>
Android, Included in Expo Go

Expo UI Progress Indicators match the official Jetpack Compose [Progress Indicator API](https://developer.android.com/develop/ui/compose/components/progress).

Image: Indeterminate circular progress indicator with two determinate linear progress bars at 30% and 75%

## Installation

```sh
# npm
npx expo install @expo/ui

# yarn
yarn expo install @expo/ui

# pnpm
pnpm expo install @expo/ui

# bun
bun expo install @expo/ui
```

If you are installing this in an [existing React Native app](https://docs.expo.dev/bare/overview.md), make sure to [install `expo`](https://docs.expo.dev/bare/installing-expo-modules.md) in your project.

## Usage

### Linear progress

A horizontal bar that fills to indicate progress. Provide a `progress` value between `0` and `1` for determinate mode.

```tsx LinearExample.tsx
import {
  Host,
  LinearProgressIndicator,
} from '@expo/ui/jetpack-compose';

export default function LinearExample() {
  return (
    <Host matchContents>
      <LinearProgressIndicator progress={0.5} />
    </Host>
  );
}
```

### Circular progress

A spinning circle whose stroke grows to indicate progress.

```tsx CircularExample.tsx
import {
  Host,
  CircularProgressIndicator,
} from '@expo/ui/jetpack-compose';

export default function CircularExample() {
  return (
    <Host matchContents>
      <CircularProgressIndicator progress={0.75} />
    </Host>
  );
}
```

### Indeterminate

Omit the `progress` prop to animate continuously without indicating a specific completion level.

```tsx IndeterminateExample.tsx
import {
  CircularProgressIndicator,
  CircularWavyProgressIndicator,
  Column,
  Host,
  LinearProgressIndicator,
  LinearWavyProgressIndicator,
} from '@expo/ui/jetpack-compose';

export default function IndeterminateExample() {
  return (
    <Host matchContents>
      <Column verticalArrangement={{ spacedBy: 16 }}>
        <LinearProgressIndicator />
        <CircularProgressIndicator />
        <CircularWavyProgressIndicator />
        <LinearWavyProgressIndicator />
      </Column>
    </Host>
  );
}
```

### Custom colors

Use `color` for the indicator and `trackColor` for the background track.

```tsx ColorsExample.tsx
import {
  Host,
  CircularProgressIndicator,
} from '@expo/ui/jetpack-compose';

export default function ColorsExample() {
  return (
    <Host matchContents>
      <CircularProgressIndicator
        progress={0.6}
        color="red"
        trackColor="#cccccc"
      />
    </Host>
  );
}
```

### Wavy variants

`LinearWavyProgressIndicator` and `CircularWavyProgressIndicator` add an expressive wave animation from Material 3 Expressive.

```tsx WavyExample.tsx
import {
  Host,
  LinearWavyProgressIndicator,
  CircularWavyProgressIndicator,
  Column,
} from '@expo/ui/jetpack-compose';

export default function WavyExample() {
  return (
    <Host matchContents>
      <Column verticalArrangement={{ spacedBy: 16 }}>
        <LinearWavyProgressIndicator progress={0.6} />
        <CircularWavyProgressIndicator progress={0.6} />
      </Column>
    </Host>
  );
}
```

## API

```tsx
import {
  LinearProgressIndicator,
  CircularProgressIndicator,
  LinearWavyProgressIndicator,
  CircularWavyProgressIndicator,
} from '@expo/ui/jetpack-compose';
```

## Components

### `CircularProgressIndicator`

Supported platforms: Android.

Type: React.[Element](https://www.typescriptlang.org/docs/handbook/jsx.html#function-component)<ComponentType<[CircularProgressIndicatorProps](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/progress.md#circularprogressindicatorprops)\>\>

A circular progress indicator that displays progress in a circular format.

Matches the Jetpack Compose `CircularProgressIndicator`.

Common props shared by all progress indicator variants.

CircularProgressIndicatorProps

### `gapSize`

Supported platforms: Android.

Optional • Type: `number`

Gap size between the indicator and track in dp.

### `strokeCap`

Supported platforms: Android.

Optional • Type: [StrokeCap](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/progress.md#strokecap) • Default: `'round'`

Stroke cap style for the indicator ends.

### `strokeWidth`

Supported platforms: Android.

Optional • Type: `number`

Width of the circular stroke in dp.

#### Inherited props

-   [ProgressCommonConfig](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/progress.md#progresscommonconfig)

### `CircularWavyProgressIndicator`

Supported platforms: Android.

Type: React.[Element](https://www.typescriptlang.org/docs/handbook/jsx.html#function-component)<ComponentType<[CircularWavyProgressIndicatorProps](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/progress.md#circularwavyprogressindicatorprops)\>\>

A circular progress indicator with wavy animation style.

Matches the Jetpack Compose `CircularWavyProgressIndicator`.

Common props shared by all progress indicator variants.

CircularWavyProgressIndicatorProps

#### Inherited props

-   [ProgressCommonConfig](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/progress.md#progresscommonconfig)

### `LinearProgressIndicator`

Supported platforms: Android.

Type: React.[Element](https://www.typescriptlang.org/docs/handbook/jsx.html#function-component)<ComponentType<[LinearProgressIndicatorProps](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/progress.md#linearprogressindicatorprops)\>\>

A linear progress indicator that displays progress in a horizontal bar.

Matches the Jetpack Compose `LinearProgressIndicator`.

Common props shared by all progress indicator variants.

LinearProgressIndicatorProps

### `drawStopIndicator`

Supported platforms: Android.

Optional • Type: [DrawStopIndicatorConfig](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/progress.md#drawstopindicatorconfig)

Configuration for the stop indicator dot at the end of the determinate progress track.

### `gapSize`

Supported platforms: Android.

Optional • Type: `number`

Gap size between the indicator and track in dp.

### `strokeCap`

Supported platforms: Android.

Optional • Type: [StrokeCap](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/progress.md#strokecap) • Default: `'round'`

Stroke cap style for the indicator ends.

#### Inherited props

-   [ProgressCommonConfig](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/progress.md#progresscommonconfig)

### `LinearWavyProgressIndicator`

Supported platforms: Android.

Type: React.[Element](https://www.typescriptlang.org/docs/handbook/jsx.html#function-component)<ComponentType<[LinearWavyProgressIndicatorProps](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/progress.md#linearwavyprogressindicatorprops)\>\>

A linear progress indicator with wavy animation style.

Matches the Jetpack Compose `LinearWavyProgressIndicator`.

Common props shared by all progress indicator variants.

LinearWavyProgressIndicatorProps

### `stopSize`

Supported platforms: Android.

Optional • Type: `number`

Size of the stop indicator in dp at the end of the determinate progress track.

#### Inherited props

-   [ProgressCommonConfig](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/progress.md#progresscommonconfig)

## Types

### `DrawStopIndicatorConfig`

Supported platforms: Android.

Configuration for the stop indicator dot at the end of the determinate linear progress track. When provided, draws a stop indicator with the given options. Omit to use the Compose default.

| Property | Type | Description |
| --- | --- | --- |
| color(optional) | [ColorValue](https://reactnative.dev/docs/colors) | Color of the stop indicator. Defaults to the indicator's color. |
| stopSize(optional) | `number` | Size of the stop indicator in dp. Defaults to the Material 3 default. |
| strokeCap(optional) | [StrokeCap](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/progress.md#strokecap) | Stroke cap style for the stop indicator. Defaults to the indicator's strokeCap. |

### `ProgressCommonConfig`

Supported platforms: Android.

Common props shared by all progress indicator variants.

| Property | Type | Description |
| --- | --- | --- |
| color(optional) | [ColorValue](https://reactnative.dev/docs/colors) | Progress indicator color. |
| modifiers(optional) | `ModifierConfig[]` | Modifiers for the component. |
| progress(optional) | `number | null` | The current progress value between `0` and `1`. Omit for indeterminate. |
| trackColor(optional) | [ColorValue](https://reactnative.dev/docs/colors) | Track (background) color. |

### `StrokeCap`

Supported platforms: Android.

Literal type: `string`

Stroke cap style for progress indicators.

Acceptable values are: `'round'` | `'butt'` | `'square'`
