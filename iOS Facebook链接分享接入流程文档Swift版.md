#iOS Facebook链接分享接入流程文档Swift版

#### 准备工作
* facebook 账号, 并申请注册为开发者 [开发者网站](https://developers.facebook.com/)打不开的用户请科学上网
* facebook 开发者网站创建自己的应用.
* iOS 开发者安装并使用cocoapods

#### iOS端 接入流程
* 给创建的工程添加pod

* 在Podflie文件中添加如下pod , 并安装	

	```swift
	pod 'FBSDKCoreKit'  
	pod 'FBSDKLoginKit'
	pod 'FBSDKShareKit'
	pod 'FBSDKPlacesKit'
	```
	
* 项目info.plist 文件里面的操作
	
	添加以下代码  ( your-app-id / your-app-name 指的是 Facebook开发者后台创建的应用 )
	
	```xaml
	<key>CFBundleURLTypes</key>
	<array>
	  <dict>
	    <key>CFBundleURLSchemes</key>
	    <array>
	      <string>fb{your-app-id}</string>
	    </array>
	  </dict>
	</array>
	<key>FacebookAppID</key>
	<string>{your-app-id}</string>
	<key>FacebookDisplayName</key>
	<string>{your-app-name}</string>
	<key>LSApplicationQueriesSchemes</key>
	<array>
	  <string>fbapi</string>
	  <string>fb-messenger-share-api</string>
	  <string>fbauth2</string>
	  <string>fbshareextension</string>
	</array>
	```
	
* Appdelegate里面的操作
	
	导入以下头文件

		import FBSDKCoreKit
	
	添加以下方法 ( 在已有方法中添加对应的Facebook代码 )

	``` swift 
	
	func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool { 
        
		ApplicationDelegate.shared.application(application, didFinishLaunchingWithOptions: launchOptions)
        
        return true
    }
    
    func application(_ app: UIApplication, open url: URL, options: [UIApplication.OpenURLOptionsKey : Any] = [:]) -> Bool {
        
        let handle = ApplicationDelegate.shared.application(app, open: url, options: options)
        
        return handle
    }
    
    func applicationDidBecomeActive(_ application: UIApplication) {
        AppEvents.activateApp()
    }
	```
	
* 需要使用分享的控制器里的操作
	
	导入以下头文件
	
		import FBSDKShareKit

	添加以下方法(方法的调用适开发者自身项目而定)
	
	``` swift
	  /// share the link to facebook
    /// - Parameters:
    ///   - url: URL for the content being shared.
    ///             This URL will be checked for all link meta tags for linking in platform specific ways.
    ///             See documentation for App Links (https://developers.facebook.com/docs/applinks/)
    ///   - quote: Some quote text of the link. If specified, the quote text will render with custom styling on top of the link.
    func shareLinkToFacebook(url: String!, quote: String?) {
  
        let content = ShareLinkContent.init()
        content.contentURL = URL.init(string: url) ?? URL.init(fileURLWithPath: "")
        content.quote = quote
  
        let dialog = ShareDialog.init(fromViewController: self, content: content, delegate: nil)
        dialog.show()
    }
        
	```
	

***注意: 以上只是个人一点总结, 定有不足之处. 同学们也可以参考 [官方接入文档](https://developers.facebook.com/docs/ios/getting-started/)***