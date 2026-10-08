---
modificationDate: August 21, 2026
title: Picker
description: A single-selection input with menu and wheel appearances.
sourceCodeUrl: 'https://github.com/expo/expo/tree/sdk-57/packages/expo-ui'
packageName: '@expo/ui'
platforms: ['android', 'ios', 'web', 'expo-go']
---

This documentation is available as Markdown for AI agents and LLMs. See the [full Markdown index](https://docs.expo.dev/llms.txt) or append .md to any documentation URL.

# Picker

A single-selection input with menu and wheel appearances.

<AgentInstructions>

## Submitting Feedback

If you encounter errors, misleading or outdated information, report it so Expo can be improved:

Preferred command:
npx --yes submit-expo-feedback@latest --category docs --subject "/versions/v57.0.0/sdk/ui/universal/picker/" "<actionable feedback>"

Direct HTTP fallback:
curl -X POST https://api.expo.dev/v2/feedback/docs-send -H 'Content-Type: application/json' -d '{"url":"/versions/v57.0.0/sdk/ui/universal/picker/","feedback":"🤖 Agent feedback for docs: <specific, actionable description> (<model>, <harness>)"}'

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
- [Picker](https://docs.expo.dev/versions/v57.0.0/sdk/ui/universal/picker.md) (this page)
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

`Picker` is a single-selection input. You can use `<Picker.Item label value />` children to declare options so that the parent `Picker` reads them and renders a platform-appropriate dropdown or rotor.

The universal `Picker` is independent of [`@expo/ui/community/picker`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/drop-in-replacements/picker.md), which remains a compat shim for `@react-native-picker/picker`. Prefer this universal `Picker` for new code unless you specifically need the RN-Picker API surface.

Image: Three labeled rows with dropdown pickers set to Apple, Medium, and Blue

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

### Menu appearance (default)

```tsx PickerMenuExample.tsx
import { useState } from 'react';
import { useColorScheme } from 'react-native';
import { Host, Row, Picker, Spacer, Text } from '@expo/ui';

const FLAVOURS = [
  { label: 'Vanilla', value: 'vanilla' },
  { label: 'Chocolate', value: 'chocolate' },
  { label: 'Strawberry', value: 'strawberry' },
];

export default function PickerMenuExample() {
  const [value, setValue] = useState('vanilla');
  const colorScheme = useColorScheme();

  return (
    <Host matchContents={{ vertical: true }} style={{ width: '100%' }}>
      <Row alignment="center" spacing={12} style={{ padding: 16 }}>
        <Text textStyle={{ color: colorScheme === 'dark' ? '#FFFFFF' : '#000000' }}>Flavour:</Text>
        <Spacer flexible />
        <Picker selectedValue={value} onValueChange={setValue}>
          {FLAVOURS.map(f => (
            <Picker.Item key={f.value} label={f.label} value={f.value} />
          ))}
        </Picker>
      </Row>
    </Host>
  );
}
```

### Wheel appearance

`appearance="wheel"` renders an inline scrollable rotor on iOS. On Android and web, this falls back to the platform's default dropdown (Material 3 doesn't ship a wheel-style picker).

```tsx PickerWheelExample.tsx
import { useState } from 'react';
import { Host, Column, Picker } from '@expo/ui';

const FLAVOURS = [
  { label: 'Vanilla', value: 'vanilla' },
  { label: 'Chocolate', value: 'chocolate' },
  { label: 'Strawberry', value: 'strawberry' },
];

export default function PickerWheelExample() {
  const [value, setValue] = useState('chocolate');

  return (
    <Host matchContents={{ vertical: true }} style={{ width: '100%' }}>
      <Column spacing={8} style={{ padding: 16 }}>
        <Picker selectedValue={value} onValueChange={setValue} appearance="wheel">
          {FLAVOURS.map(f => (
            <Picker.Item key={f.value} label={f.label} value={f.value} />
          ))}
        </Picker>
      </Column>
    </Host>
  );
}
```

## API

```tsx
import { Picker } from '@expo/ui';
```

## Component

### `Picker`

Supported platforms: Android, iOS, Web.

Type: React.[Element](https://www.typescriptlang.org/docs/handbook/jsx.html#function-component)<[PickerProps](https://docs.expo.dev/versions/v57.0.0/sdk/ui/universal/picker.md#pickerprops)<T\>\>

A single-selection input. Declare options via `<Picker.Item label value />` children.

Props for the [`Picker`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/universal/picker.md#picker) component, a single-selection input.

PickerProps

### `appearance`

Supported platforms: Android, iOS, Web.

Optional • Type: [PickerAppearance](https://docs.expo.dev/versions/v57.0.0/sdk/ui/universal/picker.md#pickerappearance) • Default: `'menu'`

Visual appearance of the picker. See [`PickerAppearance`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/universal/picker.md#pickerappearance).

### `children`

Supported platforms: Android, iOS, Web.

Optional • Type: [ReactNode](https://reactnative.dev/docs/react-node)

`<Picker.Item>` children that declare the available options.

### `enabled`

Supported platforms: Android, iOS, Web.

Optional • Type: `boolean` • Default: `true`

Whether the picker accepts input.

### `onValueChange`

Supported platforms: Android, iOS, Web.

Type: `(value: T) => void`

Called when the user selects an option.

### `selectedValue`

Supported platforms: Android, iOS, Web.

Type: `T`

The currently selected value. Must match the `value` of one of the `<Picker.Item>` children.

### `testID`

Supported platforms: Android, iOS, Web.

Optional • Type: `string`

Identifier used to locate the component in end-to-end tests.

## Interfaces

### `ExtractedPickerItem`

Supported platforms: Android, iOS, Web.

Internal: extracted item data from `<Picker.Item>` children.

| Property | Type | Description |
| --- | --- | --- |
| label | `string` | - |
| value | `T` | - |

## Types

### `PickerAppearance`

Supported platforms: Android, iOS, Web.

Literal type: `string`

Visual appearance of the picker.

-   `'menu'` — Compact button that opens a popup/dropdown on tap. Cross-platform default.
-   `'wheel'` — Scrollable rotor UI that's always visible inline. iOS only; on Android and web this falls back to the platform's default dropdown.

Acceptable values are: `'wheel'` | `'menu'`

### `PickerItemValue`

Supported platforms: Android, iOS, Web.

Literal type: `union`

The type of values a [`Picker.Item`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/universal/picker.md#picker) can carry.

Acceptable values are: `string` | `number`
