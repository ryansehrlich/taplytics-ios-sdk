Setting up Push Notifications using Taplytics is simple. Follow the steps below to get started.

| # | Step |
| - | ----------------- |
| 1 | [Setup](#1-setup) |
| 2 | [Receiving Push Notifications](#2-receiving-push-notifictions) |
| 3 | [Resetting Users](#3-resetting-users) |

## 1. Setup

### Implement functions
In order for iOS and Taplytics to know that your app accepts Push Notifications, you must implement the following methods on your  `UIApplicationDelegate`.

    ```objc
    // Implement these methods for Taplytics Push Notifications
    - (void)application:(UIApplication *)application
    didRegisterUserNotificationSettings:(UIUserNotificationSettings *)notificationSettings {
    }
     
    - (void)application:(UIApplication *)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData *)deviceToken {
    }
     
    - (void)application:(UIApplication *)application didFailToRegisterForRemoteNotificationsWithError:(NSError *)error {
    }
     
    - (void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo {
    }
     
    - (void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo
    fetchCompletionHandler:(void (^)(UIBackgroundFetchResult))completionHandler {
    completionHandler(UIBackgroundFetchResultNoData);
    }
    ```

---

## 2. Register for Push Notifications

You'll also need to register for push notifications with iOS. When you do so, iOS will ask your users for permission and enable the ability to receive notifications to that device.

If you are not already registering for push notifications all you have to do is call registerPushNotifications: on Taplytics, and we take care of all the rest!

Please note that calling this function will show the permission dialog to the user.

```objc
/* Example usage */
[Taplytics registerPushNotifications];
```

---


## 2. Receiving Push Notifictions

In order to be able to send your users Push Notifications, we'll need you to upload your Google Cloud Messaging credentials. Please follow [this guide](https://taplytics.com/docs/guides/push-notifications/google-push-certificates) to do so.


---

## 3. Resetting Users

If you're using our User Attributes feature, you can easily disconnect a user from the device when they log out. This will prevent our system from sending pushes to that device if you attempt to send a targetted push notification to the user who used to be logged in on it. You can do this by calling our `resetUser:` function:

```objc
[Taplytics resetUser:^{
  // Finished User Reset
}];
```
    