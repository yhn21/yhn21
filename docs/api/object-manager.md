# Object Manager

> 所有函数在使用时将以 `ni.objectmanager` 作为前缀.

---

## contains

参数:

- **object** `token|guid|name`

返回值: `boolean`

如果传递的值在对象管理器表内（该对象在你周围）,则返回真或假.

```lua
if ni.objectmanager.contains("巫妖王") then
	--巫妖王在我的范围内
end
```

## objectGUID

参数:

- **object** `token|guid|name`

返回值: `string`

只要对象在对象管理器表中,就返回传递值的对象GUID.

```lua
local lich_king = ni.objectmanager.objectGUID("巫妖王");
if lich_king ~= nil then
	--巫妖王在我的范围内,现在我们有了他的GUID,可以在其他函数中使用
end
```

---

> 对象管理器还提供了一组函数和特殊方式,为lua提供了一种面向对象类型的编程.访问此功能的所有方式都是通过 `ni.objects` . 函数、变量和示例如下:

## guid

类型:

- **variable**

返回值: `string`

这是返回已访问对象GUID的变量.

```lua
local tar = ni.objects["target"];
if tar:exists() then
	print(tar.guid) --将打印目标的GUID
end
```

## name

类型:

- **variable**

返回值: `string`

这是返回已访问对象名称的变量.

```lua
local tar = ni.objects["target"];
if tar:exists() then
	print(tar.name) --将打印目标的名称
end
```

## type

类型:

- **variable**

返回值: `number`

这是返回已访问对象类型的变量.

```lua
local tar = ni.objects["target"];
if tar:exists() then
	if tar.type == 3 then
		--对象是一个单位
	elseif tar.type == 4 then
		--对象是一个玩家
	elseif tar.type == 5 then
		--对象是一个游戏对象
	elseif tar.type == 6 then
		--对象是一个动态对象
	end
end
```

## exists

类型:

- **function**

参数:

返回值: `boolean`

如果对象存在可以被选中且可以攻击,则返回 true 或 false.

```lua
local tar = ni.objects["focus"];
if tar:exists() then
	--焦点对象存在
end
```

## info

类型:

- **function**

参数:

返回值: `multi-ret`

返回有关对象的详细信息.

```lua
local tar = ni.objects["focus"];
if tar:exists() then
	local x, y, z, facing, type, target, height = tar:info()
	if target ~= 0 then
		--我们得到了焦点对象的目标GUID
	end
end
```

## hp

类型:

- **function**

参数:

返回值: `number`

返回对象的健康百分比.

```lua
local tar = ni.objects["The Lich King"];
if tar:exists() and tar:hp() < 20 then
	--对象的生命值低于20%
end
```

## power

类型:

- **function**

参数:

- **type** `string` _可选参数_

返回值: `number`

返回对象当前能量的百分比（例如法力、能量、集中等）.

```lua
local tar = ni.objects["target"];
if tar:exists() and tar:power("mana") >= 80 then
	--目标的法力值达到或超过了80%
end
```

## powermax

类型:

- **function**

参数:

- **type** `string` _可选参数_

返回值: `number`

返回对象能量的最大值（例如法力值、能量值、集中值等）.

```lua
local tar = ni.objects["target"];
if tar:exists() and tar:powermax("mana") >= 20000 then
	--目标的法力值达到或超过了20000
end
```

## unit

类型:

- **function**

参数:

返回值: `boolean`

返回真（true）或假（false）,判断对象是否是一个单位.

```lua
local tar = ni.objects["target"];
if tar:exists() and tar:unit() then
	--对象是一个单位.
end
```

## player

类型:

- **function**

参数:

返回值: `boolean`

如果对象是玩家,则返回真（true）或假（false）.

```lua
local tar = ni.objects["target"];
if tar:exists() and tar:player() then
	--对象是一个玩家.
end
```

## canattack

类型:

- **function**

参数:

- **string** `token|guid` _可选参数_

返回值: `boolean`

如果对象可以攻击指定的目标（或者如果未指定,则为玩家）,则返回真（true）或假（false）.

```lua
local tar = ni.objects["target"];
if tar:exists() and tar:canattack() then
	--对象可以攻击玩家.
end
```

## canassist

类型:

- **function**

参数:

- **string** `token|guid` _可选参数_

返回值: `boolean`

如果对象可以协助指定的目标,或者如果未指定则默认协助玩家,则返回真（true）或假（false）.

```lua
local tar = ni.objects["target"];
if tar:exists() and tar:canassist() then
	--对象可以协助玩家（它们是友好的）.
end
```

## los

类型:

- **function**

参数:

- **string** `token|guid` _可选参数_

返回值: `boolean`

如果对象与指定的目标之间存在视线,或者如果未指定则默认与玩家之间存在视线,则返回真（true）或假（false）.

```lua
local tar = ni.objects["target"];
if tar:exists() and tar:los() then
	--对象与玩家之间存在视线.
end
```

## cast

类型:

- **function**

参数:

- **string or number** `name|id`

返回值: `void`

函数用于对对象施放一个法术.

```lua
local tar = ni.objects["The Lich King"];
if tar:exists() and tar:los() then
	tar:cast("火球术");
	--对对象施放火球术
end
```

## castat

类型:

- **function**

参数:

- **string or number** `name|id`

返回值: `void`

如果对象处于视线内,就在对象所在位置施放一个法术的功能.

```lua
local tar = ni.objects["The Lich King"];
if tar:exists() then
	tar:cast("暴风雪");
	--在对象正下方施放暴风雪
end
```

## combat

类型:

- **function**

参数:

返回值: `boolean`

如果对象处于战斗状态,则返回真（true）,否则返回假（false）.

```lua
local tar = ni.objects["The Lich King"];
if tar:exists() and tar:combat() then
	--对象处于战斗状态.
end
```

## isbehind

类型:

- **function**

参数:

- **target** `token|guid` _可选参数_
- **reverse** `boolean` _可选参数_

返回值: `boolean`

返回布尔值,表明对象是否位于指定标记之后,如果没有指定标记则默认为玩家.如果参数 `reverse` 被设置为真（true）,则方向相反（即玩家位于对象之后）.

```lua
local tar = ni.objects["target"];
if tar:exists() then
	if tar:isbehind("player", true) then
		--玩家在对象背后
	end
	if tar:isbehind() then
		--玩家在对象背后
	end
end
```

## isfacing

类型:

- **function**

参数:

- **target** `token|guid` _可选参数_
- **reverse** `boolean` _可选参数_

返回值: `boolean`

返回布尔值,指示对象是否面向指定的标记对象,如果未指定则默认为玩家.如果参数 `reverse` 被设置为真（true）,则意味着相反的方向（即玩家面向对象）.

```lua
local tar = ni.objects["target"];
if tar:exists() then
	if tar:isfacing("player", true) then
		--玩家面向对象
	end
	if tar:isfacing() then
		--对象面向玩家
	end
end
```

## distance

类型:

- **function**

参数:

- **string** `token|guid` _可选参数_

返回值: `number`

返回对象与指定标记的距离,如果未指定标记则默认与玩家的距离.

```lua
local tar = ni.objects["target"];
if tar:exists() and tar:distance() < 3 then
	--对象与玩家的距离在3码以内.
end
```

## range

类型:

- **function**

参数:

- **string** `token|guid` _可选参数_

返回值: `boolean`

返回布尔值,判断对象是否在40码以内相对于指定的标记,若未指定则默认相对于玩家.

```lua
local tar = ni.objects["target"];
if tar:exists() and tar:range() then
	--对象与玩家的距离在40码以内.
end
```

## creator

类型:

- **function**

参数:

返回值: `string`

返回对象创建者的GUID（全局唯一标识符）,如果对象有创建者的话.

```lua
local tar = ni.objects["target"];
if tar:exists() then
	local creator = tar:creator();
	if creator then
		--对象有创建者,现在我们获取了他们的GUID
	end
end
```

## target

类型:

- **function**

参数:

返回值: `string`

返回对象目标的GUID（全局唯一标识符）,如果对象有目标的话；否则返回"0x0000000000000000".

```lua
local tar = ni.objects["target"];
if tar:exists() then
	local target = tar:target();
	if UnitExists(target) then
		--对象有一个目标,现在我们有了它们的GUID
	end
end
```

## location

类型:

- **function**

参数:

返回值: `table`

返回一个包含对象位置及其朝向的表.

```lua
local tar = ni.objects["target"];
if tar:exists() then
	local location = tar:location();
	--使用对象的location.x, location.y, location.z和location.r来做一些事情
end
```

---

> 在钓鱼脚本中的迭代对象的另一个例子可以是像下面这样.通过这种方式迭代,你可以同样访问所有上面列出的变量和函数.示例如下:

```lua
local playerguid = UnitGUID("player");
for k, v in pairs(ni.objects) do
	if type(k) ~= "function" and (type(k) == "string" and type(v) == "table") then
		if v.name == "Fishing Bobber" then
			local creator = v:creator();
			if creator == playerguid then
				local ptr = ni.memory.objectpointer(v.guid);
				if ptr then
					local result = ni.memory.read("byte", ptr, offset);
					if result == 1 then
						ni.player.interact(v.guid);
						return true;
					end
				end
			end 
		end
	end
end
```