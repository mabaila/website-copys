---
modificationDate: August 21, 2026
title: BottomSheet
description: A modal sheet that slides up from the bottom of the screen.
sourceCodeUrl: 'https://github.com/expo/expo/tree/sdk-57/packages/expo-ui'
packageName: '@expo/ui'
platforms: ['android', 'ios', 'web', 'expo-go']
---

This documentation is available as Markdown for AI agents and LLMs. See the [full Markdown index](https://docs.expo.dev/llms.txt) or append .md to any documentation URL.

# BottomSheet

A modal sheet that slides up from the bottom of the screen.

<AgentInstructions>

## Submitting Feedback

If you encounter errors, misleading or outdated information, report it so Expo can be improved:

Preferred command:
npx --yes submit-expo-feedback@latest --category docs --subject "/versions/v57.0.0/sdk/ui/universal/bottomsheet/" "<actionable feedback>"

Direct HTTP fallback:
curl -X POST https://api.expo.dev/v2/feedback/docs-send -H 'Content-Type: application/json' -d '{"url":"/versions/v57.0.0/sdk/ui/universal/bottomsheet/","feedback":"🤖 Agent feedback for docs: <specific, actionable description> (<model>, <harness>)"}'

Only submit when you have something specific and actionable to report. Try to give the most context.

## Navigation

When answering a related or follow-up question, fetch the relevant page below as Markdown (.md) instead of guessing; use llms.txt for the full map.

You are here: Reference (v57.0.0) > Expo UI > Universal
Pages in this section:
- [Overview](https://docs.expo.dev/versions/v57.0.0/sdk/ui/universal.md)
- [BottomSheet](https://docs.expo.dev/versions/v57.0.0/sdk/ui/universal/bottomsheet.md) (this page)
- [Button](https://docs.expo.dev/versions/v57.0.0/sdk/ui/universal/button.md)
- [Checkbox](https://docs.expo.dev/versions/v57.0.0/sdk/ui/universal/checkbox.md)
- [Collapsible](https://docs.expo.dev/versions/v57.0.0/sdk/ui/universal/collapsible.md)
- [Column](https://docs.expo.dev/versions/v57.0.0/sdk/ui/universal/column.md)
- [FieldGroup](https://docs.expo.dev/versions/v57.0.0/sdk/ui/universal/fieldgroup.md)
- [Host](https://docs.expo.dev/versions/v57.0.0/sdk/ui/universal/host.md)
- [Icon](https://docs.expo.dev/versions/v57.0.0/sdk/ui/universal/icon.md)
- [List](https://docs.expo.dev/versions/v57.0.0/sdk/ui/universal/list.md)
- [Picker](https://docs.expo.dev/versions/v57.0.0/sdk/ui/universal/picker.md)
- [RNHostView](https://docs.expo.dev/versions/v57.0.0/sdk/ui/universal/rnhostview.md)
- [Row](https://docs.expo.dev/versions/v57.0.0/sdk/ui/universal/row.md)
- [ScrollView](https://docs.expo.dev/versions/v57.0.0/sdk/ui/universal/scrollview.md)
- [Slider](https://docs.expo.dev/versions/v57.0.0/sdk/ui/universal/slider.md)
- [Spacer](https://docs.expo.dev/versions/v57.0.0/sdk/ui/universal/spacer.md)
- [Switch](https://docs.expo.dev/versions/v57.0.0/sdk/ui/universal/switch.md)
- [Text](https://docs.expo.dev/versions/v57.0.0/sdk/ui/universal/text.md)
- [TextInput](https://docs.expo.dev/versions/v57.0.0/sdk/ui/universal/textinput.md)
Full documentation tree: [llms.txt](https://docs.expo.dev/llms.txt)

</AgentInstructions>
Android, iOS, Web, Included in Expo Go

A modal sheet that slides up from the bottom of the screen. The sheet's visibility is controlled — toggle [`isPresented`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/universal/bottomsheet.md#ispresented) from React state and dismiss it from [`onDismiss`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/universal/bottomsheet.md#ondismiss) (called when the user swipes down or taps the overlay).

Image: Modal bottom sheet with title, description, and action buttons

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

### Basic bottom sheet

```tsx BottomSheetExample.tsx
import { useState } from 'react';
import { useColorScheme } from 'react-native';
import { Host, Column, Button, BottomSheet, Text } from '@expo/ui';

export default function BottomSheetExample() {
  const [isPresented, setIsPresented] = useState(false);
  const colorScheme = useColorScheme();
  const ink = { color: colorScheme === 'dark' ? '#FFFFFF' : '#000000' };

  return (
    <>
      <Host matchContents>
        <Button label="Open sheet" onPress={() => setIsPresented(true)} />
      </Host>
      <BottomSheet isPresented={isPresented} onDismiss={() => setIsPresented(false)}>
        <Column spacing={12}>
          <Text textStyle={{ ...ink, fontSize: 18, fontWeight: '700' }}>Sheet contents</Text>
          <Text textStyle={ink}>Drag down or tap the overlay to dismiss.</Text>
          <Button label="Close" onPress={() => setIsPresented(false)} />
        </Column>
      </BottomSheet>
    </>
  );
}
```

### Hiding the drag indicator

Pass [`showDragIndicator={false}`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/universal/bottomsheet.md#showdragindicator) for sheets without a handle.

```tsx BottomSheetNoIndicatorExample.tsx
import { useState } from 'react';
import { useColorScheme } from 'react-native';
import { Host, Button, BottomSheet, Text } from '@expo/ui';

export default function BottomSheetNoIndicatorExample() {
  const [isPresented, setIsPresented] = useState(false);
  const colorScheme = useColorScheme();
  const ink = { color: colorScheme === 'dark' ? '#FFFFFF' : '#000000' };

  return (
    <>
      <Host matchContents>
        <Button label="Open" onPress={() => setIsPresented(true)} />
      </Host>
      <BottomSheet
        isPresented={isPresented}
        onDismiss={() => setIsPresented(false)}
        showDragIndicator={false}>
        <Text textStyle={ink}>No drag handle.</Text>
      </BottomSheet>
    </>
  );
}
```

### Snap points

Pass [`snapPoints`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/universal/bottomsheet.md#snappoints) to let the user drag the sheet between multiple resting heights. You can use the semantic values `'half'` and `'full'` for cross-platform parity. The `{ fraction }` and `{ height }` forms are honored precisely on iOS and web.

When sheet content can be taller than the smallest snap point, wrap it in a `ScrollView` so the overflow scrolls correctly.

```tsx BottomSheetSnapPointsExample.tsx
import { useState } from 'react';
import { useColorScheme } from 'react-native';
import { Host, BottomSheet, Button, Column, ScrollView, Text } from '@expo/ui';

export default function BottomSheetSnapPointsExample() {
  const [isPresented, setIsPresented] = useState(false);
  const colorScheme = useColorScheme();
  const ink = { color: colorScheme === 'dark' ? '#FFFFFF' : '#000000' };

  return (
    <>
      <Host matchContents>
        <Button label="Open" onPress={() => setIsPresented(true)} />
      </Host>
      <BottomSheet
        isPresented={isPresented}
        onDismiss={() => setIsPresented(false)}
        snapPoints={['half', 'full']}>
        <ScrollView>
          <Column spacing={12}>
            <Text textStyle={{ ...ink, fontSize: 20, fontWeight: '700' }}>Half / full sheet</Text>
            <Text textStyle={ink}>Drag the sheet between half and full screen height.</Text>
          </Column>
        </ScrollView>
      </BottomSheet>
    </>
  );
}
```

> On Android, `{ fraction }` and `{ height }` snap to the nearest of `'half'` / `'full'` — the underlying `ModalBottomSheet` only supports two resting states. The partial state is only visible when content is tall enough to exceed Material's partial threshold; give the content an explicit height or fill the available space if you need the half state on short content.

## API

```tsx
import { BottomSheet } from '@expo/ui';
```

## Component

### `BottomSheet`

Supported platforms: Android, iOS, Web.

Type: React.[Element](https://www.typescriptlang.org/docs/handbook/jsx.html#function-component)<[BottomSheetProps](https://docs.expo.dev/versions/v57.0.0/sdk/ui/universal/bottomsheet.md#bottomsheetprops)\>

A modal sheet that slides up from the bottom of the screen.

Props for the [`BottomSheet`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/universal/bottomsheet.md#bottomsheet) component, a modal sheet that slides up from the bottom of the screen.

BottomSheetProps

### `children`

Supported platforms: Android, iOS, Web.

Optional • Type: [ReactNode](https://reactnative.dev/docs/react-node)

Content to render inside the bottom sheet.

### `isPresented`

Supported platforms: Android, iOS, Web.

Type: `boolean`

Whether the bottom sheet is currently visible.

### `modifiers`

Supported platforms: Android, iOS, Web.

Optional • Type: `ModifierConfig[]`

Platform-specific modifier escape hatch. Pass an array of modifier configs from `@expo/ui/swift-ui/modifiers` or `@expo/ui/jetpack-compose/modifiers`.

### `onDismiss`

Supported platforms: Android, iOS, Web.

Type: `() => void`

Called when the bottom sheet is dismissed by the user (e.g. swiping down or tapping the overlay).

### `showDragIndicator`

Supported platforms: Android, iOS, Web.

Optional • Type: `boolean` • Default: `true`

Whether to show a drag indicator at the top of the sheet.

### `snapPoints`

Supported platforms: Android, iOS, Web.

Optional • Type: [SnapPoint[]](https://docs.expo.dev/versions/v57.0.0/sdk/ui/universal/bottomsheet.md#snappoint)

Heights the sheet can rest at. When omitted, the sheet auto-sizes to its content. See [`SnapPoint`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/universal/bottomsheet.md#snappoint) for the supported values.

Example

\`\`['half', 'full'] `— draggable between half and full`

Example

\`\`['full'] `— always full height`

### `testID`

Supported platforms: Android, iOS, Web.

Optional • Type: `string`

Identifier used to locate the component in end-to-end tests.

## Types

### `SnapPoint`

Supported platforms: Android, iOS, Web.

A snap point describing one of the heights a [`BottomSheet`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/universal/bottomsheet.md#bottomsheet) can rest at.

-   `'half'` — Approximately half-screen.
-   `'full'` — Fully expanded.
-   `{ fraction }` — A fraction of the screen height (0–1). iOS / web only.
-   `{ height }` — A fixed pixel height. iOS / web only.

On Android, `{ fraction }` and `{ height }` snap to the nearest of `'half'` / `'full'`. See the component docs for platform behavior notes.

Type: `'half'` or `'full'` or `object` shaped as below:

| Property | Type | Description |
| --- | --- | --- |
| fraction | `number` | - |

Or `object` shaped as below:

| Property | Type | Description |
| --- | --- | --- |
| height | `number` | - |
