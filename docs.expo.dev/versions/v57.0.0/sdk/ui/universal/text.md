---
modificationDate: August 21, 2026
title: Text
description: A component for displaying styled text content.
sourceCodeUrl: 'https://github.com/expo/expo/tree/sdk-57/packages/expo-ui'
packageName: '@expo/ui'
platforms: ['android', 'ios', 'web', 'expo-go']
---

This documentation is available as Markdown for AI agents and LLMs. See the [full Markdown index](https://docs.expo.dev/llms.txt) or append .md to any documentation URL.

# Text

A component for displaying styled text content.

<AgentInstructions>

## Submitting Feedback

If you encounter errors, misleading or outdated information, report it so Expo can be improved:

Preferred command:
npx --yes submit-expo-feedback@latest --category docs --subject "/versions/v57.0.0/sdk/ui/universal/text/" "<actionable feedback>"

Direct HTTP fallback:
curl -X POST https://api.expo.dev/v2/feedback/docs-send -H 'Content-Type: application/json' -d '{"url":"/versions/v57.0.0/sdk/ui/universal/text/","feedback":"🤖 Agent feedback for docs: <specific, actionable description> (<model>, <harness>)"}'

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
- [ScrollView](https://docs.expo.dev/versions/v57.0.0/sdk/ui/universal/scrollview.md)
- [Slider](https://docs.expo.dev/versions/v57.0.0/sdk/ui/universal/slider.md)
- [Spacer](https://docs.expo.dev/versions/v57.0.0/sdk/ui/universal/spacer.md)
- [Switch](https://docs.expo.dev/versions/v57.0.0/sdk/ui/universal/switch.md)
- [Text](https://docs.expo.dev/versions/v57.0.0/sdk/ui/universal/text.md) (this page)
- [TextInput](https://docs.expo.dev/versions/v57.0.0/sdk/ui/universal/textinput.md)
Full documentation tree: [llms.txt](https://docs.expo.dev/llms.txt)

</AgentInstructions>
Android, iOS, Web, Included in Expo Go

A component for displaying text. Adapts to the platform color scheme (light/dark) by default and exposes a focused subset of typography knobs through [`textStyle`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/universal/text.md#textstyle).

Image: Material 3 typography hierarchy: headline, title, body, and label

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

### Basic text

```tsx TextExample.tsx
import { useColorScheme } from 'react-native';
import { Host, Text } from '@expo/ui';

export default function TextExample() {
  const colorScheme = useColorScheme();

  return (
    <Host matchContents>
      <Text textStyle={{ color: colorScheme === 'dark' ? '#FFFFFF' : '#000000' }}>
        Hello, world!
      </Text>
    </Host>
  );
}
```

### Styled text

Use [`textStyle`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/universal/text.md#textstyle) for typography-specific properties (font size, weight, alignment).

```tsx StyledTextExample.tsx
import { useColorScheme } from 'react-native';
import { Host, Text } from '@expo/ui';

export default function StyledTextExample() {
  const colorScheme = useColorScheme();

  return (
    <Host matchContents>
      <Text
        textStyle={{
          color: colorScheme === 'dark' ? '#FFFFFF' : '#000000',
          fontSize: 24,
          fontWeight: '700',
          textAlign: 'center',
        }}>
        Headline
      </Text>
    </Host>
  );
}
```

### Truncating long text

Use [`numberOfLines`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/universal/text.md#numberoflines) to clamp long text with a trailing ellipsis.

```tsx TruncatedTextExample.tsx
import { useColorScheme } from 'react-native';
import { Host, Text } from '@expo/ui';

export default function TruncatedTextExample() {
  const colorScheme = useColorScheme();

  return (
    <Host matchContents={{ vertical: true }} style={{ width: '100%' }}>
      <Text numberOfLines={1} textStyle={{ color: colorScheme === 'dark' ? '#FFFFFF' : '#000000' }}>
        A very long line of text that will be truncated when it does not fit on a single line.
      </Text>
    </Host>
  );
}
```

## API

```tsx
import { Text } from '@expo/ui';
```

## Component

### `Text`

Supported platforms: Android, iOS, Web.

Type: React.[Element](https://www.typescriptlang.org/docs/handbook/jsx.html#function-component)<[TextProps](https://reactnative.dev/docs/text#props)\>

A component for displaying styled text content.

Props for the [`Text`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/universal/text.md#text) component.

TextProps

### `children`

Supported platforms: Android, iOS, Web.

Optional • Type: `string`

The text content to display.

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

### `numberOfLines`

Supported platforms: Android, iOS, Web.

Optional • Type: `number`

Maximum number of lines to display. Text is truncated with an ellipsis when exceeded.

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

### `textStyle`

Supported platforms: Android, iOS, Web.

Optional • Type: `{ color: string, fontFamily: string, fontSize: number, fontWeight: 'normal' | 'bold' | '100' | '200' | '300' | '400' | '500' | '600' | '700' | '800' | '900', letterSpacing: number, lineHeight: number, textAlign: 'center' | 'left' | 'right' }`

Text-specific styling (font, color, alignment).
