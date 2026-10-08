---
modificationDate: August 31, 2026
title: RNHostView
description: A component that enables React Native views inside SwiftUI.
sourceCodeUrl: 'https://github.com/expo/expo/tree/sdk-57/packages/expo-ui'
packageName: '@expo/ui'
platforms: ['ios', 'tvos', 'expo-go']
---

This documentation is available as Markdown for AI agents and LLMs. See the [full Markdown index](https://docs.expo.dev/llms.txt) or append .md to any documentation URL.

# RNHostView

A component that enables React Native views inside SwiftUI.

<AgentInstructions>

## Submitting Feedback

If you encounter errors, misleading or outdated information, report it so Expo can be improved:

Preferred command:
npx --yes submit-expo-feedback@latest --category docs --subject "/versions/v57.0.0/sdk/ui/swift-ui/rnhostview/" "<actionable feedback>"

Direct HTTP fallback:
curl -X POST https://api.expo.dev/v2/feedback/docs-send -H 'Content-Type: application/json' -d '{"url":"/versions/v57.0.0/sdk/ui/swift-ui/rnhostview/","feedback":"🤖 Agent feedback for docs: <specific, actionable description> (<model>, <harness>)"}'

Only submit when you have something specific and actionable to report. Try to give the most context.

## Navigation

When answering a related or follow-up question, use llms.txt to find the relevant page as Markdown (.md) instead of guessing.

You are here: Reference (v57.0.0) > Expo UI > SwiftUI (45 pages in this section)
Full documentation tree: [llms.txt](https://docs.expo.dev/llms.txt)

</AgentInstructions>
iOS, tvOS, Included in Expo Go

A component that enables proper layout behavior when React Native views are rendered inside SwiftUI components. It syncs layout information from SwiftUI back to React Native's Yoga layout system by updating the shadow node size.

When React Native views are placed inside SwiftUI components like [`BottomSheet`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/swift-ui/bottomsheet.md), [`Popover`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/swift-ui/popover.md) or [`HStack`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/swift-ui/hstack.md) and so on, the layout systems need to communicate. `RNHostView` bridges this gap:

-   **With `matchContents`**: The shadow node size is set to match the child React Native view's intrinsic size, allowing the SwiftUI parent to size itself based on the React Native content.
-   **Without `matchContents`**: The shadow node size is set to match the parent SwiftUI view's size, allowing the React Native content to fill the available space (useful for `flex: 1` layouts).

> **Note:** Pass a single React Native element as the child. `RNHostView` measures and lays out only its first child, so wrap several views in one parent `View` and let that view arrange them.

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

### Basic usage with matchContents

Use `matchContents` when you want the SwiftUI parent to size itself based on the React Native content.

```tsx RNHostView with matchContents
import { useState } from 'react';
import { Pressable, Text, View } from 'react-native';
import {
  Host,
  BottomSheet,
  Button,
  RNHostView,
} from '@expo/ui/swift-ui';

function Example() {
  const [isPresented, setIsPresented] = useState(false);

  return (
    <Host style={{ flex: 1 }}>
      <Button
        label="Open sheet"
        onPress={() => setIsPresented(true)}
      />
      <BottomSheet
        isPresented={isPresented}
        onIsPresentedChange={setIsPresented}>
        <RNHostView matchContents>
          <View style={{ padding: 24 }}>
            <Text style={{ fontSize: 18, fontWeight: 'bold' }}>
              React Native Content
            </Text>
            <Pressable
              style={{
                backgroundColor: '#007AFF',
                padding: 12,
                borderRadius: 8,
                marginTop: 16,
              }}
              onPress={() => setIsPresented(false)}>
              <Text style={{ color: 'white', textAlign: 'center' }}>
                Close
              </Text>
            </Pressable>
          </View>
        </RNHostView>
      </BottomSheet>
    </Host>
  );
}
```

### Flexible content without matchContents

When using `flex: 1` in your React Native content, omit the `matchContents` prop so the content fills the available SwiftUI space.

```tsx RNHostView with flex content
import { useState } from 'react';
import { Text, View } from 'react-native';
import {
  Host,
  BottomSheet,
  Button,
  Group,
  RNHostView,
} from '@expo/ui/swift-ui';
import { presentationDetents } from '@expo/ui/swift-ui/modifiers';

function Example() {
  const [isPresented, setIsPresented] = useState(false);

  return (
    <Host style={{ flex: 1 }}>
      <Button
        label="Open sheet"
        onPress={() => setIsPresented(true)}
      />
      <BottomSheet
        isPresented={isPresented}
        onIsPresentedChange={setIsPresented}>
        <Group
          modifiers={[presentationDetents(['medium', 'large'])]}>
          <RNHostView>
            <View
              style={{
                flex: 1,
                backgroundColor: '#007AFF',
                padding: 24,
              }}>
              <Text style={{ color: 'white', fontSize: 18 }}>
                This content fills the available space
              </Text>
            </View>
          </RNHostView>
        </Group>
      </BottomSheet>
    </Host>
  );
}
```

### Usage with Popover

`RNHostView` works well inside [`Popover`](https://docs.expo.dev/versions/latest/sdk/ui/swift-ui/popover.md) to display interactive React Native content.

```tsx RNHostView in Popover
import { useState } from 'react';
import { Pressable, Text, View } from 'react-native';
import {
  Host,
  Button,
  Popover,
  RNHostView,
} from '@expo/ui/swift-ui';

function Example() {
  const [isPresented, setIsPresented] = useState(false);
  const [counter, setCounter] = useState(0);

  return (
    <Host style={{ flex: 1 }}>
      <Popover
        isPresented={isPresented}
        onIsPresentedChange={setIsPresented}>
        <Popover.Trigger>
          <Button
            onPress={() => setIsPresented(true)}
            label="Show Popover"
          />
        </Popover.Trigger>
        <Popover.Content>
          <RNHostView matchContents>
            <View style={{ padding: 24 }}>
              <Text
                style={{
                  fontSize: 16,
                  fontWeight: 'bold',
                  marginBottom: 8,
                }}>
                React Native Content
              </Text>
              <Text style={{ color: '#666', marginBottom: 12 }}>
                Counter: {counter}
              </Text>
              <Pressable
                style={{
                  backgroundColor: '#007AFF',
                  padding: 12,
                  borderRadius: 8,
                  alignItems: 'center',
                }}
                onPress={() => setCounter(counter + 1)}>
                <Text style={{ color: 'white', fontWeight: '600' }}>
                  Increment
                </Text>
              </Pressable>
            </View>
          </RNHostView>
        </Popover.Content>
      </Popover>
    </Host>
  );
}
```

## API

```tsx
import { RNHostView } from '@expo/ui/swift-ui';
```

## Component

### `RNHostView`

Supported platforms: iOS, tvOS.

Type: React.[Element](https://www.typescriptlang.org/docs/handbook/jsx.html#function-component)<[RNHostViewProps](https://docs.expo.dev/versions/v57.0.0/sdk/ui/swift-ui/rnhostview.md#rnhostviewprops)\>

RNHostViewProps

### `children`

Supported platforms: iOS, tvOS.

Type: `ReactElement`

The RN View to be hosted.

### `matchContents`

Supported platforms: iOS, tvOS.

Optional • Type: `boolean` • Default: `false`

When `true`, the RNHost will update its size in the React Native view tree to match the children's size. When `false`, the RNHost will use the size of the parent SwiftUI View. Can be only set once on mount.
