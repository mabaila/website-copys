---
modificationDate: August 18, 2026
title: ContextMenu
description: A SwiftUI ContextMenu component for displaying context menus.
sourceCodeUrl: 'https://github.com/expo/expo/tree/sdk-57/packages/expo-ui'
packageName: '@expo/ui'
platforms: ['ios', 'tvos', 'expo-go']
---

This documentation is available as Markdown for AI agents and LLMs. See the [full Markdown index](https://docs.expo.dev/llms.txt) or append .md to any documentation URL.

# ContextMenu

A SwiftUI ContextMenu component for displaying context menus.

<AgentInstructions>

## Submitting Feedback

If you encounter errors, misleading or outdated information, report it so Expo can be improved:

Preferred command:
npx --yes submit-expo-feedback@latest --category docs --subject "/versions/v57.0.0/sdk/ui/swift-ui/contextmenu/" "<actionable feedback>"

Direct HTTP fallback:
curl -X POST https://api.expo.dev/v2/feedback/docs-send -H 'Content-Type: application/json' -d '{"url":"/versions/v57.0.0/sdk/ui/swift-ui/contextmenu/","feedback":"🤖 Agent feedback for docs: <specific, actionable description> (<model>, <harness>)"}'

Only submit when you have something specific and actionable to report. Try to give the most context.

## Navigation

When answering a related or follow-up question, use llms.txt to find the relevant page as Markdown (.md) instead of guessing.

You are here: Reference (v57.0.0) > Expo UI > SwiftUI (45 pages in this section)
Full documentation tree: [llms.txt](https://docs.expo.dev/llms.txt)

</AgentInstructions>
iOS, tvOS, Included in Expo Go

Expo UI ContextMenu matches the official SwiftUI [contextMenu API](https://developer.apple.com/documentation/swiftui/view/contextmenu\(menuitems:\)) and displays a menu when long-pressed. For single-tap menu interactions, use [`Menu`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/swift-ui/menu.md) instead.

Image: A long-pressed tile shown as an enlarged preview with a Share, Favorite, Delete menu beneath it

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

### Basic context menu

```tsx BasicContextMenuExample.tsx
import { Host, ContextMenu, Button, Text } from '@expo/ui/swift-ui';

export default function BasicContextMenuExample() {
  return (
    <Host style={{ flex: 1 }}>
      <ContextMenu>
        <ContextMenu.Items>
          <Button
            label="Edit"
            onPress={() => console.log('Edit')}
          />
          <Button
            label="Delete"
            role="destructive"
            onPress={() => console.log('Delete')}
          />
        </ContextMenu.Items>
        <ContextMenu.Trigger>
          <Text>Long press me</Text>
        </ContextMenu.Trigger>
      </ContextMenu>
    </Host>
  );
}
```

### Context menu with system images

```tsx ContextMenuWithImagesExample.tsx
import { Host, ContextMenu, Button, Text } from '@expo/ui/swift-ui';

export default function ContextMenuWithImagesExample() {
  return (
    <Host style={{ flex: 1 }}>
      <ContextMenu>
        <ContextMenu.Items>
          <Button
            label="Share"
            systemImage="square.and.arrow.up"
            onPress={() => console.log('Share')}
          />
          <Button
            label="Favorite"
            systemImage="heart"
            onPress={() => console.log('Favorite')}
          />
          <Button
            label="Delete"
            systemImage="trash"
            role="destructive"
            onPress={() => console.log('Delete')}
          />
        </ContextMenu.Items>
        <ContextMenu.Trigger>
          <Text>Long press me</Text>
        </ContextMenu.Trigger>
      </ContextMenu>
    </Host>
  );
}
```

### Context menu with preview

Use `ContextMenu.Preview` to show a custom preview above the menu when opened.

```tsx ContextMenuWithPreviewExample.tsx
import { View, Text as RNText } from 'react-native';
import {
  Host,
  ContextMenu,
  Button,
  RNHostView,
  Text,
} from '@expo/ui/swift-ui';

export default function ContextMenuWithPreviewExample() {
  return (
    <Host style={{ flex: 1 }}>
      <ContextMenu>
        <ContextMenu.Items>
          <Button
            label="Edit"
            onPress={() => console.log('Edit')}
          />
          <Button
            label="Delete"
            role="destructive"
            onPress={() => console.log('Delete')}
          />
        </ContextMenu.Items>
        <ContextMenu.Trigger>
          <Text>Long press me</Text>
        </ContextMenu.Trigger>
        <ContextMenu.Preview>
          <RNHostView matchContents>
            <View
              style={{
                width: 200,
                height: 100,
                backgroundColor: '#f0f0f0',
                padding: 16,
              }}>
              <RNText>Preview content</RNText>
            </View>
          </RNHostView>
        </ContextMenu.Preview>
      </ContextMenu>
    </Host>
  );
}
```

### Context menu with picker

```tsx ContextMenuWithPickerExample.tsx
import { useState } from 'react';
import {
  Host,
  ContextMenu,
  Button,
  Text,
  Picker,
} from '@expo/ui/swift-ui';
import { pickerStyle, tag } from '@expo/ui/swift-ui/modifiers';

export default function ContextMenuWithPickerExample() {
  const [selectedIndex, setSelectedIndex] = useState<
    number | undefined
  >(0);

  return (
    <Host style={{ flex: 1 }}>
      <ContextMenu>
        <ContextMenu.Items>
          <Button
            label="Action"
            onPress={() => console.log('Action')}
          />
          <Picker
            label="Size"
            modifiers={[pickerStyle('menu')]}
            selection={selectedIndex}
            onSelectionChange={setSelectedIndex}>
            {['Small', 'Medium', 'Large'].map((option, index) => (
              <Text key={index} modifiers={[tag(index)]}>
                {option}
              </Text>
            ))}
          </Picker>
        </ContextMenu.Items>
        <ContextMenu.Trigger>
          <Text>Long press me</Text>
        </ContextMenu.Trigger>
      </ContextMenu>
    </Host>
  );
}
```

### Context menu with sections

Use `Section` and `Divider` components to organize menu items.

```tsx ContextMenuWithSectionsExample.tsx
import {
  Host,
  ContextMenu,
  Button,
  Text,
  Section,
  Divider,
} from '@expo/ui/swift-ui';

export default function ContextMenuWithSectionsExample() {
  return (
    <Host style={{ flex: 1 }}>
      <ContextMenu>
        <ContextMenu.Items>
          <Section title="Actions">
            <Button
              label="Edit"
              onPress={() => console.log('Edit')}
            />
            <Button
              label="Duplicate"
              onPress={() => console.log('Duplicate')}
            />
          </Section>
          <Divider />
          <Button
            label="Delete"
            role="destructive"
            onPress={() => console.log('Delete')}
          />
        </ContextMenu.Items>
        <ContextMenu.Trigger>
          <Text>Long press me</Text>
        </ContextMenu.Trigger>
      </ContextMenu>
    </Host>
  );
}
```

### Disabled items

Use the [`disabled(true)`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/swift-ui/modifiers.md#disableddisabled) modifier on a menu `Button` to render it greyed-out and non-interactive.

```tsx DisabledContextMenuItemExample.tsx
import { Host, ContextMenu, Button, Text } from '@expo/ui/swift-ui';
import { disabled } from '@expo/ui/swift-ui/modifiers';

export default function DisabledContextMenuItemExample() {
  return (
    <Host style={{ flex: 1 }}>
      <ContextMenu>
        <ContextMenu.Items>
          <Button
            label="Edit"
            onPress={() => console.log('Edit')}
          />
          <Button
            label="Locked"
            systemImage="lock"
            modifiers={[disabled(true)]}
            onPress={() => console.log('This never fires')}
          />
        </ContextMenu.Items>
        <ContextMenu.Trigger>
          <Text>Long press me</Text>
        </ContextMenu.Trigger>
      </ContextMenu>
    </Host>
  );
}
```

### Selectable items (checkmarks)

A SwiftUI [`Toggle`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/swift-ui/toggle.md) inside `ContextMenu.Items` automatically renders as a row with a leading SF Symbol and a trailing checkmark when `isOn` is `true`.

```tsx CheckmarkContextMenuItemExample.tsx
import { Host, ContextMenu, Toggle, Text } from '@expo/ui/swift-ui';
import { useState } from 'react';

export default function CheckmarkContextMenuItemExample() {
  const [pinned, setPinned] = useState(false);

  return (
    <Host style={{ flex: 1 }}>
      <ContextMenu>
        <ContextMenu.Items>
          <Toggle
            isOn={pinned}
            label="Pin"
            systemImage="pin"
            onIsOnChange={setPinned}
          />
        </ContextMenu.Items>
        <ContextMenu.Trigger>
          <Text>Long press me</Text>
        </ContextMenu.Trigger>
      </ContextMenu>
    </Host>
  );
}
```

### Nested context menus

Use nested `ContextMenu` components to create submenus.

```tsx NestedContextMenuExample.tsx
import { Host, ContextMenu, Button, Text } from '@expo/ui/swift-ui';

export default function NestedContextMenuExample() {
  return (
    <Host style={{ flex: 1 }}>
      <ContextMenu>
        <ContextMenu.Items>
          <Button
            label="Action"
            onPress={() => console.log('Action')}
          />
          <ContextMenu>
            <ContextMenu.Items>
              <Button
                label="Sub Action 1"
                onPress={() => console.log('Sub 1')}
              />
              <Button
                label="Sub Action 2"
                onPress={() => console.log('Sub 2')}
              />
            </ContextMenu.Items>
            <ContextMenu.Trigger>
              <Button label="More Options" />
            </ContextMenu.Trigger>
          </ContextMenu>
        </ContextMenu.Items>
        <ContextMenu.Trigger>
          <Text>Long press me</Text>
        </ContextMenu.Trigger>
      </ContextMenu>
    </Host>
  );
}
```

## API

```tsx
import { ContextMenu } from '@expo/ui/swift-ui';
```

## Components

### `ContextMenu`

Supported platforms: iOS, tvOS.

Type: React.[Element](https://www.typescriptlang.org/docs/handbook/jsx.html#function-component)<[ContextMenuProps](https://docs.expo.dev/versions/v57.0.0/sdk/ui/swift-ui/contextmenu.md#contextmenuprops)\>

`ContextMenu` allows you to create a context menu, which can be used to provide additional options to the user.

Props of the `ContextMenu` component.

ContextMenuProps

### `children`

Supported platforms: iOS, tvOS.

Type: [ReactNode](https://reactnative.dev/docs/react-node)

The contents of the context menu. Should include `ContextMenu.Trigger`, `ContextMenu.Items`, and optionally `ContextMenu.Preview`.

#### Inherited props

-   [CommonViewModifierProps](https://docs.expo.dev/versions/v57.0.0/sdk/ui/swift-ui/modifiers.md)

### `Items`

Supported platforms: iOS, tvOS.

Type: React.[Element](https://www.typescriptlang.org/docs/handbook/jsx.html#function-component)<{ children: [ReactNode](https://reactnative.dev/docs/react-node) }\>

Items visible inside the context menu. It could be `Section`, `Divider`, `Button`, `Toggle`, `Picker` or even `ContextMenu` itself for nested menus. Remember to use components from the `@expo/ui/swift-ui` library.

### `Preview`

Supported platforms: iOS, tvOS.

Type: React.[Element](https://www.typescriptlang.org/docs/handbook/jsx.html#function-component)<{ children: [ReactNode](https://reactnative.dev/docs/react-node) }\>

The component visible above the menu when it is opened.

### `Trigger`

Supported platforms: iOS, tvOS.

Type: React.[Element](https://www.typescriptlang.org/docs/handbook/jsx.html#function-component)<{ children: [ReactNode](https://reactnative.dev/docs/react-node) }\>

The component visible all the time that triggers the context menu when long-pressed.
