#iOS Firebase埋点文档Swift版

#### 准备工作
* 没啥准备工作,让运营同学在后台创建项目和我们的工程关联起来就可以了
* 给运营同学提供 Bundle ID
* 具体准备工作可以看看[官方文档](https://firebase.google.cn/docs/ios/setup)

#### iOS端 接入流程

* 在Podflie文件中添加如下pod , 并安装(安装比较慢)

	```swift
	pod 'Firebase/Analytics'
	```
		
* Appdelegate里面的操作
	
	导入以下头文件

		import Firebase
		
	配置一个 FirebaseApp 共享实例（通常在应用的 application:didFinishLaunchingWithOptions: 方法中配置）：
	
	```
	FirebaseApp.configure()
	```
	
*   webView里面的操作

	导入以下头文件

		import Firebase
	
	实现如下交互方法

	```swift
	private func registerFirebaseEvent() {
        brige?.registerHandler("firebaseTrackEvent", handler: { (data, responseCallback) in
            if let event = data as? String {
                Analytics.logEvent(event, parameters: nil)
            }
        })
    }
	
	```

***注意: 以上只是个人一点总结, 定有不足之处. 同学们也可以参考 
[官方iOS入门接入文档](https://firebase.google.cn/docs/ios/setup)&
[官方iOS Analytics 文档](https://firebase.google.cn/docs/analytics/ios/start)***