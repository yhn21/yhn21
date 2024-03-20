# 快速开始

如果你已经下载了NI插件 [NI泥多灰汉化版下载地址](https://gitee.com/smallzyc/nifi0.0.6.2/raw/master/NI.v0.0.62.zip) 这份入门指南将帮助你快速上手.

让我们从配置文件的位置开始.

```
addon
└───Core
└───Settings
└───Rotations
│	└───Data
│	└───Warlock
```

我们感兴趣的两个文件夹是 `Data` 和以我们角色的职业命名的文件夹.在这份指南中,我们将为 `Warlock（术士）`创建一个简单的配置文件.这意味着我们将关注这两个文件夹.

我们的配置文件需要有一个名字 - 对于这份指南,我们将其命名为 `Warlock_Example` .

请按照以下步骤操作:

#### 1. 在文件夹 addon/Rotations/Warlock 内创建一个名为 `Warlock_Example.lua` 的文件.你的文件夹应该看起来像这样 :

```
addon
└───Core
└───Settings
└───Rotations
│	└───Data
│	└───Warlock
│	│	└───Warlock_Example.lua
```

2. 创建文件后,使用你最喜欢的文本编辑器打开它. 

#### 3. 复制并粘贴以下样板代码:

```lua
local queue = {
	"Print Hello"
};

local abilities = {
	["Print Hello"] = function()
		print("Hello")
	end
};

ni.bootstrap.profile("Warlock_Example", queue, abilities)
```

!> 确保文件的名称与传递给 `ni.bootstrap.profile` 的名称匹配

这就是 **ni** 运行配置文件所需的全部.按 `F1` 看看控制台是否打印出了 `Hello` .

#### 4. 如果我们想要有一个动态队列,可以实时变化的多个队列,我们也可以传递一个 `function` .

```lua
local ishelloprinted = false;

local queue = {
	"Print Hello"
};

local queue2 = {
	"Print Hello World"
};

local abilities = {
	["Print Hello"] = function()
		ishelloprinted = true
		print("Hello")
	end,
	["Print Hello World"] = function()
		ishelloprinted = false
		print("Hello World")
	end
};

local dynamicqueue = function()
	if ishelloprinted then
		return queue
	end

	return queue2
end;

ni.bootstrap.profile("Warlock_Example", dynamicqueue, abilities)
```
!> 此示例仅在不使用 `Data` 文件的情况下工作.

!> 只能使用一种方式设置优先队列（静态或动态）.

#### 5. 如果我们有一些通用的函数或变量想在多个配置文件之间共享 - 我们可以通过在 `Data` 文件夹中创建 Lua 文件来实现.让我们创建 `Data_Example.lua` .

```
addon
└───Core
└───Settings
└───Rotations
│	└───Data
│	│	└───Data_Example.lua
│	└───Warlock
│	│	└───Warlock_Example.lua
```

> 你可以随意命名 **Warlock** 和 **Data** 中的文件,它们不需要遵循任何约定.

#### 6. 在 Data 和 Profile 文件之间传递变量和函数可以通过两种方式完成:

- 通过声明和分配全局变量（不推荐）
- 通过使用 `data` 并拥有一个新的唯一命名空间（`table`）

让我们使用第二种方式,并向 `Rotations/Data/Data_Example.lua` 中添加以下内容.

```lua
local data = {};

data.example = function()
	return select(2, UnitClass("player"));
end;

return data;
```

#### 7. 加载 Data 文件可以通过创建一个包含文件名字符串的表,并将该表作为第四个参数传递给 `ni.bootstrap.rotation` 来完成.

```lua
local data = ni.utils.require("Data_Example");

local queue = {
	"Print Hello"
};

local queue2 = {
	"Print Hello World"
};

local abilities = {
	["Print Hello"] = function()
		if data.example() == "WARLOCK" then
			print("Hello")
			return true;
		end
	end,
	["Print Hello World"] = function()
		if data.example() ~= "WARLOCK" then
			print("Hello World")
			return true;
		end
	end
};

local dynamicqueue = function()
	if ni.data.example.ishelloprinted then
		return queue
	end

	return queue2
end;

ni.bootstrap.rotation("Warlock_Example", dynamicqueue, abilities, data)
```

#### 8. 创建配置文件 GUI:
请点击这里查看示例 [here](https://github.com/darhanger/ni/blob/main/addon/Rotations/Generic/GUIExample.lua)