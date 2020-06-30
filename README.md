
# Kagii iOS SDK

Kagii protects the enterprise by carefully authenticating authorized users seeking access to the network and to applications. Grant users secure access to all protected applications (on-premises or cloud-based) through a uniform, frictionless interface accessible from anywhere.

## Full example
A full example which integrates Kagii SDK with KYCExpert SDK is available in the repository
[Sedicii/KYCexpert-High-Assurance-Example](https://github.com/Sedicii/KYCexpert-High-Assurance-Example)

## Requirements

* iOS 13.0 and higher
* Internet connection
* Permissions for camera

## Permissions

The permissions declared in the SDK are assigned automatically to the client application.

According to the Apple documentation, an iOS app linked on or after iOS 10.0,
must describe the reason why your app needs that permission.

It is necessary to include the **NSCameraUsageDescription**, **NSPhotoLibraryUsageDescription**
and **NSMicrophoneUsageDescription** keys in your app's Info.plist file and provide
a purpose string for this key.

## Include SDK in Project

This framework can be included in your project with [__Carthage__](https://github.com/Carthage/Carthage):

```
github "Sedicii/Kagii-iOS"
```

Or you can include it manually downloading [__the latest version__](https://github.com/Sedicii/Kagii-iOS/releases/latest).

### Dependencies

This framework depends on the following frameworks:

```
github "Sedicii/SediciiCoreSDK-iOS"
github "Sedicii/SediciiZkpSDK-iOS"
```

You can include them manually downloading
[SediciiCoreSDK latest version](https://github.com/Sedicii/SediciiCoreSDK-iOS/releases/latest) and
[SediciiZkpSDK latest version](https://github.com/Sedicii/SediciiZkpSDK-iOS/releases/latest)

## SDK Configuration

These are the available variables to configure the SDK:

| Name                    | Required  | Description                                                                   |
|-------------------------|-----------|-------------------------------------------------------------------------------|
| API_ENDPOINT            |   true    | The API_ENDPOINT of the backend used by the SDK, Sedicii will provide it.     |
| API_KEY                 |   true    | The API_KEY of the backend used by the SDK, Sedicii will provide it.          |
| CLIENT_ID               |   true    | The CLIENT_ID is the unique identifier of the client, Sedicii will provide it.|
| REDIRECT_URI            |   true    | The REDIRECT_URI of the authorised domain, Sedicii will provide it.           |
| PASSWORD_CONFIRM_NEEDED |   false   | If true, it'll show a password confirmation field. By default, it's false.    |

To configure the SDK in iOS a plist type file is needed located in the main project path, with name **Kagii-Info.plist**
(make sure it is added in *BuildPhases* > *Copy Bundle Resources*), which can have the following values:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
    <dict>
        <key>API_ENDPOINT</key>
        <string>https://example.acc.sedicii.com</string>
        <key>API_KEY</key>
        <string>xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx</string>
        <key>CLIENT_ID</key>
        <string>example</string>
        <key>REDIRECT_URI</key>
        <string>https://example.kyc.sedicii.com/admin/login</string>
        <key>PASSWORD_CONFIRM_NEEDED</key>
        <true/>
    </dict>
</plist>
```

## SDK Initialisation

To initialise the SDK, it is needed to call the method `Kagii.userInterface.logInUser` as follows:

```swift
Kagii.userInterface.logInUser { kagiiResult in
    switch kagiiResult {
    case .failure(let error):
        // error - LogInUserError
    case .success(let response):
        // response - LogInUserResponse
    }
}
```

#### LogInUserError
LogInUserError is the enumeration which is returned in case of failure in the `Kagii.userInterface.logInUser` call.

```swift
public enum LogInUserError: Error {
    case error(Error)
    case sdkClosed
}
```

#### LogInUserResponse
LogInUserResponse is the data structure which is returned in the successfull case in the `Kagii.userInterface.logInUser` call.

```swift
public struct LogInUserData {
    public var id: String
}

public struct LogInUserResponse {
    public var user: LogInUserData
    public var code: String
}
```

### Appearance

The full appearance definition is available in [appearance section](/docs/appearance.md).

Defining the appearance. This is way to define your own appearance.

```swift
Kagii.userInterface.appearance = ClientAppearance.appearance
```

### Logging

To get logs for this SDK you can set the `loggerLevel`:

```swift
Kagii.loggerLevel = .error // There are several levels to choose
```
