# AppTrackingTransparency
iOS 14 Checklist-App Tracking Transparency（ATT）Suitable for requesting user authorization and accessing application-related data to track users or devices

# User authorization renderings

<img src="./READMEIMAGE/Simulator Screen Shot - iPhone 8 - 2020-12-23 at 13.28.49.png" style="zoom:25%;" />

<img src="./READMEIMAGE/Simulator Screen Shot - iPhone 8 - 2020-12-23 at 14.06.08.png" style="zoom:25%;" />



# 注意事项：
*  App Tracking Transparency（ATT）Suitable for requesting user authorization and accessing application-related data to track users or devices。 access https://developer.apple.com/documentation/apptrackingtransparency to know more information.

* SKAdNetwork (SKAN) is Apple’s attribution solution that helps advertisers measure ad campaigns while maintaining user privacy. After using Apple’s SKAdNetwork, even if IDFA is unavailable, the ad network can correctly obtain attribution results for app installations. Visit https://developer.apple.com/documentation/storekit/skadnetwork for more information.
Before Apple does not require developers to configure ATT, developers should not configure ATT. After the current configuration, it will affect the acquisition of idfa and thus affect advertising revenue.


# Checklist
* Upgrade the application compilation environment to Xcode 12.0 and above

* If a third-party advertising SDK is integrated, it needs to provide iOS 14 and SKAdNetwork support

* Add the SKAdNetwork ID of the third-party advertising SDK to info.plist to ensure the correct operation of SKAdNetwork

```xml
	<key>SKAdNetworkItems</key>
  <array>
    <dict>
      <key>SKAdNetworkIdentifier</key>
      <string>238da6jt44.skadnetwork</string>
    </dict>
    <dict>
      <key>SKAdNetworkIdentifier</key>
      <string>22mmun2rn5.skadnetwork</string>
    </dict>
  </array>
```

* Support Apple ATT: Starting from iOS 14, if the developer sets App Tracking Transparency to apply for tracking authorization from the user, IDFA will not be available until the user authorizes it. If the user rejects this request, the IDFA obtained by the app will be automatically cleared, which may result in a decrease in your advertising revenue
  To obtain App Tracking Transparency permissions, please update your Info.plist to add the NSUserTrackingUsageDescription field and custom text description. Code example:
```xml
<key>NSUserTrackingUsageDescription</key>
<string>This identifier will be used to deliver personalized ads to you</string>
```



# Swift code example
```swift
import AppTrackingTransparency
import AdSupport
func requestIDFA() {
  ATTrackingManager.requestTrackingAuthorization(completionHandler: { 	status in
    // Tracking authorization completed. Start loading ads here.
    // loadAd()
  })
}
```


# Objective-C code example

```objective-c
#import <AppTrackingTransparency/AppTrackingTransparency.h>
#import <AdSupport/AdSupport.h>
- (void)requestIDFA {
  [ATTrackingManager 		requestTrackingAuthorizationWithCompletionHandler:^(ATTrackingManagerAuth	orizationStatus status) {
    // Tracking authorization completed. Start loading ads here.
    // [self loadAd];
  }];
}
```
