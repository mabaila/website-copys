---
modificationDate: August 18, 2026
title: Divider
description: Jetpack Compose Divider components for creating visual separators.
sourceCodeUrl: 'https://github.com/expo/expo/tree/sdk-57/packages/expo-ui'
packageName: '@expo/ui'
platforms: ['android', 'expo-go']
---

This documentation is available as Markdown for AI agents and LLMs. See the [full Markdown index](https://docs.expo.dev/llms.txt) or append .md to any documentation URL.

# Divider

Jetpack Compose Divider components for creating visual separators.

<AgentInstructions>

## Submitting Feedback

If you encounter errors, misleading or outdated information, report it so Expo can be improved:

Preferred command:
npx --yes submit-expo-feedback@latest --category docs --subject "/versions/v57.0.0/sdk/ui/jetpack-compose/divider/" "<actionable feedback>"

Direct HTTP fallback:
curl -X POST https://api.expo.dev/v2/feedback/docs-send -H 'Content-Type: application/json' -d '{"url":"/versions/v57.0.0/sdk/ui/jetpack-compose/divider/","feedback":"🤖 Agent feedback for docs: <specific, actionable description> (<model>, <harness>)"}'

Only submit when you have something specific and actionable to report. Try to give the most context.

## Navigation

When answering a related or follow-up question, use llms.txt to find the relevant page as Markdown (.md) instead of guessing.

You are here: Reference (v57.0.0) > Expo UI > Jetpack Compose (51 pages in this section)
Full documentation tree: [llms.txt](https://docs.expo.dev/llms.txt)

</AgentInstructions>
Android, Included in Expo Go

Expo UI provides [`HorizontalDivider`](https://developer.android.com/reference/kotlin/androidx/compose/material3/package-summary#HorizontalDivider\(androidx.compose.ui.Modifier,androidx.compose.ui.unit.Dp,androidx.compose.ui.graphics.Color\)) and [`VerticalDivider`](https://developer.android.com/reference/kotlin/androidx/compose/material3/package-summary#VerticalDivider\(androidx.compose.ui.Modifier,androidx.compose.ui.unit.Dp,androidx.compose.ui.graphics.Color\)) matching the official Jetpack Compose Divider API.

Image: Three text sections separated by horizontal Material 3 dividers

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

### Horizontal divider

A thin horizontal line to visually separate content in lists and layouts.

```tsx HorizontalDividerExample.tsx
import {
  Host,
  HorizontalDivider,
  Column,
  Text,
  useMaterialColors,
} from '@expo/ui/jetpack-compose';

export default function HorizontalDividerExample() {
  const colors = useMaterialColors();

  return (
    <Host style={{ flex: 1 }}>
      <Column>
        <Text style={{ fontSize: 28 }} color={colors.onBackground}>
          First section
        </Text>
        <HorizontalDivider />
        <Text style={{ fontSize: 28 }} color={colors.onBackground}>
          Second section
        </Text>
      </Column>
    </Host>
  );
}
```

### Custom thickness and color

Both `HorizontalDivider` and `VerticalDivider` accept `thickness` and `color` props. Use `StyleSheet.hairlineWidth` for a single-pixel line, or set a custom thickness and color.

```tsx CustomDividerExample.tsx
import {
  Host,
  HorizontalDivider,
  Column,
  Text,
  useMaterialColors,
} from '@expo/ui/jetpack-compose';
import { StyleSheet } from 'react-native';

export default function CustomDividerExample() {
  const colors = useMaterialColors();

  return (
    <Host style={{ flex: 1 }}>
      <Column>
        <Text style={{ fontSize: 28 }} color={colors.onBackground}>
          Hairline divider (1 pixel)
        </Text>
        <HorizontalDivider thickness={StyleSheet.hairlineWidth} />
        <Text style={{ fontSize: 28 }} color={colors.onBackground}>
          Thick colored divider
        </Text>
        <HorizontalDivider thickness={4} color="#E91E63" />
        <Text style={{ fontSize: 28 }} color={colors.onBackground}>
          Below
        </Text>
      </Column>
    </Host>
  );
}
```

### Vertical divider

A vertical line to separate items side by side in a row layout.

```tsx VerticalDividerExample.tsx
import {
  Host,
  VerticalDivider,
  Row,
  Text,
  useMaterialColors,
} from '@expo/ui/jetpack-compose';
import { height } from '@expo/ui/jetpack-compose/modifiers';

export default function VerticalDividerExample() {
  const colors = useMaterialColors();

  return (
    <Host matchContents>
      <Row
        verticalAlignment="center"
        horizontalArrangement={{ spacedBy: 16 }}
        modifiers={[height(48)]}>
        <Text style={{ fontSize: 28 }} color={colors.onBackground}>
          Left
        </Text>
        <VerticalDivider />
        <Text style={{ fontSize: 28 }} color={colors.onBackground}>
          Right
        </Text>
      </Row>
    </Host>
  );
}
```

## API

```tsx
import {
  HorizontalDivider,
  VerticalDivider,
} from '@expo/ui/jetpack-compose';
```

## Components

### `HorizontalDivider`

Supported platforms: Android.

Type: React.[Element](https://www.typescriptlang.org/docs/handbook/jsx.html#function-component)<ComponentType<[DividerCommonConfig](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/divider.md#dividercommonconfig)\>\>

A horizontal divider line that groups content in lists and layouts, matching Compose's `HorizontalDivider`.

### `VerticalDivider`

Supported platforms: Android.

Type: React.[Element](https://www.typescriptlang.org/docs/handbook/jsx.html#function-component)<ComponentType<[DividerCommonConfig](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/divider.md#dividercommonconfig)\>\>

A vertical divider line that groups content in layouts, matching Compose's `VerticalDivider`.

## Types

### `DividerCommonConfig`

Supported platforms: Android.

| Property | Type | Description |
| --- | --- | --- |
| color(optional) | [ColorValue](https://reactnative.dev/docs/colors) | Color of the divider line. |
| modifiers(optional) | `ModifierConfig[]` | Modifiers for the component. |
| thickness(optional) | `number` | Thickness of the divider line. Accepts dp values; use `StyleSheet.hairlineWidth` for a single-pixel line. |
