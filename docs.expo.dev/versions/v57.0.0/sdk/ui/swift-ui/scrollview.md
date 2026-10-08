---
modificationDate: September 18, 2026
title: ScrollView
description: A SwiftUI ScrollView component for scrollable content.
sourceCodeUrl: 'https://github.com/expo/expo/tree/sdk-57/packages/expo-ui'
packageName: '@expo/ui'
platforms: ['ios', 'tvos', 'expo-go']
---

This documentation is available as Markdown for AI agents and LLMs. See the [full Markdown index](https://docs.expo.dev/llms.txt) or append .md to any documentation URL.

# ScrollView

A SwiftUI ScrollView component for scrollable content.

<AgentInstructions>

## Submitting Feedback

If you encounter errors, misleading or outdated information, report it so Expo can be improved:

Preferred command:
npx --yes submit-expo-feedback@latest --category docs --subject "/versions/v57.0.0/sdk/ui/swift-ui/scrollview/" "<actionable feedback>"

Direct HTTP fallback:
curl -X POST https://api.expo.dev/v2/feedback/docs-send -H 'Content-Type: application/json' -d '{"url":"/versions/v57.0.0/sdk/ui/swift-ui/scrollview/","feedback":"🤖 Agent feedback for docs: <specific, actionable description> (<model>, <harness>)"}'

Only submit when you have something specific and actionable to report. Try to give the most context.

## Navigation

When answering a related or follow-up question, use llms.txt to find the relevant page as Markdown (.md) instead of guessing.

You are here: Reference (v57.0.0) > Expo UI > SwiftUI (45 pages in this section)
Full documentation tree: [llms.txt](https://docs.expo.dev/llms.txt)

</AgentInstructions>
iOS, tvOS, Included in Expo Go

> For cross-platform usage, see the universal [`ScrollView`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/universal/scrollview.md) — it renders the appropriate native component per platform.

Expo UI ScrollView matches the official SwiftUI [ScrollView API](https://developer.apple.com/documentation/swiftui/scrollview) and provides a scrollable container for its children.

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

### Basic vertical scroll view

A simple vertically scrollable list of text items.

```tsx ScrollViewVerticalExample.tsx
import { Host, ScrollView, VStack, Text } from '@expo/ui/swift-ui';
import { padding } from '@expo/ui/swift-ui/modifiers';

export default function ScrollViewVerticalExample() {
  return (
    <Host style={{ flex: 1 }}>
      <ScrollView>
        <VStack spacing={8}>
          {Array.from({ length: 30 }, (_, i) => (
            <Text key={i} modifiers={[padding({ horizontal: 16 })]}>
              {`Item ${i + 1}`}
            </Text>
          ))}
        </VStack>
      </ScrollView>
    </Host>
  );
}
```

### Horizontal scroll view

Use the `axes` prop to scroll horizontally.

```tsx ScrollViewHorizontalExample.tsx
import {
  Host,
  ScrollView,
  HStack,
  RoundedRectangle,
} from '@expo/ui/swift-ui';
import {
  frame,
  foregroundStyle,
} from '@expo/ui/swift-ui/modifiers';

export default function ScrollViewHorizontalExample() {
  return (
    <Host style={{ flex: 1 }}>
      <ScrollView axes="horizontal">
        <HStack spacing={8}>
          {Array.from({ length: 20 }, (_, i) => (
            <RoundedRectangle
              key={i}
              cornerRadius={12}
              modifiers={[
                frame({ width: 100, height: 100 }),
                foregroundStyle(`hsl(${i * 18}, 70%, 50%)`),
              ]}
            />
          ))}
        </HStack>
      </ScrollView>
    </Host>
  );
}
```

### Hidden scroll indicators

Set `showsIndicators` to `false` to hide the scroll bars.

```tsx ScrollViewHiddenIndicatorsExample.tsx
import { Host, ScrollView, VStack, Text } from '@expo/ui/swift-ui';

export default function ScrollViewHiddenIndicatorsExample() {
  return (
    <Host style={{ flex: 1 }}>
      <ScrollView showsIndicators={false}>
        <VStack spacing={8}>
          {Array.from({ length: 30 }, (_, i) => (
            <Text key={i}>{`Item ${i + 1}`}</Text>
          ))}
        </VStack>
      </ScrollView>
    </Host>
  );
}
```

### Shared scroll position

> Requires iOS 17 or later. On older versions, the modifier is a no-op.

Track the leading scroll target id from JavaScript and scroll to a target by writing to the state. Mark each scroll target with the `id` modifier, wrap the content container in `scrollTargetLayout`, and apply the `scrollPosition` modifier to the `ScrollView`. The optional `onChange` callback fires on the JS thread when the leading target changes.

The `scrollPosition` modifier also works on other scrollable containers like `LazyVStack` and `LazyHStack`.

> Writes to `state.value` must run on the UI runtime. Wrap the write in `scheduleOnUI` from `react-native-worklets`, or call them from inside a `'worklet'` function. Writes from the JS runtime trip Main Thread Checker, Xcode's runtime tool that flags UIKit calls made from a background thread.

```tsx ScrollViewSharedPositionExample.tsx
import {
  Button,
  Host,
  ScrollView,
  Text,
  VStack,
  useNativeState,
} from '@expo/ui/swift-ui';
import {
  id,
  padding,
  scrollPosition,
  scrollTargetLayout,
} from '@expo/ui/swift-ui/modifiers';
import { scheduleOnUI } from 'react-native-worklets';

export default function ScrollViewSharedPositionExample() {
  const activeID = useNativeState<string | null>(null);

  return (
    <Host style={{ flex: 1 }}>
      <VStack spacing={12}>
        <ScrollView
          modifiers={[
            scrollPosition(activeID, {
              onChange: newID => {
                console.log('[JS thread] leading target:', newID);
              },
            }),
          ]}>
          <VStack modifiers={[scrollTargetLayout()]}>
            {Array.from({ length: 30 }, (_, i) => (
              <Text
                key={`item-${i}`}
                modifiers={[
                  id(`item-${i}`),
                  padding({ horizontal: 16, vertical: 12 }),
                ]}>
                {`Item ${i}`}
              </Text>
            ))}
          </VStack>
        </ScrollView>
        <Button
          label="Scroll to item 10 from worklet"
          onPress={() => {
            scheduleOnUI(() => {
              'worklet';
              activeID.value = 'item-10';
            });
          }}
        />
      </VStack>
    </Host>
  );
}
```

## API

```tsx
import { ScrollView } from '@expo/ui/swift-ui';
```

## Component

### `ScrollView`

Supported platforms: iOS, tvOS.

Type: React.[Element](https://www.typescriptlang.org/docs/handbook/jsx.html#function-component)<[ScrollViewProps](https://docs.expo.dev/versions/v57.0.0/sdk/ui/swift-ui/scrollview.md#scrollviewprops)\>

SwiftUI `ScrollView` wrapper. To control scroll position, pair this with the `scrollPosition(state, { onChange })` modifier and a `useNativeState`-backed id. Write `state.value = targetId` for an instant scroll, or wrap the write in `withAnimation(...)` from `@expo/ui/swift-ui` for an animated one.

ScrollViewProps

### `axes`

Supported platforms: iOS, tvOS.

Optional • Literal type: `string` • Default: `'vertical'`

The scrollable axes. Pass `'both'` to enable 2D (horizontal + vertical) scrolling.

Acceptable values are: `'vertical'` | `'horizontal'` | `'both'`

### `children`

Supported platforms: iOS, tvOS.

Type: [ReactNode](https://reactnative.dev/docs/react-node)

### `showsIndicators`

Supported platforms: iOS, tvOS.

Optional • Type: `boolean` • Default: `true`

Whether to show scroll indicators. For richer visibility control (e.g. `'never'`) or per-axis control, use the `scrollIndicators(...)` modifier instead.

#### Inherited props

-   [CommonViewModifierProps](https://docs.expo.dev/versions/v57.0.0/sdk/ui/swift-ui/modifiers.md)

## Types

### `ScrollGeometry`

Supported platforms: iOS, tvOS.

Snapshot of a `ScrollView`'s scroll geometry, emitted by the `useScrollGeometryChange(...)` and `onScrollPhaseChange(...)` modifiers (iOS 18+).

| Property | Type | Description |
| --- | --- | --- |
| containerHeight | `number` | Height of the visible scroll container, in points. |
| containerWidth | `number` | Width of the visible scroll container, in points. |
| contentHeight | `number` | Total height of the scrollable content, in points. |
| contentOffsetX | `number` | Horizontal content offset, in points. |
| contentOffsetY | `number` | Vertical content offset, in points. |
| contentWidth | `number` | Total width of the scrollable content, in points. |

### `ScrollPhase`

Supported platforms: iOS, tvOS.

Literal type: `string`

Scroll phase emitted by the `onScrollPhaseChange(...)` modifier. Mirrors SwiftUI's `ScrollPhase` (iOS 18+).

Acceptable values are: `'idle'` | `'tracking'` | `'interacting'` | `'animating'` | `'decelerating'`
