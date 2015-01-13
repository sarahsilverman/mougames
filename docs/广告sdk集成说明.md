
# 广告SDK集成说明

*Version 0.1.4*

### 使用framework的方法
- 把`AdsPackage.framework` 和 `__vungle.db`拽到您的项目里

	![](./screenshot_2.png =150x)
	
- 进入项目的`Build Settings`, 设置`Other Linker Flags`为`-ObjC`

	![](./screenshot_3.png =400x)
	 
- 进入项目的`Build Phase`, 在顶部菜单选择`Edtior`->`Add Build Phase`->`Add Copy Files Bild Phase`; 在 `Copy Files`栏下方, 在`Destination`选择`Frameworks`, 然后添加`AdsPackage.framework`

	![](./screenshot_4.png =500x)	
	
- 确认项目的`Build Phase`里的`Copy Bundle Resources`栏目里有`appids.json`和`__vungle.db`文件

	![](./screenshot_5.png =400x)
	
- 在项目需要的头文件里添加header: `#import <AdsPackage/AdsPackage.h>`
- 在项目`AppDelegate.m`文件的`- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {}`函数里, 添加:

[[AdsPackage sharedInstance] startWithPath:[[NSBundle mainBundle] pathForResource:@"appids" ofType:@"json"] viewController:self.window.rootViewController];

- 任何地方如果需要进行Debug, 调用`[[AdsPackage sharedInstance] addAdViewPublic:@"2013"]`
- 本framework目前只支持`armv7s`, `armv7`, 和`arm64`（真机测试）, 不支持`i386` and `x86_64`（）模拟器调试）
 
	![](./screenshot_6.png =400x)



