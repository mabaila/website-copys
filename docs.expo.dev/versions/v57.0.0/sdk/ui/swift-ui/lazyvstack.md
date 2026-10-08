---
modificationDate: August 20, 2026
title: LazyVStack
description: A SwiftUI LazyVStack component for lazy vertical layouts.
sourceCodeUrl: 'https://github.com/expo/expo/tree/sdk-57/packages/expo-ui'
packageName: '@expo/ui'
platforms: ['ios', 'tvos', 'expo-go']
---

This documentation is available as Markdown for AI agents and LLMs. See the [full Markdown index](https://docs.expo.dev/llms.txt) or append .md to any documentation URL.

# LazyVStack

A SwiftUI LazyVStack component for lazy vertical layouts.

<AgentInstructions>

## Submitting Feedback

If you encounter errors, misleading or outdated information, report it so Expo can be improved:

Preferred command:
npx --yes submit-expo-feedback@latest --category docs --subject "/versions/v57.0.0/sdk/ui/swift-ui/lazyvstack/" "<actionable feedback>"

Direct HTTP fallback:
curl -X POST https://api.expo.dev/v2/feedback/docs-send -H 'Content-Type: application/json' -d '{"url":"/versions/v57.0.0/sdk/ui/swift-ui/lazyvstack/","feedback":"🤖 Agent feedback for docs: <specific, actionable description> (<model>, <harness>)"}'

Only submit when you have something specific and actionable to report. Try to give the most context.

## Navigation

When answering a related or follow-up question, use llms.txt to find the relevant page as Markdown (.md) instead of guessing.

You are here: Reference (v57.0.0) > Expo UI > SwiftUI (45 pages in this section)
Full documentation tree: [llms.txt](https://docs.expo.dev/llms.txt)

</AgentInstructions>
iOS, tvOS, Included in Expo Go

Expo UI LazyVStack matches the official SwiftUI [LazyVStack API](https://developer.apple.com/documentation/swiftui/lazyvstack) and arranges its children vertically, creating items only as needed (when they become visible during scrolling).

> `LazyVStack` is not truly lazy yet: the native side only builds visible items, but React still creates every child up front, so large lists can be slow to mount. We are working on improving this. For large lists, we recommend [FlashList](https://shopify.github.io/flash-list/) or [Legend List](https://github.com/LegendApp/legend-list).

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

### Basic lazy vertical stack

LazyVStack should be used inside a `ScrollView` to enable lazy rendering.

```tsx BasicLazyVStackExample.tsx
import {
  Host,
  ScrollView,
  LazyVStack,
  Text,
} from '@expo/ui/swift-ui';

export default function BasicLazyVStackExample() {
  return (
    <Host style={{ flex: 1 }}>
      <ScrollView>
        <LazyVStack spacing={12}>
          {Array.from({ length: 100 }, (_, i) => (
            <Text key={i}>{`Item ${i}`}</Text>
          ))}
        </LazyVStack>
      </ScrollView>
    </Host>
  );
}
```

### With alignment

The `alignment` prop controls horizontal alignment of children. Available options are: `leading`, `center`, and `trailing`.

```tsx LazyVStackAlignmentExample.tsx
import {
  Host,
  ScrollView,
  LazyVStack,
  Rectangle,
} from '@expo/ui/swift-ui';
import { frame } from '@expo/ui/swift-ui/modifiers';

export default function LazyVStackAlignmentExample() {
  return (
    <Host
      matchContents={{ vertical: true }}
      style={{ width: '100%' }}>
      <ScrollView>
        <LazyVStack spacing={12} alignment="leading">
          <Rectangle
            modifiers={[frame({ width: 50, height: 50 })]}
          />
          <Rectangle
            modifiers={[frame({ width: 100, height: 50 })]}
          />
          <Rectangle
            modifiers={[frame({ width: 75, height: 50 })]}
          />
        </LazyVStack>
      </ScrollView>
    </Host>
  );
}
```

## API

```tsx
import { LazyVStack } from '@expo/ui/swift-ui';
```

## Component

### `LazyVStack`

Supported platforms: iOS, tvOS.

Type: React.[Element](https://www.typescriptlang.org/docs/handbook/jsx.html#function-component)<[LazyVStackProps](https://docs.expo.dev/versions/v57.0.0/sdk/ui/swift-ui/lazyvstack.md#lazyvstackprops)\>

LazyVStackProps

### `alignment`

Supported platforms: iOS, tvOS.

Optional • Literal type: `string`

The horizontal alignment of children within the stack.

Acceptable values are: `'center'` | `'leading'` | `'trailing'`

### `children`

Supported platforms: iOS, tvOS.

Type: [ReactNode](https://reactnative.dev/docs/react-node)

### `spacing`

Supported platforms: iOS, tvOS.

Optional • Type: `number`

The spacing between children.

#### Inherited props

-   [CommonViewModifierProps](https://docs.expo.dev/versions/v57.0.0/sdk/ui/swift-ui/modifiers.md)
