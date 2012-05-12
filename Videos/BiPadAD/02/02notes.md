### 第二章 编写第一个 Application - Hello World


#### 学习内容

  * 使用 Xcode 创建我们的第一个 iPad 应用程序
  * 使用 Interface Builder 为 iPad 程序设计用户界面（UI）
  * 通过写一些代码，让程序可以根据设备的方向去调整内容的显示位置
  * 为应用程序添加 icon

#### 使用 Interface Builder 

xib 文件 - xml 格式的扩展，用于 iOS 设备的界面绘制。可以使用文本编辑器修改，也可以使用 Interface Builder 修改。

xcode 的个版本之间调用 Interface Builder 的方式稍有不同，在 4.2 版本中，界面配置文件的扩展名为 **storyboard**，不再是原先的 xib 扩展名。

#### 视图方向控制
iOS 应用程序是否可以根据设备朝向的变化而变化，是由下面的代码进行设置的：

    - (BOOL)shouldAutorotateToInterfaceOrientation:(UIInterfaceOrientation)interfaceOrientation
	{
	    // Return YES for supported orientations
	    return YES;
	}

这段代码位于 ViewController.m 文件中。

试着修改为下面的内容：

	- (BOOL)shouldAutorotateToInterfaceOrientation:(UIInterfaceOrientation)interfaceOrientation
	{
	    // Return YES for supported orientations
	    // return YES;
	    return (interfaceOrientation == UIInterfaceOrientationPortrait ||
		    interfaceOrientation == UIInterfaceOrientationLandscapeLeft);
	}

当屏幕垂直放置时，系统会调整 view ，当 home 键位于左侧时，系统也会对 view 进行调整。

#### View 的重置
实际应用中，我们需要空间大小随着屏幕放置位置的不同而发生改变，从而提供更好的用户体验。这一点可以在 Interface Builder 中通过工具完成设置。


#### 编写代码

#### 自定义 Application Icon
要求

    1. 72x72 - iPad 主界面需要
    2. 512x512 - 商店需要
    3. 48x48 - iPad 设置界面需要
