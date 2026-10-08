---
modificationDate: August 21, 2026
title: Collapsible
description: A labelled tappable header that toggles visibility of its content.
sourceCodeUrl: 'https://github.com/expo/expo/tree/sdk-57/packages/expo-ui'
packageName: '@expo/ui'
platforms: ['android', 'ios', 'web', 'expo-go']
---

This documentation is available as Markdown for AI agents and LLMs. See the [full Markdown index](https://docs.expo.dev/llms.txt) or append .md to any documentation URL.

# Collapsible

A labelled tappable header that toggles visibility of its content.

<AgentInstructions>

## Submitting Feedback

If you encounter errors, misleading or outdated information, report it so Expo can be improved:

Preferred command:
npx --yes submit-expo-feedback@latest --category docs --subject "/versions/v57.0.0/sdk/ui/universal/collapsible/" "<actionable feedback>"

Direct HTTP fallback:
curl -X POST https://api.expo.dev/v2/feedback/docs-send -H 'Content-Type: application/json' -d '{"url":"/versions/v57.0.0/sdk/ui/universal/collapsible/","feedback":"🤖 Agent feedback for docs: <specific, actionable description> (<model>, <harness>)"}'

Only submit when you have something specific and actionable to report. Try to give the most context.

## Navigation

When answering a related or follow-up question, fetch the relevant page below as Markdown (.md) instead of guessing; use llms.txt for the full map.

You are here: Reference (v57.0.0) > Expo UI > Universal
Pages in this section:
- [Overview](https://docs.expo.dev/versions/v57.0.0/sdk/ui/universal.md)
- [BottomSheet](https://docs.expo.dev/versions/v57.0.0/sdk/ui/universal/bottomsheet.md)
- [Button](https://docs.expo.dev/versions/v57.0.0/sdk/ui/universal/button.md)
- [Checkbox](https://docs.expo.dev/versions/v57.0.0/sdk/ui/universal/checkbox.md)
- [Collapsible](https://docs.expo.dev/versions/v57.0.0/sdk/ui/universal/collapsible.md) (this page)
- [Column](https://docs.expo.dev/versions/v57.0.0/sdk/ui/universal/column.md)
- [FieldGroup](https://docs.expo.dev/versions/v57.0.0/sdk/ui/universal/fieldgroup.md)
- [Host](https://docs.expo.dev/versions/v57.0.0/sdk/ui/universal/host.md)
- [Icon](https://docs.expo.dev/versions/v57.0.0/sdk/ui/universal/icon.md)
- [List](https://docs.expo.dev/versions/v57.0.0/sdk/ui/universal/list.md)
- [Picker](https://docs.expo.dev/versions/v57.0.0/sdk/ui/universal/picker.md)
- [RNHostView](https://docs.expo.dev/versions/v57.0.0/sdk/ui/universal/rnhostview.md)
- [Row](https://docs.expo.dev/versions/v57.0.0/sdk/ui/universal/row.md)
- [ScrollView](https://docs.expo.dev/versions/v57.0.0/sdk/ui/universal/scrollview.md)
- [Slider](https://docs.expo.dev/versions/v57.0.0/sdk/ui/universal/slider.md)
- [Spacer](https://docs.expo.dev/versions/v57.0.0/sdk/ui/universal/spacer.md)
- [Switch](https://docs.expo.dev/versions/v57.0.0/sdk/ui/universal/switch.md)
- [Text](https://docs.expo.dev/versions/v57.0.0/sdk/ui/universal/text.md)
- [TextInput](https://docs.expo.dev/versions/v57.0.0/sdk/ui/universal/textinput.md)
Full documentation tree: [llms.txt](https://docs.expo.dev/llms.txt)

</AgentInstructions>
Android, iOS, Web, Included in Expo Go

`Collapsible` is a primitive that shows or hides its content with a tap on a labelled header. Controlled via [`isOpen`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/universal/collapsible.md#isopen) and [`onOpenChange`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/universal/collapsible.md#onopenchange) — each `Collapsible` manages independent state.

Image: An expanded About section with a chevron and description text

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

### Basic collapsible

```tsx CollapsibleExample.tsx
import { useState } from 'react';
import { useColorScheme } from 'react-native';
import { Host, Column, Collapsible, Text } from '@expo/ui';

export default function CollapsibleExample() {
  const [open, setOpen] = useState(false);
  const colorScheme = useColorScheme();
  const ink = { color: colorScheme === 'dark' ? '#FFFFFF' : '#000000' };

  return (
    <Host matchContents={{ vertical: true }} style={{ width: '100%' }}>
      <Column spacing={8} style={{ padding: 16 }}>
        <Collapsible isOpen={open} onOpenChange={setOpen} label="About">
          <Text textStyle={ink}>
            A primitive that toggles visibility of its content via a labelled tappable header.
          </Text>
        </Collapsible>
      </Column>
    </Host>
  );
}
```

### Accordion (one section open at a time)

Wire each `Collapsible`'s `isOpen` to a shared parent value. The component doesn't enforce exclusivity — composition is up to the consumer.

```tsx CollapsibleAccordionExample.tsx
import { useState } from 'react';
import { useColorScheme } from 'react-native';
import { Host, Column, Collapsible, Text } from '@expo/ui';

type Section = 'a' | 'b' | 'c' | null;

export default function CollapsibleAccordionExample() {
  const [openSection, setOpenSection] = useState<Section>('a');
  const colorScheme = useColorScheme();
  const ink = { color: colorScheme === 'dark' ? '#FFFFFF' : '#000000' };

  return (
    <Host matchContents={{ vertical: true }} style={{ width: '100%' }}>
      <Column spacing={8} style={{ padding: 16 }}>
        <Collapsible
          isOpen={openSection === 'a'}
          onOpenChange={open => setOpenSection(open ? 'a' : null)}
          label="Section A">
          <Text textStyle={ink}>Opening B or C closes this one.</Text>
        </Collapsible>
        <Collapsible
          isOpen={openSection === 'b'}
          onOpenChange={open => setOpenSection(open ? 'b' : null)}
          label="Section B">
          <Text textStyle={ink}>Opening A or C closes this one.</Text>
        </Collapsible>
        <Collapsible
          isOpen={openSection === 'c'}
          onOpenChange={open => setOpenSection(open ? 'c' : null)}
          label="Section C">
          <Text textStyle={ink}>Opening A or B closes this one.</Text>
        </Collapsible>
      </Column>
    </Host>
  );
}
```

## API

```tsx
import { Collapsible } from '@expo/ui';
```

## Component

### `Collapsible`

Supported platforms: Android, iOS, Web.

Type: React.[Element](https://www.typescriptlang.org/docs/handbook/jsx.html#function-component)<[CollapsibleProps](https://docs.expo.dev/versions/v57.0.0/sdk/ui/universal/collapsible.md#collapsibleprops)\>

A primitive that toggles visibility of its content via a labelled tappable header. Controlled via `isOpen` + `onOpenChange`.

Props for the [`Collapsible`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/universal/collapsible.md#collapsible) component, a primitive that shows or hides its content with a tap on a labelled header.

CollapsibleProps

### `children`

Supported platforms: Android, iOS, Web.

Optional • Type: [ReactNode](https://reactnative.dev/docs/react-node)

Content rendered when `isOpen` is `true`.

### `isOpen`

Supported platforms: Android, iOS, Web.

Type: `boolean`

Whether the content is currently expanded.

### `label`

Supported platforms: Android, iOS, Web.

Optional • Type: `string`

Text rendered in the tappable header.

### `labelStyle`

Supported platforms: Android, iOS, Web.

Optional • Type: `{ color: string, fontFamily: string, fontSize: number, fontWeight: 'normal' | 'bold' | '100' | '200' | '300' | '400' | '500' | '600' | '700' | '800' | '900', letterSpacing: number, lineHeight: number, textAlign: 'center' | 'left' | 'right' }`

Text-specific styling for the tappable header label.

### `onOpenChange`

Supported platforms: Android, iOS, Web.

Type: `(isOpen: boolean) => void`

Called when the user taps the header to toggle the open state.
