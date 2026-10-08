---
modificationDate: August 24, 2026
title: Picker
description: A picker compatible with @react-native-picker/picker.
sourceCodeUrl: 'https://github.com/expo/expo/tree/sdk-57/packages/expo-ui'
packageName: '@expo/ui'
platforms: ['android', 'ios', 'web', 'expo-go']
---

This documentation is available as Markdown for AI agents and LLMs. See the [full Markdown index](https://docs.expo.dev/llms.txt) or append .md to any documentation URL.

# Picker

A picker compatible with @react-native-picker/picker.

<AgentInstructions>

## Submitting Feedback

If you encounter errors, misleading or outdated information, report it so Expo can be improved:

Preferred command:
npx --yes submit-expo-feedback@latest --category docs --subject "/versions/v57.0.0/sdk/ui/drop-in-replacements/picker/" "<actionable feedback>"

Direct HTTP fallback:
curl -X POST https://api.expo.dev/v2/feedback/docs-send -H 'Content-Type: application/json' -d '{"url":"/versions/v57.0.0/sdk/ui/drop-in-replacements/picker/","feedback":"🤖 Agent feedback for docs: <specific, actionable description> (<model>, <harness>)"}'

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
- [Picker](https://docs.expo.dev/versions/v57.0.0/sdk/ui/drop-in-replacements/picker.md) (this page)
- [SegmentedControl](https://docs.expo.dev/versions/v57.0.0/sdk/ui/drop-in-replacements/segmentedcontrol.md)
- [Slider](https://docs.expo.dev/versions/v57.0.0/sdk/ui/drop-in-replacements/slider.md)
Full documentation tree: [llms.txt](https://docs.expo.dev/llms.txt)

</AgentInstructions>
Android, iOS, Web, Included in Expo Go

A `Picker` component with an API compatible with `@react-native-picker/picker`. It uses a SwiftUI wheel `Picker` on iOS, a Material 3 `ExposedDropdownMenuBox` on Android, and a native `<select>` element on web.

Under the hood this component wraps the platform-specific `@expo/ui` primitives:

-   **Android**: [Jetpack Compose ExposedDropdownMenuBox](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/exposeddropdownmenubox.md)
-   **iOS**: [SwiftUI Picker](https://docs.expo.dev/versions/v57.0.0/sdk/ui/swift-ui/picker.md) with `pickerStyle('wheel')`

If you need lower-level control, use those primitives directly.

Image: A dropdown field showing Java

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

## Migrating from `@react-native-picker/picker`

-   Update the import from `import { Picker } from '@react-native-picker/picker'` to `import { Picker } from '@expo/ui/community/picker'`.
-   `mode`, `prompt`, `dropdownIconColor`, `dropdownIconRippleColor`, `numberOfLines`, `selectionColor`, `itemStyle`, and `accessibilityLabel` props are not supported.
-   On `Picker.Item`, the `style` prop only applies `color`, `backgroundColor`, `fontFamily`, and `fontSize`. The top-level `color` and `fontFamily` props are still supported as aliases for the corresponding `style` values.
-   `enabled` on `Picker.Item` only applies on Android.
-   The `ref` `focus()` and `blur()` methods only have an effect on Android (open/close the dropdown). On iOS, the wheel picker is always visible.

## Basic usage

```tsx PickerExample.tsx
import { useState } from 'react';
import { Text, useColorScheme, View } from 'react-native';
import { Picker } from '@expo/ui/community/picker';

export default function PickerExample() {
  const [language, setLanguage] = useState('java');
  const colorScheme = useColorScheme();

  return (
    <View>
      <Picker selectedValue={language} onValueChange={value => setLanguage(value)}>
        <Picker.Item label="Java" value="java" />
        <Picker.Item label="JavaScript" value="js" />
        <Picker.Item label="Objective C" value="objc" />
        <Picker.Item label="Swift" value="swift" />
      </Picker>
      <Text style={{ color: colorScheme === 'dark' ? '#FFFFFF' : '#000000' }}>
        Selected: {language}
      </Text>
    </View>
  );
}
```

## Per-item styling and state

Pass a `style` to `Picker.Item` to control `color`, `backgroundColor`, `fontFamily`, and `fontSize` per item, and `enabled={false}` to disable specific items on Android.

`fontFamily` accepts iOS font names (for example, `'Menlo'`) on iOS, and Compose generic families (`'monospace'`, `'serif'`, `'sansSerif'`, `'cursive'`) or fonts loaded with [`expo-font`](https://docs.expo.dev/versions/v57.0.0/sdk/font.md) on Android.

```tsx StyledPickerExample.tsx
import { useState } from 'react';
import { Platform } from 'react-native';
import { Picker } from '@expo/ui/community/picker';

const monospace = Platform.select({ ios: 'Menlo', android: 'monospace' });
const serif = Platform.select({ ios: 'Georgia', android: 'serif' });

export default function StyledPickerExample() {
  const [language, setLanguage] = useState('java');

  return (
    <Picker selectedValue={language} onValueChange={value => setLanguage(value)}>
      <Picker.Item
        label="Java"
        value="java"
        style={{ color: '#e11d48', fontFamily: monospace, fontSize: 14 }}
      />
      <Picker.Item
        label="JavaScript"
        value="js"
        style={{ color: '#2563eb', fontFamily: serif, fontSize: 18 }}
        enabled={false}
      />
      <Picker.Item
        label="Objective C"
        value="objc"
        style={{ color: '#059669', fontFamily: monospace, fontSize: 16 }}
      />
      <Picker.Item
        label="Swift"
        value="swift"
        style={{ color: '#d97706', fontFamily: serif, fontSize: 30 }}
        enabled={false}
      />
    </Picker>
  );
}
```

## Imperative focus and blur (Android)

Use a ref to programmatically open and close the dropdown on Android. On iOS, these methods are no-ops because the wheel picker is always visible.

```tsx RefPickerExample.tsx
import { useRef, useState } from 'react';
import { Button } from 'react-native';
import { Picker, type PickerRef } from '@expo/ui/community/picker';

export default function RefPickerExample() {
  const [language, setLanguage] = useState('java');
  const pickerRef = useRef<PickerRef>(null);

  return (
    <>
      <Button
        title="Open and close after 2s"
        onPress={() => {
          pickerRef.current?.focus();
          setTimeout(() => pickerRef.current?.blur(), 2000);
        }}
      />
      <Picker ref={pickerRef} selectedValue={language} onValueChange={setLanguage}>
        <Picker.Item label="Java" value="java" />
        <Picker.Item label="JavaScript" value="js" />
        <Picker.Item label="Objective C" value="objc" />
        <Picker.Item label="Swift" value="swift" />
      </Picker>
    </>
  );
}
```

## API

```tsx
import { Picker } from '@expo/ui/community/picker';
```

## Components

### `Picker`

Supported platforms: Android, iOS, Web.

Type: React.[Element](https://www.typescriptlang.org/docs/handbook/jsx.html#function-component)<[PickerProps](https://docs.expo.dev/versions/v57.0.0/sdk/ui/drop-in-replacements/picker.md#pickerprops)<T\>\>

A drop-in replacement for `@react-native-picker/picker` on web. Renders a native `<select>` element.

Props for the `Picker` component. Compatible with `@react-native-picker/picker`.

PickerProps

### `children`

Supported platforms: Android, iOS, Web.

Optional • Type: [ReactNode](https://reactnative.dev/docs/react-node)

`Picker.Item` children that define the available options.

### `enabled`

Supported platforms: Android, iOS, Web.

Optional • Type: `boolean`

Whether the picker is enabled.

### `onValueChange`

Supported platforms: Android, iOS, Web.

Optional • Type: `(itemValue: T, itemIndex: number) => void`

Callback when an item is selected. Called with `(itemValue, itemIndex)`.

### `ref`

Supported platforms: Android, iOS, Web.

Optional • Type: Ref<[PickerRef](https://docs.expo.dev/versions/v57.0.0/sdk/ui/drop-in-replacements/picker.md#pickerref)\>

Ref handle exposing `focus()` and `blur()` methods.

### `selectedValue`

Supported platforms: Android, iOS, Web.

Optional • Type: `T`

The currently selected value. Must match the `value` of one of the `Picker.Item` children.

### `style`

Supported platforms: Android, iOS, Web.

Optional • Type: StyleProp<[ViewStyle](https://reactnative.dev/docs/view-style-props)\>

Style applied to the picker container.

### `testID`

Supported platforms: Android, iOS, Web.

Optional • Type: `string`

Test identifier.

### `Picker.Item`

Supported platforms: Android, iOS, Web.

Type: React.[Element](https://www.typescriptlang.org/docs/handbook/jsx.html#function-component)<ComponentType<[PickerItemProps](https://docs.expo.dev/versions/v57.0.0/sdk/ui/drop-in-replacements/picker.md#pickeritemprops)\>\>

Props for the `Picker.Item` component. Compatible with `@react-native-picker/picker`.

PickerItemProps

### `color`

Supported platforms: Android, iOS, Web.

Optional • Type: `string`

Text color for the item. Equivalent to setting `color` in the `style` prop.

### `enabled`

Supported platforms: Android.

Optional • Type: `boolean`

Whether the item is enabled.

### `fontFamily`

Supported platforms: Android, iOS, Web.

Optional • Type: `string`

Custom font family for the item. Equivalent to setting `fontFamily` in the `style` prop.

### `label`

Supported platforms: Android, iOS, Web.

Optional • Type: `string`

Display text for the item.

### `style`

Supported platforms: Android, iOS, Web.

Optional • Type: StyleProp<[TextStyle](https://reactnative.dev/docs/text-style-props)\>

Style applied to the item label. Only the following values take effect: `color`, `backgroundColor`, `fontFamily`, and `fontSize`. When also set via the top-level `color` or `fontFamily` props, values from `style` win.

### `testID`

Supported platforms: Android, iOS, Web.

Optional • Type: `string`

Test identifier.

### `value`

Supported platforms: Android, iOS, Web.

Optional • Type: `T`

Value passed to `onValueChange` when this item is selected.

## Types

### `PickerItemValue`

Supported platforms: Android, iOS, Web.

Literal type: `union`

Acceptable values are: `string` | `number` | `null`

### `PickerRef`

Supported platforms: Android, iOS, Web.

Ref handle for the `Picker` component. Compatible with `@react-native-picker/picker`.

| Property | Type | Description |
| --- | --- | --- |
| blur | `() => void` | Supported platforms: Android. Programmatically closes the picker. |
| focus | `() => void` | Supported platforms: Android. Programmatically opens the picker. |
