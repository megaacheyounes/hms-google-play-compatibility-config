## Improving HMS SDK Compatibility with Google Play

This document provides configurations to improve the compatibility between Huawei Mobile Services (HMS) SDK and Google Play Store policies, to help prevent release rejections.

## Content

- [Excluding HMS Core Installer](#excluding-hms-core-installer)
- [Removing Sensitive Permissions](#removing-sensitive-permissions)
- [**[Important]** Considerations after adding above configuration](#considerations-after-adding-above-configuration)
- [Disclaimer](#disclaimer)
- [Contribute to this document](#contribute-to-this-document)

### Excluding HMS Core Installer

Some HMS dependencies include a sub-dependency that might prompt users to download or update HMS Core, which may violate Google Play Store policies. Excluding this dependency ensures compliance which should not have an impact on SDK functionalities.

in app level `build.gradle`:

```groovy
android {
    // ...
}

dependencies {
    // ...
}

configurations {
    all*.exclude group: "com.huawei.hms", module: "hmscoreinstaller"
}
```

### Removing Sensitive Permissions

Certain HMS dependencies declare sensitive permissions for various reasons, such as serving personalized ads. Removing these permissions generally is safe for most HMS services and should not affect core SDK functionalities.

in `AndroidManifest.xml`:

```xml
<manifest ... >

    <uses-permission
        android:name="android.permission.QUERY_ALL_PACKAGES"
        tools:ignore="QueryAllPackagesPermission"
        tools:node="remove" />

    <uses-permission
        android:name="android.permission.REQUEST_INSTALL_PACKAGES"
        tools:node="remove" />


    <application ... >
      ...
</manifest>
```

### Considerations after adding above configuration

- **Testing:** Carry out comprehensive testing to make sure these modifications don't affect the functions of your app, HMS SDK, and other dependencies.
- **SDK Updates:** Keep HMS SDK versions up-to-date, as newer releases might address compatibility issues.

### Disclaimer

While the above configurations can help improve compatibility, there's no guaranteed solution. Always test thoroughly and consider consulting with Google support for specific rejection rejection and .

### Contribute to this document

If you have received a warning or rejection from Google Play due to HMS SDK issues, please create an <a href="https://github.com/megaacheyounes/hms-google-play-compatibility-config/issues" target="_blank">issue</a> and share your experience. Include screenshots or relevant messages to improve this document and help fellow developers avoid rejections 🙏.
