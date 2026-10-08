---
modificationDate: August 31, 2026
title: RNHostView
description: A cross-platform component for hosting React Native views inside @expo/ui views.
sourceCodeUrl: 'https://github.com/expo/expo/tree/sdk-57/packages/expo-ui'
packageName: '@expo/ui'
platforms: ['android', 'ios', 'web', 'expo-go']
---

This documentation is available as Markdown for AI agents and LLMs. See the [full Markdown index](https://docs.expo.dev/llms.txt) or append .md to any documentation URL.

# RNHostView

A cross-platform component for hosting React Native views inside @expo/ui views.

<AgentInstructions>

## Submitting Feedback

If you encounter errors, misleading or outdated information, report it so Expo can be improved:

Preferred command:
npx --yes submit-expo-feedback@latest --category docs --subject "/versions/v57.0.0/sdk/ui/universal/rnhostview/" "<actionable feedback>"

Direct HTTP fallback:
curl -X POST https://api.expo.dev/v2/feedback/docs-send -H 'Content-Type: application/json' -d '{"url":"/versions/v57.0.0/sdk/ui/universal/rnhostview/","feedback":"🤖 Agent feedback for docs: <specific, actionable description> (<model>, <harness>)"}'

Only submit when you have something specific and actionable to report. Try to give the most context.

## Navigation

When answering a related or follow-up question, fetch the relevant page below as Markdown (.md) instead of guessing; use llms.txt for the full map.

You are here: Reference (v57.0.0) > Expo UI > Universal
Pages in this section:
- [Overview](https://docs.expo.dev/versions/v57.0.0/sdk/ui/universal.md)
- [BottomSheet](https://docs.expo.dev/versions/v57.0.0/sdk/ui/universal/bottomsheet.md)
- [Button](https://docs.expo.dev/versions/v57.0.0/sdk/ui/universal/button.md)
- [Checkbox](https://docs.expo.dev/versions/v57.0.0/sdk/ui/universal/checkbox.md)
- [Collapsible](https://docs.expo.dev/versions/v57.0.0/sdk/ui/universal/collapsible.md)
- [Column](https://docs.expo.dev/versions/v57.0.0/sdk/ui/universal/column.md)
- [FieldGroup](https://docs.expo.dev/versions/v57.0.0/sdk/ui/universal/fieldgroup.md)
- [Host](https://docs.expo.dev/versions/v57.0.0/sdk/ui/universal/host.md)
- [Icon](https://docs.expo.dev/versions/v57.0.0/sdk/ui/universal/icon.md)
- [List](https://docs.expo.dev/versions/v57.0.0/sdk/ui/universal/list.md)
- [Picker](https://docs.expo.dev/versions/v57.0.0/sdk/ui/universal/picker.md)
- [RNHostView](https://docs.expo.dev/versions/v57.0.0/sdk/ui/universal/rnhostview.md) (this page)
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

Hosts a React Native view subtree inside a universal `@expo/ui` layout. On Android and iOS, it re-exports the platform-native [`RNHostView` for Jetpack Compose](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/rnhostview.md)/[`RNHostView` for SwiftUI](https://docs.expo.dev/versions/v57.0.0/sdk/ui/swift-ui/rnhostview.md), so React Native children bridge into the surrounding Compose/SwiftUI tree. On web, there is no native host tree to bridge into, so it falls back to a React Native [`View`](https://reactnative.dev/docs/view) that wraps the children.

> **Note:** Pass a single React Native element as the child. `RNHostView` measures and lays out only its first child, so wrap several views in one parent `View` and let that view arrange them.

Image: A bold label above a purple React Native chip

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

### Basic usage

Place a React Native view subtree anywhere inside a universal `@expo/ui` layout.

```tsx RNHostViewExample.tsx
import { Host, Column, RNHostView, Text } from '@expo/ui';
import { Text as RNText, View, useColorScheme } from 'react-native';

export default function RNHostViewExample() {
  const colorScheme = useColorScheme();

  return (
    <Host matchContents>
      <Column spacing={12} style={{ padding: 16 }}>
        <Text
          textStyle={{ color: colorScheme === 'dark' ? '#FFFFFF' : '#000000', fontWeight: 'bold' }}>
          Native UI label
        </Text>
        <RNHostView matchContents>
          <View
            style={{
              alignSelf: 'flex-start',
              padding: 16,
              backgroundColor: '#9B59B6',
              borderRadius: 10,
            }}>
            <RNText style={{ color: 'white' }}>Plain React Native content</RNText>
          </View>
        </RNHostView>
      </Column>
    </Host>
  );
}
```

### Fill parent vs. match child

By default `RNHostView` fills its native parent. Set `matchContents` to have it shrink to fit its React Native children instead.

```tsx RNHostViewSizingExample.tsx
import { Host, Column, Row, Text, RNHostView } from '@expo/ui';
import { View, useColorScheme } from 'react-native';

export default function RNHostViewSizingExample() {
  const colorScheme = useColorScheme();
  const ink = { color: colorScheme === 'dark' ? '#FFFFFF' : '#000000' };

  return (
    <Host matchContents>
      <Column spacing={24} style={{ padding: 16 }}>
        <Column spacing={8}>
          <Text textStyle={{ ...ink, fontSize: 18, fontWeight: 'bold' }}>Fill parent size</Text>
          <Text textStyle={{ fontSize: 12, color: '#666666' }}>
            The RNHostView fills the native parent's 100×100 frame.
          </Text>
          <Row style={{ width: 100, height: 100 }}>
            <RNHostView>
              <View style={{ flex: 1, backgroundColor: '#9B59B6', borderRadius: 10, margin: 4 }} />
            </RNHostView>
          </Row>
        </Column>

        <Column spacing={8}>
          <Text textStyle={{ ...ink, fontSize: 18, fontWeight: 'bold' }}>Match child size</Text>
          <Text textStyle={{ fontSize: 12, color: '#666666' }}>
            The RNHostView shrinks to wrap its 50×50 child.
          </Text>
          <Row style={{ padding: 8 }}>
            <RNHostView matchContents>
              <View
                style={{ width: 50, height: 50, backgroundColor: '#9B59B6', borderRadius: 10 }}
              />
            </RNHostView>
          </Row>
        </Column>
      </Column>
    </Host>
  );
}
```

## API

```tsx
import { RNHostView } from '@expo/ui';
```

## Component

### `RNHostView`

Supported platforms: Android, iOS, Web.

Type: React.[Element](https://www.typescriptlang.org/docs/handbook/jsx.html#function-component)<[RNHostViewProps](https://docs.expo.dev/versions/v57.0.0/sdk/ui/universal/rnhostview.md#rnhostviewprops)\>

Hosts React Native views inside Jetpack Compose or SwiftUI views.

Props for the [`RNHostView`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/universal/rnhostview.md#rnhostview) component.

RNHostViewProps

### `children`

Supported platforms: Android, iOS, Web.

Type: `ReactElement`

The React Native view to host.

### `disabled`

Supported platforms: Android, iOS, Web.

Optional • Type: `boolean`

Whether the component is disabled. Disabled components do not respond to user interaction.

### `hidden`

Supported platforms: Android, iOS, Web.

Optional • Type: `boolean`

Whether the component is hidden.

### `matchContents`

Supported platforms: Android, iOS.

Optional • Type: `boolean` • Default: `false`

When `true`, the host updates its size in the native view tree to match the children's size. When `false`, the host uses the size of the parent native view.

Can only be set once on mount; changing it remounts the component.

### `modifiers`

Supported platforms: Android, iOS.

Optional • Type: `ModifierConfig[]`

Platform-specific modifier escape hatch. Pass an array of modifier configs from `@expo/ui/swift-ui/modifiers` or `@expo/ui/jetpack-compose/modifiers`. A modifier supplied here replaces any modifier of the same type that the component derives from `style` or other props.

### `onAppear`

Supported platforms: Android, iOS, Web.

Optional • Type: `() => void`

Called when the component appears on screen.

### `onDisappear`

Supported platforms: Android, iOS, Web.

Optional • Type: `() => void`

Called when the component is removed from screen.

### `onPress`

Supported platforms: Android, iOS, Web.

Optional • Type: `() => void`

Called when the component is pressed.

### `style`

Supported platforms: Android, iOS, Web.

Optional • Type: [Pick](https://www.typescriptlang.org/docs/handbook/utility-types.html#picktype-keys)<[ViewStyle](https://reactnative.dev/docs/view-style-props), 'padding' | 'paddingHorizontal' | 'paddingVertical' | 'paddingTop' | 'paddingBottom' | 'paddingLeft' | 'paddingRight' | 'backgroundColor' | 'borderRadius' | 'borderWidth' | 'borderColor' | 'opacity' | 'width' | 'height'\>

Platform-agnostic style properties. These are translated to SwiftUI modifiers on iOS and Jetpack Compose modifiers on Android.

### `testID`

Supported platforms: Android, iOS, Web.

Optional • Type: `string`

Identifier used to locate the component in end-to-end tests.
