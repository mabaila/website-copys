---
modificationDate: August 18, 2026
title: ToggleButton
description: Jetpack Compose ToggleButton components for displaying native Material3 toggle buttons.
sourceCodeUrl: 'https://github.com/expo/expo/tree/sdk-57/packages/expo-ui'
packageName: '@expo/ui'
platforms: ['android', 'expo-go']
---

This documentation is available as Markdown for AI agents and LLMs. See the [full Markdown index](https://docs.expo.dev/llms.txt) or append .md to any documentation URL.

# ToggleButton

Jetpack Compose ToggleButton components for displaying native Material3 toggle buttons.

<AgentInstructions>

## Submitting Feedback

If you encounter errors, misleading or outdated information, report it so Expo can be improved:

Preferred command:
npx --yes submit-expo-feedback@latest --category docs --subject "/versions/v57.0.0/sdk/ui/jetpack-compose/togglebutton/" "<actionable feedback>"

Direct HTTP fallback:
curl -X POST https://api.expo.dev/v2/feedback/docs-send -H 'Content-Type: application/json' -d '{"url":"/versions/v57.0.0/sdk/ui/jetpack-compose/togglebutton/","feedback":"🤖 Agent feedback for docs: <specific, actionable description> (<model>, <harness>)"}'

Only submit when you have something specific and actionable to report. Try to give the most context.

## Navigation

When answering a related or follow-up question, use llms.txt to find the relevant page as Markdown (.md) instead of guessing.

You are here: Reference (v57.0.0) > Expo UI > Jetpack Compose (51 pages in this section)
Full documentation tree: [llms.txt](https://docs.expo.dev/llms.txt)

</AgentInstructions>
Android, Included in Expo Go

Expo UI provides four toggle button components that match the official Jetpack Compose Toggle Button API: [`ToggleButton`](https://kotlinlang.org/api/compose-multiplatform/material3/androidx.compose.material3/-toggle-button.html), [`IconToggleButton`](https://kotlinlang.org/api/compose-multiplatform/material3/androidx.compose.material3/-icon-toggle-button.html), [`FilledIconToggleButton`](https://kotlinlang.org/api/compose-multiplatform/material3/androidx.compose.material3/-filled-icon-toggle-button.html), and [`OutlinedIconToggleButton`](https://kotlinlang.org/api/compose-multiplatform/material3/androidx.compose.material3/-outlined-icon-toggle-button.html).

Image: A toggle button with text and two icon toggle buttons in checked and unchecked states

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

### Basic toggle button

A toggle button with text and icon content.

```tsx BasicToggleButtonExample.tsx
import { useState } from 'react';
import { Host, ToggleButton, Text } from '@expo/ui/jetpack-compose';

export default function BasicToggleButtonExample() {
  const [checked, setChecked] = useState(false);

  return (
    <Host matchContents>
      <ToggleButton checked={checked} onCheckedChange={setChecked}>
        <Text>Favorite</Text>
      </ToggleButton>
    </Host>
  );
}
```

### Icon toggle button variants

Use different icon toggle button components to convey varying levels of emphasis.

```tsx IconToggleButtonVariantsExample.tsx
import { useState } from 'react';
import {
  Host,
  IconToggleButton,
  FilledIconToggleButton,
  OutlinedIconToggleButton,
  Icon,
  Row,
  Surface,
} from '@expo/ui/jetpack-compose';

const starIcon = require('./assets/star.png');

export default function IconToggleButtonVariantsExample() {
  const [checked1, setChecked1] = useState(false);
  const [checked2, setChecked2] = useState(true);
  const [checked3, setChecked3] = useState(false);

  return (
    <Host matchContents>
      <Surface>
        <Row horizontalArrangement={{ spacedBy: 8 }}>
          <IconToggleButton
            checked={checked1}
            onCheckedChange={setChecked1}>
            <Icon source={starIcon} size={24} />
          </IconToggleButton>
          <FilledIconToggleButton
            checked={checked2}
            onCheckedChange={setChecked2}>
            <Icon source={starIcon} size={24} />
          </FilledIconToggleButton>
          <OutlinedIconToggleButton
            checked={checked3}
            onCheckedChange={setChecked3}>
            <Icon source={starIcon} size={24} />
          </OutlinedIconToggleButton>
        </Row>
      </Surface>
    </Host>
  );
}
```

### Custom colors

Override checked and unchecked colors using the `colors` prop.

```tsx CustomColorsToggleButtonExample.tsx
import { useState } from 'react';
import { Host, ToggleButton, Text } from '@expo/ui/jetpack-compose';

export default function CustomColorsToggleButtonExample() {
  const [checked, setChecked] = useState(true);

  return (
    <Host matchContents>
      <ToggleButton
        checked={checked}
        onCheckedChange={setChecked}
        colors={{
          checkedContainerColor: '#4CAF50',
          checkedContentColor: '#FFFFFF',
          containerColor: '#E0E0E0',
          contentColor: '#333333',
        }}>
        <Text>{checked ? 'ON' : 'OFF'}</Text>
      </ToggleButton>
    </Host>
  );
}
```

### Disabled toggle button

```tsx DisabledToggleButtonExample.tsx
import { Host, ToggleButton, Text } from '@expo/ui/jetpack-compose';

export default function DisabledToggleButtonExample() {
  return (
    <Host matchContents>
      <ToggleButton checked={false} enabled={false}>
        <Text>Disabled</Text>
      </ToggleButton>
    </Host>
  );
}
```

## API

```tsx
import {
  ToggleButton,
  IconToggleButton,
  FilledIconToggleButton,
  OutlinedIconToggleButton,
} from '@expo/ui/jetpack-compose';
```

## Components

### `FilledIconToggleButton`

Supported platforms: Android.

Type: React.[Element](https://www.typescriptlang.org/docs/handbook/jsx.html#function-component)<[ToggleButtonProps](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/togglebutton.md#togglebuttonprops)\>

A filled icon toggle button with a solid background.

### `IconToggleButton`

Supported platforms: Android.

Type: React.[Element](https://www.typescriptlang.org/docs/handbook/jsx.html#function-component)<[ToggleButtonProps](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/togglebutton.md#togglebuttonprops)\>

An icon toggle button with no background.

### `OutlinedIconToggleButton`

Supported platforms: Android.

Type: React.[Element](https://www.typescriptlang.org/docs/handbook/jsx.html#function-component)<[ToggleButtonProps](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/togglebutton.md#togglebuttonprops)\>

An outlined icon toggle button with a border and no fill.

### `ToggleButton`

Supported platforms: Android.

Type: React.[Element](https://www.typescriptlang.org/docs/handbook/jsx.html#function-component)<[ToggleButtonProps](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/togglebutton.md#togglebuttonprops)\>

A toggle button component that can be toggled on and off.

ToggleButtonProps

### `checked`

Supported platforms: Android.

Type: `boolean`

Whether the toggle button is checked.

### `children`

Supported platforms: Android.

Type: [ReactNode](https://reactnative.dev/docs/react-node)

Content to display inside the toggle button.

### `colors`

Supported platforms: Android.

Optional • Type: [ToggleButtonColors](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/togglebutton.md#togglebuttoncolors)

Colors for toggle button elements.

### `enabled`

Supported platforms: Android.

Optional • Type: `boolean` • Default: `true`

Whether the button is enabled for user interaction.

### `modifiers`

Supported platforms: Android.

Optional • Type: `ModifierConfig[]`

Modifiers for the component.

### `onCheckedChange`

Supported platforms: Android.

Optional • Type: `(checked: boolean) => void`

Callback that is called when the checked state changes.

### `ToggleButton.DefaultIconSize`

Supported platforms: Android.

Type: React.[Element](https://www.typescriptlang.org/docs/handbook/jsx.html#function-component)<number\>

## Types

### `ToggleButtonColors`

Supported platforms: Android.

Colors for toggle button elements.

| Property | Type | Description |
| --- | --- | --- |
| checkedContainerColor(optional) | [ColorValue](https://reactnative.dev/docs/colors) | - |
| checkedContentColor(optional) | [ColorValue](https://reactnative.dev/docs/colors) | - |
| containerColor(optional) | [ColorValue](https://reactnative.dev/docs/colors) | - |
| contentColor(optional) | [ColorValue](https://reactnative.dev/docs/colors) | - |
| disabledContainerColor(optional) | [ColorValue](https://reactnative.dev/docs/colors) | - |
| disabledContentColor(optional) | [ColorValue](https://reactnative.dev/docs/colors) | - |
