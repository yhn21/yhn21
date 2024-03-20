# Spell

> 所有使用的函数将以 `ni.spell` 作为前缀 .

---

## available

参数:

- **spell** `id|string`
- **stutter** `boolean` _默认值: true_

返回值: `boolean`

检查指定的法术是否可用.包括以下检查:

- [`ni.spell.gcd`](api/spell.md#gcd)
- [`ni.vars.combar.casting`](api/vars.md)
- [`ni.spell.cd`](api/spell.md#cd)
- [`ni.stopcastingtracker.shouldstop`](api/stopcasting.md)
- [`ni.player.powerraw`](api/player.md)
- [`ni.player.hpraw`](api/player.md)

!> [`ni.spell.available`](api/spell.md#available) 与 [`ni.spell.valid`](api/spell.md#valid)不同.

```lua
if ni.spell.available("恐惧") then
  -- 恐惧通过了检查,处于可用状态
end
```

## cast

参数:

- **spell** `id|string`
- **target** `token|guid`

返回值: `void`

施放指定的法术.如果提供了目标,将对那个目标施放；否则,法术将对自己施放.

```lua
ni.spell.cast("恐惧", "target")
```

## delaycast

参数:

- **spell** `id|string`
- **target** `token|guid`
- **delay** `number` _可选参数_

返回值: `boolean`

就像普通的施法一样,然而你可以指定延迟时间,如果自上次施法以来的时间超过了延迟,它将施放法术并返回true.如果时间小于延迟,函数将返回false.

```lua
if ni.spell.delaycast("恐惧", "target", 1.5) then
	--自从上次施放恐惧以来已经超过1.5秒了,所以它施放了
else
	--法术没有施放,因为自上次施放以来还不到1.5秒
end
--其它用法就像普通施法一样,只是为了确保如果在延迟时间内不施放
if true then
	ni.spell.delaycast("恐惧", "target", 1.5)
end
```


## castat

参数:

- **spell** `id|string`
- **target** `token|guid|mouse`
- **offset** `number`

返回值: `void`

施放需要点击地面的指定法术（例如,死亡凋零、火焰之雨、暴风雪）.

```lua
ni.spell.castat("死亡凋零", "target")
```

## castatqueue

参数:

- **spell** `id|string`
- **target** `token|guid|mouse`

返回值: `void`

将指定的法术加入队列,在其可用时自动对地面施放.

```lua
ni.spell.castatqueue("死亡凋零", "target")
```

## castqueue

参数:

- **spell** `id|string`
- **target** `token|guid`

返回值: `void`

将指定法术加入队列,一旦它可用就立即施放.这种队列机制常用于确保在法术冷却完毕的一瞬间立刻施放,从而最大化效率和输出.

```lua
ni.spell.castqueue("恐惧", "target")
```

## castspells

参数:

- **spell** `id|string`
- **target** `token|guid`

返回值: `void`

施放由竖线(`|`)分隔的指定法术.如果指定了目标,则会对那个目标施放法术；否则,法术会施放在自身.如果多个法术触发全局冷却时间,这种方法则无法工作.

```lua
ni.spell.castspells("烈焰震级|风剪", "target")
```

## casttime

参数:

- **spell** `id|string`

返回值: `number`

计算指定法术的施放时间.

```lua
local casttime = ni.spell.casttime("暗影箭") 
```

## cd

参数:

- **spell** `id|string`

返回值: `number`

计算指定法术的冷却时间.如果法术没有在冷却中,则返回0.

```lua
if not ni.spell.cd("寒冰屏障") then
  -- 寒冰屏障不在冷却中
end
```

## gcd

参数:

返回值: `boolean`

检查是否触发了全局冷却时间（GCD）.

```lua
if not ni.spell.gcd() then
  -- 全局冷却时间未激活,可以采取行动
end
```

## id

参数:

- **spellname** `string`

返回值: `number|nil`

将法术名称转换为法术ID.如果法术不存在则返回nil.

```lua
local spellid = ni.spell.id("暗影烈焰") -- 返回值61290
```

## isinstant

参数:

- **spell** `string|id`

返回值: `boolean`

检查传入的法术是否为瞬发法术.

```lua
if ni.spell.isinstant("生命分流") then
  -- 生命分流是瞬发法术
end
```

## stopcasting

参数:

返回值: `void`

停止施法读条.

```lua
ni.spell.stopcasting()
```

## stopchanneling

参数:

返回值: `void`

停止引导读条.

```lua
ni.spell.stopchanneling()
```


## shouldinterrupt

参数：

- **target** `token|guid`
- **shou** `number`

返回值: `boolean`

检查单位的施法进度.

```lua
if  ni.spell.shouldinterrupt("target", 35) then
-- 目标施法进度大于等于35%的时候返回true,否则返回false
end
```


## valid

参数:

- **target** `token|guid`
- **spell** `id|string`
- **facing（面向目标）** `boolean` _默认值：假_
- **los（是否有视野）** `boolean` _默认值：假_
- **friendly（是否友善）** `boolean` _默认值：假_

返回值: `boolean`

此函数确保一个法术能够在特定目标上施放.它包括了如下的检查:

!> [`ni.spell.valid`](api/spell.md#valid) is not the same as [`ni.spell.available`](api/spell.md#available).
- [`ni.unit.exists`](api/unit.md#exists)
- [`ni.player.los`](api/player.md#los)
- [`ni.player.isfacing`](api/player.md#isfacing)
- `IsSpellInRange`

```lua
if ni.spell.valid("target","恐惧",true,true,false) then
  -- 玩家当前面向目标,对目标有视野,并且不判断目标是否是友善的,可以施放恐惧
end
```
