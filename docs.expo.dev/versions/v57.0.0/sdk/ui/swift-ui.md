---
modificationDate: September 23, 2026
title: SwiftUI
description: SwiftUI components for building native iOS interfaces with @expo/ui.
sourceCodeUrl: 'https://github.com/expo/expo/tree/sdk-57/packages/expo-ui'
packageName: '@expo/ui'
platforms: ['ios', 'tvos', 'expo-go']
---

This documentation is available as Markdown for AI agents and LLMs. See the [full Markdown index](https://docs.expo.dev/llms.txt) or append .md to any documentation URL.

# SwiftUI

SwiftUI components for building native iOS interfaces with @expo/ui.

<AgentInstructions>

## Submitting Feedback

If you encounter errors, misleading or outdated information, report it so Expo can be improved:

Preferred command:
npx --yes submit-expo-feedback@latest --category docs --subject "/versions/v57.0.0/sdk/ui/swift-ui/" "<actionable feedback>"

Direct HTTP fallback:
curl -X POST https://api.expo.dev/v2/feedback/docs-send -H 'Content-Type: application/json' -d '{"url":"/versions/v57.0.0/sdk/ui/swift-ui/","feedback":"🤖 Agent feedback for docs: <specific, actionable description> (<model>, <harness>)"}'

Only submit when you have something specific and actionable to report. Try to give the most context.

## Navigation

When answering a related or follow-up question, use llms.txt to find the relevant page as Markdown (.md) instead of guessing.

You are here: Reference (v57.0.0) > Expo UI > SwiftUI (45 pages in this section)
Full documentation tree: [llms.txt](https://docs.expo.dev/llms.txt)

</AgentInstructions>
iOS, tvOS, Included in Expo Go

The SwiftUI components in `@expo/ui/swift-ui` allow you to build fully native iOS interfaces using SwiftUI from React Native.

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

Expo UI has several SwiftUI components available. You can use them in your app by importing them from `@expo/ui/swift-ui`. However, to cross the boundary from React Native (UIKit) to SwiftUI, you need to use the [`Host`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/swift-ui/host.md) component. The [`Host`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/swift-ui/host.md) is the container for SwiftUI views. You can think of it like [`<svg>`](https://developer.mozilla.org/en-US/docs/Web/SVG/Reference/Element/svg) in the DOM or [`<Canvas>`](https://shopify.github.io/react-native-skia/docs/canvas/overview/) in [`react-native-skia`](https://shopify.github.io/react-native-skia/). Under the hood, it uses [`UIHostingController`](https://developer.apple.com/documentation/swiftui/uihostingcontroller) to render SwiftUI views in UIKit.

```tsx
import { Host, Button } from '@expo/ui/swift-ui';

export function SaveButton() {
  return (
    <Host style={{ flex: 1 }}>
      <Button label="Save changes" />
    </Host>
  );
}
```

[Extending with SwiftUI](https://docs.expo.dev/versions/v57.0.0/sdk/ui/swift-ui/extending.md) — Create custom SwiftUI components and modifiers that integrate with Expo UI.

[Expo UI iOS Liquid Glass Tutorial](https://www.youtube.com/watch?v=2wXYLWz3YEQ) — Learn how to build real SwiftUI views in your React Native app with the new Expo UI.

## Available components

| Component | Description |
| --- | --- |
| [`AccessoryWidgetBackground`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/swift-ui/accessorywidgetbackground.md) | Adaptive background view that provides a standard appearance based on the widget's environment. |
| [`Alert`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/swift-ui/alert.md) | Alert component for presenting native iOS alert dialogs. |
| [`BottomSheet`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/swift-ui/bottomsheet.md) | BottomSheet component that presents content from the bottom of the screen. |
| [`Button`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/swift-ui/button.md) | Button component for displaying native buttons. |
| [`ColorPicker`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/swift-ui/colorpicker.md) | ColorPicker component for selecting colors. |
| [`ConfirmationDialog`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/swift-ui/confirmationdialog.md) | ConfirmationDialog component for presenting confirmation prompts. |
| [`ContextMenu`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/swift-ui/contextmenu.md) | ContextMenu component for displaying context menus. |
| [`ControlGroup`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/swift-ui/controlgroup.md) | ControlGroup component for grouping interactive controls. |
| [`DatePicker`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/swift-ui/datepicker.md) | DatePicker component for selecting dates and times. |
| [`DisclosureGroup`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/swift-ui/disclosuregroup.md) | DisclosureGroup component for displaying expandable content. |
| [`Divider`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/swift-ui/divider.md) | Divider component for creating visual separators. |
| [`Form`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/swift-ui/form.md) | Form component for collecting user input in a structured layout. |
| [`Gauge`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/swift-ui/gauge.md) | Gauge component for displaying progress with visual indicators. |
| [`Group`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/swift-ui/group.md) | Group component for grouping views without affecting layout. |
| [`Host`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/swift-ui/host.md) | Host component that enables SwiftUI components in React Native. |
| [`HStack`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/swift-ui/hstack.md) | HStack component for horizontal layouts. |
| [`Image`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/swift-ui/image.md) | Image component for displaying SF Symbols. |
| [`Label`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/swift-ui/label.md) | Label component for displaying text with an icon. |
| [`LazyHStack`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/swift-ui/lazyhstack.md) | LazyHStack component for lazy horizontal layouts. |
| [`LazyVStack`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/swift-ui/lazyvstack.md) | LazyVStack component for lazy vertical layouts. |
| [`Link`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/swift-ui/link.md) | Link component for displaying clickable links. |
| [`List`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/swift-ui/list.md) | List component for displaying scrollable lists of items. |
| [`Menu`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/swift-ui/menu.md) | Menu component for displaying dropdown menus. |
| [`Modifiers`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/swift-ui/modifiers.md) | View modifiers for customizing component appearance and behavior. |
| [`Namespace`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/swift-ui/namespace.md) | A Namespace component that allows you create Namespaces in SwiftUI |
| [`Overlay`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/swift-ui/overlay.md) | Overlay component for layering content on top of another view. |
| [`Picker`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/swift-ui/picker.md) | Picker component for selecting options from a list. |
| [`Popover`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/swift-ui/popover.md) | Popover component for displaying content in a floating overlay. |
| [`ProgressView`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/swift-ui/progressview.md) | ProgressView component for displaying progress indicators. |
| [`RNHostView`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/swift-ui/rnhostview.md) | A component that enables React Native views inside SwiftUI. |
| [`ScrollView`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/swift-ui/scrollview.md) | ScrollView component for scrollable content. |
| [`Section`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/swift-ui/section.md) | Section component for grouping content within lists and forms. |
| [`SecureField`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/swift-ui/securefield.md) | SecureField component for password input. |
| [`Slider`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/swift-ui/slider.md) | Slider component for selecting values from a range. |
| [`Spacer`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/swift-ui/spacer.md) | Spacer component for flexible spacing. |
| [`SwipeActions`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/swift-ui/swipeactions.md) | SwipeActions component for adding leading and trailing swipe actions to row content. |
| [`TabView`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/swift-ui/tabview.md) | TabView component for paged or tabbed content. |
| [`Text`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/swift-ui/text.md) | Text component for displaying styled text with support for nested texts. |
| [`TextField`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/swift-ui/textfield.md) | TextField component for text input. |
| [`Toggle`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/swift-ui/toggle.md) | Toggle component for displaying native toggles. |
| [`useNativeState`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/swift-ui/usenativestate.md) | A React hook that creates observable state shared between JavaScript and native SwiftUI views. |
| [`VStack`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/swift-ui/vstack.md) | VStack component for vertical layouts. |
| [`ZStack`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/swift-ui/zstack.md) | ZStack component for overlapping layouts. |

## Examples

### Modifiers

[SwiftUI modifiers](https://developer.apple.com/documentation/swiftui/view/modifier\(_:\)) customize the appearance and behavior of SwiftUI components. Expo UI also provides modifiers for SwiftUI components. You can import modifiers from `@expo/ui/swift-ui/modifiers` and pass them as an array to the `modifiers` prop. In the following example, the [`expo-mesh-gradient`](https://docs.expo.dev/versions/v57.0.0/sdk/mesh-gradient.md) and the `glassEffect` modifier are combined to create Liquid Glass text.

> The `glassEffect` modifier requires Xcode 26+ and iOS 26+.

```tsx GlassEffectExample.tsx
import { Host, Text } from '@expo/ui/swift-ui';
import {
  font,
  glassEffect,
  padding,
} from '@expo/ui/swift-ui/modifiers';
import { MeshGradientView } from 'expo-mesh-gradient';
import { View } from 'react-native';

export default function GlassEffectExample() {
  return (
    <View style={{ flex: 1 }}>
      <MeshGradientView
        style={{ flex: 1 }}
        columns={3}
        rows={3}
        colors={[
          'red',
          'purple',
          'indigo',
          'orange',
          'white',
          'blue',
          'yellow',
          'green',
          'cyan',
        ]}
        points={[
          [0.0, 0.0],
          [0.5, 0.0],
          [1.0, 0.0],
          [0.0, 0.5],
          [0.5, 0.5],
          [1.0, 0.5],
          [0.0, 1.0],
          [0.5, 1.0],
          [1.0, 1.0],
        ]}
      />
      <Host
        style={{
          position: 'absolute',
          top: 0,
          right: 0,
          left: 0,
          bottom: 0,
        }}>
        <Text
          modifiers={[
            font({ size: 32 }),
            padding({
              all: 16,
            }),
            glassEffect({
              glass: {
                variant: 'clear',
              },
            }),
          ]}>
          Glass effect text
        </Text>
      </Host>
    </View>
  );
}
```

### iOS Settings app

Combining the Expo UI components and modifiers, you can build a UI like the iOS Settings app.

```tsx SettingsFormExample.tsx
import {
  Button,
  Form,
  Host,
  HStack,
  Image,
  Section,
  Spacer,
  Toggle,
  Text,
} from '@expo/ui/swift-ui';
import {
  background,
  buttonStyle,
  foregroundStyle,
  clipShape,
  frame,
} from '@expo/ui/swift-ui/modifiers';
import { Link } from 'expo-router';
import { useState } from 'react';

export default function SettingsFormExample() {
  const [isAirplaneMode, setIsAirplaneMode] = useState(true);

  return (
    <Host style={{ flex: 1 }}>
      <Form>
        <Section>
          <HStack spacing={8}>
            <Image
              systemName="airplane"
              color="white"
              size={18}
              modifiers={[
                frame({ width: 28, height: 28 }),
                background('#ffa500'),
                clipShape('roundedRectangle'),
              ]}
            />
            <Text>Airplane Mode</Text>
            <Spacer />
            <Toggle
              isOn={isAirplaneMode}
              onIsOnChange={setIsAirplaneMode}
            />
          </HStack>

          <Link href="/wifi" asChild>
            {/* Use buttonStyle('plain') to prevent default blue button styling */}
            <Button modifiers={[buttonStyle('plain')]}>
              <HStack spacing={8}>
                <Image
                  systemName="wifi"
                  color="white"
                  size={18}
                  modifiers={[
                    frame({ width: 28, height: 28 }),
                    background('#007aff'),
                    clipShape('roundedRectangle'),
                  ]}
                />
                {/* Text inside a Link needs an explicit color. A hierarchical style adapts to light and dark mode. */}
                <Text
                  modifiers={[
                    foregroundStyle({
                      type: 'color',
                      color: 'primary',
                    }),
                  ]}>
                  Wi-Fi
                </Text>
                <Spacer />
                <Image
                  systemName="chevron.right"
                  size={14}
                  color="secondary"
                />
              </HStack>
            </Button>
          </Link>
        </Section>
      </Form>
    </Host>
  );
}
```

### Secondary text styling

Use `foregroundStyle` to apply a [hierarchical style](https://docs.expo.dev/versions/v57.0.0/sdk/ui/swift-ui/modifiers.md#foregroundstylestyle), which makes text appear lighter and more subtle.

```tsx SecondaryTextExample.tsx
import {
  Button,
  Form,
  Host,
  HStack,
  Image,
  List,
  Section,
  Spacer,
  Text,
} from '@expo/ui/swift-ui';
import {
  buttonStyle,
  font,
  foregroundStyle,
  padding,
} from '@expo/ui/swift-ui/modifiers';

export default function SecondaryTextExample() {
  return (
    <Host style={{ flex: 1 }}>
      <Form>
        <Section>
          <List>
            <Button
              onPress={() => console.log('Navigate')}
              modifiers={[buttonStyle('plain')]}>
              <HStack>
                <Text>Night Shift</Text>
                <Spacer />
                <Text
                  modifiers={[
                    foregroundStyle({
                      type: 'hierarchical',
                      style: 'secondary',
                    }),
                    padding({ trailing: 8 }),
                  ]}>
                  22:00 to 07:00
                </Text>
                <Image
                  systemName="chevron.right"
                  size={14}
                  color="#C7C7CC"
                />
              </HStack>
            </Button>
          </List>
          <List>
            <Text
              modifiers={[
                foregroundStyle({
                  type: 'hierarchical',
                  style: 'secondary',
                }),
                font({ size: 14 }),
              ]}>
              Save up to 280.7 MB. This will permanently delete all
              photos and videos kept in the "Recently Deleted"
              album.
            </Text>
          </List>
        </Section>
      </Form>
    </Host>
  );
}
```

### Slider with icons

A common pattern for brightness or volume controls is to flank a `Slider` with icons.

```tsx SliderWithIconsExample.tsx
import { useState } from 'react';
import {
  Form,
  Host,
  HStack,
  Image,
  List,
  Section,
  Slider,
  Spacer,
  Text,
  Toggle,
} from '@expo/ui/swift-ui';
import { padding } from '@expo/ui/swift-ui/modifiers';

export default function SliderWithIconsExample() {
  const [brightness, setBrightness] = useState(0.5);
  const [trueToneEnabled, setTrueToneEnabled] = useState(true);

  return (
    <Host style={{ flex: 1 }}>
      <Form>
        <Section
          header={<Text>Brightness</Text>}
          footer={
            <Text>
              Automatically adapt iPhone display based on ambient
              lighting conditions to make colors appear consistent
              in different environments.
            </Text>
          }>
          <List>
            <HStack modifiers={[padding({ vertical: 6 })]}>
              <Image
                systemName="sun.min.fill"
                size={22}
                color="#8E8E93"
              />
              <Spacer />
              <Slider
                value={brightness}
                onValueChange={setBrightness}
              />
              <Spacer />
              <Image
                systemName="sun.max.fill"
                size={22}
                color="#8E8E93"
              />
            </HStack>
            <Toggle
              label="True Tone"
              isOn={trueToneEnabled}
              onIsOnChange={setTrueToneEnabled}
            />
          </List>
        </Section>
      </Form>
    </Host>
  );
}
```

### Multi-line list items

Use `VStack` with `alignment="leading"` for list items with a title and subtitle.

```tsx MultiLineListItemExample.tsx
import {
  Button,
  Form,
  Host,
  HStack,
  Image,
  List,
  Section,
  Spacer,
  Text,
  VStack,
} from '@expo/ui/swift-ui';
import {
  buttonStyle,
  font,
  foregroundStyle,
  padding,
} from '@expo/ui/swift-ui/modifiers';

export default function MultiLineListItemExample() {
  return (
    <Host style={{ flex: 1 }}>
      <Form>
        <Section>
          <List>
            <HStack>
              <Image
                systemName="safari"
                size={22}
                modifiers={[padding({ trailing: 6 })]}
              />
              <Spacer />
              <Button
                onPress={() => console.log('Navigate')}
                modifiers={[
                  buttonStyle('plain'),
                  padding({ vertical: 6 }),
                ]}>
                <VStack spacing={4} alignment="leading">
                  <Text>Chrome</Text>
                  <Text
                    modifiers={[
                      foregroundStyle({
                        type: 'hierarchical',
                        style: 'secondary',
                      }),
                      font({ size: 14 }),
                    ]}>
                    Last used: Today
                  </Text>
                </VStack>
                <Spacer />
                <Text
                  modifiers={[
                    foregroundStyle({
                      type: 'hierarchical',
                      style: 'secondary',
                    }),
                    font({ size: 16 }),
                  ]}>
                  1.57 GB
                </Text>
                <Image
                  systemName="chevron.right"
                  size={14}
                  color="#C7C7CC"
                />
              </Button>
            </HStack>
          </List>
        </Section>
      </Form>
    </Host>
  );
}
```
