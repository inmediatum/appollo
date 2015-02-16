# Appollo

### Initialize

1.- Drag and drop Appollo.framework into your project and ```#import <Appollo/Appollo.h>``` on your AppDelegate

2.- Initialize Appollo in your AppDelegate::application:didFinishLaunchingWithOptions: and replace the Api Key.

    [APCore
        appolloWithApiKey: @"YOUR-API-KEY"
        useBackgroundRefresh: YES
    ];
    
    [[APCore monitor] startMonitoringAll];
    
3.- On AppDelegate::application:didRegisterForRemoteNotificationsWithDeviceToken: add

    [APCore suscribeToChangesNotifications:deviceToken];
    
4.- On AppDelegate::application:didReceiveRemoteNotification:fetchCompletionHandler: add

    [APCore fetchUpdateInBackground:^(UIBackgroundFetchResult result) {
        dispatch_async(dispatch_get_main_queue(), ^{
            // Here your optional code
            completionHandler( result );
        });
    }];
    
5.- On AppDelegate::application:didReceiveLocalNotification: add

    id remoteData = [APCore didReceiveLocalNotification:notification];
    
  * remoteData contains the custom payload passed on web interface.

6.- Enable Background Modes Capabilities:
  * Location Updates
  * Uses Background LE accesories
  * Acts as a Bluetooth LE Accesory
  * Remote Notifications

7.- In your Info.plist add NSLocationAlwaysUsageDescription in value explain to the user why the app should use them location.

8.- In Build Settings -> Other Linker Flags add -ObjC

### Requeriments

Appollo is designed to work in iOS 8 o greater.
