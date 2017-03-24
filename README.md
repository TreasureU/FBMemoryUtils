#介绍：
======
	FBMemoryUtils是FBMemoryProfiles的静态库，打出来的包是一个framework，mach-o Type是Static Library。
	官方库[FBMemoryProfiles](https://github.com/facebook/FBMemoryProfiler)地址。


#内容：
======
	内含FBMemoryProfiles、FBAllocationTracker、FBRetainCycleDetector三个库的代码
	FBAllocationTracker：是一个对象生成与生存期检测工具
	FBRetainCycleDetector：是一个循环引用监测工具
	FBMemoryProfiles：对上面两种功能进行了集合，并且提供可视化界面、插件功能以及筛选过滤功能。

#使用说明：
========
	1.选中CrossGenerate target，然后直接Build即可。（Debug/Release模式将会决定打包配置，并且取决于CrossGenerate Scheme的配置）
	2.Build完成后，会自动合成集合库，并且open集合库所在的文件夹
	3.将打出的包赋值到工程目录合适的地方，并引入工程
	4.在Link Binary With Libraries中添加：UIKit、CoreGraphics、Foundation
	4.在工程中需要使用时，在该文件中“#import <FBMemoryUtils/FBMemoryUtils>”即可。

#代码内使用简单示例：
==================
	1.建议在main中启动对象生成追踪
```Objective-C
	[FBAssociationManager hook];
	[[FBAllocationTrackerManager sharedManager] startTrackingAllocations];
	[[FBAllocationTrackerManager sharedManager] enableGenerations];
```


	2.建议在AppDelegate中启动内存分析：
```Objective-C
	self.memoryProfiler = [[FBMemoryProfiler alloc] init];
	[self.memoryProfiler enable];
```