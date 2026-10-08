---
modificationDate: August 24, 2026
title: SegmentedControl
description: A segmented control compatible with @react-native-segmented-control/segmented-control.
sourceCodeUrl: 'https://github.com/expo/expo/tree/sdk-57/packages/expo-ui'
packageName: '@expo/ui'
platforms: ['android', 'ios', 'web', 'expo-go']
---

This documentation is available as Markdown for AI agents and LLMs. See the [full Markdown index](https://docs.expo.dev/llms.txt) or append .md to any documentation URL.

# SegmentedControl

A segmented control compatible with @react-native-segmented-control/segmented-control.

<AgentInstructions>

## Submitting Feedback

If you encounter errors, misleading or outdated information, report it so Expo can be improved:

Preferred command:
npx --yes submit-expo-feedback@latest --category docs --subject "/versions/v57.0.0/sdk/ui/drop-in-replacements/segmentedcontrol/" "<actionable feedback>"

Direct HTTP fallback:
curl -X POST https://api.expo.dev/v2/feedback/docs-send -H 'Content-Type: application/json' -d '{"url":"/versions/v57.0.0/sdk/ui/drop-in-replacements/segmentedcontrol/","feedback":"🤖 Agent feedback for docs: <specific, actionable description> (<model>, <harness>)"}'

Only submit when you have something specific and actionable to report. Try to give the most context.

## Navigation

When answering a related or follow-up question, fetch the relevant page below as Markdown (.md) instead of guessing; use llms.txt for the full map.

You are here: Reference (v57.0.0) > Expo UI > Drop-in replacements
Pages in this section:
- [Overview](https://docs.expo.dev/versions/v57.0.0/sdk/ui/drop-in-replacements.md)
- [BottomSheet](https://docs.expo.dev/versions/v57.0.0/sdk/ui/drop-in-replacements/bottomsheet.md)
- [DateTimePicker](https://docs.expo.dev/versions/v57.0.0/sdk/ui/drop-in-replacements/datetimepicker.md)
- [MaskedView](https://docs.expo.dev/versions/v57.0.0/sdk/ui/drop-in-replacements/maskedview.md)
- [Menu](https://docs.expo.dev/versions/v57.0.0/sdk/ui/drop-in-replacements/menu.md)
- [PagerView](https://docs.expo.dev/versions/v57.0.0/sdk/ui/drop-in-replacements/pagerview.md)
- [Picker](https://docs.expo.dev/versions/v57.0.0/sdk/ui/drop-in-replacements/picker.md)
- [SegmentedControl](https://docs.expo.dev/versions/v57.0.0/sdk/ui/drop-in-replacements/segmentedcontrol.md) (this page)
- [Slider](https://docs.expo.dev/versions/v57.0.0/sdk/ui/drop-in-replacements/slider.md)
Full documentation tree: [llms.txt](https://docs.expo.dev/llms.txt)

</AgentInstructions>
Android, iOS, Web, Included in Expo Go

A `SegmentedControl` component with an API compatible with `@react-native-segmented-control/segmented-control`. It uses Jetpack Compose `SingleChoiceSegmentedButtonRow` on Android and SwiftUI `Picker` with segmented style on iOS.

Under the hood this component wraps the platform-specific `@expo/ui` primitives:

-   **Android**: [Jetpack Compose SegmentedButton](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/segmentedbutton.md)
-   **iOS**: [SwiftUI Picker](https://docs.expo.dev/versions/v57.0.0/sdk/ui/swift-ui/picker.md) with `pickerStyle('segmented')`

If you need lower-level control (custom modifiers, styles, or layouts), use those primitives directly.

Image: A Material 3 segmented button row with One selected

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

## Migrating from `@react-native-segmented-control/segmented-control`

-   Update the import from `import SegmentedControl from '@react-native-segmented-control/segmented-control'` to `import SegmentedControl from '@expo/ui/community/segmented-control'`.
-   Image values in the `values` array are not supported, only strings.
-   `momentary`, `backgroundColor`, `fontStyle`, and `activeFontStyle` props are not supported.
-   `tintColor` only works on Android (sets the active segment container color). On iOS, it has no effect.

## Basic usage

```tsx SegmentedControlExample.tsx
import { useState } from 'react';
import SegmentedControl from '@expo/ui/community/segmented-control';

export default function SegmentedControlExample() {
  const [selectedIndex, setSelectedIndex] = useState(0);

  return (
    <SegmentedControl
      values={['One', 'Two', 'Three']}
      selectedIndex={selectedIndex}
      onChange={event => {
        setSelectedIndex(event.nativeEvent.selectedSegmentIndex);
      }}
    />
  );
}
```

## API

```tsx
import SegmentedControl from '@expo/ui/community/segmented-control';
```

## Component

### `SegmentedControl`

Supported platforms: Android, iOS, Web.

Type: React.[Element](https://www.typescriptlang.org/docs/handbook/jsx.html#function-component)<[SegmentedControlProps](https://docs.expo.dev/versions/v57.0.0/sdk/ui/drop-in-replacements/segmentedcontrol.md#segmentedcontrolprops)\>

SegmentedControlProps

### `appearance`

Supported platforms: Android, iOS, Web.

Optional • Literal type: `string`

Overrides the control's appearance irrespective of the system theme.

Acceptable values are: `'light'` | `'dark'`

### `enabled`

Supported platforms: Android, iOS, Web.

Optional • Type: `boolean` • Default: `true`

If `false`, the user cannot interact with the control.

### `onChange`

Supported platforms: Android, iOS, Web.

Optional • Type: (event: [NativeSegmentedControlChangeEvent](https://docs.expo.dev/versions/v57.0.0/sdk/ui/drop-in-replacements/segmentedcontrol.md#nativesegmentedcontrolchangeevent)) => void

Called when the user taps a segment. The event carries `nativeEvent.selectedSegmentIndex` and `nativeEvent.value`.

### `onValueChange`

Supported platforms: Android, iOS, Web.

Optional • Type: `(value: string) => void`

Called when the user taps a segment. Receives the segment's string value.

### `selectedIndex`

Supported platforms: Android, iOS, Web.

Optional • Type: `number`

The index of the selected segment.

### `style`

Supported platforms: Android, iOS, Web.

Optional • Type: StyleProp<[ViewStyle](https://reactnative.dev/docs/view-style-props)\>

### `testID`

Supported platforms: Android, iOS, Web.

Optional • Type: `string`

### `tintColor`

Supported platforms: Android, web.

Optional • Type: `string`

Accent color of the control.

### `values`

Supported platforms: Android, iOS, Web.

Optional • Type: `string[]`

The labels for the control's segment buttons, in order.

## Types

### `NativeSegmentedControlChangeEvent`

Supported platforms: Android, iOS, Web.

Shape of the native event passed to `onChange`. Matches `@react-native-segmented-control/segmented-control`.

| Property | Type | Description |
| --- | --- | --- |
| nativeEvent | `{ selectedSegmentIndex: number, value: string }` | - |

> **Deprecated:** use NativeSegmentedControlChangeEvent

### `NativeSegmentedControlIOSChangeEvent`

Supported platforms: Android, iOS, Web.

Type: [NativeSegmentedControlChangeEvent](https://docs.expo.dev/versions/v57.0.0/sdk/ui/drop-in-replacements/segmentedcontrol.md#nativesegmentedcontrolchangeevent)

Shape of the native event passed to `onChange`. Matches `@react-native-segmented-control/segmented-control`.
