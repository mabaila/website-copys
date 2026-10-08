---
modificationDate: August 18, 2026
title: LazyColumn
description: A Jetpack Compose LazyColumn component for displaying scrollable lists.
sourceCodeUrl: 'https://github.com/expo/expo/tree/sdk-57/packages/expo-ui'
packageName: '@expo/ui'
platforms: ['android', 'expo-go']
---

This documentation is available as Markdown for AI agents and LLMs. See the [full Markdown index](https://docs.expo.dev/llms.txt) or append .md to any documentation URL.

# LazyColumn

A Jetpack Compose LazyColumn component for displaying scrollable lists.

<AgentInstructions>

## Submitting Feedback

If you encounter errors, misleading or outdated information, report it so Expo can be improved:

Preferred command:
npx --yes submit-expo-feedback@latest --category docs --subject "/versions/v57.0.0/sdk/ui/jetpack-compose/lazycolumn/" "<actionable feedback>"

Direct HTTP fallback:
curl -X POST https://api.expo.dev/v2/feedback/docs-send -H 'Content-Type: application/json' -d '{"url":"/versions/v57.0.0/sdk/ui/jetpack-compose/lazycolumn/","feedback":"🤖 Agent feedback for docs: <specific, actionable description> (<model>, <harness>)"}'

Only submit when you have something specific and actionable to report. Try to give the most context.

## Navigation

When answering a related or follow-up question, use llms.txt to find the relevant page as Markdown (.md) instead of guessing.

You are here: Reference (v57.0.0) > Expo UI > Jetpack Compose (51 pages in this section)
Full documentation tree: [llms.txt](https://docs.expo.dev/llms.txt)

</AgentInstructions>
Android, Included in Expo Go

A lazily-loaded vertical list component that only renders visible items for efficient scrolling. See the [official Jetpack Compose documentation](https://developer.android.com/develop/ui/compose/lists) for more information.

> `LazyColumn` is not truly lazy yet: the native side only composes visible items, but React still creates every child up front, so large lists can be slow to mount. We are working on improving this. For large lists, we recommend [FlashList](https://shopify.github.io/flash-list/) or [Legend List](https://github.com/LegendApp/legend-list).

Image: LazyColumn rendering a settings list of five Material 3 list items

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

### Basic lazy column

```tsx BasicLazyColumn.tsx
import {
  Host,
  LazyColumn,
  ListItem,
  Text,
} from '@expo/ui/jetpack-compose';

const items = Array.from(
  { length: 100 },
  (_, i) => `Item ${i + 1}`
);

export default function BasicLazyColumn() {
  return (
    <Host style={{ height: 400 }}>
      <LazyColumn>
        {items.map(item => (
          <ListItem key={item}>
            <ListItem.HeadlineContent>
              <Text>{item}</Text>
            </ListItem.HeadlineContent>
          </ListItem>
        ))}
      </LazyColumn>
    </Host>
  );
}
```

### With arrangement

Use the `verticalArrangement` prop to control how items are spaced within the list. Pass a string value like `'spaceBetween'` or an object like `{ spacedBy: 8 }` for fixed spacing in dp.

```tsx LazyColumnArrangement.tsx
import {
  Host,
  LazyColumn,
  ListItem,
  Text,
} from '@expo/ui/jetpack-compose';

export default function LazyColumnArrangement() {
  return (
    <Host style={{ height: 400 }}>
      <LazyColumn
        verticalArrangement={{ spacedBy: 8 }}
        horizontalAlignment="center">
        <ListItem>
          <ListItem.HeadlineContent>
            <Text>Spaced Item 1</Text>
          </ListItem.HeadlineContent>
        </ListItem>
        <ListItem>
          <ListItem.HeadlineContent>
            <Text>Spaced Item 2</Text>
          </ListItem.HeadlineContent>
        </ListItem>
        <ListItem>
          <ListItem.HeadlineContent>
            <Text>Spaced Item 3</Text>
          </ListItem.HeadlineContent>
        </ListItem>
      </LazyColumn>
    </Host>
  );
}
```

### With content padding

Use the `contentPadding` prop to add padding around the list content in dp.

```tsx LazyColumnPadding.tsx
import {
  Host,
  LazyColumn,
  ListItem,
  Text,
} from '@expo/ui/jetpack-compose';

export default function LazyColumnPadding() {
  return (
    <Host style={{ height: 400 }}>
      <LazyColumn
        contentPadding={{ start: 16, top: 8, end: 16, bottom: 8 }}>
        <ListItem>
          <ListItem.HeadlineContent>
            <Text>Padded item 1</Text>
          </ListItem.HeadlineContent>
        </ListItem>
        <ListItem>
          <ListItem.HeadlineContent>
            <Text>Padded item 2</Text>
          </ListItem.HeadlineContent>
        </ListItem>
        <ListItem>
          <ListItem.HeadlineContent>
            <Text>Padded item 3</Text>
          </ListItem.HeadlineContent>
        </ListItem>
      </LazyColumn>
    </Host>
  );
}
```

## API

```tsx
import { LazyColumn } from '@expo/ui/jetpack-compose';
```

## Component

### `LazyColumn`

Supported platforms: Android.

Type: React.[Element](https://www.typescriptlang.org/docs/handbook/jsx.html#function-component)<[LazyColumnProps](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/lazycolumn.md#lazycolumnprops)\>

A lazy column component that efficiently displays a vertically scrolling list.

LazyColumnProps

### `children`

Supported platforms: Android.

Optional • Type: [ReactNode](https://reactnative.dev/docs/react-node)

The content to display inside the lazy column.

### `contentPadding`

Supported platforms: Android.

Optional • Type: [ContentPadding](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/lazycolumn.md#contentpadding)

Content padding in dp.

### `horizontalAlignment`

Supported platforms: Android.

Optional • Literal type: `string`

The horizontal alignment of items.

Acceptable values are: `'start'` | `'end'` | `'center'`

### `modifiers`

Supported platforms: Android.

Optional • Type: `ModifierConfig[]`

Modifiers for the component.

### `verticalArrangement`

Supported platforms: Android.

Optional • Literal type: `union`

The vertical arrangement of items. Can be a preset string or an object with `spacedBy` to specify spacing in dp.

Acceptable values are: `'center'` | `'spaceBetween'` | `'spaceAround'` | `'spaceEvenly'` | `'top'` | `'bottom'` | `{ spacedBy: number }`

## Types

### `ContentPadding`

Supported platforms: Android.

Content padding values for LazyColumn.

| Property | Type | Description |
| --- | --- | --- |
| bottom(optional) | `number` | Bottom padding in dp. |
| end(optional) | `number` | End padding in dp. |
| start(optional) | `number` | Start padding in dp. |
| top(optional) | `number` | Top padding in dp. |
