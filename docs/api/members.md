# Members

> 下面使用的所有函数都要以 `ni.members`.

---
## 遍历成员表
如果你不需要按照距离和生命值来排序他们:

```lua
for i = 1, #ni.members do
    ...
end
```
如果你要按照距离来排序:

```lua
for i = 1, #ni.members.inrange("player", 40) do
    ...
end
```

如果你要按照距离和生命值来排序:
```lua
for i = 1, #ni.members.sort() do
    ...
end
```

## istank

返回值: `布尔值`

如果单位是坦克,则返回turn,否则返回false.

```lua
for i = 1, #ni.members do
	if ni.members[i]:istank() then
		-- 如果目标是坦克,就执行.
	end
end
```

## ishealer

返回值: `布尔值`

如果单位是治疗者,则返回turn,否则返回false.

```lua
for i = 1, #ni.members do
	if ni.members[i]:ishealer() then
		-- 如果目标是治疗者,就执行 
	end
end
```

## isdps

返回值: `布尔值`

如果单位是DPS,则返回turn,否则返回false.

```lua
for i = 1, #ni.members do
	if ni.members[i]:isdps() then
		-- 如果目标是DPS,就执行 
	end
end
```

## iscaster

返回值: `布尔值`

如果单位是法术DPS或者具有法术DPS的单位,则返回turn,否则返回false.

```lua
for i = 1, #ni.members do
	if ni.members[i]:iscaster() then
		-- 如果目标是法术DPS,就执行 
	end
end
```

## ismelee

返回值: `布尔值`

如果单位是近战DPS或者具有近战DPS的单位,则返回turn,否则返回false.

```lua
for i = 1, #ni.members do
	if ni.members[i]:ismelee() then
		-- 如果目标是近战DPS,就执行 
	end
end
```

## location

返回值: `number`, `number`, `number`, `number`

单位的当前位置由四个独立的值表示: x, y, z, and r (朝向).

```lua
for i = 1, #ni.members do
	local x, y, z, r = ni.members[i]:location()
	if x and y and z and r then
		-- 成功获取了单位的位置信息
	end
end
```

## combat

返回值: `布尔值`

如果单位在战斗中,则返回turn,否则返回false.

```lua
for i = 1, #ni.members do
	if ni.members[i]:combat() then
		-- The unit is in combat
	end
end
```

## aura

参数:

- **aura：** `number` or `string`

返回值: `布尔值`

如果单位拥有指定的光环效果,则返回turn,否则返回false.

```lua
if ni.members[1]:aura(12345) then
    -- 如果该单位有12345的光环效果,就执行
end

if ni.members[1]:aura("虔诚光环") then
    -- 如果该单位有"虔诚光环"的效果,就执行
end
```

注意：您可以使用光环ID或光环名称作为这个函数的参数.

## auras
参数:

- **ids** `光环名称|光环id`
- **filter** `任何人|玩家` _可选参数_

参数: `布尔值`

检查指定单位是否有指定的光环效果,使用 `&&` 或者 `||`进行分隔.

```lua
if ni.members[1]:auras("63321&&虔诚光环") then
    -- 单位同时拥有id63321和虔诚光环的光环效果
end

if ni.members[1]:auras("63321||虔诚光环", "EXACT") then
    -- 单位拥有id63321或者虔诚光环的光环效果
end
```

注意：您可以使用光环效果的ID或名称作为这个函数的参数.

## buffs

参数:

- **ids** `法术名|法术id`
- **filter** `任何人|玩家` _可选参数_

参数: `布尔值`

检查是否有指定的buff,使用 `&&` 或者 `||`进行分隔.

```lua
if ni.members[1]:buffs("63321 && 寒冰屏障", "EXACT") then
    -- 单位同时拥有id63321和寒冰屏障的buff
end

if ni.members[1]:buffs("63321 || 寒冰屏障") then
   -- 单位拥有id63321或者寒冰屏障的buff
end
```

注意：您可以使用增益效果的ID或名称作为这个函数的参数.

## debuffs

参数:

- **ids** `法术名|法术id`
- **filter** `任何人|玩家` _可选参数_

参数: `布尔值`

检查是否有指定的debuff,使用 `&&` 或者 `||`进行分隔.

```lua
if ni.members[1]:debuffs("63321 & 献祭", "player") then
    -- 单位同时拥有id63321和献祭的debuff
end

if ni.members[1]:debuffs("63321 || 献祭") then
    -- 单位拥有id63321或者献祭的debuff
end
```

注意：您可以使用减益效果的ID或名称作为这个函数的参数.

## debufftype

类型:

- **函数：**

参数:

- **字符串：** `debuff 类型`

参数: `布尔值`

如果有指定的减益类型,则返回turn,否则返回false.

```lua
for i = 1, #ni.members do
	if ni.members[i]:debufftype("Disease") then
		-- 这个成员身上有类型为“疾病”的减益效果
	end
end
```
注意：此函数检查指定类型的任何减益效果,不考虑它们的具体名称或ID.

## bufftype

类型:

- **函数：**

参数:

- **字符串：** `buff 类型`

参数: `布尔值`

如果有指定的增益类型,则返回turn,否则返回false.

```lua
for i = 1, #ni.members do
	if ni.members[i]:bufftype("Magic") then
		-- 这个成员身上有类型为“魔法”的增益效果
	end
end
```

注意：此函数检查指定类型的任何增益效果,不考虑它们的具体名称或ID.

## buff

类型:

- **函数：**

参数:

- **增益效果** `法术名|法术id`
- **filter** `任何人|玩家` _可选参数_

返回值: `UnitBuff`

如果他们身上的增益效果与UnitBuff相同,则返回turn,否则返回false.

```lua
for i = 1, #ni.members do
	if ni.members[i]:buff("真言术：盾", "player") then
		-- 该成员身上有玩家施放的“真言术：盾”效果
	end
end
```

注意：如果没有指定filter参数,这个函数将返回它找到的第一个匹配增益效果,不考虑其类型.

## debuff

类型:

- **函数**

参数:

- **debuff** `法术名|法术id`
- **filter** `任何人|玩家` _可选参数_

参数: `UnitDebuff`

如果他们身上的减益效果与UnitDeBuff相同,则返回turn,否则返回false.

```lua
for i = 1, #ni.members do
	if ni.members[i]:debuff("虚弱灵魂") then
		-- 这个成员身上有虚弱灵魂效果
	end
end
```

注意：如果没有指定filter参数,这个函数将返回它找到的第一个匹配减益效果,不考虑其类型.

## buffstacks

参数:

- **增益效果** `法术名|法术id`
- **filter** `任何人|玩家` _可选参数_

```lua
for i = 1, #ni.members do
	if ni.members[i]:buffstacks("大地之盾") < 3 then
		-- 这个成员的大地之盾少于3层
	end
end
```

如果没有指定filter参数,这个函数会返回它找到的第一个匹配的减益效果,不管它的类型是什么.

## debuffstacks

参数:

- **减益效果** `法术名|法术id`
- **filter** `任何人|玩家` _可选参数_

```lua
for i = 1, #ni.members do
	if ni.members[i]:debuffstacks("冰冻之骨") > 5 then
		-- 这个成员身上的冰冻之骨减益效果超过了5层
	end
end
```

如果没有指定filter参数,这个函数会返回它找到的第一个匹配的减益效果,不管它的类型是什么.

## dispel

类型:

- **variable**

参数: `布尔值`

如果成员有你可以驱散的减益效果,则返回turn,否则返回false.

```lua
for i = 1, #ni.members do
	if ni.members[i]:dispel() then
		-- 这位成员身上有一个你可以驱散的减益效果
	end
end
```

## cast

参数:

- **spell** `法术名|法术id`

参数: `void`

对成员施放指定的法术.

```lua
for i = 1, #ni.members do
	if ni.members[i]:dispel() then
		return ni.members[i]:cast(988) -- 施放驱散魔法
	end
end

for i = 1, #ni.members do
	if ni.members[i]:buffstacks("大地之盾") < 3 then
		return ni.members[i]:cast("大地之盾") -- 对该单位施放大地之盾
	end
end
```

## hpraw

类型:

- **variable**

参数: `number`

这是一个检测团队成员剩余生命值数值的函数.

```lua
for i = 1, #ni.members do
	if ni.members[i]:hpraw() < 30000 then
		-- 这个团队成员的剩余生命值小于30000
	end
end
```

## hpmax

类型:

- **variable**

参数: `number`

这是一个检查团队成员最大生命值数值的函数.

```lua
for i = 1, #ni.members do
	local maxHealth = ni.members[i]:hpmax()
		...
end
```

## hp

类型:

- **variable**

参数: `number`

这是一个检查团队成员剩余生命值百分比的函数.

```lua
for i = 1, #ni.members do
	if ni.members[i]:hp() < 20 then
		-- 这个团队成员剩余生命百分比小于20%
	end
end
```

## range

参数: None

返回值: `布尔值`

如果单位距离玩家40码以内,则为turn,否则为false.

```lua
for i = 1, #ni.members do
	if ni.members[i]:range() then
		-- 单位在玩家40码范围内
	end
end	
```

## los

参数: None

返回值: `布尔值`

如果玩家对单位有视野,则为turn,否则为false.

```lua
for i = 1, #ni.members do
	if ni.members[i]:los() then
		-- 玩家对单位有视野
	end
end	
```

## facing

参数: None

返回值: `布尔值`

如果玩家面向单位,则为turn,否则为false.

```lua
for i = 1, #ni.members do
	if ni.members[i]:facing() then
		-- 玩家正面对着该单位
	end
end	
```

## valid

参数:

- **spell** `法术id|法术名`
- **facing** `布尔值` _默认: false_
- **los** `布尔值` _默认: false_

返回值: `布尔值`

该函数确保可以对特定单位施放法术. 它包括如下检查:

- [`los（视野）`](api/members.md#los)
- [`facing（面向）`](api/members.md#facing)
- `IsSpellInRange（施法范围内）`

```lua
for i = 1, #ni.members do
	if ni.members[i]:valid(48441, false, true) then
		-- 所有的条件都是有效的
	end
end	

for i = 1, #ni.members do
	if ni.members[i]:valid("Power Word: Shield", false, true) then
		-- 所有的条件都是有效的
	end
end	
```

## threat

类型:

- **variable**

返回值: `number`

这是一个返回被访问成员威胁值的函数（返回值数字在-1到3之间）.

```lua
for i = 1, #ni.members do
	if ni.members[i]:threat() == -1 then
		-- 这位成员不在任何怪物的威胁列表上（99%的几率是刚刚结束战斗）
	end
end
```

## subgroup

类型:

- **variable**

返回值: `number`

这个函数用来查询小队的编号.

```lua
for i = 1, #ni.members do
	if ni.members[i]:subgroup == 1
	or ni.members[i]:subgroup == 2 then
		-- 仅对团队中1和2小队的成员执行操作
	end
end
```

## role

返回单位在小组中分配的角色.

返回值:

- 一个代表单位在小组中分配角色的字符串.
- 如果该单位没有分配角色,则返回空字符串.

示例:

```lua
for i = 1, #ni.members do
	if ni.members[i].role == "TANK" then
		-- 为坦克执行特定操作
	elseif ni.members[i].role == "HEALER"
		-- 为治疗者执行特定操作
	elseif ni.members[i].role == "CASTER"
		-- 为法术施放者执行特定操作
	elseif ni.members[i].role == "MELEE"
		-- 为近战执行特定操作		
	end
end
```

## spec

返回小组中单位的职业专精.

返回值:

- 如果单位没有加天赋,则返回None.

示例:

```lua
for i = 1, #ni.members do
	if ni.members[i].spec == "Fire" then
		-- 为选择火焰天赋的法师执行特定操作	
	end
end
```

## below

参数:

- **percent** `number`

返回值: `number`

返回小组成员中生命值百分比低于参数百分比的人数.

```lua
local count = ni.members.below(90); 
if #count >= 3 then
	-- 团队中生命值低于90%大于等于3个
end
```

## average

参数:

- **unit** `guid|token`
- **distance** `number`

返回值: `number`

计算指定距离内小组成员的平均健康百分比.

```lua
local avarage = ni.members.average("player", 20);
if avarage <= 40
	-- 如果玩家周围20码内所有成员的平均生命值低于40%
end
```

## averageof

参数:

- **count** `number`
- **unit** `guid|token`
- **distance** `number`

返回值: `number`

计算指定单位指定距离内的指定数量成员的平均生命值百分比.

```lua
local averageHealth = ni.members.averageof(5, "focus", 30) 
-- 计算在焦点目标30码内最近的5个成员的平均生命值百分比.
```

## subgroupbelow

参数:

- `percent` (`number`): 被认为健康值低的生命值百分比阈值.
- `radius` (`number`): 搜索低生命值成员的最大半径（以码为单位）.
- `owngroup` (`布尔值`, 可选项): 如果为真,仅在玩家自己的小队中搜索.否则,在所有小队中搜索.

返回值: 
- `near` (`number`): 小组内低于设定百分比健康值的成员数量.
- `lowestMember` (`table`): 包含健康值最低且离玩家最近的小组成员信息的表格.该表格包含以下键:
    - `unit` (`string`): 单位的名称.
    - `hp` (`number`): 单位的生命值百分比.
    - `near` (`number`): 在指定半径内,同样健康值低的其他成员数量.

```lua
-- 在10码内搜索生命值低于20%的小组成员中生命值最低的成员.
local total, lowestMember = ni.members.subgroupbelow(20, 10)
-- 如果找到至少3个生命值低于20%的成员,并且最低的成员满足特定条件,则对其施放法术
if lowest and total >= 3
and lowest:valid(48072, false, true) then
	spellCast(48072, lowest.unit)
	return true;	
end
```

注意：此函数搜索玩家小组中健康值最低的成员,并返回在一定半径内具有低健康值的成员数量以及健康值最低的成员.

## inrange

参数:

- **unit** `guid|token`
- **distance** `number`

参数: `table`

返回一个包含在指定距离内距离指定单位的所有成员信息的表格.

```lua
local members_around_me = ni.members.inrange("player", 10); --返回一个表格,包含所有在玩家周围10码内的成员
```

## inrangebelow

参数:

- **unit** `guid|token`
- **distance** `number`
- **hp** `number`

参数: `table`

返回一个表,包含在指定单位指定距离内,并且生命值低于传入百分比的所有成员信息.

```lua
local members_below = ni.members.inrangebelow("player", 10, 60); --返回一个表,包含所有在玩家周围10码内并且生命值低于60%的成员
```

---

> 除了主要的 ni.members 函数之外,ni.members 本身也是一个表,包含了小队/团队中的所有成员信息.这是为了通过迭代来实现治疗配置或需要访问成员信息的配置而设计的.以下是该表的访问器、函数和示例:

## inrangewithbuff

参数:

- **unit** `guid|token`
- **distance** `number`
- **buff** `name|id`
- **filter** `EXACT|PLAYER` _可选参数_

返回值: `table`

返回一个表,包含在指定单位指定距离内,并且拥有指定增益效果的所有成员信息.

```lua
local members_with_riptide = ni.members.inrangewithbuff("player", 10, "真言术：盾", "player"); --返回一个表,包含所有在玩家周围10码内且拥有由玩家施放的真言术：盾增益效果的成员
```

## inrangewithoutbuff

参数:

- **unit** `guid|token`
- **distance** `number`
- **buff** `name|id`
- **filter** `EXACT|PLAYER` _可选参数_

参数: `table`

返回一个表,包含在指定单位指定距离内,并且没有指定增益效果的所有成员信息.

```lua
local members_without_riptide = ni.members.inrangewithoutbuff("player", 10, "真言术：盾"); --返回一个表,包含所有在玩家周围10码内且没有真言术：盾增益效果的成员
```

## inrangewithdebufftype

参数:

- **unit** `guid|token`
- **distance** `number`
- **str** `string`

返回值: `table`

返回一个表,包含在指定单位指定距离内,并且有指定类型减益效果的所有成员信息.

```lua
local members_with_poison = ni.members.inrangewithdebufftype("player", 10, "Poison"); --返回一个表,包含所有在玩家周围10码内且有中毒减益效果的成员
```

## inrangewithbufftype

参数:

- **unit** `guid|token`
- **distance** `number`
- **str** `string`

返回值: `table`

返回一个表,包含在指定单位指定距离内,并且有指定类型增益效果的所有成员信息.

```lua
local members_with_magic_buff = ni.members.inrangewithbufftype("player", 10, "Magic"); --返回一个表,包含所有在玩家10码内并且有魔法类型增益效果的成员
```

## inrangewithbuffbelow

参数:

- **unit** `guid|token`
- **distance** `number`
- **buff** `name|id`
- **hp** `number`
- **filter** `EXACT|PLAYER` _可选参数_

返回值: `table`

返回一个表,包含在指定单位指定距离内,有生命值百分比低于或等于传入百分比,并且有指定增益效果的所有成员信息.

```lua
local members_with_buff_below_50 = ni.members.inrangewithbuffbelow("player", 10, "真言术：盾", 50, "player"); 
-- 返回一个表,包含所有在玩家10码内,生命值百分比低于或等于50%,且有玩家施放的真言术：盾增益效果的成员 
```

## inrangewithoutbuffbelow

参数:

- **unit** `guid|token`
- **distance** `number`
- **buff** `name|id`
- **hp** `number`
- **filter** `EXACT|PLAYER` _可选参数_

返回值: `table`

返回一个表,包含在指定单位指定距离内,有生命值百分比低于或等于 hp,并且没有指定增益效果的所有成员信息.

```lua
local members_without_buff_below_50 = ni.members.inrangewithoutbuffbelow("player", 10, "真言术：盾", 50); 
-- 返回一个表,包含所有在玩家10码内,生命值百分比低于或等于50%,且没有真言术：盾增益效果的成员
```

## inrangewithdebuff

参数:

- **unit** `guid|token`
- **distance** `number`
- **debuff** `name|id`
- **filter** `EXACT|PLAYER` _可选参数_

返回值: `table`

返回一个表,包含在指定单位指定距离内,并且有指定减益效果的所有成员信息.

```lua
local members_with_scorch = ni.members.inrangewithdebuff("target", 10, "恐惧", "palyer"); 
--	返回一个表,包含所有在目标10码内,且有由玩家施放的恐惧减益效果的成员
```

## inrangewithdebuffbelow

参数:

- **unit** `guid|token`
- **distance** `number`
- **debuff** `name|id`
- **hp** `number`
- **filter** `EXACT|PLAYER` _可选参数_

返回值: `table`

返回一个表,包含在指定单位指定距离内,生命值百分比低于或等于传入百分比,且有指定减益效果的所有成员信息.

```lua
local members_with_scorch_below_50 = ni.members.inrangewithdebuffbelow("target", 10, "恐惧", 50, "player"); 
-- 返回一个表,包含所有在目标10码内,有由玩家施放的恐惧减益效果且生命值低于或等于50%的成员
```

## inrangewithoutdebuff

参数:

- **unit** `guid|token`
- **distance** `number`
- **debuff** `name|id`
- **filter** `EXACT|PLAYER` _可选参数_

返回值: `table`

返回一个表,包含在指定单位指定距离内,并且没有指定减益效果的所有成员信息.

```lua
local members_without_curse = ni.members.inrangewithoutdebuff("player", 10, "恐惧", "player"); 
-- 返回一个表,包含所有在玩家10码内,且没有由玩家施放的恐惧减益效果的成员
```

## inrangewithoutdebuffbelow

参数:

- **unit** `guid|token`
- **distance** `number`
- **debuff** `name|id`
- **hp** `number`
- **filter** `EXACT|PLAYER` _可选参数_

返回值: `table`

返回一个表,包含在指定单位指定距离内,生命值百分比低于或等于传入百分比且没有指定减益效果的所有成员信息.

```lua
local members_without_curse_below_50_percent_hp = ni.members.inrangewithoutdebuffbelow("player", 10, "恐惧", 50, "player"); 
-- 返回一个表,包含所有在玩家10码内,且生命值低于或等于50%,并且没有由玩家施放的恐惧减益效果的成员
```

## addcustom

参数:

- **unit** `string`: 要添加为自定义成员的单位的名称.
- **guid** `string` _可选参数_: 要添加为自定义成员的单位的全局唯一标识符.如果未提供,将通过 `UnitGUID(unit)` 获取.

这个函数用于将一个自定义成员添加到成员表中,它会创建一个带有提供的单位名称和GUID的新 `GroupMember` 对象,并将其添加到成员表中,如果自定义成员成功添加,将使用 `updatemembers` 函数更新成员表.

## removecustom

参数:
- **unit** `string`: 要从成员表中移除的单位名称.

这个函数用于从成员表中移除一个自定义成员,它将遍历成员表,并移除与提供的单位名称匹配的第一个元素,同时会从 `memberssetup` 对象的 `cache` 表中移除该单位,如果自定义成员成功移除,将使用 `updatemembers` 函数更新成员表.