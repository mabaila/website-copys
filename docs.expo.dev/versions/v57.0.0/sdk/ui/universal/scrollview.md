---
modificationDate: September 06, 2026
title: ScrollView
description: A scrollable container that supports vertical or horizontal scrolling.
sourceCodeUrl: 'https://github.com/expo/expo/tree/sdk-57/packages/expo-ui'
packageName: '@expo/ui'
platforms: ['android', 'ios', 'web', 'expo-go']
---

This documentation is available as Markdown for AI agents and LLMs. See the [full Markdown index](https://docs.expo.dev/llms.txt) or append .md to any documentation URL.

# ScrollView

A scrollable container that supports vertical or horizontal scrolling.

<AgentInstructions>

## Submitting Feedback

If you encounter errors, misleading or outdated information, report it so Expo can be improved:

Preferred command:
npx --yes submit-expo-feedback@latest --category docs --subject "/versions/v57.0.0/sdk/ui/universal/scrollview/" "<actionable feedback>"

Direct HTTP fallback:
curl -X POST https://api.expo.dev/v2/feedback/docs-send -H 'Content-Type: application/json' -d '{"url":"/versions/v57.0.0/sdk/ui/universal/scrollview/","feedback":"🤖 Agent feedback for docs: <specific, actionable description> (<model>, <harness>)"}'

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
- [RNHostView](https://docs.expo.dev/versions/v57.0.0/sdk/ui/universal/rnhostview.md)
- [Row](https://docs.expo.dev/versions/v57.0.0/sdk/ui/universal/row.md)
- [ScrollView](https://docs.expo.dev/versions/v57.0.0/sdk/ui/universal/scrollview.md) (this page)
- [Slider](https://docs.expo.dev/versions/v57.0.0/sdk/ui/universal/slider.md)
- [Spacer](https://docs.expo.dev/versions/v57.0.0/sdk/ui/universal/spacer.md)
- [Switch](https://docs.expo.dev/versions/v57.0.0/sdk/ui/universal/switch.md)
- [Text](https://docs.expo.dev/versions/v57.0.0/sdk/ui/universal/text.md)
- [TextInput](https://docs.expo.dev/versions/v57.0.0/sdk/ui/universal/textinput.md)
Full documentation tree: [llms.txt](https://docs.expo.dev/llms.txt)

</AgentInstructions>
Android, iOS, Web, Included in Expo Go

A scrollable container, defaulting to vertical scrolling. Use [`direction="horizontal"`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/universal/scrollview.md#direction) for horizontal lists.

## Native implementations

| Platform | Backing component |
| --- | --- |
| Android | A Jetpack Compose `Column` or `Row` with the [`verticalScroll` or `horizontalScroll` modifier](https://developer.android.com/develop/ui/compose/touch-input/pointer-input/scroll#scroll-modifiers). This implementation renders all children and is not a lazy container. |
| iOS | SwiftUI [`ScrollView`](https://developer.apple.com/documentation/swiftui/scrollview). |
| Web | React Native [`ScrollView`](https://reactnative.dev/docs/scrollview). |

Image: A vertical list of six items inside a scroll view

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

### Vertical scrolling

```tsx VerticalScrollViewExample.tsx
import { useColorScheme } from 'react-native';
import { Host, ScrollView, Column, Text } from '@expo/ui';

export default function VerticalScrollViewExample() {
  const colorScheme = useColorScheme();
  const ink = { color: colorScheme === 'dark' ? '#FFFFFF' : '#000000' };

  return (
    <Host style={{ flex: 1 }}>
      <ScrollView>
        <Column spacing={8}>
          {Array.from({ length: 30 }).map((_, i) => (
            <Text key={i} textStyle={ink}>
              {`Row ${i + 1}`}
            </Text>
          ))}
        </Column>
      </ScrollView>
    </Host>
  );
}
```

### Horizontal scrolling

```tsx HorizontalScrollViewExample.tsx
import { useColorScheme } from 'react-native';
import { Host, ScrollView, Row, Text } from '@expo/ui';

export default function HorizontalScrollViewExample() {
  const colorScheme = useColorScheme();
  const ink = { color: colorScheme === 'dark' ? '#FFFFFF' : '#000000' };

  return (
    <Host matchContents={{ vertical: true }} style={{ width: '100%' }}>
      <ScrollView direction="horizontal">
        <Row spacing={12}>
          {Array.from({ length: 20 }).map((_, i) => (
            <Text key={i} textStyle={ink}>
              {`Item ${i + 1}`}
            </Text>
          ))}
        </Row>
      </ScrollView>
    </Host>
  );
}
```

## API

```tsx
import { ScrollView } from '@expo/ui';
```

## Component

### `ScrollView`

Supported platforms: Android, iOS, Web.

Type: React.[Element](https://www.typescriptlang.org/docs/handbook/jsx.html#function-component)<[ScrollViewProps](https://docs.expo.dev/versions/v57.0.0/sdk/ui/universal/scrollview.md#scrollviewprops)\>

A scrollable container that supports vertical or horizontal scrolling.

Props for the [`ScrollView`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/universal/scrollview.md#scrollview) component.

ScrollViewProps

### `children`

Supported platforms: Android, iOS, Web.

Optional • Type: [ReactNode](https://reactnative.dev/docs/react-node)

Content to render inside the scroll view.

### `direction`

Supported platforms: Android, iOS, Web.

Optional • Literal type: `string` • Default: `'vertical'`

Scroll direction.

Acceptable values are: `'vertical'` | `'horizontal'`

### `disabled`

Supported platforms: Android, iOS, Web.

Optional • Type: `boolean`

Whether the component is disabled. Disabled components do not respond to user interaction.

### `hidden`

Supported platforms: Android, iOS, Web.

Optional • Type: `boolean`

Whether the component is hidden.

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

### `showsIndicators`

Supported platforms: iOS, Web.

Optional • Type: `boolean` • Default: `true`

Whether to show scroll indicators.

### `style`

Supported platforms: Android, iOS, Web.

Optional • Type: [Pick](https://www.typescriptlang.org/docs/handbook/utility-types.html#picktype-keys)<[ViewStyle](https://reactnative.dev/docs/view-style-props), 'padding' | 'paddingHorizontal' | 'paddingVertical' | 'paddingTop' | 'paddingBottom' | 'paddingLeft' | 'paddingRight' | 'backgroundColor' | 'borderRadius' | 'borderWidth' | 'borderColor' | 'opacity' | 'width' | 'height'\>

Platform-agnostic style properties. These are translated to SwiftUI modifiers on iOS and Jetpack Compose modifiers on Android.

### `testID`

Supported platforms: Android, iOS, Web.

Optional • Type: `string`

Identifier used to locate the component in end-to-end tests.
