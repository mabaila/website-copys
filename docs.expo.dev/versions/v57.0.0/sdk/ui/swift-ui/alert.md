---
modificationDate: August 18, 2026
title: Alert
description: A SwiftUI Alert component for presenting native iOS alert dialogs.
sourceCodeUrl: 'https://github.com/expo/expo/tree/sdk-57/packages/expo-ui'
packageName: '@expo/ui'
platforms: ['ios', 'tvos', 'expo-go']
---

This documentation is available as Markdown for AI agents and LLMs. See the [full Markdown index](https://docs.expo.dev/llms.txt) or append .md to any documentation URL.

# Alert

A SwiftUI Alert component for presenting native iOS alert dialogs.

<AgentInstructions>

## Submitting Feedback

If you encounter errors, misleading or outdated information, report it so Expo can be improved:

Preferred command:
npx --yes submit-expo-feedback@latest --category docs --subject "/versions/v57.0.0/sdk/ui/swift-ui/alert/" "<actionable feedback>"

Direct HTTP fallback:
curl -X POST https://api.expo.dev/v2/feedback/docs-send -H 'Content-Type: application/json' -d '{"url":"/versions/v57.0.0/sdk/ui/swift-ui/alert/","feedback":"🤖 Agent feedback for docs: <specific, actionable description> (<model>, <harness>)"}'

Only submit when you have something specific and actionable to report. Try to give the most context.

## Navigation

When answering a related or follow-up question, use llms.txt to find the relevant page as Markdown (.md) instead of guessing.

You are here: Reference (v57.0.0) > Expo UI > SwiftUI (45 pages in this section)
Full documentation tree: [llms.txt](https://docs.expo.dev/llms.txt)

</AgentInstructions>
iOS, tvOS, Included in Expo Go

Expo UI Alert matches the official SwiftUI [alert API](https://developer.apple.com/documentation/swiftui/view/alert\(_:ispresented:actions:message:\)) and presents a native iOS alert dialog with a title, actions, and an optional message.

Image: Alert asking the user to confirm signing out

`Alert` is the centered modal counterpart to [`ConfirmationDialog`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/swift-ui/confirmationdialog.md), which renders as an action sheet from the bottom of the screen. Both share the same trigger/actions/message slot model so callers can swap between them by changing the component name.

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

### Basic alert

Use `Alert.Trigger` to define the visible element and `Alert.Actions` to provide the dialog buttons.

```tsx BasicAlertExample.tsx
import { useState } from 'react';
import { Host, Alert, Button } from '@expo/ui/swift-ui';

export default function BasicAlertExample() {
  const [isPresented, setIsPresented] = useState(false);

  return (
    <Host style={{ flex: 1 }}>
      <Alert
        title="Saved"
        isPresented={isPresented}
        onIsPresentedChange={setIsPresented}>
        <Alert.Trigger>
          <Button
            label="Show alert"
            onPress={() => setIsPresented(true)}
          />
        </Alert.Trigger>
        <Alert.Actions>
          <Button
            label="OK"
            onPress={() => setIsPresented(false)}
          />
        </Alert.Actions>
      </Alert>
    </Host>
  );
}
```

### Cancel and confirm

Combine `role="cancel"` with a confirm button to build a standard yes/no alert.

```tsx CancelConfirmAlertExample.tsx
import { useState } from 'react';
import { Host, Alert, Button, Text } from '@expo/ui/swift-ui';

export default function CancelConfirmAlertExample() {
  const [isPresented, setIsPresented] = useState(false);

  return (
    <Host style={{ flex: 1 }}>
      <Alert
        title="Sign out?"
        isPresented={isPresented}
        onIsPresentedChange={setIsPresented}>
        <Alert.Trigger>
          <Button
            label="Sign out"
            onPress={() => setIsPresented(true)}
          />
        </Alert.Trigger>
        <Alert.Actions>
          <Button
            label="Sign out"
            onPress={() => console.log('Signed out')}
          />
          <Button label="Cancel" role="cancel" />
        </Alert.Actions>
        <Alert.Message>
          <Text>
            You will need to sign in again to access your account.
          </Text>
        </Alert.Message>
      </Alert>
    </Host>
  );
}
```

### Destructive action

Use `role="destructive"` on a `Button` inside `Alert.Actions` to style it as a destructive action.

```tsx DestructiveAlertExample.tsx
import { useState } from 'react';
import { Host, Alert, Button, Text } from '@expo/ui/swift-ui';

export default function DestructiveAlertExample() {
  const [isPresented, setIsPresented] = useState(false);

  return (
    <Host style={{ flex: 1 }}>
      <Alert
        title="Delete account?"
        isPresented={isPresented}
        onIsPresentedChange={setIsPresented}>
        <Alert.Trigger>
          <Button
            label="Delete account"
            role="destructive"
            onPress={() => setIsPresented(true)}
          />
        </Alert.Trigger>
        <Alert.Actions>
          <Button
            label="Delete"
            role="destructive"
            onPress={() => {
              console.log('Deleted');
              setIsPresented(false);
            }}
          />
          <Button label="Cancel" role="cancel" />
        </Alert.Actions>
        <Alert.Message>
          <Text>
            This permanently deletes your account and all data. This
            cannot be undone.
          </Text>
        </Alert.Message>
      </Alert>
    </Host>
  );
}
```

## API

```tsx
import { Alert } from '@expo/ui/swift-ui';
```

## Component

### `Alert`

Supported platforms: iOS, tvOS.

Type: React.[Element](https://www.typescriptlang.org/docs/handbook/jsx.html#function-component)<[AlertProps](https://docs.expo.dev/versions/v57.0.0/sdk/ui/swift-ui/alert.md#alertprops)\>

`Alert` presents a SwiftUI alert with a title, optional message, and action buttons.

> **See:** Official [SwiftUI documentation](https://developer.apple.com/documentation/swiftui/view/alert\(_:ispresented:actions:message:\)).

Props of the `Alert` component.

AlertProps

### `children`

Supported platforms: iOS, tvOS.

Type: `React.ReactNode`

The contents of the alert. Should include `Alert.Trigger`, `Alert.Actions`, and optionally `Alert.Message`.

### `isPresented`

Supported platforms: iOS, tvOS.

Optional • Type: `boolean`

Whether the alert is presented.

### `onIsPresentedChange`

Supported platforms: iOS, tvOS.

Optional • Type: `(isPresented: boolean) => void`

A callback that is called when the `isPresented` state changes.

### `title`

Supported platforms: iOS, tvOS.

Type: `string`

The title of the alert.

#### Inherited props

-   [CommonViewModifierProps](https://docs.expo.dev/versions/v57.0.0/sdk/ui/swift-ui/modifiers.md)
