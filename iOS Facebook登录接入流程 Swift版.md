# Facebook登录流程

[toc]

## 准备工作

- Facebook后台创建应用
- 绑定bundleid
- 开启登录权限

## 使用cocoapods安装SDK

```swift
pod 'FBSDKLoginKit'
```



## infoPlist文件配置

- 绑定用

```swift

<key>CFBundleURLTypes</key>
<array>
<dict>
<key>CFBundleURLSchemes</key>
<array>
<string>fb[APP_ID]</string>
</array>
</dict>
</array>
<key>FacebookAppID</key>
<string>[APP_ID]</string>
<key>FacebookDisplayName</key>
<string>[APP_NAME]</string>
```

- 白名单跳转用

```swift

<key>LSApplicationQueriesSchemes</key>
<array>
<string>fbapi</string>
<string>fbapi20130214</string>
<string>fbapi20130410</string>
<string>fbapi20130702</string>
<string>fbapi20131010</string>
<string>fbapi20131219</string>
<string>fbapi20140410</string>
<string>fbapi20140116</string>
<string>fbapi20150313</string>
<string>fbapi20150629</string>
<string>fbapi20160328</string>
<string>fbauth</string>
<string>fb-messenger-share-api</string>
<string>fbauth2</string>
<string>fbshareextension</string>
</array>
```



## 启动代码

```swift

// Swift // AppDelegate.swift // 将 AppDelegate.swift 中的代码替换为以下代码。 
import UIKit 
import FBSDKCoreKit 
@UIApplicationMain 
class AppDelegate:UIResponder, UIApplicationDelegate {  
      func application( _ application: UIApplication, didFinishLaunchingWithOptions 							launchOptions: [UIApplication.LaunchOptionsKey: Any]? ) -> Bool { 															ApplicationDelegate.shared.application(application, didFinishLaunchingWithOptions:launchOptions) 
                                                                                                                                                      			return true 
    	} 
  		func application( _ app:UIApplication, open url:URL, options:          [UIApplication.OpenURLOptionsKey :Any] = [:]) -> Bool {
        ApplicationDelegate.shared.application(app, open: url, sourceApplication: options[UIApplication.OpenURLOptionsKey.sourceApplication] as? String, annotation: options[UIApplication.OpenURLOptionsKey.annotation])
    }
}

    
```

## H5交互方法中调用登录

```swift
func newLogin() {
        LoginManager.init().logIn(permissions: ["public_profile"], from: self) { [weak self] (result, error) in
            self?.getUserInfoWithResult(result: result, error: error)
        }
        
    }

func getUserInfoWithResult(result: LoginManagerLoginResult?, error: Error?) {
        if error != nil {
            print("process error")
        } else if result?.isCancelled ?? false {
            print("cancelled")
        } else {
            print("logged in")
        }
    }
```

## 登录成功后，获取用户名和头像

```swift
NotificationCenter.default.addObserver(forName: NSNotification.Name.ProfileDidChange, object: nil, queue: OperationQueue.main) { (notification) in
            if Profile.current != nil {
                //获取头像
                let pic = FBProfilePictureView.init()
                //获取用户名
                Profile.loadCurrentProfile { (profile, error) in
                    if profile != nil {
                        let name = profile?.firstName
                    }
                }
            }
        }
```

## 

## 获取Token

```swift
//获取token
AccessToken.current?.tokenString
```

