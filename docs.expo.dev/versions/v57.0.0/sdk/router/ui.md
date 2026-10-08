---
modificationDate: September 29, 2026
title: Router UI
description: An Expo Router submodule that provides headless tab components to create custom tab layouts.
sourceCodeUrl: 'https://github.com/expo/expo/tree/sdk-57/packages/expo-router'
packageName: 'expo-router'
platforms: ['android', 'ios', 'tvos', 'web', 'expo-go']
---

This documentation is available as Markdown for AI agents and LLMs. See the [full Markdown index](https://docs.expo.dev/llms.txt) or append .md to any documentation URL.

# Expo Router UI

An Expo Router submodule that provides headless tab components to create custom tab layouts.

<AgentInstructions>

## Submitting Feedback

If you encounter errors, misleading or outdated information, report it so Expo can be improved:

Preferred command:
npx --yes submit-expo-feedback@latest --category docs --subject "/versions/v57.0.0/sdk/router/ui/" "<actionable feedback>"

Direct HTTP fallback:
curl -X POST https://api.expo.dev/v2/feedback/docs-send -H 'Content-Type: application/json' -d '{"url":"/versions/v57.0.0/sdk/router/ui/","feedback":"🤖 Agent feedback for docs: <specific, actionable description> (<model>, <harness>)"}'

Only submit when you have something specific and actionable to report. Try to give the most context.

## Navigation

When answering a related or follow-up question, fetch the relevant page below as Markdown (.md) instead of guessing; use llms.txt for the full map.

You are here: Reference (v57.0.0) > Expo Router
Pages in this section:
- [Overview](https://docs.expo.dev/versions/v57.0.0/sdk/router.md)
- [Color](https://docs.expo.dev/versions/v57.0.0/sdk/router/color.md)
- [Experimental Stack](https://docs.expo.dev/versions/v57.0.0/sdk/router/experimental-stack.md)
- [Link](https://docs.expo.dev/versions/v57.0.0/sdk/router/link.md)
- [Native tabs](https://docs.expo.dev/versions/v57.0.0/sdk/router/native-tabs.md)
- [Split View](https://docs.expo.dev/versions/v57.0.0/sdk/router/split-view.md)
- [Stack](https://docs.expo.dev/versions/v57.0.0/sdk/router/stack.md)
- [UI](https://docs.expo.dev/versions/v57.0.0/sdk/router/ui.md) (this page)
Full documentation tree: [llms.txt](https://docs.expo.dev/llms.txt)

</AgentInstructions>
Android, iOS, tvOS, Web, Included in Expo Go

`expo-router/ui` is a submodule of `expo-router` that exports headless components and hooks to build [custom tab layouts](https://docs.expo.dev/router/advanced/custom-tabs.md). You can use it instead of the built-in navigators bundled with Expo Router, such as [JavaScript tabs](https://docs.expo.dev/router/advanced/tabs.md) and [native tabs](https://docs.expo.dev/router/advanced/native-tabs.md).

> See the [Expo Router](https://docs.expo.dev/versions/v57.0.0/sdk/router.md) reference for more information about the file-based routing library for native and web app.

## Installation

To use `expo-router/ui` in your project, you need to install `expo-router` in your project. Follow the instructions from the Expo Router's installation guide:

[Install Expo Router](https://docs.expo.dev/router/installation.md) — Learn how to install Expo Router in your project.

## Configuration in app config

If you are using the [default](https://docs.expo.dev/more/create-expo.md#--template) template to create a new project, `expo-router`'s [config plugin](https://docs.expo.dev/config-plugins/introduction.md) is already configured in your app config.

### Example app.json with config plugin

```json app.json
{
  "expo": {
    "plugins": ["expo-router"]
  }
}
```

## Usage

For information about using `expo-router/ui` in Custom tab layouts guide:

[Custom tab layouts](https://docs.expo.dev/router/advanced/custom-tabs.md)

## API

```js
import { Tabs, TabList, TabTrigger, TabSlot } from 'expo-router/ui';
```

## Components

### `TabContext`

Supported platforms: Android, iOS, tvOS, Web.

Type: React.[Element](https://www.typescriptlang.org/docs/handbook/jsx.html#function-component)<Context<[ExpoTabsNavigatorScreenOptions](https://docs.expo.dev/versions/v57.0.0/sdk/router/ui.md#expotabsnavigatorscreenoptions)\>\>

### `TabList`

Supported platforms: Android, iOS, tvOS, Web.

Type: React.[Element](https://www.typescriptlang.org/docs/handbook/jsx.html#function-component)<[TabListProps](https://docs.expo.dev/versions/v57.0.0/sdk/router/ui.md#tablistprops)\>

Wrapper component for `TabTriggers`. `TabTriggers` within the `TabList` define the tabs.

Example

```tsx
<Tabs>
 <TabSlot />
 <TabList>
  <TabTrigger name="home" href="/" />
 </TabList>
</Tabs>
```

TabListProps

### `asChild`

Supported platforms: Android, iOS, tvOS, Web.

Optional • Type: `boolean`

Forward props to child component and removes the extra `<View>`. Useful for custom wrappers.

#### Inherited props

-   [ViewProps](https://reactnative.dev/docs/view#props)

### `Tabs`

Supported platforms: Android, iOS, tvOS, Web.

Type: React.[Element](https://www.typescriptlang.org/docs/handbook/jsx.html#function-component)<[TabsProps](https://docs.expo.dev/versions/v57.0.0/sdk/router/ui.md#tabsprops)\>

Root component for the headless tabs.

> **See:** [`useTabsWithChildren`](https://docs.expo.dev/versions/v57.0.0/sdk/router/ui.md#usetabswithchildrenoptions) for a hook version of this component.

Example

```tsx
<Tabs>
 <TabSlot />
 <TabList>
  <TabTrigger name="home" href="/" />
 </TabList>
</Tabs>
```

TabsProps

### `asChild`

Supported platforms: Android, iOS, tvOS, Web.

Optional • Type: `boolean`

Forward props to child component and removes the extra `<View>`. Useful for custom wrappers.

### `options`

Supported platforms: Android, iOS, tvOS, Web.

Optional • Type: [UseTabsOptions](https://docs.expo.dev/versions/v57.0.0/sdk/router/ui.md#usetabsoptions)

#### Inherited props

-   [ViewProps](https://reactnative.dev/docs/view#props)

### `TabSlot`

Supported platforms: Android, iOS, tvOS, Web.

Type: React.[Element](https://www.typescriptlang.org/docs/handbook/jsx.html#function-component)<[TabSlotProps](https://docs.expo.dev/versions/v57.0.0/sdk/router/ui.md#tabslotprops)\>

Renders the current tab.

> **See:** [`useTabSlot`](https://docs.expo.dev/versions/v57.0.0/sdk/router/ui.md#usetabslot) for a hook version of this component.

Example

```tsx
<Tabs>
 <TabSlot />
 <TabList>
  <TabTrigger name="home" href="/" />
 </TabList>
</Tabs>
```

TabSlotProps

### `detachInactiveScreens`

Supported platforms: Android, iOS, tvOS, Web.

Optional • Type: `boolean`

Remove inactive screens.

### `renderFn`

Supported platforms: Android, iOS, tvOS, Web.

Optional • Type: `defaultTabsSlotRender`

Override how the `Screen` component is rendered.

#### Inherited props

-   `ComponentProps<ScreenContainer>`

### `TabTrigger`

Supported platforms: Android, iOS, tvOS, Web.

Type: React.[Element](https://www.typescriptlang.org/docs/handbook/jsx.html#function-component)<[TabTriggerProps](https://docs.expo.dev/versions/v57.0.0/sdk/router/ui.md#tabtriggerprops)\>

Creates a trigger to navigate to a tab. When used as child of `TabList`, its functionality slightly changes since the `href` prop is required, and the trigger also defines what routes are present in the `Tabs`.

When used outside of `TabList`, this component no longer requires an `href`.

Example

```tsx
<Tabs>
 <TabSlot />
 <TabList>
  <TabTrigger name="home" href="/" />
 </TabList>
</Tabs>
```

TabTriggerProps

### `asChild`

Supported platforms: Android, iOS, tvOS, Web.

Optional • Type: `boolean`

Forward props to child component. Useful for custom wrappers.

### `href`

Supported platforms: Android, iOS, tvOS, Web.

Optional • Type: [Href](https://docs.expo.dev/versions/v57.0.0/sdk/router.md#hreft)

Name of tab. Required when used within a `TabList`.

### `name`

Supported platforms: Android, iOS, tvOS, Web.

Type: `string`

Name of tab. When used within a `TabList` this sets the name of the tab. Otherwise, this references the name.

### `resetOnFocus`

Supported platforms: Android, iOS, tvOS, Web.

Optional • Type: `boolean`

Resets the route when switching to a tab.

#### Inherited props

-   `PressablePropsWithoutFunctionChildren`

### `useTabSlot`

Supported platforms: Android, iOS, tvOS, Web.

Type: React.[Element](https://www.typescriptlang.org/docs/handbook/jsx.html#function-component)<[TabSlotProps](https://docs.expo.dev/versions/v57.0.0/sdk/router/ui.md#tabslotprops)\>

Returns a `ReactElement` of the current tab.

Example

```tsx
function MyTabSlot() {
  const slot = useTabSlot();

  return slot;
}
```

## Hooks

### `useTabSlot(namedParameters)`

Supported platforms: Android, iOS, tvOS, Web.

| Parameter | Type |
| --- | --- |
| `namedParameters`(optional) | [TabSlotProps](https://docs.expo.dev/versions/v57.0.0/sdk/router/ui.md#tabslotprops) |

  

Returns a `ReactElement` of the current tab.

Returns: `Element`

Example

```tsx
function MyTabSlot() {
  const slot = useTabSlot();

  return slot;
}
```

### `useTabsWithChildren(options)`

Supported platforms: Android, iOS, tvOS, Web.

| Parameter | Type |
| --- | --- |
| `options` | [UseTabsWithChildrenOptions](https://docs.expo.dev/versions/v57.0.0/sdk/router/ui.md#usetabswithchildrenoptions) |

  

Hook version of `Tabs`. The returned NavigationContent component should be rendered. Using the hook requires using the `<TabList />` and `<TabTrigger />` components exported from Expo Router.

The `useTabsWithTriggers()` hook can be used for custom components.

Returns: `{ describe: (route: RouteProp<ParamListBase>, placeholder: boolean) => Descriptor<ExpoTabsNavigatorScreenOptions, Omit<NavigationHelpersCommon<ParamListBase, TabNavigationState<any>>, 'getParent'> & { } & NavigationHelpersRoute<ParamListBase, string> & EventConsumer<TabNavigationEventMap & EventMapCore<TabNavigationState<any>>> & PrivateValueStore<[ParamListBase, string, TabNavigationEventMap]> & TabActionHelpers<ParamListBase>, RouteProp<ParamListBase>>, descriptors: Record<string, Descriptor<ExpoTabsNavigatorScreenOptions, Omit<NavigationHelpersCommon<ParamListBase, TabNavigationState<any>>, 'getParent'> & { } & NavigationHelpersRoute<ParamListBase, string> & EventConsumer<TabNavigationEventMap & EventMapCore<TabNavigationState<any>>> & PrivateValueStore<[ParamListBase, string, TabNavigationEventMap]> & TabActionHelpers<ParamListBase>, RouteProp<ParamListBase>>>, navigation: { } & PrivateValueStore<[ParamListBase, unknown, unknown]> & EventEmitter<TabNavigationEventMap> & NavigationHelpersRoute<ParamListBase, string> & TabActionHelpers<ParamListBase>, NavigationContent: (__namedParameters: { children: ReactNode }) => Element, state: TabNavigationState<any> }`

> **See:** [`Tabs`](https://docs.expo.dev/versions/v57.0.0/sdk/router/ui.md#tabs) for the component version of this hook.

Example

```tsx
export function MyTabs({ children }) {
 const { NavigationContent } = useTabsWithChildren({ children })

 return <NavigationContent />
}
```

### `useTabsWithTriggers(options)`

Supported platforms: Android, iOS, tvOS, Web.

| Parameter | Type |
| --- | --- |
| `options` | [UseTabsWithTriggersOptions](https://docs.expo.dev/versions/v57.0.0/sdk/router/ui.md#usetabswithtriggersoptions) |

  

Alternative hook version of `Tabs` that uses explicit triggers instead of `children`.

Returns: `{ describe: (route: RouteProp<ParamListBase>, placeholder: boolean) => Descriptor<ExpoTabsNavigatorScreenOptions, Omit<NavigationHelpersCommon<ParamListBase, TabNavigationState<any>>, 'getParent'> & { } & NavigationHelpersRoute<ParamListBase, string> & EventConsumer<TabNavigationEventMap & EventMapCore<TabNavigationState<any>>> & PrivateValueStore<[ParamListBase, string, TabNavigationEventMap]> & TabActionHelpers<ParamListBase>, RouteProp<ParamListBase>>, descriptors: Record<string, Descriptor<ExpoTabsNavigatorScreenOptions, Omit<NavigationHelpersCommon<ParamListBase, TabNavigationState<any>>, 'getParent'> & { } & NavigationHelpersRoute<ParamListBase, string> & EventConsumer<TabNavigationEventMap & EventMapCore<TabNavigationState<any>>> & PrivateValueStore<[ParamListBase, string, TabNavigationEventMap]> & TabActionHelpers<ParamListBase>, RouteProp<ParamListBase>>>, navigation: { } & PrivateValueStore<[ParamListBase, unknown, unknown]> & EventEmitter<TabNavigationEventMap> & NavigationHelpersRoute<ParamListBase, string> & TabActionHelpers<ParamListBase>, NavigationContent: (__namedParameters: { children: ReactNode }) => Element, state: TabNavigationState<any> }`

> **See:** [`Tabs`](https://docs.expo.dev/versions/v57.0.0/sdk/router/ui.md#tabs) for the component version of this hook.

Example

```tsx
export function MyTabs({ children }) {
  const { NavigationContent } = useTabsWithChildren({ triggers: [] })

  return <NavigationContent />
}
```

### `useTabTrigger(options)`

Supported platforms: Android, iOS, tvOS, Web.

| Parameter | Type |
| --- | --- |
| `options` | [TabTriggerProps](https://docs.expo.dev/versions/v57.0.0/sdk/router/ui.md#tabtriggerprops) |

  

Utility hook creating custom `TabTrigger`.

Returns: `UseTabTriggerResult`

## Types

### `ExpoTabsNavigationProp`

Supported platforms: Android, iOS, tvOS, Web.

Type: NavigationProp<ParamList, RouteName, [NavigatorID](https://reactnavigation.org/docs/custom-navigators/#type-checking-navigators), [TabNavigationState](https://reactnavigation.org/docs/custom-navigators/#type-checking-navigators)<ParamListBase\>, [ExpoTabsScreenOptions](https://docs.expo.dev/versions/v57.0.0/sdk/router/ui.md#expotabsscreenoptions), [TabNavigationEventMap](https://docs.expo.dev/versions/v57.0.0/sdk/router/ui.md#tabnavigationeventmap)\>

### `ExpoTabsNavigatorOptions`

Supported platforms: Android, iOS, tvOS, Web.

Literal type: `union`

Acceptable values are: [DefaultNavigatorOptions](https://reactnavigation.org/docs/custom-navigators/#type-checking-navigators)<ParamListBase, string | undefined, [TabNavigationState](https://reactnavigation.org/docs/custom-navigators/#type-checking-navigators)<ParamListBase\>, [ExpoTabsScreenOptions](https://docs.expo.dev/versions/v57.0.0/sdk/router/ui.md#expotabsscreenoptions), [TabNavigationEventMap](https://docs.expo.dev/versions/v57.0.0/sdk/router/ui.md#tabnavigationeventmap), [ExpoTabsNavigationProp](https://docs.expo.dev/versions/v57.0.0/sdk/router/ui.md#expotabsnavigationprop)<ParamListBase\>\> | [Omit](https://www.typescriptlang.org/docs/handbook/utility-types.html#omittype-keys)<[TabRouterOptions](https://reactnavigation.org/docs/custom-navigators/#type-checking-navigators), 'initialRouteName'\> | [ExpoTabsNavigatorScreenOptions](https://docs.expo.dev/versions/v57.0.0/sdk/router/ui.md#expotabsnavigatorscreenoptions)

### `ExpoTabsNavigatorScreenOptions`

Supported platforms: Android, iOS, tvOS, Web.

| Property | Type | Description |
| --- | --- | --- |
| detachInactiveScreens(optional) | `boolean` | - |
| freezeOnBlur(optional) | `boolean` | - |
| lazy(optional) | `boolean` | - |
| unmountOnBlur(optional) | `boolean` | - |

### `ExpoTabsScreenOptions`

Supported platforms: Android, iOS, tvOS, Web.

Type: [Pick](https://www.typescriptlang.org/docs/handbook/utility-types.html#picktype-keys)<BottomTabNavigationOptions, 'title' | 'lazy' | 'freezeOnBlur'\> extended by:

| Property | Type | Description |
| --- | --- | --- |
| action | `NavigationAction` | - |
| params(optional) | `object` | - |
| title | `string` | - |

### `SwitchToOptions`

Supported platforms: Android, iOS, tvOS, Web.

Options for `switchTab` function.

| Property | Type | Description |
| --- | --- | --- |
| resetOnFocus(optional) | `boolean` | Navigate and reset the history on route focus. |

### `TabNavigationEventMap`

Supported platforms: Android, iOS, tvOS, Web.

| Property | Type | Description |
| --- | --- | --- |
| tabLongPress | `{ data: undefined }` | Event which fires on long press on the tab in the tab bar. |
| tabPress | `{ canPreventDefault: true, data: undefined }` | Event which fires on tapping on the tab in the tab bar. |

### `TabsContextValue`

Supported platforms: Android, iOS, tvOS, Web.

Type: `ReturnType<useNavigationBuilder>`

The React Navigation custom navigator.

> **See:** [`useNavigationBuilder`](https://reactnavigation.org/docs/custom-navigators/#usenavigationbuilder) hook from React Navigation for more information.

### `TabsSlotRenderOptions`

Supported platforms: Android, iOS, tvOS, Web.

Options provided to the `UseTabSlotOptions`.

| Property | Type | Description |
| --- | --- | --- |
| detachInactiveScreens | `boolean` | Should the screen be unloaded when inactive. |
| index | `number` | Index of screen. |
| isFocused | `boolean` | Whether the screen is focused. |
| loaded | `boolean` | Whether the screen has been loaded. |

### `TabTriggerOptions`

Supported platforms: Android, iOS, tvOS, Web.

| Property | Type | Description |
| --- | --- | --- |
| href | [Href](https://docs.expo.dev/versions/v57.0.0/sdk/router.md#hreft) | - |
| name | `string` | - |

### `Trigger`

Supported platforms: Android, iOS, tvOS, Web.

Type: extended by:

| Property | Type | Description |
| --- | --- | --- |
| isFocused | `boolean` | - |
| resolvedHref | `string` | - |
| route | `[number]` | - |

### `UseTabsOptions`

Supported platforms: Android, iOS, tvOS, Web.

Options to provide to the Tab Router.

Type: [Omit](https://www.typescriptlang.org/docs/handbook/utility-types.html#omittype-keys)<[DefaultNavigatorOptions](https://reactnavigation.org/docs/custom-navigators/#type-checking-navigators)<ParamListBase, any, [TabNavigationState](https://reactnavigation.org/docs/custom-navigators/#type-checking-navigators)<any\>, [ExpoTabsScreenOptions](https://docs.expo.dev/versions/v57.0.0/sdk/router/ui.md#expotabsscreenoptions), [TabNavigationEventMap](https://docs.expo.dev/versions/v57.0.0/sdk/router/ui.md#tabnavigationeventmap), any\>, 'children'\> extended by:

| Property | Type | Description |
| --- | --- | --- |
| backBehavior(optional) | `TabRouterOptions[backBehavior]` | - |

### `UseTabsWithChildrenOptions`

Supported platforms: Android, iOS, tvOS, Web.

Type: PropsWithChildren<[UseTabsOptions](https://docs.expo.dev/versions/v57.0.0/sdk/router/ui.md#usetabsoptions)\>

### `UseTabsWithTriggersOptions`

Supported platforms: Android, iOS, tvOS, Web.

Type: [UseTabsOptions](https://docs.expo.dev/versions/v57.0.0/sdk/router/ui.md#usetabsoptions) extended by:

| Property | Type | Description |
| --- | --- | --- |
| triggers | `ScreenTrigger[]` | - |

### `UseTabTriggerResult`

Supported platforms: Android, iOS, tvOS, Web.

| Property | Type | Description |
| --- | --- | --- |
| getTrigger | (name: string) => [Trigger](https://docs.expo.dev/versions/v57.0.0/sdk/router/ui.md#trigger) | undefined | - |
| switchTab | (name: string, options: [SwitchToOptions](https://docs.expo.dev/versions/v57.0.0/sdk/router/ui.md#switchtooptions)) => void | - |
| trigger(optional) | [Trigger](https://docs.expo.dev/versions/v57.0.0/sdk/router/ui.md#trigger) | - |
| triggerProps | `TriggerProps` | - |
