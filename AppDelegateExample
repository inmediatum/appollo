//
//  AppDelegate.m
//  Appollo Console
//
//  Copyright (c) 2015 Inmediatum. All rights reserved.
//

#import "AppDelegate.h"
#import <Appollo/Appollo.h>

@interface AppDelegate ()

@end

@implementation AppDelegate


- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
{
    [self registerForNotifications];

    [APCore
        appolloWithApiKey: @"YOUR-API-KEY"
        useBackgroundRefresh: YES
    ];

    [[APCore monitor] startMonitoringAll];

    return YES;
}

- (void)registerForNotifications
{
    [[UIApplication sharedApplication] registerForRemoteNotifications];
    
    UIUserNotificationSettings *settings = [UIUserNotificationSettings
        settingsForTypes:(
            UIUserNotificationTypeBadge |
            UIUserNotificationTypeSound |
            UIUserNotificationTypeAlert
        )
        categories:nil];
    
    [[UIApplication sharedApplication] registerUserNotificationSettings:settings];
}

- (void)application:(UIApplication *)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData *)deviceToken
{
    [APCore suscribeToChangesNotifications:deviceToken];
}

- (void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo fetchCompletionHandler:(void (^)(UIBackgroundFetchResult))completionHandler
{
    [APCore fetchUpdateInBackground:^(UIBackgroundFetchResult result) {
        dispatch_async(dispatch_get_main_queue(), ^{
            // Here your optional code
            completionHandler( result );
        });
    }];
}

- (void)application:(UIApplication *)application didReceiveLocalNotification:(UILocalNotification *)notification
{
    id remoteData = [APCore didReceiveLocalNotification:notification];
}

@end
