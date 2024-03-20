# Player

> 使用时,所有函数都将以 `ni.player` 为前缀.

除了下面列出的函数,还可以使用 `ni.player` 作为简写,调用 [Unit](api/unit.md) 中的任何函数,并将 `player` 作为第一个参数传递.


```lua
ni.player.buff("王者祝福") -- 等同于 ni.unit.buff("player", "王者祝福")
ni.player.hp() -- 等同于 ni.unit.hp("player")
```

---
## cancelbuff

参数:

- **id** `id`

取消玩家身上的特定增益效果.

```lua
if ni.player.buff(48443) then
--如果玩家有id48443的增益效果
	ni.player.cancelbuff(48443)
  --取消玩家id48443的增益效果
end
```

## clickat

参数:

- **unit** `token|guid|x,y,z|mouse`

返回值: `void`

在特定位置点击.

```lua
ni.player.clickat("target") --在目标的 x/y/z 位置点击
ni.player.clickat("mouse") --在鼠标当前位置点击
```

## checkslots

返回值: `number`

检查玩家背包中的空闲槽位
```lua
if ni.player.checkslots() < 2 then
	-- 玩家的空闲槽位少于2个
end
```

## hasglyph

参数:

- **glyph** `id`

返回值: `boolean`

检查玩家是否装备了特定的雕文.

```lua
if ni.player.hasglyphWotlk(42455) then
  -- 玩家装备了id42455的雕文
end
```

## hasitem

参数:

- **item** `id`

返回值: `boolean`

检查玩家是否拥有特定的物品.

```lua
if ni.player.hasitem(51378) then
  -- 玩家拥有物品id51378的物品
end
```

## hasitemequipped

参数:

- **item** `id`

返回值: `boolean`

检查玩家是否装备了特定的物品.

```lua
if ni.player.hasitemequipped(51378) then
  -- 玩家已装备物品id51378的物品
end
```

## hassetequiped

参数:

- **table** `id`
- **pieces** `number`


返回值: `boolean`

检查玩家是否装备了特定的套装.

```lua
local t8 = {46122, 46121, 46120, 46119, 46118, 45339, 45338, 45337, 45336, 45335};

if ni.player.hassetequiped(t8, 4) then
  -- 玩家已装备4件T8套装
end
```

## interact

参数:

- **unit** `token|guid`

返回值: `void`

与指定单位进行交互（例如,与NPC打开对话框,拾取容器）.

```lua
ni.player.interact("target")
```

## itemicon

- **item** `id`
- **width** `number`
- **height** `number`

返回值: `string`

在图形用户界面（GUI）中绘制物品图标.

```lua
	{ type = "entry", text = ni.player.itemicon(57191, 22, 22).." Heal Potion", tooltip = "Use Heal Potions (if you have) when player |cff00D700HP|r < %.",  enabled = true, value = 30, min = 20, max = 60, step = 1, width = 40, key = "healpotionuse" },
```

## itemcd

参数:

- **slot** `id`

返回值: `number`

检查一个特定的库存物品是否处于冷却状态,并返回剩余的冷却时间.

```lua
if ni.player.itemcd(41119) > 0 then
  -- 物品id41119的物品正在冷却中
end
```

## itemready

参数:

- **slot** `id`

返回值: `boolean`

检查一个特定的库存物品是否已经准备就绪.这意味着玩家拥有该物品,它不处于冷却状态,并且可以被使用.

```lua
if ni.player.itemready(41119) then
  -- 玩家拥有物品id41119的物品并且能够使用它
end
```

## lookat

参数:

- **unit** `token|guid`
- **inv** `boolean` _default: false_

返回值: `void`

朝向单位的方向看.可以通过将 `true` 作为第二个参数传递来实现反向朝向.

```lua
ni.player.lookat("target")
ni.player.lookat("target", true) --朝向与目标相反的方向
```

## moveto

参数:

- **unit** `token|guid|x,y,z`

返回值: `void`

将玩家移动到特定目标或坐标.

```lua
ni.player.moveto("target")
```

## petcd

参数:

- **spell** `id|name`

返回值: `number`

检查宠物技能是否处于冷却时间中,并返回剩余时间.

```lua
if ni.player.petcd("爪击") > 0 then
  -- 爪击处于冷却中
end
```

## runtext

参数:

- **text** `string`

返回值: `void`

将传入的文本作为宏运行.

```lua
ni.player.runtext("/s Hello") -- 将“Hello”写入说话频道.
```

## slotcastable

参数:

- **slot** `id`

返回值: `boolean`

检查玩家的装备是否是一个可以主动施放属性,比如工程手套加速附魔,主动触发的饰品等.

```lua
if ni.player.slotcastable(10) then
  -- 玩家的手套是一个可以主动施放的装备
end
```

## slotcd

参数:

- **slot** `id`

返回值: `number`

检查玩家的装备主动施放效果是否处于冷却当中.

```lua
if ni.player.slotcd(10) > 0 then
  -- 手套的使用效果处于冷却中
end

if ni.player.slotcd(10) == 0 then
  -- 手套的使用效果处于冷却完毕
end
```

## slotusable

参数:

- **slot** `id`

返回值: `boolean`

检查玩家的装备是否是主动施放的装备,并且可以使用了.

```lua
if ni.player.slotusable(10) then
  -- 手套是主动施放的装备且准备好可以使用了
end
```

## stopmoving

参数:

返回值: `void`

使玩家停止所有移动.

```lua
ni.player.stopmoving()
```

## target

参数:

- **unit** `token|guid`

返回值: `void`

将指定的单位设置为玩家的目标.

```lua
ni.player.target("炸弹机器人")
-- 将炸弹机器人设为玩家当前的目标
```

## useinventoryitem

参数:

- **item** `id`

返回值: `void`

使用装备的物品.

```lua
ni.player.useinventoryitem(10) -- 使用手套
ni.player.useinventoryitem(13) -- 使用饰品（上）
```

## useitem

参数:

- **item** `id|name`
- **target** `token|guid`

返回值: `void`

使用库存中的物品.如果指定了单位,则将物品使用在它身上.

```lua
ni.player.useitem(36895) -- 使用灵魂石
ni.player.useitem(36895, "focus") -- 给焦点目标使用灵魂石
```

## movingfor

参数:

- **duration** `number`

返回值: `boolean`

如果玩家已经移动了指定的时长,则返回true或false.

```lua
if ni.player.movingfor(2) then
	--玩家已经移动了至少2秒钟
end
```

## getmovingtime

参数:

返回值: `number`

返回玩家已经移动的时间.

```lua
if ni.player.getmovingtime() > 60 then
	--玩家已经移动了超过60秒
end
```