# 治疗

> 下面使用的所有函数都要以 `ni.healing` 为前缀.

---

## debufftoblacklist

参数:

- **id：** `number`: 要添加到表里的负面效果的id.

这个表记录不需要被驱散的负面效果.

```lua
local bad = { 47867, 47813, 47864 };
for i = 1, #bad
	local badDebuff = bad[i];
	if UnitLevel("player") >= 80 then
		ni.healing.debufftoblacklist(badDebuff)
	end
end
```

## dontdispel

参数:

- **unit** `string`: 需要检查的单位.

返回值:

- `布尔型`: 如果单位的负面效果被列入黑名单或者不能被驱散,则为true；否则为false.

使用这个函数来检查一个单位的负面效果是否被列入黑名单或者不能被驱散.

```lua
	if ni.healing.dontdispel("player") then
		-- 执行操作
	end
```

## candispel

参数:

- **unit** `string`: 需要检查的单位.

返回值:

- `布尔型`: 如果单位的负面效果可以被驱散,则为true；否则为false.

使用这个函数来检查一个单位的负面效果是否可以被驱散.

```lua
	if ni.healing.candispel("player") then
		-- 执行操作
	end
```

## debufftypedispellable

参数:

- **debufftype** `string`: 要检查的负面效果类型.

返回值:

- `布尔型`: 如果当前职业可以驱散该类型的负面效果,则为true；否则为false.

使用这个函数来检查一个特定职业是否可以驱散某种类型的负面效果.

```lua
	if healing.debufftypedispellable("Poison") then
		-- 你的职业可以驱散中毒类负面效果
	end
```

# Tanks

> 所有的相关函数调用都需要在前面加上 `ni.tanks()`.

---

返回值:

如果在游戏用户界面中已经手动指定了主坦克（main tank）和副坦克（off-tank）单位,这个函数将返回那些单位.如果没有,函数将尝试根据玩家当前所在的小队/团队中的单位来找到两个坦克.如果组里没有足够的坦克,函数将返回最大生命值最高的两个坦克..

```lua
local mainTank, offTank = ni.tanks()
```


## Example

除了下面列出的函数,还可以使用 mainTank 或 offTank 作为缩写来调用 [Members](api/members.md) 中的任何函数,并将 mainTank 或 offTank 作为第一个参数传递.

```lua
local mainTank, offTank = ni.tanks()
if mainTank then
	if mainTank:combat()
	and mainTank:debufftype("Poison")
	and mainTank:dispel() then
		-- 执行操作
	end
end
if offTank then
	if offTank:combat()
	and not offTank:auras("48066||6788") then
		ni.spell.cast(48066, offTank.unit)
	end
end
```

```lua
-- 返回主坦克和副坦克的units
local mainTank, offTank = ni.tanks()

-- 如果我们能确定坦克的位置,我们就可以在战斗中使用它们
if mainTank then
	if UnitExists(mainTank.unit)
	and mainTank:valid(48378, false, true) then -- 检查主坦克是否在法术编号48378的法术范围内
		if mainTank:hp() < 40
		and not ni.player.ismoving()
		and ni.spell.available(48378) then
			ni.spell.cast(48378, mainTank.unit)
		end			
		if mainTank:hp() < 90 
		and ni.spell.available(48441)
		and not mainTank:buff(48441, "player") then
			ni.spell.cast(48441, mainTank.unit)
		end	
	end
end
if offTank then
	if UnitExists(offTank.unit)
	and offTank:valid(48378, false, true) then -- 检查主坦克是否在法术编号48378的法术范围内
		if offTank:hp() < 70
		and ni.spell.available(48451) 
		and (not offTank:buff(48451, player) 
		or ni.unit.buffstacks(offTank.unit, 48451, "player") < 3) then
			ni.spell.cast(48451, offTank.unit)
		end			
		if offTank:hp() < 90 
		and ni.spell.available(48441)
		and not offTank:buff(48441, "player") then
			ni.spell.cast(48441, offTank.unit)
		end	
	end
end
```