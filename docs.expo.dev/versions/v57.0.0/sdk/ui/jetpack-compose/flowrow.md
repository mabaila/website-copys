---
modificationDate: August 18, 2026
title: FlowRow
description: A Jetpack Compose FlowRow component for wrapping children horizontally.
sourceCodeUrl: 'https://github.com/expo/expo/tree/sdk-57/packages/expo-ui'
packageName: '@expo/ui'
platforms: ['android', 'expo-go']
---

This documentation is available as Markdown for AI agents and LLMs. See the [full Markdown index](https://docs.expo.dev/llms.txt) or append .md to any documentation URL.

# FlowRow

A Jetpack Compose FlowRow component for wrapping children horizontally.

<AgentInstructions>

## Submitting Feedback

If you encounter errors, misleading or outdated information, report it so Expo can be improved:

Preferred command:
npx --yes submit-expo-feedback@latest --category docs --subject "/versions/v57.0.0/sdk/ui/jetpack-compose/flowrow/" "<actionable feedback>"

Direct HTTP fallback:
curl -X POST https://api.expo.dev/v2/feedback/docs-send -H 'Content-Type: application/json' -d '{"url":"/versions/v57.0.0/sdk/ui/jetpack-compose/flowrow/","feedback":"🤖 Agent feedback for docs: <specific, actionable description> (<model>, <harness>)"}'

Only submit when you have something specific and actionable to report. Try to give the most context.

## Navigation

When answering a related or follow-up question, use llms.txt to find the relevant page as Markdown (.md) instead of guessing.

You are here: Reference (v57.0.0) > Expo UI > Jetpack Compose (51 pages in this section)
Full documentation tree: [llms.txt](https://docs.expo.dev/llms.txt)

</AgentInstructions>
Android, Included in Expo Go

Expo UI FlowRow matches the official Jetpack Compose [FlowRow](https://developer.android.com/reference/kotlin/androidx/compose/foundation/layout/package-summary#FlowRow) API and arranges children in a horizontal flow that wraps to the next line when it runs out of space.

Image: Six assist chip tags wrapping across multiple lines

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

`FlowRow` arranges children in a horizontal flow that wraps to the next line when it runs out of space.

```tsx FlowRowExample.tsx
import {
  Host,
  FlowRow,
  Text,
  useMaterialColors,
} from '@expo/ui/jetpack-compose';
import {
  border,
  padding,
  paddingAll,
} from '@expo/ui/jetpack-compose/modifiers';

export default function FlowRowExample() {
  const colors = useMaterialColors();
  const tags = [
    'React Native',
    'Expo',
    'Android',
    'Jetpack Compose',
    'Material 3',
    'Kotlin',
  ];

  return (
    <Host style={{ flex: 1 }}>
      <FlowRow
        horizontalArrangement={{ spacedBy: 8 }}
        verticalArrangement={{ spacedBy: 8 }}
        modifiers={[paddingAll(16)]}>
        {tags.map(tag => (
          <Text
            key={tag}
            style={{ fontSize: 28 }}
            color={colors.onBackground}
            modifiers={[
              border(1, colors.outline),
              padding(12, 6, 12, 6),
            ]}>
            {tag}
          </Text>
        ))}
      </FlowRow>
    </Host>
  );
}
```

## API

```tsx
import { FlowRow } from '@expo/ui/jetpack-compose';
```

## Component

### `FlowRow`

Supported platforms: Android.

Type: React.[Element](https://www.typescriptlang.org/docs/handbook/jsx.html#function-component)<[FlowRowProps](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/flowrow.md#flowrowprops)\>

FlowRowProps

### `children`

Supported platforms: Android.

Optional • Type: [ReactNode](https://reactnative.dev/docs/react-node)

### `horizontalArrangement`

Supported platforms: Android.

Optional • Type: `HorizontalArrangement`

Horizontal arrangement of children.

### `verticalArrangement`

Supported platforms: Android.

Optional • Type: `VerticalArrangement`

Vertical arrangement of children.

#### Inherited props

-   `PrimitiveBaseProps`
