# iOS 接Google登录流程

[TOC]



## 准备工作

- 去到Google开发者网站注册一个app,[点击跳转](https://developers.google.com/mobile/add?platform=ios)
- 注册app之后，记得将google登录的权限打开
- 将GoogleService-Info.plist文件下载下来，放入工程根目录



## cocoapods导入SDK

```swift
pod 'GoogleSignIn'
```

### 检查依赖库

- LocalAuthentication.framework
- SafariServices.framework
- SystemConfiguration.framework

以上三个依赖库没有的话，自行添加



## 配置URLType

![image-20191224151156110](https://img-blog.csdnimg.cn/20191224154217252.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzM1NjEyOTI5,size_16,color_FFFFFF,t_70)

**URL Schemes是颠倒的Client_ID,Client_ID可以从GoogleService-Info.plist中获取到**



## 初始化

**在appdelegate中，添加如下截图方法**

![image-20191224151632521](https://img-blog.csdnimg.cn/20191224154249987.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzM1NjEyOTI5,size_16,color_FFFFFF,t_70)

**如下截图，设置clientID可以写在任意位置，剩余两个方法必须写在需要Google登录的Controller**

![image-20191224151537139](https://img-blog.csdnimg.cn/2019122415432584.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzM1NjEyOTI5,size_16,color_FFFFFF,t_70)



## 调起Google登录的方法

```swift
GIDSignIn.sharedInstance()?.signIn()
```



## 登录回调方法

```swift
func sign(_ signIn: GIDSignIn!, didSignInFor user: GIDGoogleUser!, withError error: Error!) {
        if (error == nil) {
          // 登录成功
        } eles {
          // 登录失败或取消登录
        }
            
}
```

