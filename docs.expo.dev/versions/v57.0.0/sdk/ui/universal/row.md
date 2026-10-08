---
modificationDate: August 21, 2026
title: Row
description: A horizontal layout container for universal @expo/ui components.
sourceCodeUrl: 'https://github.com/expo/expo/tree/sdk-57/packages/expo-ui'
packageName: '@expo/ui'
platforms: ['android', 'ios', 'web', 'expo-go']
---

This documentation is available as Markdown for AI agents and LLMs. See the [full Markdown index](https://docs.expo.dev/llms.txt) or append .md to any documentation URL.

# Row

A horizontal layout container for universal @expo/ui components.

<AgentInstructions>

## Submitting Feedback

If you encounter errors, misleading or outdated information, report it so Expo can be improved:

Preferred command:
npx --yes submit-expo-feedback@latest --category docs --subject "/versions/v57.0.0/sdk/ui/universal/row/" "<actionable feedback>"

Direct HTTP fallback:
curl -X POST https://api.expo.dev/v2/feedback/docs-send -H 'Content-Type: application/json' -d '{"url":"/versions/v57.0.0/sdk/ui/universal/row/","feedback":"🤖 Agent feedback for docs: <specific, actionable description> (<model>, <harness>)"}'

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
- [Row](https://docs.expo.dev/versions/v57.0.0/sdk/ui/universal/row.md) (this page)
- [ScrollView](https://docs.expo.dev/versions/v57.0.0/sdk/ui/universal/scrollview.md)
- [Slider](https://docs.expo.dev/versions/v57.0.0/sdk/ui/universal/slider.md)
- [Spacer](https://docs.expo.dev/versions/v57.0.0/sdk/ui/universal/spacer.md)
- [Switch](https://docs.expo.dev/versions/v57.0.0/sdk/ui/universal/switch.md)
- [Text](https://docs.expo.dev/versions/v57.0.0/sdk/ui/universal/text.md)
- [TextInput](https://docs.expo.dev/versions/v57.0.0/sdk/ui/universal/textinput.md)
Full documentation tree: [llms.txt](https://docs.expo.dev/llms.txt)

</AgentInstructions>
Android, iOS, Web, Included in Expo Go

A horizontal layout container that arranges its children from start to end. Delegates to Jetpack Compose's [`Row`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/row.md) on Android, SwiftUI's [`HStack`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/swift-ui/hstack.md) on iOS, and a flex `View` on web.

Image: Three colored boxes laid out horizontally inside a Row

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

### Basic row

```tsx RowExample.tsx
import { useColorScheme } from 'react-native';
import { Host, Row, Text } from '@expo/ui';

export default function RowExample() {
  const colorScheme = useColorScheme();
  const ink = { color: colorScheme === 'dark' ? '#FFFFFF' : '#000000' };

  return (
    <Host matchContents>
      <Row spacing={8}>
        <Text textStyle={ink}>One</Text>
        <Text textStyle={ink}>Two</Text>
        <Text textStyle={ink}>Three</Text>
      </Row>
    </Host>
  );
}
```

### Alignment

Use [`alignment`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/universal/row.md#alignment) to position children along the cross (vertical) axis.

```tsx RowAlignmentExample.tsx
import { useColorScheme } from 'react-native';
import { Host, Row, Text } from '@expo/ui';

export default function RowAlignmentExample() {
  const colorScheme = useColorScheme();
  const ink = { color: colorScheme === 'dark' ? '#FFFFFF' : '#000000' };

  return (
    <Host style={{ width: '100%', height: 160 }}>
      <Row spacing={8} alignment="center">
        <Text textStyle={{ ...ink, fontSize: 30 }}>Large</Text>
        <Text textStyle={ink}>centered</Text>
      </Row>
    </Host>
  );
}
```

### Pushing content apart with Spacer

Pair `Row` with a flexible [`Spacer`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/universal/spacer.md) to push its children to the opposite ends.

```tsx RowSpacerExample.tsx
import { useColorScheme } from 'react-native';
import { Host, Row, Text, Spacer } from '@expo/ui';

export default function RowSpacerExample() {
  const colorScheme = useColorScheme();
  const ink = { color: colorScheme === 'dark' ? '#FFFFFF' : '#000000' };

  return (
    <Host matchContents={{ vertical: true }} style={{ width: '100%' }}>
      <Row>
        <Text textStyle={ink}>Leading</Text>
        <Spacer flexible />
        <Text textStyle={ink}>Trailing</Text>
      </Row>
    </Host>
  );
}
```

## API

```tsx
import { Row } from '@expo/ui';
```

## Component

### `Row`

Supported platforms: Android, iOS, Web.

Type: React.[Element](https://www.typescriptlang.org/docs/handbook/jsx.html#function-component)<[RowProps](https://docs.expo.dev/versions/v57.0.0/sdk/ui/universal/row.md#rowprops)\>

A horizontal layout container that arranges its children from start to end.

Props for the [`Row`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/universal/row.md#row) component, a horizontal layout container.

RowProps

### `alignment`

Supported platforms: Android, iOS, Web.

Optional • Literal type: `string` • Default: `'start'`

Cross-axis (vertical) alignment of children.

Acceptable values are: `'start'` | `'center'` | `'end'`

### `children`

Supported platforms: Android, iOS, Web.

Optional • Type: [ReactNode](https://reactnative.dev/docs/react-node)

Content to render inside the row.

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

### `spacing`

Supported platforms: Android, iOS, Web.

Optional • Type: `number`

Horizontal spacing between children, in density-independent pixels.

### `style`

Supported platforms: Android, iOS, Web.

Optional • Type: [Pick](https://www.typescriptlang.org/docs/handbook/utility-types.html#picktype-keys)<[ViewStyle](https://reactnative.dev/docs/view-style-props), 'padding' | 'paddingHorizontal' | 'paddingVertical' | 'paddingTop' | 'paddingBottom' | 'paddingLeft' | 'paddingRight' | 'backgroundColor' | 'borderRadius' | 'borderWidth' | 'borderColor' | 'opacity' | 'width' | 'height'\>

Platform-agnostic style properties. These are translated to SwiftUI modifiers on iOS and Jetpack Compose modifiers on Android.

### `testID`

Supported platforms: Android, iOS, Web.

Optional • Type: `string`

Identifier used to locate the component in end-to-end tests.
