---
modificationDate: August 18, 2026
title: LazyRow
description: A Jetpack Compose LazyRow component for displaying horizontally scrolling lists.
sourceCodeUrl: 'https://github.com/expo/expo/tree/sdk-57/packages/expo-ui'
packageName: '@expo/ui'
platforms: ['android', 'expo-go']
---

This documentation is available as Markdown for AI agents and LLMs. See the [full Markdown index](https://docs.expo.dev/llms.txt) or append .md to any documentation URL.

# LazyRow

A Jetpack Compose LazyRow component for displaying horizontally scrolling lists.

<AgentInstructions>

## Submitting Feedback

If you encounter errors, misleading or outdated information, report it so Expo can be improved:

Preferred command:
npx --yes submit-expo-feedback@latest --category docs --subject "/versions/v57.0.0/sdk/ui/jetpack-compose/lazyrow/" "<actionable feedback>"

Direct HTTP fallback:
curl -X POST https://api.expo.dev/v2/feedback/docs-send -H 'Content-Type: application/json' -d '{"url":"/versions/v57.0.0/sdk/ui/jetpack-compose/lazyrow/","feedback":"🤖 Agent feedback for docs: <specific, actionable description> (<model>, <harness>)"}'

Only submit when you have something specific and actionable to report. Try to give the most context.

## Navigation

When answering a related or follow-up question, use llms.txt to find the relevant page as Markdown (.md) instead of guessing.

You are here: Reference (v57.0.0) > Expo UI > Jetpack Compose (51 pages in this section)
Full documentation tree: [llms.txt](https://docs.expo.dev/llms.txt)

</AgentInstructions>
Android, Included in Expo Go

A lazily-loaded horizontal list component that only renders visible items for efficient scrolling. See the [official Jetpack Compose documentation](https://developer.android.com/develop/ui/compose/lists) for more information.

> `LazyRow` is not truly lazy yet: the native side only composes visible items, but React still creates every child up front, so large lists can be slow to mount. We are working on improving this. For large lists, we recommend [FlashList](https://shopify.github.io/flash-list/) or [Legend List](https://github.com/LegendApp/legend-list).

Image: LazyRow rendering colored category cards in a horizontally scrolling list

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

### Basic lazy row

```tsx BasicLazyRow.tsx
import {
  Host,
  LazyRow,
  Text,
  useMaterialColors,
} from '@expo/ui/jetpack-compose';
import {
  border,
  padding,
} from '@expo/ui/jetpack-compose/modifiers';

const items = Array.from(
  { length: 100 },
  (_, i) => `Item ${i + 1}`
);

export default function BasicLazyRow() {
  const colors = useMaterialColors();

  return (
    <Host style={{ height: 100 }}>
      <LazyRow>
        {items.map(item => (
          <Text
            key={item}
            style={{ fontSize: 28 }}
            color={colors.onBackground}
            modifiers={[
              border(1, colors.outline),
              padding(12, 6, 12, 6),
            ]}>
            {item}
          </Text>
        ))}
      </LazyRow>
    </Host>
  );
}
```

### With arrangement

Use the `horizontalArrangement` prop to control how items are spaced within the list. Pass a string value like `'spaceBetween'` or an object like `{ spacedBy: 8 }` for fixed spacing in dp.

```tsx LazyRowArrangement.tsx
import {
  Host,
  LazyRow,
  Text,
  useMaterialColors,
} from '@expo/ui/jetpack-compose';
import {
  border,
  padding,
} from '@expo/ui/jetpack-compose/modifiers';

export default function LazyRowArrangement() {
  const colors = useMaterialColors();

  return (
    <Host style={{ height: 100 }}>
      <LazyRow
        horizontalArrangement={{ spacedBy: 16 }}
        verticalAlignment="center">
        <Text
          style={{ fontSize: 28 }}
          color={colors.onBackground}
          modifiers={[
            border(1, colors.outline),
            padding(12, 6, 12, 6),
          ]}>
          Spaced item 1
        </Text>
        <Text
          style={{ fontSize: 28 }}
          color={colors.onBackground}
          modifiers={[
            border(1, colors.outline),
            padding(12, 6, 12, 6),
          ]}>
          Spaced item 2
        </Text>
        <Text
          style={{ fontSize: 28 }}
          color={colors.onBackground}
          modifiers={[
            border(1, colors.outline),
            padding(12, 6, 12, 6),
          ]}>
          Spaced item 3
        </Text>
      </LazyRow>
    </Host>
  );
}
```

### With content padding

Use the `contentPadding` prop to add padding around the list content in dp.

```tsx LazyRowPadding.tsx
import {
  Host,
  LazyRow,
  Text,
  useMaterialColors,
} from '@expo/ui/jetpack-compose';
import {
  border,
  padding,
} from '@expo/ui/jetpack-compose/modifiers';

export default function LazyRowPadding() {
  const colors = useMaterialColors();

  return (
    <Host style={{ height: 100 }}>
      <LazyRow
        contentPadding={{ start: 16, top: 8, end: 16, bottom: 8 }}>
        <Text
          style={{ fontSize: 28 }}
          color={colors.onBackground}
          modifiers={[
            border(1, colors.outline),
            padding(12, 6, 12, 6),
          ]}>
          Padded item 1
        </Text>
        <Text
          style={{ fontSize: 28 }}
          color={colors.onBackground}
          modifiers={[
            border(1, colors.outline),
            padding(12, 6, 12, 6),
          ]}>
          Padded item 2
        </Text>
        <Text
          style={{ fontSize: 28 }}
          color={colors.onBackground}
          modifiers={[
            border(1, colors.outline),
            padding(12, 6, 12, 6),
          ]}>
          Padded item 3
        </Text>
      </LazyRow>
    </Host>
  );
}
```

## API

```tsx
import { LazyRow } from '@expo/ui/jetpack-compose';
```

## Component

### `LazyRow`

Supported platforms: Android.

Type: React.[Element](https://www.typescriptlang.org/docs/handbook/jsx.html#function-component)<[LazyRowProps](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/lazyrow.md#lazyrowprops)\>

A lazy row component that efficiently displays a horizontally scrolling list.

LazyRowProps

### `children`

Supported platforms: Android.

Optional • Type: [ReactNode](https://reactnative.dev/docs/react-node)

The content to display inside the lazy row.

### `contentPadding`

Supported platforms: Android.

Optional • Type: [ContentPadding](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/lazyrow.md#contentpadding)

Content padding in dp.

### `horizontalArrangement`

Supported platforms: Android.

Optional • Literal type: `union`

The horizontal arrangement of items. Can be a preset string or an object with `spacedBy` to specify spacing in dp.

Acceptable values are: `'start'` | `'end'` | `'center'` | `'spaceBetween'` | `'spaceAround'` | `'spaceEvenly'` | `{ spacedBy: number }`

### `modifiers`

Supported platforms: Android.

Optional • Type: `ModifierConfig[]`

Modifiers for the component.

### `verticalAlignment`

Supported platforms: Android.

Optional • Literal type: `string`

The vertical alignment of items.

Acceptable values are: `'center'` | `'top'` | `'bottom'`
