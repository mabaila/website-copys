---
modificationDate: September 18, 2026
title: List
description: A SwiftUI List component for displaying scrollable lists of items.
sourceCodeUrl: 'https://github.com/expo/expo/tree/sdk-57/packages/expo-ui'
packageName: '@expo/ui'
platforms: ['ios', 'tvos', 'expo-go']
---

This documentation is available as Markdown for AI agents and LLMs. See the [full Markdown index](https://docs.expo.dev/llms.txt) or append .md to any documentation URL.

# List

A SwiftUI List component for displaying scrollable lists of items.

<AgentInstructions>

## Submitting Feedback

If you encounter errors, misleading or outdated information, report it so Expo can be improved:

Preferred command:
npx --yes submit-expo-feedback@latest --category docs --subject "/versions/v57.0.0/sdk/ui/swift-ui/list/" "<actionable feedback>"

Direct HTTP fallback:
curl -X POST https://api.expo.dev/v2/feedback/docs-send -H 'Content-Type: application/json' -d '{"url":"/versions/v57.0.0/sdk/ui/swift-ui/list/","feedback":"🤖 Agent feedback for docs: <specific, actionable description> (<model>, <harness>)"}'

Only submit when you have something specific and actionable to report. Try to give the most context.

## Navigation

When answering a related or follow-up question, use llms.txt to find the relevant page as Markdown (.md) instead of guessing.

You are here: Reference (v57.0.0) > Expo UI > SwiftUI (45 pages in this section)
Full documentation tree: [llms.txt](https://docs.expo.dev/llms.txt)

</AgentInstructions>
iOS, tvOS, Included in Expo Go

> For cross-platform usage, see the universal [`List`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/universal/list.md) — it renders the appropriate native component per platform.

Expo UI List matches the official SwiftUI [List API](https://developer.apple.com/documentation/swiftui/list) and supports styling via the [`listStyle`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/swift-ui/modifiers.md#liststylestyle) modifier, various row/section modifiers, as well as selection, reordering, and editing capabilities.

> `List` does not lazily render rows yet: React creates every row up front, so large lists can be slow to mount. We are working on improving this. For large lists, we recommend [FlashList](https://shopify.github.io/flash-list/) or [Legend List](https://github.com/LegendApp/legend-list).

Image: A List with Favorites and Recents sections, each row showing a colored SF Symbol icon and a label

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

### Basic list

```tsx BasicListExample.tsx
import { Host, List, Text, Section } from '@expo/ui/swift-ui';

export default function BasicListExample() {
  return (
    <Host style={{ flex: 1 }}>
      <List>
        <Section title="Fruits">
          <Text>Apple</Text>
          <Text>Banana</Text>
          <Text>Orange</Text>
        </Section>
        <Section title="Vegetables">
          <Text>Carrot</Text>
          <Text>Broccoli</Text>
          <Text>Spinach</Text>
        </Section>
      </List>
    </Host>
  );
}
```

### List with labels and icons

```tsx ListWithLabelsExample.tsx
import { Host, List, Label, Section } from '@expo/ui/swift-ui';

export default function ListWithLabelsExample() {
  return (
    <Host style={{ flex: 1 }}>
      <List>
        <Section title="Settings">
          <Label title="Wi-Fi" systemImage="wifi" />
          <Label
            title="Bluetooth"
            systemImage="antenna.radiowaves.left.and.right"
          />
          <Label
            title="Cellular"
            systemImage="antenna.radiowaves.left.and.right.circle"
          />
        </Section>
      </List>
    </Host>
  );
}
```

### List styles

Use the [`listStyle`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/swift-ui/modifiers.md#liststylestyle) modifier to change the list's appearance.

> **Note:** The `inset`, `insetGrouped`, and `sidebar` styles are not available on tvOS.

```tsx ListStylesExample.tsx
import { useState } from 'react';
import {
  Host,
  List,
  Text,
  Section,
  Picker,
} from '@expo/ui/swift-ui';
import {
  listStyle,
  pickerStyle,
  tag,
} from '@expo/ui/swift-ui/modifiers';

const styles = [
  'automatic',
  'plain',
  'inset',
  'insetGrouped',
  'grouped',
  'sidebar',
] as const;

export default function ListStylesExample() {
  const [styleIndex, setStyleIndex] = useState(0);

  return (
    <Host style={{ flex: 1 }}>
      <List modifiers={[listStyle(styles[styleIndex])]}>
        <Section title="Style Picker">
          <Picker
            label="List Style"
            selection={styleIndex}
            onSelectionChange={setStyleIndex}
            modifiers={[pickerStyle('menu')]}>
            {styles.map((style, index) => (
              <Text key={style} modifiers={[tag(index)]}>
                {style}
              </Text>
            ))}
          </Picker>
        </Section>
        <Section title="Sample Items">
          <Text>Item 1</Text>
          <Text>Item 2</Text>
          <Text>Item 3</Text>
        </Section>
      </List>
    </Host>
  );
}
```

### Selection and edit mode

Enable selection, deletion, and reordering of list items using the [`List.ForEach`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/swift-ui/list.md#listforeach) compound component with `onDelete` and `onMove` props.

-   Use the [`environment`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/swift-ui/modifiers.md#environmentkey-value) modifier to enable edit mode
-   Use the [`tag`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/swift-ui/modifiers.md#tagtag) modifier to identify items
-   Use the [`selection`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/swift-ui/list.md#selection) prop to control selected items
-   Use [`moveDisabled`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/swift-ui/modifiers.md#movedisableddisabled) and [`deleteDisabled`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/swift-ui/modifiers.md#deletedisableddisabled) modifiers to disable these actions on individual items

```tsx EditableListExample.tsx
import { useState } from 'react';
import {
  Host,
  List,
  Label,
  Section,
  Button,
  Toggle,
} from '@expo/ui/swift-ui';
import { environment, tag } from '@expo/ui/swift-ui/modifiers';

type Task = { id: string; title: string };

const INITIAL_TASKS: Task[] = [
  { id: '1', title: 'Task 1' },
  { id: '2', title: 'Task 2' },
  { id: '3', title: 'Task 3' },
  { id: '4', title: 'Task 4' },
];

export default function EditableListExample() {
  const [tasks, setTasks] = useState<Task[]>(INITIAL_TASKS);
  const [selectedIds, setSelectedIds] = useState<string[]>([]);
  const [editMode, setEditMode] = useState(false);

  const handleDelete = (indices: number[]) => {
    setTasks(prev => prev.filter((_, i) => !indices.includes(i)));
  };

  const handleMove = (
    sourceIndices: number[],
    destination: number
  ) => {
    setTasks(prev => {
      const newTasks = [...prev];
      const [removed] = newTasks.splice(sourceIndices[0], 1);
      const adjustedDest =
        sourceIndices[0] < destination
          ? destination - 1
          : destination;
      newTasks.splice(adjustedDest, 0, removed);
      return newTasks;
    });
  };

  return (
    <Host style={{ flex: 1 }}>
      <List
        selection={selectedIds}
        onSelectionChange={ids => setSelectedIds(ids.map(String))}
        modifiers={[
          environment('editMode', editMode ? 'active' : 'inactive'),
        ]}>
        <Section title="Settings">
          <Toggle
            label="Edit mode"
            isOn={editMode}
            onIsOnChange={setEditMode}
          />
        </Section>
        <Section title="Tasks">
          <List.ForEach onDelete={handleDelete} onMove={handleMove}>
            {tasks.map(task => (
              <Label
                key={task.id}
                title={task.title}
                modifiers={[tag(task.id)]}
              />
            ))}
          </List.ForEach>
        </Section>
      </List>
    </Host>
  );
}
```

### Pull to refresh

Use the [`refreshable`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/swift-ui/modifiers.md#refreshablehandler) modifier to enable pull-to-refresh functionality.

```tsx RefreshableListExample.tsx
import { useState } from 'react';
import { Host, List, Text, Section } from '@expo/ui/swift-ui';
import { refreshable } from '@expo/ui/swift-ui/modifiers';

export default function RefreshableListExample() {
  const [lastRefresh, setLastRefresh] = useState<Date | null>(null);

  const handleRefresh = async () => {
    // Simulate async data fetching
    await new Promise(resolve => setTimeout(resolve, 1500));
    setLastRefresh(new Date());
  };

  return (
    <Host style={{ flex: 1 }}>
      <List modifiers={[refreshable(handleRefresh)]}>
        <Section title="Data">
          <Text>Pull down to refresh</Text>
          {lastRefresh && (
            <Text>
              Last refresh: {lastRefresh.toLocaleTimeString()}
            </Text>
          )}
        </Section>
      </List>
    </Host>
  );
}
```

### Row styling

Use [`listRowBackground`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/swift-ui/modifiers.md#listrowbackgroundcolor), [`listRowSeparator`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/swift-ui/modifiers.md#listrowseparatorvisibility-edges), [`listRowSeparatorTint`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/swift-ui/modifiers.md#listrowseparatortintcolor-edges), and [`listRowInsets`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/swift-ui/modifiers.md#listrowinsetsparams) modifiers to customize individual rows. Use [`alignmentGuide`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/swift-ui/modifiers.md#alignmentguideguide-value) with the `listRowSeparatorLeading` guide to set where a row separator starts.

```tsx RowStylingExample.tsx
import { Host, List, Text, Section } from '@expo/ui/swift-ui';
import {
  alignmentGuide,
  listRowBackground,
  listRowSeparator,
  listRowSeparatorTint,
  listRowInsets,
} from '@expo/ui/swift-ui/modifiers';

export default function RowStylingExample() {
  return (
    <Host style={{ flex: 1 }}>
      <List>
        <Section title="Styled Rows">
          <Text modifiers={[listRowBackground('blue')]}>
            Blue background
          </Text>
          <Text modifiers={[listRowSeparator('hidden')]}>
            Hidden separator
          </Text>
          <Text modifiers={[listRowSeparatorTint('red')]}>
            Red separator
          </Text>
          <Text modifiers={[listRowInsets({ leading: 40 })]}>
            Extra leading inset
          </Text>
          <Text
            modifiers={[
              listRowInsets({ leading: 0, trailing: 0 }),
            ]}>
            No horizontal insets
          </Text>
          <Text
            modifiers={[
              alignmentGuide('listRowSeparatorLeading', 32),
            ]}>
            Separator starts 32 points in
          </Text>
        </Section>
      </List>
    </Host>
  );
}
```

### Keyboard dismiss behavior

Use the [`scrollDismissesKeyboard`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/swift-ui/modifiers.md#scrolldismisseskeyboardmode) modifier to control how the keyboard is dismissed when scrolling.

```tsx KeyboardDismissExample.tsx
import { Host, List, Section, TextField } from '@expo/ui/swift-ui';
import { scrollDismissesKeyboard } from '@expo/ui/swift-ui/modifiers';

export default function KeyboardDismissExample() {
  return (
    <Host style={{ flex: 1 }}>
      <List modifiers={[scrollDismissesKeyboard('interactively')]}>
        <Section title="Form">
          <TextField placeholder="Name" />
          <TextField placeholder="Email" />
          <TextField placeholder="Phone" />
        </Section>
      </List>
    </Host>
  );
}
```

### Header prominence

Use the [`headerProminence`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/swift-ui/modifiers.md#headerprominenceprominence) modifier to adjust the visual prominence of section headers.

```tsx HeaderProminenceExample.tsx
import { Host, List, Text, Section } from '@expo/ui/swift-ui';
import { headerProminence } from '@expo/ui/swift-ui/modifiers';

export default function HeaderProminenceExample() {
  return (
    <Host style={{ flex: 1 }}>
      <List modifiers={[headerProminence('increased')]}>
        <Section title="Important Section">
          <Text>This section has increased header prominence</Text>
        </Section>
        <Section title="Another Section">
          <Text>Headers are more prominent</Text>
        </Section>
      </List>
    </Host>
  );
}
```

## API

```tsx
import { List } from '@expo/ui/swift-ui';
```

## Components

### `List`

Supported platforms: iOS, tvOS.

Type: React.[Element](https://www.typescriptlang.org/docs/handbook/jsx.html#function-component)<[ListProps](https://docs.expo.dev/versions/v57.0.0/sdk/ui/swift-ui/list.md#listprops)\>

A list component that renders its children using a native SwiftUI `List`.

ListProps

### `children`

Supported platforms: iOS, tvOS.

Type: [ReactNode](https://reactnative.dev/docs/react-node)

The children elements to be rendered inside the list.

### `onSelectionChange`

Supported platforms: iOS, tvOS.

Optional • Type: `(selection: (string | number)[]) => void`

Callback triggered when the selection changes in a list. Returns an array of selected item tags.

### `selection`

Supported platforms: iOS, tvOS.

Optional • Type: `(string | number)[]`

The currently selected item tags.

#### Inherited props

-   [CommonViewModifierProps](https://docs.expo.dev/versions/v57.0.0/sdk/ui/swift-ui/modifiers.md)

### `ListForEach`

Supported platforms: iOS, tvOS.

Type: React.[Element](https://www.typescriptlang.org/docs/handbook/jsx.html#function-component)<[ListForEachProps](https://docs.expo.dev/versions/v57.0.0/sdk/ui/swift-ui/list.md#listforeachprops)\>

A compound component of `List` that enables item deletion and reordering. This component must be used as a child of `List` (as `List.ForEach`).

ListForEachProps

### `children`

Supported platforms: iOS, tvOS.

Type: [ReactNode](https://reactnative.dev/docs/react-node)

The children elements to be rendered inside the `List.ForEach`.

### `onDelete`

Supported platforms: iOS, tvOS.

Optional • Type: `(indices: number[]) => void`

Callback triggered when items are deleted. Receives an array of indices that were deleted.

> **See:** Official [SwiftUI documentation](https://developer.apple.com/documentation/swiftui/dynamicviewcontent/ondelete\(perform:\)).

### `onMove`

Supported platforms: iOS, tvOS.

Optional • Type: `(sourceIndices: number[], destination: number) => void`

Callback triggered when items are moved. Receives the source indices and destination index.

> **See:** Official [SwiftUI documentation](https://developer.apple.com/documentation/swiftui/dynamicviewcontent/onmove\(perform:\)).

#### Inherited props

-   [CommonViewModifierProps](https://docs.expo.dev/versions/v57.0.0/sdk/ui/swift-ui/modifiers.md)
