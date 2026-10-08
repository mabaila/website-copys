---
modificationDate: August 18, 2026
title: ProgressView
description: A SwiftUI ProgressView component for displaying progress indicators.
sourceCodeUrl: 'https://github.com/expo/expo/tree/sdk-57/packages/expo-ui'
packageName: '@expo/ui'
platforms: ['ios', 'tvos', 'expo-go']
---

This documentation is available as Markdown for AI agents and LLMs. See the [full Markdown index](https://docs.expo.dev/llms.txt) or append .md to any documentation URL.

# ProgressView

A SwiftUI ProgressView component for displaying progress indicators.

<AgentInstructions>

## Submitting Feedback

If you encounter errors, misleading or outdated information, report it so Expo can be improved:

Preferred command:
npx --yes submit-expo-feedback@latest --category docs --subject "/versions/v57.0.0/sdk/ui/swift-ui/progressview/" "<actionable feedback>"

Direct HTTP fallback:
curl -X POST https://api.expo.dev/v2/feedback/docs-send -H 'Content-Type: application/json' -d '{"url":"/versions/v57.0.0/sdk/ui/swift-ui/progressview/","feedback":"🤖 Agent feedback for docs: <specific, actionable description> (<model>, <harness>)"}'

Only submit when you have something specific and actionable to report. Try to give the most context.

## Navigation

When answering a related or follow-up question, use llms.txt to find the relevant page as Markdown (.md) instead of guessing.

You are here: Reference (v57.0.0) > Expo UI > SwiftUI (45 pages in this section)
Full documentation tree: [llms.txt](https://docs.expo.dev/llms.txt)

</AgentInstructions>
iOS, tvOS, Included in Expo Go

Expo UI ProgressView matches the official SwiftUI [ProgressView API](https://developer.apple.com/documentation/swiftui/progressview) and supports styling via the [`progressViewStyle`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/swift-ui/modifiers.md#progressviewstylestyle) modifier.

Image: Indeterminate spinner and a determinate ProgressView with a label

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

> **Note:** When using the `linear` style (which is the default for determinate progress), `ProgressView` is a flexible-width component, it expands to fill available horizontal space. When using `matchContents` on the `Host`, you should apply a [`frame`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/swift-ui/modifiers.md#frameparams) modifier on the `ProgressView` to give it an explicit width. Alternatively, give the `Host` an explicit size using `style` (for example, `style={{ width: 300 }}` or `style={{ flex: 1 }}`). The `circular` style and indeterminate spinner have a fixed size and work with `matchContents`.

### Indeterminate progress

When no `value` is provided, the progress view displays an indeterminate indicator (spinner).

```tsx IndeterminateExample.tsx
import { Host, ProgressView } from '@expo/ui/swift-ui';

export default function IndeterminateExample() {
  return (
    <Host matchContents>
      <ProgressView />
    </Host>
  );
}
```

### Determinate progress

Provide a `value` between `0` and `1` to show determinate progress.

```tsx DeterminateExample.tsx
import { Host, ProgressView } from '@expo/ui/swift-ui';

export default function DeterminateExample() {
  return (
    <Host style={{ flex: 1 }}>
      <ProgressView value={0.5} />
    </Host>
  );
}
```

### Progress view styles

Use the [`progressViewStyle`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/swift-ui/modifiers.md#progressviewstylestyle) modifier to change the progress view's appearance. Available styles are: `automatic`, `linear`, and `circular`.

```tsx ProgressViewStylesExample.tsx
import {
  Host,
  ProgressView,
  Text,
  VStack,
} from '@expo/ui/swift-ui';
import { progressViewStyle } from '@expo/ui/swift-ui/modifiers';

export default function ProgressViewStylesExample() {
  return (
    <Host style={{ flex: 1 }}>
      <VStack spacing={16}>
        <Text>Linear</Text>
        <ProgressView
          value={0.5}
          modifiers={[progressViewStyle('linear')]}
        />
        <Text>Circular</Text>
        <ProgressView
          value={0.5}
          modifiers={[progressViewStyle('circular')]}
        />
      </VStack>
    </Host>
  );
}
```

### With label

You can pass custom components as `children` to provide a label for the progress view.

```tsx LabelExample.tsx
import { Host, ProgressView, Text } from '@expo/ui/swift-ui';

export default function LabelExample() {
  return (
    <Host style={{ flex: 1 }}>
      <ProgressView value={0.25}>
        <Text>Loading...</Text>
      </ProgressView>
    </Host>
  );
}
```

### Tinted progress view

Use the `tint` modifier to change the progress view's color.

```tsx TintedExample.tsx
import { Host, ProgressView } from '@expo/ui/swift-ui';
import { tint } from '@expo/ui/swift-ui/modifiers';

export default function TintedExample() {
  return (
    <Host style={{ flex: 1 }}>
      <ProgressView value={0.7} modifiers={[tint('red')]} />
    </Host>
  );
}
```

### Timer-based progress

Use the `timerInterval` prop to create a progress view that automatically animates over a time range. This is useful for showing countdown timers or timed operations.

> **Note:** Timer-based progress is only available on iOS 16+ and tvOS 16+.

```tsx TimerExample.tsx
import {
  Host,
  ProgressView,
  Text,
  VStack,
} from '@expo/ui/swift-ui';

export default function TimerExample() {
  const startDate = new Date();
  const endDate = new Date(Date.now() + 10000); // 10 seconds from now

  return (
    <Host style={{ flex: 1 }}>
      <VStack spacing={16}>
        <ProgressView
          timerInterval={{ lower: startDate, upper: endDate }}
        />
        <ProgressView
          timerInterval={{ lower: startDate, upper: endDate }}
          countsDown={false}>
          <Text>Counting up</Text>
        </ProgressView>
      </VStack>
    </Host>
  );
}
```

## API

```tsx
import { ProgressView } from '@expo/ui/swift-ui';
```

## Component

### `ProgressView`

Supported platforms: iOS, tvOS.

Type: React.[Element](https://www.typescriptlang.org/docs/handbook/jsx.html#function-component)<[ProgressViewProps](https://docs.expo.dev/versions/v57.0.0/sdk/ui/swift-ui/progressview.md#progressviewprops)\>

Renders a SwiftUI `ProgressView` component.

ProgressViewProps

### `children`

Supported platforms: iOS, tvOS.

Optional • Type: [ReactNode](https://reactnative.dev/docs/react-node)

A label describing the progress view's purpose.

### `countsDown`

Supported platforms: iOS 16.0+, tvOS 16.0+.

Optional • Type: `boolean` • Default: `true`

A Boolean value that determines whether the view empties or fills as time passes. If `true`, which is the default, the view empties.

### `timerInterval`

Supported platforms: iOS 16.0+, tvOS 16.0+.

Optional • Type: [ClosedRangeDate](https://developer.apple.com/documentation/swift/closedrange)

The lower and upper bounds for automatic timer progress.

### `value`

Supported platforms: iOS, tvOS.

Optional • Literal type: `union`

The current progress value. A value between `0` and `1`. When `undefined`, the progress view displays an indeterminate indicator.

Acceptable values are: `number` | `null`

#### Inherited props

-   [CommonViewModifierProps](https://docs.expo.dev/versions/v57.0.0/sdk/ui/swift-ui/modifiers.md)
