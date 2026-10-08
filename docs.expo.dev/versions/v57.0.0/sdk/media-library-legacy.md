---
modificationDate: June 29, 2026
title: MediaLibrary (legacy)
description: A library that provides access to the device's media library.
sourceCodeUrl: 'https://github.com/expo/expo/tree/sdk-57/packages/expo-media-library/src/legacy'
packageName: 'expo-media-library'
iconUrl: '/static/images/packages/expo-media-library.png'
platforms: ['android', 'ios', 'tvos', 'expo-go']
---

This documentation is available as Markdown for AI agents and LLMs. See the [full Markdown index](https://docs.expo.dev/llms.txt) or append .md to any documentation URL.

# Expo MediaLibrary (legacy)

A library that provides access to the device's media library.

<AgentInstructions>

## Submitting Feedback

If you encounter errors, misleading or outdated information, report it so Expo can be improved:

Preferred command:
npx --yes submit-expo-feedback@latest --category docs --subject "/versions/v57.0.0/sdk/media-library-legacy/" "<actionable feedback>"

Direct HTTP fallback:
curl -X POST https://api.expo.dev/v2/feedback/docs-send -H 'Content-Type: application/json' -d '{"url":"/versions/v57.0.0/sdk/media-library-legacy/","feedback":"🤖 Agent feedback for docs: <specific, actionable description> (<model>, <harness>)"}'

Only submit when you have something specific and actionable to report. Try to give the most context.

## Navigation

When answering a related or follow-up question, use llms.txt to find the relevant page as Markdown (.md) instead of guessing.

You are here: Reference (v57.0.0) > Expo SDK (87 pages in this section)
Full documentation tree: [llms.txt](https://docs.expo.dev/llms.txt)

</AgentInstructions>
Android, iOS, tvOS, Included in Expo Go

> The legacy version of the MediaLibrary API is included in the `expo-media-library` library. It can be used alongside the class-based `expo-media-library` API, which is exposed from the root import. To use the legacy API, import it from `expo-media-library/legacy`.

`expo-media-library` provides access to the user's media library, allowing them to access their existing images and videos from your app, as well as save new ones. You can also subscribe to any updates made to the user's media library.

> Android allows full access to the media library (which is the purpose of this package) only for applications needing broad access to photos. See [Details on Google Play's Photo and Video Permissions policy](https://support.google.com/googleplay/android-developer/answer/14115180).

## Installation

```sh
# npm
npx expo install expo-media-library

# yarn
yarn expo install expo-media-library

# pnpm
pnpm expo install expo-media-library

# bun
bun expo install expo-media-library
```

If you are installing this in an [existing React Native app](https://docs.expo.dev/bare/overview.md), make sure to [install `expo`](https://docs.expo.dev/bare/installing-expo-modules.md) in your project.

## Configuration in app config

You can configure `expo-media-library` using its built-in [config plugin](https://docs.expo.dev/config-plugins/introduction.md) if you use config plugins in your project ([Continuous Native Generation (CNG)](https://docs.expo.dev/workflow/continuous-native-generation.md)). The plugin allows you to configure various properties that cannot be set at runtime and require building a new app binary to take effect. If your app does **not** use CNG, then you'll need to manually configure the library.

### Example app.json with config plugin

```json
{
  "expo": {
    "plugins": [
      [
        "expo-media-library",
        {
          "photosPermission": "Allow $(PRODUCT_NAME) to access your photos.",
          "savePhotosPermission": "Allow $(PRODUCT_NAME) to save photos.",
          "isAccessMediaLocationEnabled": true,
          "granularPermissions": ["audio", "photo"]
        }
      ]
    ]
  }
}
```

### Configurable properties

| Name | Default | Description |
| --- | --- | --- |
| `photosPermission` | `"Allow $(PRODUCT_NAME) to access your photos."` | Only for: iOS. Sets the iOS `NSPhotoLibraryUsageDescription` permission message in **Info.plist**. |
| `savePhotosPermission` | `"Allow $(PRODUCT_NAME) to save photos."` | Only for: iOS. Sets the iOS `NSPhotoLibraryAddUsageDescription` permission message in **Info.plist**. |
| `preventAutomaticLimitedAccessAlert` | `false` | Only for: iOS. Prevents the automatic limited access alert from being shown when the user has limited access to the photo library. Useful for apps that want to access only the limited photo library without having iOS forcibly show the alert. |
| `isAccessMediaLocationEnabled` | `false` | Only for: Android. Sets whether or not to request the `ACCESS_MEDIA_LOCATION` permission on Android. |
| `granularPermissions` | `["photo", "video", "audio"]` | Only for: Android. Sets which [`GranularPermission`](https://docs.expo.dev/versions/v57.0.0/sdk/media-library-legacy.md#granularpermission) values to include, determining which media permissions (`READ_MEDIA_IMAGES`, `READ_MEDIA_VIDEO`, `READ_MEDIA_AUDIO`) will be added to the Android manifest. Matches the behavior of the runtime API. |

#### Are you using this library in an existing React Native app?

If you're not using Continuous Native Generation ([CNG](https://docs.expo.dev/workflow/continuous-native-generation.md)) or you're using native **android** and **ios** projects manually, then you need to add following permissions and configuration to your native projects:

**Android**

-   To access asset location (latitude and longitude EXIF tags), add `ACCESS_MEDIA_LOCATION` permission to your project's **android/app/src/main/AndroidManifest.xml**:
    
    ```xml
    <uses-permission android:name="android.permission.ACCESS_MEDIA_LOCATION" />
    ```
    
-   [Scoped storage](https://developer.android.com/training/data-storage#scoped-storage) is available from Android 10. To make `expo-media-library` work with scoped storage, you need to add the following configuration to your **android/app/src/main/AndroidManifest.xml**:
    
    ```xml
    <manifest ... >
      <application android:requestLegacyExternalStorage="true" ...>
    </manifest>
    ```
    

**iOS**

-   Add `NSPhotoLibraryUsageDescription`, and `NSPhotoLibraryAddUsageDescription` keys to your project's **ios/[app]/Info.plist**:
    
    ```xml
    <key>NSPhotoLibraryUsageDescription</key>
    <string>Give $(PRODUCT_NAME) permission to access your photos</string>
    <key>NSPhotoLibraryAddUsageDescription</key>
    <string>Give $(PRODUCT_NAME) permission to save photos</string>
    ```
    

## Usage

```jsx Fetching albums and displaying assets
import { useState, useEffect } from 'react';
import { Button, Text, ScrollView, StyleSheet, Image, View, Platform } from 'react-native';
import * as MediaLibrary from 'expo-media-library/legacy';

export default function App() {
  const [albums, setAlbums] = useState(null);
  const [permissionResponse, requestPermission] = MediaLibrary.usePermissions();

  async function getAlbums() {
    if (permissionResponse.status !== 'granted') {
      await requestPermission();
    }
    const fetchedAlbums = await MediaLibrary.getAlbumsAsync({
      includeSmartAlbums: true,
    });
    setAlbums(fetchedAlbums);
  }

  return (
    <View style={styles.container}>
      <Button onPress={getAlbums} title="Get albums" />
      <ScrollView>
        {albums && albums.map((album) => <AlbumEntry album={album} />)}
      </ScrollView>
    </View>
  );
}

function AlbumEntry({ album }) {
  const [assets, setAssets] = useState([]);

  useEffect(() => {
    async function getAlbumAssets() {
      const albumAssets = await MediaLibrary.getAssetsAsync({ album });
      setAssets(albumAssets.assets);
    }
    getAlbumAssets();
  }, [album]);

  return (
    <View key={album.id} style={styles.albumContainer}>
      <Text>
        {album.title} - {album.assetCount ?? 'no'} assets
      </Text>
      <View style={styles.albumAssetsContainer}>
        {assets && assets.map((asset) => (
          <Image source={{ uri: asset.uri }} width={50} height={50} />
        ))}
      </View>
    </View>
  );
}

const styles = StyleSheet.create({ ... });
```

## Known limitations

### Empty albums

Due to system limitations on Android, it is impossible to create empty albums. It is necessary to either pass an existing asset to add to the album or a URI of a local resource, which will be used to create a new asset inside the album.

### Moving assets between albums

Android 11 introduced permission changes that make the operation of moving assets between albums require confirmation from the user every time. Therefore, when creating a new asset, instead of creating the asset and then moving it to the album, it is recommended to pass the `album` parameter to the [`createAssetAsync`](https://docs.expo.dev/versions/v57.0.0/sdk/media-library-legacy.md#medialibrarycreateassetasynclocaluri-album) method, which will automatically add the asset to the album without the need for user confirmation.

### Wrong orientation of images

On Android, when using `getAssetsAsync` without `resolveWithFullInfo: true`, image orientation may be incorrect because EXIF data (which includes orientation) is only read when that option is enabled.

## API

```js
import * as MediaLibrary from 'expo-media-library/legacy';
```

## Component

### `getAlbumsAsync`

Supported platforms: Android, iOS, tvOS.

Type: React.[Element](https://www.typescriptlang.org/docs/handbook/jsx.html#function-component)<[AlbumsOptions](https://docs.expo.dev/versions/latest/sdk/media-library-legacy.md#albumsoptions)\>

Queries for user-created albums in media gallery.

## Constants

### `MediaLibrary.MediaType`

Supported platforms: Android, iOS, tvOS.

Type: [MediaTypeObject](https://docs.expo.dev/versions/v57.0.0/sdk/media-library-legacy.md#mediatypeobject)

Possible media types.

### `MediaLibrary.SortBy`

Supported platforms: Android, iOS, tvOS.

Type: [SortByObject](https://docs.expo.dev/versions/v57.0.0/sdk/media-library-legacy.md#sortbyobject)

Supported keys that can be used to sort `getAssetsAsync` results.

## Hooks

### `usePermissions(options)`

Supported platforms: Android, iOS, tvOS.

| Parameter | Type |
| --- | --- |
| `options`(optional) | PermissionHookOptions<{ granularPermissions: [GranularPermission[]](https://docs.expo.dev/versions/v57.0.0/sdk/media-library-legacy.md#granularpermission), writeOnly: boolean }\> |

  

Check or request permissions to access the media library. This uses both `requestPermissionsAsync` and `getPermissionsAsync` to interact with the permissions.

Returns: `[PermissionResponse | null, RequestPermissionMethod<PermissionResponse>, GetPermissionMethod<PermissionResponse>]`

Example

```ts
const [permissionResponse, requestPermission] = MediaLibrary.usePermissions();
```

## Methods

### `MediaLibrary.addAssetsToAlbumAsync(assets, album, copy)`

Supported platforms: Android, iOS, tvOS.

| Parameter | Type | Description |
| --- | --- | --- |
| `assets` | [AssetRef](https://docs.expo.dev/versions/latest/sdk/media-library.md#asset) | [AssetRef[]](https://docs.expo.dev/versions/latest/sdk/media-library.md#asset) | An array of [Asset](https://docs.expo.dev/versions/v57.0.0/sdk/media-library-legacy.md#asset) or their IDs. |
| `album` | [AlbumRef](https://docs.expo.dev/versions/latest/sdk/media-library.md#album) | An [Album](https://docs.expo.dev/versions/v57.0.0/sdk/media-library-legacy.md#album) or its ID. |
| `copy`(optional) | `boolean` | **Android only.** Whether to copy assets to the new album instead of move them. Defaults to `true`. Default: `true` |

  

Adds array of assets to the album.

On Android, by default it copies assets from the current album to provided one, however it's also possible to move them by passing `false` as `copyAssets` argument. In case they're copied you should keep in mind that `getAssetsAsync` will return duplicated assets.

Returns: `Promise<boolean>`

Returns promise which fulfils with `true` if the assets were successfully added to the album.

### `MediaLibrary.albumNeedsMigrationAsync(album)`

Supported platforms: Android, iOS, tvOS.

| Parameter | Type | Description |
| --- | --- | --- |
| `album` | [AlbumRef](https://docs.expo.dev/versions/latest/sdk/media-library.md#album) | An [Album](https://docs.expo.dev/versions/v57.0.0/sdk/media-library-legacy.md#album) or its ID. |

  

Checks if the album should be migrated to a different location. In other words, it checks if the application has the write permission to the album folder. If not, it returns `true`, otherwise `false`.

> Note: For **Android below R**, **web** or **iOS**, this function always returns `false`.

Returns: `Promise<boolean>`

Returns a promise which fulfils with `true` if the album should be migrated.

### `MediaLibrary.createAlbumAsync(albumName, asset, copyAsset, initialAssetLocalUri)`

Supported platforms: Android, iOS, tvOS.

| Parameter | Type | Description |
| --- | --- | --- |
| `albumName` | `string` | Name of the album to create. |
| `asset`(optional) | [AssetRef](https://docs.expo.dev/versions/latest/sdk/media-library.md#asset) | An [Asset](https://docs.expo.dev/versions/v57.0.0/sdk/media-library-legacy.md#asset) or its ID. On Android you either need to provide an asset or a localUri. |
| `copyAsset`(optional) | `boolean` | **Android Only.** Whether to copy asset to the new album instead of move it. This parameter is ignored if `asset` was not provided. Defaults to `true`. Default: `true` |
| `initialAssetLocalUri`(optional) | `string` | A URI to the local media file, which will be used to create the initial asset inside the album. It must contain an extension. On Android it must be a local path, so it must start with `file:///`. If the `asset` was provided, this parameter will be ignored. |

  

Creates an album with given name and initial asset. The asset parameter is required on Android, since it's not possible to create empty album on this platform. On Android, by default it copies given asset from the current album to the new one, however it's also possible to move it by passing `false` as `copyAsset` argument. In case it's copied you should keep in mind that `getAssetsAsync` will return duplicated asset.

> On Android, it's not possible to create an empty album. You must provide an existing asset to copy or move into the album or an uri of a local file, which will be used to create an initial asset for the album.

Returns: `Promise<Album>`

Newly created [`Album`](https://docs.expo.dev/versions/v57.0.0/sdk/media-library-legacy.md#album).

### `MediaLibrary.createAssetAsync(localUri, album)`

Supported platforms: Android, iOS, tvOS.

| Parameter | Type | Description |
| --- | --- | --- |
| `localUri` | `string` | A URI to the image or video file. It must contain an extension. On Android it must be a local path, so it must start with `file:///` |
| `album`(optional) | [AlbumRef](https://docs.expo.dev/versions/latest/sdk/media-library.md#album) | An [Album](https://docs.expo.dev/versions/v57.0.0/sdk/media-library-legacy.md#album) or its ID. If provided, the asset will be added to this album upon creation, otherwise it will be added to the default album for the media type. The album has exist. |

  

Creates an asset from existing file. The most common use case is to save a picture taken by [Camera](https://docs.expo.dev/versions/v57.0.0/sdk/camera.md). This method requires `CAMERA_ROLL` permission.

Returns: `Promise<Asset>`

A promise which fulfils with an object representing an [`Asset`](https://docs.expo.dev/versions/v57.0.0/sdk/media-library-legacy.md#asset).

Example

```js
const { uri } = await Camera.takePictureAsync();
const asset = await MediaLibrary.createAssetAsync(uri);
```

### `MediaLibrary.deleteAlbumsAsync(albums, assetRemove)`

Supported platforms: Android, iOS, tvOS.

| Parameter | Type | Description |
| --- | --- | --- |
| `albums` | [AlbumRef](https://docs.expo.dev/versions/latest/sdk/media-library.md#album) | [AlbumRef[]](https://docs.expo.dev/versions/latest/sdk/media-library.md#album) | An array of [`Album`](https://docs.expo.dev/versions/v57.0.0/sdk/media-library-legacy.md#asset)s or their IDs. |
| `assetRemove`(optional) | `boolean` | **iOS Only.** Whether to also delete assets belonging to given albums. Defaults to `false`. Default: `false` |

  

Deletes given albums from the library. On Android by default it deletes assets belonging to given albums from the library. On iOS it doesn't delete these assets, however it's possible to do by passing `true` as `deleteAssets`.

Returns: `Promise<boolean>`

Returns a promise which fulfils with `true` if the albums were successfully deleted from the library.

### `MediaLibrary.deleteAssetsAsync(assets)`

Supported platforms: Android, iOS, tvOS.

| Parameter | Type | Description |
| --- | --- | --- |
| `assets` | [AssetRef](https://docs.expo.dev/versions/latest/sdk/media-library.md#asset) | [AssetRef[]](https://docs.expo.dev/versions/latest/sdk/media-library.md#asset) | An array of [Asset](https://docs.expo.dev/versions/v57.0.0/sdk/media-library-legacy.md#asset) or their IDs. |

  

Deletes assets from the library. On iOS it deletes assets from all albums they belong to, while on Android it keeps all copies of them (album is strictly connected to the asset). Also, there is additional dialog on iOS that requires user to confirm this action.

Returns: `Promise<boolean>`

Returns promise which fulfils with `true` if the assets were successfully deleted.

### `MediaLibrary.getAlbumAsync(title)`

Supported platforms: Android, iOS, tvOS.

| Parameter | Type | Description |
| --- | --- | --- |
| `title` | `string` | Name of the album to look for. |

  

Queries for an album with a specific name.

Returns: `Promise<Album>`

An object representing an [`Album`](https://docs.expo.dev/versions/v57.0.0/sdk/media-library-legacy.md#album), if album with given name exists, otherwise returns `null`.

### `MediaLibrary.getAssetContentUriAsync(asset)`

Supported platforms: Android.

| Parameter | Type | Description |
| --- | --- | --- |
| `asset` | [AssetRef](https://docs.expo.dev/versions/latest/sdk/media-library.md#asset) | An [`Asset`](https://docs.expo.dev/versions/v57.0.0/sdk/media-library-legacy.md#asset) or its ID. |

  

Returns the `content://` URI for the given legacy asset. Use this when migrating to the new class-based API — pass the returned URI as the ID to `new Asset(id)`.

Returns: `Promise<string>`

A promise which fulfils with the `content://` URI string for the asset.

### `MediaLibrary.getAssetInfoAsync(asset, options)`

Supported platforms: Android, iOS, tvOS.

| Parameter | Type | Description |
| --- | --- | --- |
| `asset` | [AssetRef](https://docs.expo.dev/versions/latest/sdk/media-library.md#asset) | An [Asset](https://docs.expo.dev/versions/v57.0.0/sdk/media-library-legacy.md#asset) or its ID. |
| `options`(optional) | [MediaLibraryAssetInfoQueryOptions](https://docs.expo.dev/versions/latest/sdk/media-library-legacy.md#medialibraryassetinfoqueryoptions) | - |

  

Provides more information about an asset, including GPS location, local URI and EXIF metadata. For better performance, prefer using individual getters such as `asset.getLocation()` or `asset.getExif()` to fetch only the data you need.

Returns: `Promise<AssetInfo>`

An [AssetInfo](https://docs.expo.dev/versions/v57.0.0/sdk/media-library-legacy.md#assetinfo) object, which is an `Asset` extended by an additional fields.

### `MediaLibrary.getAssetsAsync(assetsOptions)`

Supported platforms: Android, iOS, tvOS.

| Parameter | Type |
| --- | --- |
| `assetsOptions`(optional) | [AssetsOptions](https://docs.expo.dev/versions/latest/sdk/media-library-legacy.md#assetsoptions) |

  

Fetches a page of assets matching the provided criteria.

Returns: `Promise<PagedInfo<Asset>>`

A promise that fulfils with to [`PagedInfo`](https://docs.expo.dev/versions/v57.0.0/sdk/media-library-legacy.md#pagedinfo) object with array of [`Asset`](https://docs.expo.dev/versions/v57.0.0/sdk/media-library-legacy.md#asset)s.

### `MediaLibrary.getMomentsAsync()`

Supported platforms: iOS.

Fetches a list of moments, which is a group of assets taken around the same place and time.

Returns: `Promise<any>`

An array of [albums](https://docs.expo.dev/versions/v57.0.0/sdk/media-library-legacy.md#album) whose type is `moment`.

### `MediaLibrary.getPermissionsAsync(writeOnly, granularPermissions)`

Supported platforms: Android, iOS, tvOS.

| Parameter | Type | Description |
| --- | --- | --- |
| `writeOnly`(optional) | `boolean` | Default: `false` |
| `granularPermissions`(optional) | [GranularPermission[]](https://docs.expo.dev/versions/v57.0.0/sdk/media-library-legacy.md#granularpermission) | A list of [`GranularPermission`](https://docs.expo.dev/versions/v57.0.0/sdk/media-library-legacy.md#granularpermission) values. This parameter has an effect only on Android 13 and newer. By default, `expo-media-library` will ask for all possible permissions. |

  

Checks user's permissions for accessing media library.

Returns: `Promise<PermissionResponse>`

A promise that fulfils with [`PermissionResponse`](https://docs.expo.dev/versions/v57.0.0/sdk/media-library-legacy.md#permissionresponse) object.

### `MediaLibrary.isAvailableAsync()`

Supported platforms: Android, iOS, tvOS.

Returns whether the Media Library API is enabled on the current device.

Returns: `Promise<boolean>`

A promise which fulfils with a `boolean`, indicating whether the Media Library API is available on the current device.

### `MediaLibrary.migrateAlbumIfNeededAsync(album)`

Supported platforms: Android, iOS, tvOS.

| Parameter | Type | Description |
| --- | --- | --- |
| `album` | [AlbumRef](https://docs.expo.dev/versions/latest/sdk/media-library.md#album) | An [Album](https://docs.expo.dev/versions/v57.0.0/sdk/media-library-legacy.md#album) or its ID. |

  

Moves album content to the special media directories on **Android R** or **above** if needed. Those new locations are in line with the Android `scoped storage` - so your application won't lose write permission to those directories in future.

This method does nothing if:

-   app is running on **iOS**, **web** or **Android below R**
-   app has **write permission** to the album folder

The migration is possible when the album contains only compatible files types. For instance, movies and pictures are compatible with each other, but music and pictures are not. If automatic migration isn't possible, the function rejects. In that case, you can use methods from the `expo-file-system` to migrate all your files manually.

#### Why do you need to migrate files?

**Android R** introduced a lot of changes in storage system. Now applications can't save anything to the root directory. The only available locations are from the `MediaStore` API. Unfortunately, the media library stored albums in folders for which, because of those changes, the application doesn't have permissions anymore. However, it doesn't mean you need to migrate all your albums. If your application doesn't add assets to albums, you don't have to migrate. Everything will work as it used to. You can read more about scoped storage in [the Android documentation](https://developer.android.com/about/versions/11/privacy/storage).

Returns: `Promise<void>`

A promise which fulfils to `void`.

### `MediaLibrary.presentPermissionsPickerAsync(mediaTypes)`

Supported platforms: Android 14+, iOS.

| Parameter | Type | Description |
| --- | --- | --- |
| `mediaTypes`(optional) | [MediaTypeFilter[]](https://docs.expo.dev/versions/v57.0.0/sdk/media-library-legacy.md#mediatypefilter) | Limits the type(s) of media that the user will be granting access to. By default, a list that shows both photos and videos is presented. |

  

Allows the user to update the assets that your app has access to. The system modal is only displayed if the user originally allowed only `limited` access to their media library, otherwise this method is a no-op.

Returns: `Promise<void>`

A promise that either rejects if the method is unavailable, or resolves to `void`.

> **Note:** This method doesn't inform you if the user changes which assets your app has access to. That information is only exposed by iOS, and to obtain it, you need to subscribe for updates to the user's media library using [`addListener()`](https://docs.expo.dev/versions/v57.0.0/sdk/media-library-legacy.md#medialibraryaddlistenerlistener). If `hasIncrementalChanges` is `false`, the user changed their permissions.

### `MediaLibrary.removeAssetsFromAlbumAsync(assets, album)`

Supported platforms: Android, iOS, tvOS.

| Parameter | Type | Description |
| --- | --- | --- |
| `assets` | [AssetRef](https://docs.expo.dev/versions/latest/sdk/media-library.md#asset) | [AssetRef[]](https://docs.expo.dev/versions/latest/sdk/media-library.md#asset) | An array of [Asset](https://docs.expo.dev/versions/v57.0.0/sdk/media-library-legacy.md#asset) or their IDs. |
| `album` | [AlbumRef](https://docs.expo.dev/versions/latest/sdk/media-library.md#album) | An [Album](https://docs.expo.dev/versions/v57.0.0/sdk/media-library-legacy.md#album) or its ID. |

  

Removes given assets from album.

On Android, album will be automatically deleted if there are no more assets inside.

Returns: `Promise<boolean>`

Returns promise which fulfils with `true` if the assets were successfully removed from the album.

### `MediaLibrary.removeSubscription(subscription)`

Supported platforms: Android, iOS, tvOS.

| Parameter | Type |
| --- | --- |
| `subscription` | `EventSubscription` |

  

Returns: `void`

### `MediaLibrary.requestPermissionsAsync(writeOnly, granularPermissions)`

Supported platforms: Android, iOS, tvOS.

| Parameter | Type | Description |
| --- | --- | --- |
| `writeOnly`(optional) | `boolean` | Default: `false` |
| `granularPermissions`(optional) | [GranularPermission[]](https://docs.expo.dev/versions/v57.0.0/sdk/media-library-legacy.md#granularpermission) | A list of [`GranularPermission`](https://docs.expo.dev/versions/v57.0.0/sdk/media-library-legacy.md#granularpermission) values. This parameter has an effect only on Android 13 and newer. By default, `expo-media-library` will ask for all possible permissions. When using granular permissions with a custom config plugin configuration, make sure that all the requested permissions are included in plugin. |

  

Asks the user to grant permissions for accessing media in user's media library.

Returns: `Promise<PermissionResponse>`

A promise that fulfils with [`PermissionResponse`](https://docs.expo.dev/versions/v57.0.0/sdk/media-library-legacy.md#permissionresponse) object.

### `MediaLibrary.saveToLibraryAsync(localUri)`

Supported platforms: Android, iOS, tvOS.

| Parameter | Type | Description |
| --- | --- | --- |
| `localUri` | `string` | A URI to the image or video file. It must contain an extension. On Android it must be a local path, so it must start with `file:///`. |

  

Saves the file at given `localUri` to the user's media library. Unlike `createAssetAsync()`, This method doesn't return created asset. On **iOS 11+**, it's possible to use this method without asking for `CAMERA_ROLL` permission, however then yours `Info.plist` should have `NSPhotoLibraryAddUsageDescription` key.

Returns: `Promise<void>`

### `MediaLibrary.setAssetFavoriteAsync(asset, isFavorite)`

Supported platforms: iOS.

| Parameter | Type | Description |
| --- | --- | --- |
| `asset` | [AssetRef](https://docs.expo.dev/versions/latest/sdk/media-library.md#asset) | An [Asset](https://docs.expo.dev/versions/v57.0.0/sdk/media-library-legacy.md#asset) or its ID. |
| `isFavorite` | `boolean` | Whether the asset should be marked as favorite. |

  

On iOS, this adds or removes the asset from the system "Favorites" smart album.

Returns: `Promise<boolean>`

Returns a promise which fulfils with `true` if the operation was successful.

## Event subscriptions

### `MediaLibrary.addListener(listener)`

Supported platforms: Android, iOS, tvOS.

| Parameter | Type | Description |
| --- | --- | --- |
| `listener` | (event: [MediaLibraryAssetsChangeEvent](https://docs.expo.dev/versions/v57.0.0/sdk/media-library-legacy.md#medialibraryassetschangeevent)) => void | A callback that is fired when any assets have been inserted or deleted from the library. On Android it's invoked with an empty object. On iOS, it's invoked with [`MediaLibraryAssetsChangeEvent`](https://docs.expo.dev/versions/v57.0.0/sdk/media-library-legacy.md#medialibraryassetschangeevent) object. Additionally, only on iOS, the listener is also invoked when the user changes access to individual assets in media library using `presentPermissionsPickerAsync()`. |

  

Subscribes for updates in user's media library.

Returns: `EventSubscription`

An [`Subscription`](https://docs.expo.dev/versions/v57.0.0/sdk/media-library-legacy.md#subscription) object that you can call `remove()` on when you would like to unsubscribe the listener.

### `MediaLibrary.removeAllListeners()`

Supported platforms: Android, iOS, tvOS.

Removes all listeners.

Returns: `void`

## Interfaces

### `Subscription`

Supported platforms: Android, iOS, tvOS.

A subscription object that allows to conveniently remove an event listener from the emitter.

Subscription Methods

### `remove()`

Supported platforms: Android, iOS, tvOS.

Removes an event listener for which the subscription has been created. After calling this function, the listener will no longer receive any events from the emitter.

Returns: `void`

## Types

### `Album`

Supported platforms: Android, iOS, tvOS.

| Property | Type | Description |
| --- | --- | --- |
| approximateLocation(optional) | [Location](https://docs.expo.dev/versions/latest/sdk/media-library.md#location) | Supported platforms: iOS. Apply only to albums whose type is `'moment'`. Approximated location of all assets in moment. |
| assetCount | `number` | Estimated number of assets in album. |
| endTime | `number` | Supported platforms: iOS. Apply only to albums whose type is `'moment'`. Latest creation timestamp of all assets in moment. |
| id | `string` | Album ID. |
| locationNames(optional) | `string[]` | Supported platforms: iOS. Apply only to albums whose type is `'moment'`. Names of locations grouped in moment. |
| startTime | `number` | Supported platforms: iOS. Apply only to albums whose type is `'moment'`. Earliest creation timestamp of all assets in moment. |
| title | `string` | Album title. |
| type(optional) | [AlbumType](https://docs.expo.dev/versions/v57.0.0/sdk/media-library-legacy.md#albumtype) | Supported platforms: iOS. The type of the assets album. |

### `AlbumsOptions`

Supported platforms: Android, iOS, tvOS.

| Property | Type | Description |
| --- | --- | --- |
| includeSmartAlbums(optional) | `boolean` | - |

### `AlbumType`

Supported platforms: Android, iOS, tvOS.

Literal type: `string`

Acceptable values are: `'album'` | `'moment'` | `'smartAlbum'`

### `Asset`

Supported platforms: Android, iOS, tvOS.

| Property | Type | Description |
| --- | --- | --- |
| albumId(optional) | `string` | Supported platforms: Android. Album ID that the asset belongs to. |
| creationTime | `number` | File creation timestamp. |
| duration | `number` | Duration of the video or audio asset in seconds. |
| filename | `string` | Filename of the asset. |
| height | `number` | Height of the image or video. |
| id | `string` | Internal ID that represents an asset. |
| mediaSubtypes(optional) | [MediaSubtype[]](https://docs.expo.dev/versions/v57.0.0/sdk/media-library-legacy.md#mediasubtype) | Supported platforms: iOS. An array of media subtypes. |
| mediaType | [MediaTypeValue](https://docs.expo.dev/versions/v57.0.0/sdk/media-library-legacy.md#mediatypevalue) | Media type. |
| modificationTime | `number` | Last modification timestamp. |
| uri | `string` | URI that points to the asset. `ph://*` (iOS), `file://*` (Android) |
| width | `number` | Width of the image or video. |

### `AssetInfo`

Supported platforms: Android, iOS, tvOS.

Type: [Asset](https://docs.expo.dev/versions/latest/sdk/asset.md#asset) extended by:

| Property | Type | Description |
| --- | --- | --- |
| exif(optional) | `object` | EXIF metadata associated with the image. |
| isFavorite(optional) | `boolean` | Supported platforms: iOS. Whether the asset is marked as favorite. |
| isNetworkAsset(optional) | `boolean` | Supported platforms: iOS. This field is available only if flag `shouldDownloadFromNetwork` is set to `false`. Whether the asset is stored on the network (iCloud on iOS). |
| localUri(optional) | `string` | Local URI for the asset. |
| location(optional) | [Location](https://docs.expo.dev/versions/latest/sdk/media-library.md#location) | GPS location if available. |
| orientation(optional) | `number` | Supported platforms: iOS. Display orientation of the image. Orientation is available only for assets whose `mediaType` is `MediaType.photo`. Value will range from 1 to 8, see [EXIF orientation specification](http://sylvana.net/jpegcrop/exif_orientation.html) for more details. |
| pairedVideoAsset(optional) | [Asset](https://docs.expo.dev/versions/latest/sdk/asset.md#asset) | null | Supported platforms: iOS. Contains information about the video paired with the image file. This field is available if the `mediaType` is `"photo"`, and the `mediaSubtypes` includes `"livePhoto"`. |

### `AssetsOptions`

Supported platforms: Android, iOS, tvOS.

| Property | Type | Description |
| --- | --- | --- |
| after(optional) | [AssetRef](https://docs.expo.dev/versions/latest/sdk/media-library.md#asset) | Asset ID of the last item returned on the previous page. To get the ID of the next page, pass [`endCursor`](https://docs.expo.dev/versions/v57.0.0/sdk/media-library-legacy.md#pagedinfo) as its value. |
| album(optional) | [AlbumRef](https://docs.expo.dev/versions/latest/sdk/media-library.md#album) | [Album](https://docs.expo.dev/versions/v57.0.0/sdk/media-library-legacy.md#album) or its ID to get assets from specific album. |
| createdAfter(optional) | [Date](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date) | number | `Date` object or Unix timestamp in milliseconds limiting returned assets only to those that were created after this date. |
| createdBefore(optional) | [Date](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date) | number | Similarly as `createdAfter`, but limits assets only to those that were created before specified date. |
| first(optional) | `number` | The maximum number of items on a single page. Default: `20` |
| mediaSubtypes(optional) | [MediaSubtype[]](https://docs.expo.dev/versions/v57.0.0/sdk/media-library-legacy.md#mediasubtype) | [MediaSubtype](https://docs.expo.dev/versions/v57.0.0/sdk/media-library-legacy.md#mediasubtype) | Supported platforms: iOS. An array of [MediaSubtype](https://docs.expo.dev/versions/v57.0.0/sdk/media-library-legacy.md#mediasubtype)s or a single `MediaSubtype`. |
| mediaType(optional) | [MediaTypeValue[]](https://docs.expo.dev/versions/v57.0.0/sdk/media-library-legacy.md#mediatypevalue) | [MediaTypeValue](https://docs.expo.dev/versions/v57.0.0/sdk/media-library-legacy.md#mediatypevalue) | An array of [MediaTypeValue](https://docs.expo.dev/versions/v57.0.0/sdk/media-library-legacy.md#mediatypevalue)s or a single `MediaTypeValue`. Default: `MediaType.photo` |
| resolveWithFullInfo(optional) | `boolean` | Supported platforms: Android. Whether to resolve full info for the assets during the query. This is useful to get the full EXIF data for images. It can fix the orientation of the image. Default: `false` |
| sortBy(optional) | [SortByValue[]](https://docs.expo.dev/versions/v57.0.0/sdk/media-library-legacy.md#sortbyvalue) | [SortByValue](https://docs.expo.dev/versions/v57.0.0/sdk/media-library-legacy.md#sortbyvalue) | An array of [`SortByValue`](https://docs.expo.dev/versions/v57.0.0/sdk/media-library-legacy.md#sortbyvalue)s or a single `SortByValue` value. By default, all keys are sorted in descending order, however you can also pass a pair `[key, ascending]` where the second item is a `boolean` value that means whether to use ascending order. Note that if the `SortBy.default` key is used, then `ascending` argument will not matter. Earlier items have higher priority when sorting out the results. If empty, this method uses the default sorting that is provided by the platform. |

### `EXPermissionResponse`

Supported platforms: Android, iOS, tvOS.

An object obtained by permissions get and request functions.

| Property | Type | Description |
| --- | --- | --- |
| canAskAgain | `boolean` | Indicates if user can be asked again for specific permission. If not, one should be directed to the Settings app in order to enable/disable the permission. |
| expires | `PermissionExpiration` | Determines time when the permission expires. |
| granted | `boolean` | A convenience boolean that indicates if the permission is granted. |
| status | [PermissionStatus](https://docs.expo.dev/versions/latest/sdk/expo.md#permissionstatus) | Determines the status of the permission. |

### `GranularPermission`

Supported platforms: Android 13+.

Literal type: `string`

Determines the type of media that the app will ask the OS to get access to.

Acceptable values are: `'audio'` | `'photo'` | `'video'`

### `Location`

Supported platforms: Android, iOS, tvOS.

| Property | Type | Description |
| --- | --- | --- |
| latitude | `number` | - |
| longitude | `number` | - |

### `MediaLibraryAssetInfoQueryOptions`

Supported platforms: Android, iOS, tvOS.

| Property | Type | Description |
| --- | --- | --- |
| shouldDownloadFromNetwork(optional) | `boolean` | Whether allow the asset to be downloaded from network. Only available in iOS with iCloud assets. Default: `true` |

### `MediaLibraryAssetsChangeEvent`

Supported platforms: Android, iOS, tvOS.

| Property | Type | Description |
| --- | --- | --- |
| deletedAssets(optional) | [Asset[]](https://docs.expo.dev/versions/latest/sdk/asset.md#asset) | Available only if `hasIncrementalChanges` is `true`. Array of [`Asset`](https://docs.expo.dev/versions/v57.0.0/sdk/media-library-legacy.md#asset)s that have been deleted from the library. |
| hasIncrementalChanges | `boolean` | Whether the media library's changes could be described as "incremental changes". `true` indicates the changes are described by the `insertedAssets`, `deletedAssets` and `updatedAssets` values. `false` indicates that the scope of changes is too large and you should perform a full assets reload (eg. a user has changed access to individual assets in the media library). |
| insertedAssets(optional) | [Asset[]](https://docs.expo.dev/versions/latest/sdk/asset.md#asset) | Available only if `hasIncrementalChanges` is `true`. Array of [`Asset`](https://docs.expo.dev/versions/v57.0.0/sdk/media-library-legacy.md#asset)s that have been inserted to the library. |
| updatedAssets(optional) | [Asset[]](https://docs.expo.dev/versions/latest/sdk/asset.md#asset) | Available only if `hasIncrementalChanges` is `true`. Array of [`Asset`](https://docs.expo.dev/versions/v57.0.0/sdk/media-library-legacy.md#asset)s that have been updated or completed downloading from network storage (iCloud on iOS). |

### `MediaSubtype`

Supported platforms: iOS.

Literal type: `string`

Constants identifying specific variations of asset media, such as panorama or screenshot photos, and time-lapse or high-frame-rate video. Maps to [`PHAssetMediaSubtype`](https://developer.apple.com/documentation/photokit/phassetmediasubtype#1603888).

Acceptable values are: `'depthEffect'` | `'hdr'` | `'highFrameRate'` | `'livePhoto'` | `'panorama'` | `'screenshot'` | `'stream'` | `'timelapse'` | `'spatialMedia'` | `'videoCinematic'`

### `MediaTypeFilter`

Supported platforms: Android 14+.

Literal type: `string`

Represents the possible types of media that the app will ask the OS to get access to when calling [`presentPermissionsPickerAsync()`](https://docs.expo.dev/versions/v57.0.0/sdk/media-library-legacy.md#medialibrarypresentpermissionspickerasyncmediatypes).

Acceptable values are: `'photo'` | `'video'`

### `MediaTypeObject`

Supported platforms: Android, iOS, tvOS.

| Property | Type | Description |
| --- | --- | --- |
| audio | `'audio'` | - |
| photo | `'photo'` | - |
| unknown | `'unknown'` | - |
| video | `'video'` | - |

### `MediaTypeValue`

Supported platforms: Android, iOS, tvOS.

Literal type: `string`

Acceptable values are: `'audio'` | `'photo'` | `'video'` | `'unknown'` | `'pairedVideo'`

### `PagedInfo`

Supported platforms: Android, iOS, tvOS.

| Property | Type | Description |
| --- | --- | --- |
| assets | `T[]` | A page of [`Asset`](https://docs.expo.dev/versions/v57.0.0/sdk/media-library-legacy.md#asset)s fetched by the query. |
| endCursor | `string` | A marker that indicates where the next page of results should start. On iOS, it is the ID of the last fetched asset. On Android, it is the index of the last fetched asset in query results. This value should be passed as the `after` option to load the next page. |
| hasNextPage | `boolean` | Whether there are more assets to fetch. |
| totalCount | `number` | Estimated total number of assets that match the query. |

### `PermissionExpiration`

Supported platforms: Android, iOS, tvOS.

Literal type: `union`

Permission expiration time. Currently, all permissions are granted permanently.

Acceptable values are: `'never'` | `number`

### `PermissionHookOptions`

Supported platforms: Android, iOS, tvOS.

Literal type: `union`

Acceptable values are: `PermissionHookBehavior` | `Options`

### `PermissionResponse`

Supported platforms: Android, iOS, tvOS.

Type: [EXPermissionResponse](https://docs.expo.dev/versions/v57.0.0/sdk/media-library-legacy.md#expermissionresponse) extended by:

| Property | Type | Description |
| --- | --- | --- |
| accessPrivileges(optional) | `'all' | 'limited' | 'none'` | Indicates if your app has access to the whole or only part of the photo library. Possible values are:
-   `'all'` if the user granted your app access to the whole photo library
-   `'limited'` if the user granted your app access only to selected photos (only available on Android API 14+ and iOS 14.0+)
-   `'none'` if user denied or hasn't yet granted the permission

 |

### `SortByKey`

Supported platforms: Android, iOS, tvOS.

Literal type: `string`

Acceptable values are: `'default'` | `'mediaType'` | `'width'` | `'height'` | `'creationTime'` | `'modificationTime'` | `'duration'`

### `SortByObject`

Supported platforms: Android, iOS, tvOS.

| Property | Type | Description |
| --- | --- | --- |
| creationTime | `'creationTime'` | - |
| default | `'default'` | - |
| duration | `'duration'` | - |
| height | `'height'` | - |
| mediaType | `'mediaType'` | - |
| modificationTime | `'modificationTime'` | - |
| width | `'width'` | - |

### `SortByValue`

Supported platforms: Android, iOS, tvOS.

Literal type: `union`

Acceptable values are: \[[SortByKey](https://docs.expo.dev/versions/v57.0.0/sdk/media-library-legacy.md#sortbykey), boolean\] | [SortByKey](https://docs.expo.dev/versions/v57.0.0/sdk/media-library-legacy.md#sortbykey)

## Enums

### `PermissionStatus`

Supported platforms: Android, iOS, tvOS.

#### `DENIED`

`PermissionStatus.DENIED = "denied"`

User has denied the permission.

#### `GRANTED`

`PermissionStatus.GRANTED = "granted"`

User has granted the permission.

#### `UNDETERMINED`

`PermissionStatus.UNDETERMINED = "undetermined"`

User hasn't granted or denied the permission yet.

## Permissions

### Android

The following permissions are added automatically through this library's **AndroidManifest.xml**:

| Android permission | Description |
| --- | --- |
| `READ_EXTERNAL_STORAGE` | Allows an application to read from external storage. |
| `WRITE_EXTERNAL_STORAGE` | Allows an application to write to external storage. |
| `READ_MEDIA_IMAGES` | Allows an application to read image files from external storage. |
| `READ_MEDIA_VIDEO` | Allows an application to read video files from external storage. |
| `READ_MEDIA_AUDIO` | Allows an application to read audio files from external storage. |
| `READ_MEDIA_VISUAL_USER_SELECTED` | Allows an application to read image or video files from external storage that a user has selected via the permission prompt photo picker. Apps can check this permission to verify that a user has decided to use the photo picker, instead of granting access to READ_MEDIA_IMAGES or READ_MEDIA_VIDEO. It does not prevent apps from accessing the standard photo picker manually. This permission should be requested alongside READ_MEDIA_IMAGES and/or READ_MEDIA_VIDEO, depending on which type of media is desired. |

### iOS

The following usage description keys are used by this library:

| Info.plist key | Description |
| --- | --- |
| `NSPhotoLibraryUsageDescription` | A message that tells the user why the app is requesting access to the user’s photo library. |
| `NSPhotoLibraryAddUsageDescription` | A message that tells the user why the app is requesting add-only access to the user’s photo library. |
