---
modificationDate: August 18, 2026
title: Checkbox
description: A Jetpack Compose Checkbox component for selection controls.
sourceCodeUrl: 'https://github.com/expo/expo/tree/sdk-57/packages/expo-ui'
packageName: '@expo/ui'
platforms: ['android', 'expo-go']
---

This documentation is available as Markdown for AI agents and LLMs. See the [full Markdown index](https://docs.expo.dev/llms.txt) or append .md to any documentation URL.

# Checkbox

A Jetpack Compose Checkbox component for selection controls.

<AgentInstructions>

## Submitting Feedback

If you encounter errors, misleading or outdated information, report it so Expo can be improved:

Preferred command:
npx --yes submit-expo-feedback@latest --category docs --subject "/versions/v57.0.0/sdk/ui/jetpack-compose/checkbox/" "<actionable feedback>"

Direct HTTP fallback:
curl -X POST https://api.expo.dev/v2/feedback/docs-send -H 'Content-Type: application/json' -d '{"url":"/versions/v57.0.0/sdk/ui/jetpack-compose/checkbox/","feedback":"🤖 Agent feedback for docs: <specific, actionable description> (<model>, <harness>)"}'

Only submit when you have something specific and actionable to report. Try to give the most context.

## Navigation

When answering a related or follow-up question, use llms.txt to find the relevant page as Markdown (.md) instead of guessing.

You are here: Reference (v57.0.0) > Expo UI > Jetpack Compose (51 pages in this section)
Full documentation tree: [llms.txt](https://docs.expo.dev/llms.txt)

</AgentInstructions>
Android, Included in Expo Go

> For cross-platform usage, see the universal [`Checkbox`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/universal/checkbox.md) — it renders the appropriate native component per platform.

Expo UI Checkbox matches the official Jetpack Compose [Checkbox](https://developer.android.com/develop/ui/compose/components/checkbox) API.

Image: Checked and unchecked Material 3 checkboxes

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

### Basic checkbox

```tsx CheckboxExample.tsx
import { useState } from 'react';
import { Host, Checkbox } from '@expo/ui/jetpack-compose';

export default function CheckboxExample() {
  const [checked, setChecked] = useState(false);

  return (
    <Host matchContents>
      <Checkbox value={checked} onCheckedChange={setChecked} />
    </Host>
  );
}
```

### Custom colors

```tsx CustomColorsExample.tsx
import { useState } from 'react';
import { Host, Checkbox } from '@expo/ui/jetpack-compose';

export default function CustomColorsExample() {
  const [checked, setChecked] = useState(false);

  return (
    <Host matchContents>
      <Checkbox
        value={checked}
        onCheckedChange={setChecked}
        colors={{
          checkedColor: '#6200EE',
          checkmarkColor: '#FFFFFF',
        }}
      />
    </Host>
  );
}
```

### Select all (TriStateCheckbox)

Use `TriStateCheckbox` for a parent checkbox that reflects the state of its children. It supports three states: `'on'`, `'off'`, and `'indeterminate'`.

Apply the `toggleable` modifier to each `Row` to make the entire row (checkbox + label) tappable with correct accessibility semantics. When using `toggleable` on the row, omit `onCheckedChange`/`onClick` from the checkbox itself to avoid double-handling.

```tsx SelectAllExample.tsx
import { useState } from 'react';
import {
  Host,
  Checkbox,
  TriStateCheckbox,
  Row,
  Column,
  Text,
} from '@expo/ui/jetpack-compose';
import { toggleable } from '@expo/ui/jetpack-compose/modifiers';

export default function SelectAllExample() {
  const [child1, setChild1] = useState(false);
  const [child2, setChild2] = useState(false);
  const [child3, setChild3] = useState(false);

  const parentState =
    child1 && child2 && child3
      ? 'on'
      : !child1 && !child2 && !child3
        ? 'off'
        : 'indeterminate';

  return (
    <Host matchContents>
      <Column>
        <Row
          verticalAlignment="center"
          modifiers={[
            toggleable(
              parentState === 'on',
              () => {
                const newState = parentState !== 'on';
                setChild1(newState);
                setChild2(newState);
                setChild3(newState);
              },
              { role: 'checkbox' }
            ),
          ]}>
          <TriStateCheckbox state={parentState} />
          <Text>Select all</Text>
        </Row>
        <Row
          verticalAlignment="center"
          modifiers={[
            toggleable(child1, () => setChild1(!child1), {
              role: 'checkbox',
            }),
          ]}>
          <Checkbox value={child1} />
          <Text>Option 1</Text>
        </Row>
        <Row
          verticalAlignment="center"
          modifiers={[
            toggleable(child2, () => setChild2(!child2), {
              role: 'checkbox',
            }),
          ]}>
          <Checkbox value={child2} />
          <Text>Option 2</Text>
        </Row>
        <Row
          verticalAlignment="center"
          modifiers={[
            toggleable(child3, () => setChild3(!child3), {
              role: 'checkbox',
            }),
          ]}>
          <Checkbox value={child3} />
          <Text>Option 3</Text>
        </Row>
      </Column>
    </Host>
  );
}
```

## API

```tsx
import {
  Checkbox,
  TriStateCheckbox,
} from '@expo/ui/jetpack-compose';
```

## Components

### `Checkbox`

Supported platforms: Android.

Type: React.[Element](https://www.typescriptlang.org/docs/handbook/jsx.html#function-component)<[CheckboxProps](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/checkbox.md#checkboxprops)\>

A checkbox component.

CheckboxProps

### `colors`

Supported platforms: Android.

Optional • Type: [CheckboxColors](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/checkbox.md#checkboxcolors)

Colors for checkbox core elements.

### `enabled`

Supported platforms: Android.

Optional • Type: `boolean` • Default: `true`

Whether the checkbox is enabled.

### `modifiers`

Supported platforms: Android.

Optional • Type: `ModifierConfig[]`

Modifiers for the component.

### `onCheckedChange`

Supported platforms: Android.

Optional • Type: `(value: boolean) => void`

Callback function that is called when the checked state changes.

### `value`

Supported platforms: Android.

Type: `boolean`

Indicates whether the checkbox is checked.

### `TriStateCheckbox`

Supported platforms: Android.

Type: React.[Element](https://www.typescriptlang.org/docs/handbook/jsx.html#function-component)<[TriStateCheckboxProps](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/checkbox.md#tristatecheckboxprops)\>

A tri-state checkbox component that supports `'on'`, `'off'`, and `'indeterminate'` states. Useful for "select all" patterns where the parent checkbox reflects the state of its children.

TriStateCheckboxProps

### `colors`

Supported platforms: Android.

Optional • Type: [CheckboxColors](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/checkbox.md#checkboxcolors)

Colors for checkbox core elements.

### `enabled`

Supported platforms: Android.

Optional • Type: `boolean` • Default: `true`

Whether the checkbox is enabled.

### `modifiers`

Supported platforms: Android.

Optional • Type: `ModifierConfig[]`

Modifiers for the component.

### `onClick`

Supported platforms: Android.

Optional • Type: `() => void`

Callback function that is called when the checkbox is clicked.

### `state`

Supported platforms: Android.

Type: [ToggleableState](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/checkbox.md#toggleablestate)

The toggleable state of the checkbox: `'on'`, `'off'`, or `'indeterminate'`.

## Types

### `CheckboxColors`

Supported platforms: Android.

Colors for checkbox core elements.

| Property | Type | Description |
| --- | --- | --- |
| checkedColor(optional) | [ColorValue](https://reactnative.dev/docs/colors) | - |
| checkmarkColor(optional) | [ColorValue](https://reactnative.dev/docs/colors) | - |
| disabledCheckedColor(optional) | [ColorValue](https://reactnative.dev/docs/colors) | - |
| disabledIndeterminateColor(optional) | [ColorValue](https://reactnative.dev/docs/colors) | - |
| disabledUncheckedColor(optional) | [ColorValue](https://reactnative.dev/docs/colors) | - |
| uncheckedColor(optional) | [ColorValue](https://reactnative.dev/docs/colors) | - |

### `ToggleableState`

Supported platforms: Android.

Literal type: `string`

The toggleable state of a tri-state checkbox.

Acceptable values are: `'on'` | `'off'` | `'indeterminate'`
