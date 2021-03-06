# 营销

## 简介

### 什么是 MaxLeap Marketing 服务

Marketing 服务是 MaxLeap 提供的营销和信息发布功能。目前提供两种 Marketing 形式：Push Notification和 In-App Message.您可以通过推送消息方式向指定人群推送消息，也可以通过 In-App Message，在应用内向有某种行为的用户显示特定内容。您还可以在消息中设置用户点击后的目标。消息的创建，设置和发送均在 Console 中完成。

### 为何需要 MaxLeap Marketing 服务

结合  MaxLeap 分析服务提供的分析数据，以及 MaxLeap Users 服务提供的 Segment，您可以高效地制定营销策略，并且通过 Marketing 服务实施您的策略。MaxLeap Marketing 服务的优势在于：


* **提高转化率：**随时向用户发布营销活动，维持用户活跃度并提高转化率
* **保障用户体验：**选择向指定 Segment 发送消息，更具有针对性
* **动态内容管理：**Push Notification 和 In-App Message 中的内容均在 Console 中设置，用户所见内容可实时更新

## 应用内消息

默认情况下，Marketing 功能处于关闭状态，不会接收消息。启用这个功能很简单，只需要 `[MLMarketingManager enable]` 一行代码，如下：

```
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
	[MaxLeap setApplicationId:@"your_application_id" clientKey:@"yout_client_key"];
	[MLMarketingManager enable];
}
```

此时，应用就会接收应用内消息，但是还不能接收和统计远程推送。

## 推送消息

推送消息帮助您迅速地将消息展示给大量的用户。发送推送消息后，无论用户是否打开应用，都将在状态栏看见它。您可以在Console中自定义发送消息的内容，并且传递若干参数(键值对)至客户端。用户点击推送消息后，应用会根据参数决定目标界面。

###配置

首先要申请远程推送证书。

在 `appDelegate.m` 中，您可以使用下面的代码开启远程推送

```
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    // Override point for customization after application launch.
    
    [MaxLeap setApplicationId:@"5552f51660b2056aa87dd9e0" clientKey:@"c3JscE50TWNnVzg4SkZlUnFsc3E2QQ"];
    
    [self registerRemoteNotifications];
    
    [MLMarketingManager enable];
    // 统计推送点击事件
    [MLMarketingManager handlePushNotificationOpened:launchOptions];
    
    return YES;
}

- (void)registerRemoteNotifications {
    if ([[UIApplication sharedApplication] respondsToSelector:@selector(registerUserNotificationSettings:)]) {
        UIUserNotificationSettings *pushsettings = [UIUserNotificationSettings settingsForTypes:UIUserNotificationTypeBadge|UIUserNotificationTypeSound|UIUserNotificationTypeAlert categories:nil];
        [[UIApplication sharedApplication] registerUserNotificationSettings:pushsettings];
    } else {
        [[UIApplication sharedApplication] registerForRemoteNotificationTypes:UIRemoteNotificationTypeBadge|UIRemoteNotificationTypeSound|UIRemoteNotificationTypeAlert];
    }
}

- (void)application:(UIApplication *)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData *)deviceToken {
    // 将 device token 保存到 MaxLeap 服务器，以便服务器向本设备发送远程推送
    [[MLInstallation currentInstallation] setDeviceTokenFromData:deviceToken];
    [[MLInstallation currentInstallation] saveInBackgroundWithBlock:nil];
}

- (void)application:(UIApplication *)application didRegisterUserNotificationSettings:(UIUserNotificationSettings *)notificationSettings {
    [application registerForRemoteNotifications];
}

- (void)application:(UIApplication *)application didReceiveRemoteNotification:(nonnull NSDictionary *)userInfo fetchCompletionHandler:(nonnull void (^)(UIBackgroundFetchResult))completionHandler {
    completionHandler(UIBackgroundFetchResultNoData);
}
```

### 统计推送点击率

在 `application:didFinishLaunchingWithOptions:` 方法中加入以下代码：

	```
	[MLMarketingManager handlePushNotificationOpened:launchOptions];
	```

