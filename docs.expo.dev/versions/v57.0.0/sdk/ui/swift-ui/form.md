---
modificationDate: August 18, 2026
title: Form
description: A SwiftUI Form component for collecting user input in a structured layout.
sourceCodeUrl: 'https://github.com/expo/expo/tree/sdk-57/packages/expo-ui'
packageName: '@expo/ui'
platforms: ['ios', 'tvos', 'expo-go']
---

This documentation is available as Markdown for AI agents and LLMs. See the [full Markdown index](https://docs.expo.dev/llms.txt) or append .md to any documentation URL.

# Form

A SwiftUI Form component for collecting user input in a structured layout.

<AgentInstructions>

## Submitting Feedback

If you encounter errors, misleading or outdated information, report it so Expo can be improved:

Preferred command:
npx --yes submit-expo-feedback@latest --category docs --subject "/versions/v57.0.0/sdk/ui/swift-ui/form/" "<actionable feedback>"

Direct HTTP fallback:
curl -X POST https://api.expo.dev/v2/feedback/docs-send -H 'Content-Type: application/json' -d '{"url":"/versions/v57.0.0/sdk/ui/swift-ui/form/","feedback":"🤖 Agent feedback for docs: <specific, actionable description> (<model>, <harness>)"}'

Only submit when you have something specific and actionable to report. Try to give the most context.

## Navigation

When answering a related or follow-up question, use llms.txt to find the relevant page as Markdown (.md) instead of guessing.

You are here: Reference (v57.0.0) > Expo UI > SwiftUI (45 pages in this section)
Full documentation tree: [llms.txt](https://docs.expo.dev/llms.txt)

</AgentInstructions>
iOS, tvOS, Included in Expo Go

Expo UI Form matches the official SwiftUI [Form API](https://developer.apple.com/documentation/swiftui/form). It provides a container for grouping controls used for data entry, such as in settings or inspection panes.

Image: A Form with two grouped Sections of Toggles and a footer caption

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

### Basic form

```tsx BasicFormExample.tsx
import { Host, Form, TextField } from '@expo/ui/swift-ui';

export default function BasicFormExample() {
  return (
    <Host style={{ flex: 1 }}>
      <Form>
        <TextField placeholder="Enter your name" />
      </Form>
    </Host>
  );
}
```

### Form with sections

Use the [`Section`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/swift-ui/section.md) component to group related controls within a form.

```tsx FormWithSectionsExample.tsx
import { useState } from 'react';
import {
  Host,
  Form,
  Section,
  TextField,
  Toggle,
  Button,
} from '@expo/ui/swift-ui';

export default function FormWithSectionsExample() {
  const [notifications, setNotifications] = useState(false);
  const [darkMode, setDarkMode] = useState(false);

  return (
    <Host style={{ flex: 1 }}>
      <Form>
        <Section title="Profile">
          <TextField placeholder="Name" />
          <TextField placeholder="Email" />
        </Section>

        <Section title="Preferences">
          <Toggle
            label="Enable notifications"
            isOn={notifications}
            onIsOnChange={setNotifications}
          />
          <Toggle
            label="Dark mode"
            isOn={darkMode}
            onIsOnChange={setDarkMode}
          />
        </Section>

        <Section>
          <Button
            label="Save changes"
            onPress={() => console.log('Saved!')}
          />
        </Section>
      </Form>
    </Host>
  );
}
```

### Form with custom background

Use the `scrollContentBackground` modifier to customize or hide the form's background.

```tsx FormBackgroundExample.tsx
import { Host, Form, Section, TextField } from '@expo/ui/swift-ui';
import {
  scrollContentBackground,
  background,
} from '@expo/ui/swift-ui/modifiers';

export default function FormBackgroundExample() {
  return (
    <Host style={{ flex: 1 }}>
      <Form
        modifiers={[
          scrollContentBackground('hidden'),
          background('#F0F0F0'),
        ]}>
        <Section title="Custom Background">
          <TextField placeholder="Enter text" />
        </Section>
      </Form>
    </Host>
  );
}
```

### Non-scrollable form

Use the [`scrollDisabled`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/swift-ui/modifiers.md#scrolldisableddisabled) modifier to prevent the form from scrolling.

> **Note:** The `scrollDisabled` modifier is only available on iOS 16+ and tvOS 16+.

```tsx NonScrollableFormExample.tsx
import { useState } from 'react';
import {
  Host,
  Form,
  Section,
  TextField,
  Toggle,
} from '@expo/ui/swift-ui';
import { scrollDisabled } from '@expo/ui/swift-ui/modifiers';

export default function NonScrollableFormExample() {
  const [isOn, setIsOn] = useState(false);

  return (
    <Host style={{ flex: 1 }}>
      <Form modifiers={[scrollDisabled()]}>
        <Section title="Settings">
          <Toggle
            label="Enable feature"
            isOn={isOn}
            onIsOnChange={setIsOn}
          />
        </Section>
      </Form>
    </Host>
  );
}
```

### Pull-to-refresh form

Use the `refreshable` modifier to add pull-to-refresh functionality.

```tsx RefreshableFormExample.tsx
import { useState, useCallback } from 'react';
import { Host, Form, Section, Text } from '@expo/ui/swift-ui';
import { refreshable } from '@expo/ui/swift-ui/modifiers';

export default function RefreshableFormExample() {
  const [lastRefresh, setLastRefresh] = useState(new Date());

  const handleRefresh = useCallback(async () => {
    // Simulate network request
    await new Promise(resolve => setTimeout(resolve, 1500));
    setLastRefresh(new Date());
  }, []);

  return (
    <Host style={{ flex: 1 }}>
      <Form modifiers={[refreshable(handleRefresh)]}>
        <Section title="Pull to refresh">
          <Text>
            Last refreshed: {lastRefresh.toLocaleTimeString()}
          </Text>
        </Section>
      </Form>
    </Host>
  );
}
```

## API

```tsx
import { Form } from '@expo/ui/swift-ui';
```

## Component

### `Form`

Supported platforms: iOS, tvOS.

Type: React.[Element](https://www.typescriptlang.org/docs/handbook/jsx.html#function-component)<[FormProps](https://docs.expo.dev/versions/v57.0.0/sdk/ui/swift-ui/form.md#formprops)\>

FormProps

### `children`

Supported platforms: iOS, tvOS.

Type: [ReactNode](https://reactnative.dev/docs/react-node)

The content of the form.

#### Inherited props

-   [CommonViewModifierProps](https://docs.expo.dev/versions/v57.0.0/sdk/ui/swift-ui/modifiers.md)
