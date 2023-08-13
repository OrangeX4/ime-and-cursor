<h1 align="center">光标和输入法（IME and Cursor）</h1>
<p align="center"><strong>令光标兼作中英文输入状态的指示器</strong></p>

*“要盲打，不要盲切盲输（切换输入法和输入中英文）。让打字时目光的自然注视点——光标，告诉你当前的输入语言是英文还是中文。”*

**光标和输入法**（**IME and Cursor**）是为[VSCode](https://code.visualstudio.com/)编写的一个小插件。它的功能和原理都非常简单，就是通过适时获取当前的输入语言，来相应地设置光标样式（默认英文输入状态对应普通的竖线型光标，中文输入状态对应块状光标，可设置）。

安装本插件后，为了能够及时响应输入语言的改变，需要您在使用vscode的过程中，使用本插件提供的快捷键（默认为`shift+space`，可设置）而不是系统层面的快捷键（如`shift+alt`）来进行输入语言的切换。

因为涉及到与系统的交互，本插件并不能保证“开箱即用”，很可能还需要您做一点额外工作。下面分系统加以说明。
## Windows系统：
### 安装英语语言包
如果您的系统未安装英语语言包（大概率，因为新近的windows中文版不再默认安装。可用鼠标左键点击底部任务栏右侧的输入法图标，查看弹出的列表中是否包含“英语(美国)”），则需要您手动安装一下。具体操作为：

打开 **设置** -> **时间和语言** ->**语言**（或**语言和区域**） ，找到“首选语言”栏，点击“添加语言”。

在打开的对话框中，找到“`English(United States)`”，选中然后点击下方按钮进入下一页。

如无特别需要，取消“可选语言功能”下的各复选项，然后点击“安装”按钮完成安装。


## Mac系统：

### 安装第三方输入法切换工具并完成本插件的相关设置

您可以使用任何能够获取输入法的key和使用key进行输入法切换的命令行工具。下面以[im-select](https://github.com/daipeihust/im-select)为例说明相关安装和配置工作：
#### 1. 安装 im-select（[安装说明](https://github.com/daipeihust/im-select/blob/master/README_CN.md)）
#### 2. 分别获取中文和英文输入法的key（可以简单理解为输入法的ID）
切换到英文输入法，并在终端中执行命令：

`/<path-to-im-select-installation>/im-select`

返回值即为您的英文输入法的key。

以同样的方法获取您使用的中文输入法的key。

#### 3. 对本插件进行设置

相关的设置项共有四个，分别是：

* `imeandcursor.ChineseIM`: 你的中文输入法的key
* `imeandcursor.EnglishIM`: 你的英文输入法的key
* `imeandcursor.obtainIMCmd`: 用于获取输入法的key的命令（需要使用绝对路径）
* `imeandcursor.switchIMCmd`: 用于切换输入法的命令（需要使用绝对路径，且将{im}作为切换的目标输入法ID的占位符）

下面是一个具体设置的参考样例：
```json
"imeandcursor.ChineseIM": "com.sogou.inputmethod.sogou.pinyin",
"imeandcursor.EnglishIM": "com.apple.keylayout.ABC",
"imeandcursor.obtainIMCmd": "/usr/local/bin/im-select",
"imeandcursor.switchIMCmd": "/usr/local/bin/im-select {im}"

```

## Linux系统：

Linux有许多命令行工具可以切换输入法，如ibus，xkb-switch等，可参考前面Mac系统的配置工作和[这里](https://github.com/daipeihust/im-select/blob/master/README_CN.md)的相关说明进行操作。


## 补充说明一：

> 本插件默认提供的输入语言切换快捷键`shift+space`，通常也被一些输入法用作“全角/半角”切换的快捷键，并且具有更高优先级。如果您发现安装了本插件并完成了前述配置工作后，在vscode中使用`shift+space`无法实现输入语言的切换，很可能是因为在您的输入法设置中勾选启用了“全角/半角”的快捷键，引发了冲突。这种情况建议您如无特别需要，取消对“全角/半角”快捷键的勾选。


## 补充说明二（仅针对Windows用户）：

> 对于window用户，安装了英语语言包后，本插件应该就可以正常使用了。但如有需要也可以参考前面关于Mac系统的说明，自己安装第三方输入法切换工具并完成相关设置（同时参考[这里](https://github.com/daipeihust/im-select/blob/master/README_CN.md)）。下面是Windows上本插件的一个参考配置样例：
```json
"imeandcursor.ChineseIM": "2052",
"imeandcursor.EnglishIM": "1033",
"imeandcursor.obtainIMCmd": "D:\\bin\\im-select.exe",
"imeandcursor.switchIMCmd": "D:\\bin\\im-select.exe {im}"

```


## 最后
本插件的想法源于作者以前玩Smalltalk时给Pharo做的内置输入法；技术实现则参考和借助了[VSCodeVim](https://github.com/VSCodeVim/Vim)和[im-select](https://github.com/daipeihust/im-select)，在此向它们的作者致以诚挚谢意！！
