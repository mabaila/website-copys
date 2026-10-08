---
modificationDate: August 18, 2026
title: ConfirmationDialog
description: A SwiftUI ConfirmationDialog component for presenting confirmation prompts.
sourceCodeUrl: 'https://github.com/expo/expo/tree/sdk-57/packages/expo-ui'
packageName: '@expo/ui'
platforms: ['ios', 'tvos', 'expo-go']
---

This documentation is available as Markdown for AI agents and LLMs. See the [full Markdown index](https://docs.expo.dev/llms.txt) or append .md to any documentation URL.

# ConfirmationDialog

A SwiftUI ConfirmationDialog component for presenting confirmation prompts.

<AgentInstructions>

## Submitting Feedback

If you encounter errors, misleading or outdated information, report it so Expo can be improved:

Preferred command:
npx --yes submit-expo-feedback@latest --category docs --subject "/versions/v57.0.0/sdk/ui/swift-ui/confirmationdialog/" "<actionable feedback>"

Direct HTTP fallback:
curl -X POST https://api.expo.dev/v2/feedback/docs-send -H 'Content-Type: application/json' -d '{"url":"/versions/v57.0.0/sdk/ui/swift-ui/confirmationdialog/","feedback":"🤖 Agent feedback for docs: <specific, actionable description> (<model>, <harness>)"}'

Only submit when you have something specific and actionable to report. Try to give the most context.

## Navigation

When answering a related or follow-up question, use llms.txt to find the relevant page as Markdown (.md) instead of guessing.

You are here: Reference (v57.0.0) > Expo UI > SwiftUI (45 pages in this section)
Full documentation tree: [llms.txt](https://docs.expo.dev/llms.txt)

</AgentInstructions>
iOS, tvOS, Included in Expo Go

Expo UI ConfirmationDialog matches the official SwiftUI [confirmationDialog API](https://developer.apple.com/documentation/swiftui/view/confirmationdialog\(_:ispresented:titlevisibility:actions:message:\)) and presents an action sheet-style dialog with a title, actions, and an optional message.

Image: ConfirmationDialog asking the user to confirm a destructive action

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

### Basic confirmation dialog

Use `ConfirmationDialog.Trigger` to define the visible element and `ConfirmationDialog.Actions` to provide the dialog buttons.

```tsx BasicConfirmationDialogExample.tsx
import { useState } from 'react';
import {
  Host,
  ConfirmationDialog,
  Button,
} from '@expo/ui/swift-ui';

export default function BasicConfirmationDialogExample() {
  const [isPresented, setIsPresented] = useState(false);

  return (
    <Host style={{ flex: 1 }}>
      <ConfirmationDialog
        title="Are you sure?"
        isPresented={isPresented}
        onIsPresentedChange={setIsPresented}
        titleVisibility="visible">
        <ConfirmationDialog.Trigger>
          <Button
            label="Show dialog"
            onPress={() => setIsPresented(true)}
          />
        </ConfirmationDialog.Trigger>
        <ConfirmationDialog.Actions>
          <Button
            label="Confirm"
            onPress={() => setIsPresented(false)}
          />
          <Button label="Cancel" role="cancel" />
        </ConfirmationDialog.Actions>
      </ConfirmationDialog>
    </Host>
  );
}
```

### Destructive action confirmation

Use `role="destructive"` on a `Button` inside `ConfirmationDialog.Actions` to style it as a destructive action.

```tsx DestructiveConfirmationDialogExample.tsx
import { useState } from 'react';
import {
  Host,
  ConfirmationDialog,
  Button,
  Text,
} from '@expo/ui/swift-ui';

export default function DestructiveConfirmationDialogExample() {
  const [isPresented, setIsPresented] = useState(false);

  return (
    <Host style={{ flex: 1 }}>
      <ConfirmationDialog
        title="Delete Item?"
        isPresented={isPresented}
        onIsPresentedChange={setIsPresented}
        titleVisibility="visible">
        <ConfirmationDialog.Trigger>
          <Button
            label="Delete"
            role="destructive"
            onPress={() => setIsPresented(true)}
          />
        </ConfirmationDialog.Trigger>
        <ConfirmationDialog.Actions>
          <Button
            label="Delete"
            role="destructive"
            onPress={() => {
              console.log('Deleted');
              setIsPresented(false);
            }}
          />
          <Button label="Cancel" role="cancel" />
        </ConfirmationDialog.Actions>
        <ConfirmationDialog.Message>
          <Text>This action cannot be undone.</Text>
        </ConfirmationDialog.Message>
      </ConfirmationDialog>
    </Host>
  );
}
```

### With message and multiple actions

Use `ConfirmationDialog.Message` to display a descriptive message below the title, and include multiple action buttons for different choices.

```tsx MultiActionConfirmationDialogExample.tsx
import { useState } from 'react';
import {
  Host,
  ConfirmationDialog,
  Button,
  Text,
} from '@expo/ui/swift-ui';

export default function MultiActionConfirmationDialogExample() {
  const [isPresented, setIsPresented] = useState(false);

  return (
    <Host style={{ flex: 1 }}>
      <ConfirmationDialog
        title="Save Changes?"
        isPresented={isPresented}
        onIsPresentedChange={setIsPresented}
        titleVisibility="visible">
        <ConfirmationDialog.Trigger>
          <Button
            label="Close document"
            onPress={() => setIsPresented(true)}
          />
        </ConfirmationDialog.Trigger>
        <ConfirmationDialog.Actions>
          <Button
            label="Save"
            onPress={() => console.log('Saved')}
          />
          <Button
            label="Discard"
            role="destructive"
            onPress={() => console.log('Discarded')}
          />
          <Button label="Cancel" role="cancel" />
        </ConfirmationDialog.Actions>
        <ConfirmationDialog.Message>
          <Text>
            You have unsaved changes. What would you like to do?
          </Text>
        </ConfirmationDialog.Message>
      </ConfirmationDialog>
    </Host>
  );
}
```

### Hidden title

Set `titleVisibility="hidden"` to hide the dialog title while still showing the actions and message. You should still provide a `title` for accessibility.

```tsx HiddenTitleConfirmationDialogExample.tsx
import { useState } from 'react';
import {
  Host,
  ConfirmationDialog,
  Button,
  Text,
} from '@expo/ui/swift-ui';

export default function HiddenTitleConfirmationDialogExample() {
  const [isPresented, setIsPresented] = useState(false);

  return (
    <Host style={{ flex: 1 }}>
      <ConfirmationDialog
        title="Hidden Title"
        isPresented={isPresented}
        onIsPresentedChange={setIsPresented}
        titleVisibility="hidden">
        <ConfirmationDialog.Trigger>
          <Button
            label="Show dialog"
            onPress={() => setIsPresented(true)}
          />
        </ConfirmationDialog.Trigger>
        <ConfirmationDialog.Actions>
          <Button
            label="OK"
            onPress={() => setIsPresented(false)}
          />
          <Button label="Cancel" role="cancel" />
        </ConfirmationDialog.Actions>
        <ConfirmationDialog.Message>
          <Text>Only the message and actions are visible.</Text>
        </ConfirmationDialog.Message>
      </ConfirmationDialog>
    </Host>
  );
}
```

## API

```tsx
import { ConfirmationDialog } from '@expo/ui/swift-ui';
```

## Component

### `ConfirmationDialog`

Supported platforms: iOS, tvOS.

Type: React.[Element](https://www.typescriptlang.org/docs/handbook/jsx.html#function-component)<[ConfirmationDialogProps](https://docs.expo.dev/versions/v57.0.0/sdk/ui/swift-ui/confirmationdialog.md#confirmationdialogprops)\>

`ConfirmationDialog` presents a confirmation dialog with a title, optional message, and action buttons.

> **See:** [https://developer.apple.com/documentation/swiftui/view/confirmationdialog(_:ispresented:titlevisibility:actions:message](https://developer.apple.com/documentation/swiftui/view/confirmationdialog\(_:ispresented:titlevisibility:actions:message):)

Props of the `ConfirmationDialog` component.

ConfirmationDialogProps

### `children`

Supported platforms: iOS, tvOS.

Type: [ReactNode](https://reactnative.dev/docs/react-node)

The contents of the confirmation dialog. Should include `ConfirmationDialog.Trigger`, `ConfirmationDialog.Actions`, and optionally `ConfirmationDialog.Message`.

### `isPresented`

Supported platforms: iOS, tvOS.

Optional • Type: `boolean`

Whether the confirmation dialog is presented.

### `onIsPresentedChange`

Supported platforms: iOS, tvOS.

Optional • Type: `(isPresented: boolean) => void`

A callback that is called when the `isPresented` state changes.

### `title`

Supported platforms: iOS, tvOS.

Type: `string`

The title of the confirmation dialog.

### `titleVisibility`

Supported platforms: iOS, tvOS.

Optional • Literal type: `string` • Default: `'automatic'`

The visibility of the dialog title.

Acceptable values are: `'automatic'` | `'hidden'` | `'visible'`

#### Inherited props

-   [CommonViewModifierProps](https://docs.expo.dev/versions/v57.0.0/sdk/ui/swift-ui/modifiers.md)
