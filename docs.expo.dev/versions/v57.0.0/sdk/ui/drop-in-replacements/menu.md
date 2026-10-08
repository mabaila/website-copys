---
modificationDate: September 25, 2026
title: Menu
description: A menu compatible with @react-native-menu/menu.
sourceCodeUrl: 'https://github.com/expo/expo/tree/sdk-57/packages/expo-ui'
packageName: '@expo/ui'
platforms: ['android', 'ios', 'expo-go']
---

This documentation is available as Markdown for AI agents and LLMs. See the [full Markdown index](https://docs.expo.dev/llms.txt) or append .md to any documentation URL.

# Menu

A menu compatible with @react-native-menu/menu.

<AgentInstructions>

## Submitting Feedback

If you encounter errors, misleading or outdated information, report it so Expo can be improved:

Preferred command:
npx --yes submit-expo-feedback@latest --category docs --subject "/versions/v57.0.0/sdk/ui/drop-in-replacements/menu/" "<actionable feedback>"

Direct HTTP fallback:
curl -X POST https://api.expo.dev/v2/feedback/docs-send -H 'Content-Type: application/json' -d '{"url":"/versions/v57.0.0/sdk/ui/drop-in-replacements/menu/","feedback":"🤖 Agent feedback for docs: <specific, actionable description> (<model>, <harness>)"}'

Only submit when you have something specific and actionable to report. Try to give the most context.

## Navigation

When answering a related or follow-up question, fetch the relevant page below as Markdown (.md) instead of guessing; use llms.txt for the full map.

You are here: Reference (v57.0.0) > Expo UI > Drop-in replacements
Pages in this section:
- [Overview](https://docs.expo.dev/versions/v57.0.0/sdk/ui/drop-in-replacements.md)
- [BottomSheet](https://docs.expo.dev/versions/v57.0.0/sdk/ui/drop-in-replacements/bottomsheet.md)
- [DateTimePicker](https://docs.expo.dev/versions/v57.0.0/sdk/ui/drop-in-replacements/datetimepicker.md)
- [MaskedView](https://docs.expo.dev/versions/v57.0.0/sdk/ui/drop-in-replacements/maskedview.md)
- [Menu](https://docs.expo.dev/versions/v57.0.0/sdk/ui/drop-in-replacements/menu.md) (this page)
- [PagerView](https://docs.expo.dev/versions/v57.0.0/sdk/ui/drop-in-replacements/pagerview.md)
- [Picker](https://docs.expo.dev/versions/v57.0.0/sdk/ui/drop-in-replacements/picker.md)
- [SegmentedControl](https://docs.expo.dev/versions/v57.0.0/sdk/ui/drop-in-replacements/segmentedcontrol.md)
- [Slider](https://docs.expo.dev/versions/v57.0.0/sdk/ui/drop-in-replacements/slider.md)
Full documentation tree: [llms.txt](https://docs.expo.dev/llms.txt)

</AgentInstructions>
Android, iOS, Included in Expo Go

A `MenuView` component with an API compatible with [`@react-native-menu/menu`](https://www.npmjs.com/package/@react-native-menu/menu). Supports both single-tap (default) and long-press (`shouldOpenOnLongPress`) triggers.

Under the hood this component wraps the platform-specific `@expo/ui` primitives:

-   **Android**: [Jetpack Compose DropdownMenu](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/dropdownmenu.md) anchored to an internal `Pressable` trigger.
-   **iOS**: [SwiftUI Menu](https://docs.expo.dev/versions/v57.0.0/sdk/ui/swift-ui/menu.md) for tap triggers and [SwiftUI ContextMenu](https://docs.expo.dev/versions/v57.0.0/sdk/ui/swift-ui/contextmenu.md) for long-press triggers.

If you need lower-level control, use those primitives directly.

Image: An open menu with an Edit row and a Delete row

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

## Migrating from `@react-native-menu/menu`

-   Update the import from `import { MenuView } from '@react-native-menu/menu'` to `import { MenuView } from '@expo/ui/community/menu'`.
-   `action.image` on Android differs from upstream. `@react-native-menu/menu` expects a **drawable resource name** string (for example, `'ic_menu_add'`) that it resolves against `android/app/src/main/res/drawable/`. This drop-in does **not** resolve drawable resource names — pass an `ImageSourcePropType` instead (for example, `require('@expo/material-symbols/edit.xml')`). String values are accepted on iOS as SF Symbol names. Use [`Icon.select`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/universal/icon.md) to define both per call site so the unused side tree-shakes out per platform.
-   `title` is rendered as a section header on iOS only; Android's Material `DropdownMenu` has no title slot.
-   On Android, `MenuView` wraps the trigger in its own `Pressable` to open the menu, so an `onPress`/`onLongPress` handler attached to a `Pressable` you pass as `children` won't fire — the outer wrapper claims the gesture. Move that handler into your `onPressAction` switch instead, or use the lower-level [`DropdownMenu`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/dropdownmenu.md) primitive if you need to keep separate tap and long-press actions on the trigger.
-   The imperative `ref.show()` API is **Android-only**. SwiftUI `Menu`/`ContextMenu` have no programmatic open API, so on iOS the call is a no-op (with a one-time dev warning).
-   The following props from `@react-native-menu/menu` are not supported: `themeVariant`, `hitSlop`, `isAnchoredToRight`, `subtitle`, `keepsMenuPresented`, `preferredElementSize`, and `state: 'mixed'`.

## Basic usage

Pass any view as the trigger. `MenuView` attaches its own tap or long-press handling.

```tsx MenuExample.tsx
import { Icon } from '@expo/ui';
import { MenuView } from '@expo/ui/community/menu';
import { Text, useColorScheme, View } from 'react-native';

const editIcon = Icon.select({
  ios: 'pencil',
  android: import('@expo/material-symbols/edit.xml'),
});

const deleteIcon = Icon.select({
  ios: 'trash',
  android: import('@expo/material-symbols/delete.xml'),
});

export default function MenuExample() {
  const colorScheme = useColorScheme();
  return (
    <MenuView
      actions={[
        { id: 'edit', title: 'Edit', image: editIcon },
        { id: 'delete', title: 'Delete', image: deleteIcon, attributes: { destructive: true } },
      ]}
      onPressAction={e => console.log(e.nativeEvent.event)}>
      <View>
        <Text style={{ color: colorScheme === 'dark' ? '#FFFFFF' : '#000000' }}>Open menu</Text>
      </View>
    </MenuView>
  );
}
```

## Long-press (context menu)

Set `shouldOpenOnLongPress` to render as a context menu. On Android, the same controlled `DropdownMenu` opens from a long press on the trigger instead of a tap. On iOS, this uses SwiftUI's `ContextMenu` and shows the trigger as a blurred preview.

```tsx LongPressMenuExample.tsx
import { Icon } from '@expo/ui';
import { MenuView } from '@expo/ui/community/menu';
import { Text, useColorScheme, View } from 'react-native';

const copyIcon = Icon.select({
  ios: 'doc.on.doc',
  android: import('@expo/material-symbols/content_copy.xml'),
});

const shareIcon = Icon.select({
  ios: 'square.and.arrow.up',
  android: import('@expo/material-symbols/share.xml'),
});

export default function LongPressMenuExample() {
  const colorScheme = useColorScheme();
  return (
    <MenuView
      shouldOpenOnLongPress
      actions={[
        { id: 'copy', title: 'Copy', image: copyIcon },
        { id: 'share', title: 'Share', image: shareIcon },
      ]}
      onPressAction={e => console.log(e.nativeEvent.event)}>
      <View style={{ padding: 8 }}>
        <Text style={{ color: colorScheme === 'dark' ? '#FFFFFF' : '#000000' }}>Long-press me</Text>
      </View>
    </MenuView>
  );
}
```

## Submenus and inline sections

`subactions` renders nested actions as a submenu by default. Set `displayInline: true` on the parent to render the children as an inline section instead, which is useful for grouping. On Android, only the divider appears (Material's `DropdownMenu` has no section primitive). On iOS, the parent's `title` becomes the section header.

```tsx SubmenuExample.tsx
import { MenuView } from '@expo/ui/community/menu';
import { Text, useColorScheme, View } from 'react-native';

export default function SubmenuExample() {
  const colorScheme = useColorScheme();
  return (
    <MenuView
      actions={[
        { id: 'rename', title: 'Rename' },
        {
          id: 'sort',
          title: 'Sort by',
          subactions: [
            { id: 'sort-name', title: 'Name' },
            { id: 'sort-date', title: 'Date' },
            { id: 'sort-size', title: 'Size' },
          ],
        },
        {
          id: 'share-section',
          title: 'Share',
          displayInline: true,
          subactions: [
            { id: 'share-airdrop', title: 'AirDrop' },
            { id: 'share-message', title: 'Message' },
          ],
        },
      ]}
      onPressAction={e => console.log(e.nativeEvent.event)}>
      <View>
        <Text style={{ color: colorScheme === 'dark' ? '#FFFFFF' : '#000000' }}>Open menu</Text>
      </View>
    </MenuView>
  );
}
```

## Toggle items with checkmarks

Set `state` to `'on'` or `'off'` to render an action as a toggleable item with a leading checkmark when on. Selecting the action fires `onPressAction` and the caller is responsible for updating the state.

```tsx ToggleMenuExample.tsx
import { MenuView } from '@expo/ui/community/menu';
import { useState } from 'react';
import { Text, useColorScheme, View } from 'react-native';

export default function ToggleMenuExample() {
  const colorScheme = useColorScheme();
  const [pinned, setPinned] = useState(false);
  return (
    <MenuView
      actions={[{ id: 'pin', title: 'Pin to top', state: pinned ? 'on' : 'off' }]}
      onPressAction={e => {
        if (e.nativeEvent.event === 'pin') setPinned(p => !p);
      }}>
      <View>
        <Text style={{ color: colorScheme === 'dark' ? '#FFFFFF' : '#000000' }}>
          {pinned ? 'Pinned' : 'Not pinned'}
        </Text>
      </View>
    </MenuView>
  );
}
```

## API

```tsx
import { MenuView } from '@expo/ui/community/menu';
```

## Component

### `MenuView`

Supported platforms: Android, iOS.

Type: React.[Element](https://www.typescriptlang.org/docs/handbook/jsx.html#function-component)<MenuComponentProps & { ref: Ref<[MenuComponentRef](https://docs.expo.dev/versions/v57.0.0/sdk/ui/drop-in-replacements/menu.md#menucomponentref)\> }\>

A drop-in replacement for `@react-native-menu/menu`'s `MenuView`. Wrap any trigger view; long-pressing or tapping (per `shouldOpenOnLongPress`) shows a popup menu built from the `actions` tree.

-   On Android, renders via Compose's `DropdownMenu` anchored to a `Pressable`.
-   On iOS, renders via SwiftUI's `Menu` (tap) or `ContextMenu` (long-press).
-   On web, the trigger renders the trigger but actions do not fire; a one-time `console.warn` is emitted.

## Props

### `actions`

Supported platforms: Android, iOS.

Type: [MenuAction[]](https://docs.expo.dev/versions/v57.0.0/sdk/ui/drop-in-replacements/menu.md#menuaction)

The actions to display in the menu.

### `children`

Supported platforms: Android, iOS.

Optional • Type: [ReactNode](https://reactnative.dev/docs/react-node)

Trigger view. Long-pressing or tapping (per `shouldOpenOnLongPress`) opens the menu.

### `onCloseMenu`

Supported platforms: Android.

Optional • Type: `() => void`

Callback invoked when the menu closes (either via dismissal or after an action fires).

On Android, fires from the controlled `DropdownMenu`'s dismiss path. On iOS, SwiftUI `Menu`/`ContextMenu` do not expose a close hook in a way we can forward, so this is not fired there.

### `onOpenMenu`

Supported platforms: Android.

Optional • Type: `() => void`

Callback invoked when the menu opens.

On Android, fires when the trigger's tap/long-press flips `expanded` to `true`. On iOS, SwiftUI `Menu`/`ContextMenu` do not expose an open hook, so this is not fired there.

### `onPressAction`

Supported platforms: Android, iOS.

Optional • Type: (event: [NativeActionEvent](https://docs.expo.dev/versions/v57.0.0/sdk/ui/drop-in-replacements/menu.md#nativeactionevent)) => void

Callback invoked when a menu action is selected.

### `shouldOpenOnLongPress`

Supported platforms: Android, iOS.

Optional • Type: `boolean` • Default: `false`

When `true`, the menu opens on long-press of the trigger instead of a single tap.

### `style`

Supported platforms: Android, iOS.

Optional • Type: StyleProp<[ViewStyle](https://reactnative.dev/docs/view-style-props)\>

Style applied to the trigger wrapper.

### `testID`

Supported platforms: Android, iOS.

Optional • Type: `string`

Test identifier passed through to the trigger view.

### `title`

Supported platforms: iOS.

Optional • Type: `string`

Menu title shown at the top of the menu.

## Types

### `MenuAction`

Supported platforms: Android, iOS.

A single action inside a `MenuView`. Compatible with `@react-native-menu/menu`.

| Property | Type | Description |
| --- | --- | --- |
| attributes(optional) | [MenuAttributes](https://docs.expo.dev/versions/v57.0.0/sdk/ui/drop-in-replacements/menu.md#menuattributes) | Visual/behavioral flags. |
| displayInline(optional) | `boolean` | When `true` and `subactions` is present, renders the children as an inline section inside the parent menu (with this action's `title` as the section header on iOS). |
| id(optional) | `string` | Identifier passed back via `onPressAction.nativeEvent.event` when this action is selected. Defaults to `title` if omitted. |
| image(optional) | [SFSymbol](https://github.com/nandorojo/sf-symbols-typescript) | [ImageSourcePropType](https://reactnative.dev/docs/image#imagesource) | Icon to render beside the action label.
-   When an `SFSymbol` name (e.g. `'trash'`), rendered on iOS only. Not rendered on Android — pass an `ImageSourcePropType` instead to show an icon there.
-   When an `ImageSourcePropType` (e.g. `require('./trash.xml')` or `{ uri: '...' }`), rendered on Android via Compose `Icon`. Ignored on iOS; SwiftUI menus only accept SF Symbol names for built-in `Menu`/`Button` labels.

 |
| imageColor(optional) | [ColorValue](https://reactnative.dev/docs/colors) | Tint color applied to the action's icon. Visually applied on Android via the leading `Icon`'s tint. On iOS, the value is accepted but **may not render**: SwiftUI's `Menu`/`ContextMenu` draw their items via the system menu UI, which ignores per-item color modifiers. |
| state(optional) | [MenuState](https://docs.expo.dev/versions/v57.0.0/sdk/ui/drop-in-replacements/menu.md#menustate) | Selection state. When `'on'`, the action renders a checkmark. |
| subactions(optional) | [MenuAction[]](https://docs.expo.dev/versions/v57.0.0/sdk/ui/drop-in-replacements/menu.md#menuaction) | Nested actions. Without `displayInline`, renders as a submenu; with `displayInline: true`, renders as an inline section. |
| title | `string` | Action label shown in the menu. |
| titleColor(optional) | [ColorValue](https://reactnative.dev/docs/colors) | Supported platforms: Android. Text color of the action label. |

### `MenuAttributes`

Supported platforms: Android, iOS.

Visual and behavioral attributes of a menu action. Compatible with `@react-native-menu/menu`.

| Property | Type | Description |
| --- | --- | --- |
| destructive(optional) | `boolean` | Renders the action with a destructive style (red text/icon). |
| disabled(optional) | `boolean` | Disables the action so it can't be activated. |
| hidden(optional) | `boolean` | Hides the action from the menu. |

### `MenuComponentRef`

Supported platforms: Android, iOS.

Imperative handle exposed by `MenuView` via `ref`. Compatible with `@react-native-menu/menu`'s `ref.show()` API.

| Property | Type | Description |
| --- | --- | --- |
| show | `() => void` | Supported platforms: Android. Programmatically open the menu. On Android, opens the anchored `DropdownMenu` (equivalent to the user tapping the trigger). On iOS this is a no-op — SwiftUI `Menu`/`ContextMenu` have no programmatic open API; a one-time `console.warn` is emitted in development. |

### `MenuState`

Supported platforms: Android, iOS.

Literal type: `string`

Selection state for a menu action. `'on'` renders a checkmark; `'off'` doesn't.

Acceptable values are: `'on'` | `'off'`

### `NativeActionEvent`

Supported platforms: Android, iOS.

Event payload delivered to `onPressAction` when an action is selected. Compatible with `@react-native-menu/menu`.

| Property | Type | Description |
| --- | --- | --- |
| nativeEvent | `{ event: string }` | - |
