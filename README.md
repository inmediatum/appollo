# Appollo

### Requeriments

Appollo is designed to work in iOS 8 o greater.

### Initialize

[Complete AppDelegate example](https://github.com/inmediatum/appollo/blob/master/AppDelegateExample) (Point 1-2-3-4-5)

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

![Example](http://g.recordit.co/49PhtyEP60.gif)

7.- In Info.plist add NSLocationAlwaysUsageDescription and explain in natural language why your app should use the location.

![Example](http://i.imgur.com/ck9rrgn.png)

8.- In Build Settings -> Other Linker Flags add -ObjC

![Example](http://g.recordit.co/MmKC1otP4n.gif)

### Manage notifications on foreground

[Take look Appollo Console source-code for complete example](https://github.com/inmediatum/appollo-console-ios)

1.- Implement the ```<APMonitorDelegate>``` protocol

2.- Delegate Monitor in your class.
    
    [APCore monitor].delegate = self;

Note if your class is UIViewController is a good idea to delegate in viewDidLoad method.

3.- Implement the APMonitorDelegate

    #pragma mark - APMonitorDelegate

    - (void)didReceiveNotification:(APTag *)tag
    {
        NSLog(@"Tag: %@", tag);
    }
    
    - (void)userRejectPermissions
    {
        NSLog(@"User reject permissions");
    }
    
    - (void)userAcceptPermissions
    {
        NSLog(@"User accept permissions");
    }
    
    - (void)uncompatibleDevice
    {
        NSLog(@"Uncompatible device");
    }
