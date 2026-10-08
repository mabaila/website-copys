---
modificationDate: September 30, 2026
title: MaskedView
description: A masked view compatible with @react-native-masked-view/masked-view.
sourceCodeUrl: 'https://github.com/expo/expo/tree/sdk-57/packages/expo-ui'
packageName: '@expo/ui'
platforms: ['android', 'ios']
---

This documentation is available as Markdown for AI agents and LLMs. See the [full Markdown index](https://docs.expo.dev/llms.txt) or append .md to any documentation URL.

# MaskedView

A masked view compatible with @react-native-masked-view/masked-view.

<AgentInstructions>

## Submitting Feedback

If you encounter errors, misleading or outdated information, report it so Expo can be improved:

Preferred command:
npx --yes submit-expo-feedback@latest --category docs --subject "/versions/v57.0.0/sdk/ui/drop-in-replacements/maskedview/" "<actionable feedback>"

Direct HTTP fallback:
curl -X POST https://api.expo.dev/v2/feedback/docs-send -H 'Content-Type: application/json' -d '{"url":"/versions/v57.0.0/sdk/ui/drop-in-replacements/maskedview/","feedback":"🤖 Agent feedback for docs: <specific, actionable description> (<model>, <harness>)"}'

Only submit when you have something specific and actionable to report. Try to give the most context.

## Navigation

When answering a related or follow-up question, fetch the relevant page below as Markdown (.md) instead of guessing; use llms.txt for the full map.

You are here: Reference (v57.0.0) > Expo UI > Drop-in replacements
Pages in this section:
- [Overview](https://docs.expo.dev/versions/v57.0.0/sdk/ui/drop-in-replacements.md)
- [BottomSheet](https://docs.expo.dev/versions/v57.0.0/sdk/ui/drop-in-replacements/bottomsheet.md)
- [DateTimePicker](https://docs.expo.dev/versions/v57.0.0/sdk/ui/drop-in-replacements/datetimepicker.md)
- [MaskedView](https://docs.expo.dev/versions/v57.0.0/sdk/ui/drop-in-replacements/maskedview.md) (this page)
- [Menu](https://docs.expo.dev/versions/v57.0.0/sdk/ui/drop-in-replacements/menu.md)
- [PagerView](https://docs.expo.dev/versions/v57.0.0/sdk/ui/drop-in-replacements/pagerview.md)
- [Picker](https://docs.expo.dev/versions/v57.0.0/sdk/ui/drop-in-replacements/picker.md)
- [SegmentedControl](https://docs.expo.dev/versions/v57.0.0/sdk/ui/drop-in-replacements/segmentedcontrol.md)
- [Slider](https://docs.expo.dev/versions/v57.0.0/sdk/ui/drop-in-replacements/slider.md)
Full documentation tree: [llms.txt](https://docs.expo.dev/llms.txt)

</AgentInstructions>
Android, iOS

A `MaskedView` component with an API compatible with `@react-native-masked-view/masked-view`. The opaque pixels of `maskElement` reveal the masked content behind it; transparent pixels hide it.

Under the hood this component bridges arbitrary React Native children into the platform-specific `@expo/ui` masking primitives:

-   **Android**: Jetpack Compose graphics layer compositing with `BlendMode.DstIn`.
-   **iOS**: SwiftUI [`.mask`](https://developer.apple.com/documentation/swiftui/view/mask\(alignment:_:\)) modifier.

Image: The word EXPO filled with a rainbow gradient

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

## Migrating from `@react-native-masked-view/masked-view`

-   Update the import from `import MaskedView from '@react-native-masked-view/masked-view'` to `import { MaskedView } from '@expo/ui/community/masked-view'`.
-   The `androidRenderingMode` prop is not supported. The Compose-based implementation always uses an offscreen graphics layer, so the prop has no equivalent and is omitted from the public types.
-   Web is not implemented. On web, children render unmasked and a one-time console warning is logged. For web targets, prefer the CSS primitive that fits your specific case:
    -   **Gradient text** — `background-clip: text` with `color: 'transparent'` and a CSS gradient/image as the background.
    -   **Alpha fade** — `mask-image: linear-gradient(...)` (or `WebkitMaskImage`) directly on the content view.
    -   **Shape mask** (circle, rounded rectangle, and so on) — `clip-path: circle(...)` / `inset(...)` / `path(...)`, or `border-radius` + `overflow: 'hidden'`.

## Android screen capture

On Android, native screenshot and session replay integrations must capture `MaskedView` on the [UI thread](https://developer.android.com/topic/performance/threads#main). Drawing its Jetpack Compose layout from a background thread can crash the app with `IllegalArgumentException: Detected multithreaded access to SnapshotStateObserver`. Image processing and encoding can run on a background thread.

## Basic usage

```tsx MaskedViewExample.tsx
import { MaskedView } from '@expo/ui/community/masked-view';
import { StyleSheet, Text, View } from 'react-native';

export default function MaskedViewExample() {
  return (
    <MaskedView
      style={{ width: 300, height: 80 }}
      maskElement={
        <View style={{ flex: 1, alignItems: 'center', justifyContent: 'center' }}>
          <Text style={{ fontSize: 64, fontWeight: 'bold' }}>EXPO</Text>
        </View>
      }>
      <View
        style={[
          StyleSheet.absoluteFill,
          {
            experimental_backgroundImage:
              'linear-gradient(135deg, #FF3B30, #FF9500, #FFCC00, #34C759, #007AFF, #AF52DE)',
          },
        ]}
      />
    </MaskedView>
  );
}
```

## Alpha-fade mask

Only the alpha channel of the `maskElement` matters: opaque pixels reveal content, transparent pixels hide it. Use a `LinearGradient` (from `expo-linear-gradient`) that goes from opaque to transparent — `'black'` (for example) to `'transparent'` below — to fade content out along an axis.

```tsx AlphaFadeExample.tsx
import { MaskedView } from '@expo/ui/community/masked-view';
import { LinearGradient } from 'expo-linear-gradient';
import { StyleSheet, View } from 'react-native';

export default function AlphaFadeExample() {
  return (
    <MaskedView
      style={{ width: 300, height: 80, flexDirection: 'row' }}
      maskElement={
        <LinearGradient
          colors={['black', 'transparent']}
          start={{ x: 0, y: 0 }}
          end={{ x: 1, y: 0 }}
          style={StyleSheet.absoluteFill}
        />
      }>
      <View style={{ flex: 1, backgroundColor: '#3D5A80' }} />
      <View style={{ flex: 1, backgroundColor: '#DAA520' }} />
      <View style={{ flex: 1, backgroundColor: '#E07A5F' }} />
    </MaskedView>
  );
}
```

## API

```tsx
import { MaskedView } from '@expo/ui/community/masked-view';
```

## Component

### `MaskedView`

Supported platforms: Android, iOS.

Type: React.[Element](https://www.typescriptlang.org/docs/handbook/jsx.html#function-component)<[MaskedViewProps](https://docs.expo.dev/versions/v57.0.0/sdk/ui/drop-in-replacements/maskedview.md#maskedviewprops)\>

Renders `children` with the alpha channel of `maskElement` applied as a mask: opaque pixels of `maskElement` reveal `children`, transparent pixels hide them.

API-compatible with `@react-native-masked-view/masked-view`.

Drop-in props for `@react-native-masked-view/masked-view`'s `MaskedView`.

> **See:** [https://github.com/callstack/masked-view](https://github.com/callstack/masked-view)

MaskedViewProps

### `children`

Supported platforms: Android, iOS.

Optional • Type: [ReactNode](https://reactnative.dev/docs/react-node)

Content rendered behind the mask.

### `maskElement`

Supported platforms: Android, iOS.

Type: `ReactElement`

The element used as the mask. Only opaque pixels of `maskElement` make the masked content visible — transparent pixels hide it.

#### Inherited props

-   [ViewProps](https://reactnative.dev/docs/view#props)
