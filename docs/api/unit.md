# Unit

> 所有使用的函数将以 `ni.unit` 作为前缀.

---

## aura

参数:

- **unit** `guid|token`
- **aura** `id|name`

返回值: `boolean`

检查指定单位是否拥有光环（这个检查比魔兽世界的UnitAura更深入,因为它可以对普通客户端看不到的被动光环返回true）.

```lua
if ni.unit.aura("player", 32223) then
  -- 玩家拥有十字军光环
end
if ni.unit.aura("player", "十字军光环") then
	-- 玩家拥有十字军光环
end
```

## auras

参数:

- **unit** `guid|token`

返回值: `table`

返回一个表,包含单位上所有光环的ID和名称（通过这个方法可以看到通常客户端看不到的光环,这个函数更多是供开发者使用,用于获取单位上所有光环的列表,以便与光环函数一起使用）.

```lua
local auras = ni.unit.auras("target");
for k, v in ipairs(auras) do
	if v.name == "十字军光环" then
		--单位通过名称检查拥有十字军光环
	end
	if v.ID == 32223 then
		--单位通过ID检查拥有十字军光环
	end
end
```

## buff

参数:

- **target** `guid|token`
- **id** `name|id`
- **filter** `EXACT|PLAYER` _可选参数_

返回值: `UnitBuff`

Checks if specified unit has certain buff.

```lua
if ni.unit.buff("target", "Life Tap", "player") then
  -- Target has Life Tap active
end
if ni.unit.buff("player", 533, "exact") then
  -- Player has the buff that exactly matches ID 533
end
```

## buffremaining

参数:

- **target** `guid|token`
- **id** `name|id`
- **filter** `EXACT|PLAYER` _可选参数_

返回值: `boolean`

计算目标上的增益效果剩余时间（以秒为单位）.

```lua
if ni.unit.buffremaining("target", "回春术", "player") < 5 then
  -- 目标上的回春术剩余时间少于5秒
end
```

## buffstacks

参数:

- **target** `guid|token`
- **id** `name|id`
- **filter** `EXACT|PLAYER` _可选参数_

返回值: `number`

获取目标身上增益效果的层数.

```lua
if ni.unit.buffstacks("target", 1234) < 5 then
  -- 目标身上的1234效果堆叠次数少于5次
end
```

## buffs

参数:

- **target** `guid|token`
- **ids** `name|id`
- **filter** `EXACT|PLAYER` _可选参数_

返回值: `boolean`

检查指定单位是否拥有通过`&&` 或者 `||`分隔的增益效果.

```lua
if ni.unit.buffs("target", "生命分流&&邪甲术中", "player") then
  -- 目标同时拥有生命分流和邪甲术
end
if ni.unit.buffs("target", "生命分流||邪甲术中") then
  -- 目标拥有生命分流或邪甲术中的至少一种
end
```

## bufftype

参数:

- **target** `guid|token`
- **types** `string|string`

返回值: `boolean`

如果指定单位具有特定的buff类型.可以使用(`|`)传递多个类型.

| Type   |
| ------ |
| Magic  |
| Enrage |

```lua
if ni.unit.bufftype("target", "Enrage|Magic") then
        -- 目标拥有激怒或者魔法增益的效果
end
```

## combatreach

参数:

- **target** `guid|token`

返回值: `number`

检查单位的战斗触及范围（默认返回值为0）.

```lua
local combatreach = ni.unit.combatreach("player");
-- 最有可能打印出玩家单位的战斗范围为1.5
```

## creations

参数:

- **target** `guid|token`

返回值: `table|nil`

检查单位创建物的表格（例如图腾、宠物）,如果没有则为nil.

```lua
local creations = ni.unit.creations("player");

for i = 1, #creations do
  local creature = creations[i]

end
```

## creator

参数:

- **target** `guid|token`

返回值: `guid|nil`

如果指定的单位有创建者,则返回一个 `guid` ；如果没有,则返回 `nil` .

```lua
local creator = ni.unit.creator("playerpet");

if UnitGUID("player") == creator then
  -- 我们是被检查单位的创建者
end
```

## creaturetype

参数:

- **target** `guid|token`

返回值: `number`

检查单位的类型.

| 数值     | 类型       |
| ------- | ------------ |
| 0       | 未知         |
| 1       | 野兽        |
| 2       | 龙类       |
| 3       | 恶魔        |
| 4       | 元素    |
| 5       | 巨人        |
| 6       | 亡灵      |
| 7       | 人形生物     |
| 8       | 小动物     |
| 9       | 机械单位   |
| 10      | 未指定 |
| 11      | 图腾        |
| 12      | 非战斗宠物 |
| 13      | 气体云朵     |

```lua
local type = ni.unit.creaturetype("playerpet")

if type == 3 then
  --我的宠物类型是恶魔
end
```

## debuff

参数:

- **target** `guid|token`
- **id** `name|id`
- **filter** `EXACT|PLAYER` _可选参数_

返回值: `UnitDebuff`

检查单位是否有指定的减益效果.

```lua
if ni.unit.debuff("target", "痛苦诅咒", "player") then
  -- 目标有玩家施放的痛苦诅咒减益效果
end
if ni.unit.debuff("target", 1234) then
  -- 目标有由任何单位施放的id1234的减益效果
end
```

## debuffstacks

参数:

- **target** `guid|token`
- **id** `name|id`
- **filter** `EXACT|PLAYER` _可选参数_

返回值: `number`

获取目标身上的减益效果层数.

```lua
if ni.unit.debuffstacks("target", 1234) < 5 then
  -- 目标有任何单位施放的id1234减益效果层数少于5层
end
```

## debuffremaining

参数:

- **target** `guid|token`
- **id** `name|id`
- **filter** `EXACT|PLAYER` _可选参数_

返回值: `boolean`

计算目标身上的减益效果剩余时间（以秒为单位）.

```lua
if ni.unit.debuffremaining("target", 1234, "player") < 5 then
  -- 目标身上由玩家施放的id1234的减益法术剩余时间少于5秒
end
```

## debuffs

参数:

- **target** `guid|token`
- **ids** `name|id`
- **filter** `EXACT|PLAYER` _可选参数_

返回值: `boolean`

检查指定单位是否具有由 `&&` 或 `||` 分隔的特定减益效果.

```lua
if ni.unit.debuffs("target", "精灵之火&&痛苦诅咒", "player") then
  -- 目标同时受到了精灵之火和痛苦诅咒减益效果的影响
end
if ni.unit.debuffs("target", "精灵之火||痛苦诅咒") then
  -- 目标受到了精灵之火或痛苦诅咒中任意一个减益效果的影响
end
```

## debufftype

参数:

- **target** `guid|token`
- **types** `string|string`

返回值: `boolean`

检查指定单位是否具有特定的减益效果类型.可以通过使用管道字符(`|`)传递多个类型.

| Type    |
| ------- |
| Magic   |
| Poison  |
| Curse   |
| Disease |

```lua
if ni.unit.debufftype("target", "Poison|Magic") then
        -- 目标身上存在中毒或魔法类型的减益效果
end
```

## distance

参数:

- **unit** `guid|token`
- **target** `guid|token`

返回值: `number|nil`

计算 `unit` 与 `target` 之间的距离（以码为单位）.如果任何参数没有传递,这个函数将返回nil.

```lua
if ni.unit.distance("player", "target") < 40 then
  -- 目标距离玩家小于40码
end
```

## enemiesinrange

参数:

- **unit** `guid|token`
- **range** `number`

返回值: `table`

返回一个包含所有在指定单位范围内的敌人的表.每个敌人都有 `guid` , `name` 和 `distance` 属性.

```lua
local enemies = ni.unit.enemiesinrange("player", 30)

for i = 1, #enemies do
  local target = enemies[i].guid
  local name = enemies[i].name
  local distance = enemies[i].distance
  -- 对敌人目标进行一些操作
end
```

## exists

参数:

- **target** `guid|token`

返回值: `boolean`

检查指定的单位是否存在于可视世界中.如果你想检查单位是否总体存在,你可以使用魔兽世界的 `UnitExists` 函数.

```lua
if ni.unit.exists("target") then
  -- 执行一些操作
end
```

## friendsinrange

参数:

- **unit** `guid|token`
- **range** `number`

返回值: `table`

返回一个包含所有在指定单位范围内的友方单位的表.每个友方单位都有 `guid` , `name` 和 `distance` 属性.

```lua
local friends = ni.unit.friendsinrange("player", 30)

for i = 1, #friends do
  local target = friends[i].guid
  local name = friends[i].name
  local distance = friends[i].distance
  -- 对友方目标进行一些操作
end
```

## hasheal

参数:

- **unit** `guid|token`

返回值: `boolean`

检查指定的单位是否具有治疗能力.这并不意味着该单位必然是一个治疗者.

```lua
if ni.unit.hasheal("target") then
  -- 单位具有治疗能力
end
```

## hp

参数:

- **unit** `guid|token`

返回值: `number`

返回单位当前的生命值百分比

```lua
if ni.unit.hp("target") > 90 then
  -- 单位的生命值超过90%
end
```

## hppredicted

参数:

- **unit** `guid|token`

返回值: `number`

支持版本：`4.3.4` 和 `5.4.8` 

计算并返回预测的单位生命值百分比.它通过计算当前生命值加上即将到来的治疗量来进行预测.

```lua
if ni.unit.hppredicted("target") < 30  then
  -- 单位在接受治疗后的生命值将低于30%
end
```

## hpraw

参数:

- **unit** `guid|token`

返回值: `number`

计算并返回当前单位的生命值.

```lua
if ni.unit.hpraw("target") > 20000 then
  -- 单位的生命值超过2000
end
```

## id

参数:

- **unit** `guid|token`

返回值: `number`

查询单位的 `id` .

```lua
if ni.unit.id("target") == 36597 then
  -- 如果目标的id是36597,那么他就是巫妖王
end
```

## itemlvl

参数:

- **unit** `guid|token`

返回值: `number`

返回平均物品等级.

```lua
if ni.unit.itemlvl("player") >= 245 then
	-- 玩家装备的平均物品等级达到245
end
```

## info

参数:

- **unit** `guid|token`

返回值: `number`

检索关于单位的详细信息.

```lua
local x, y, z, facing, unittype, target, height = ni.unit.info("target")
--获得单位的x,y,z,面向,单位类型,目标,高度
```

## inmelee

参数:

- **unit1** `token|guid`
- **unit2** `token|guid`

返回值: `boolean`

检查 `unit1` 是否在 `unit2` 的近战攻击范围内.

```lua
if ni.unit.inmelee("player", "target") then
  -- 目标在玩家的近战范围内
end
```

## isbehind

参数:

- **unit** `guid|token`
- **target** `guid|token`

返回值: `boolean`

检查 `unit` 是否在 `target` 的背后.

```lua
if ni.unit.isbehind("player", "target") then
  -- 玩家在目标的后面
end
```

## isboss

参数:

- **target** `guid|token`

返回值: `boolean`

检查指定的单位是否是首领.

```lua
if ni.unit.isboss("target") then
  -- 我个人感觉这里不如用魔兽自带的函数好使 UnitClassification("target") == "worldboss" 
end
```

## iscasting

参数:

- **unit** `guid|token`

返回值: `boolean`

检查指定的单位是否在施法.

```lua
if ni.unit.iscasting("target") then
  -- 目标正在施法
end
```

## ischanneling

参数:

- **unit** `guid|token`

返回值: `boolean`

检查单位是否在引导技能.

```lua
if ni.unit.ischanneling("target") then
  -- 目标在引导技能
end
```

## isdisarmed

参数:

- **unit** `guid|token`

返回值: `boolean`

检查单位是否被缴械.

```lua
if ni.unit.isdisarmed("target") then
  -- 目标被缴械了
end
```

## isdummy

参数:

- **unit** `guid|token`

返回值: `boolean`

检查单位是否是假人.

```lua
if ni.unit.isdummy("target") then
  -- 目标单位是假人
end
```

## isfacing

参数:

- **unit** `guid|token`
- **target** `guid|token`
- **degrees** `number` _可选参数_

返回值: `boolean`

检查 `unit` 是否面向 `target`, 默认的角度是180度.

```lua
if ni.unit.isfacing("player", "target") then
  -- 玩家正面对着目标
end
if ni.unit.isfacing("player", "target", 90) then
  -- 玩家以90度的精确度面对着目标（左右各45度）
end
```

## isfleeing

参数:

- **unit** `guid|token`

返回值: `boolean`

检查单位是否正在逃跑.

```lua
if ni.unit.isfleeing("target") then
  -- 目标正在逃跑
end
```

## isimmune

参数:

- **unit** `guid|token`

返回值: `boolean`

检查目标是否处于免疫状态.

```lua
if ni.unit.isimmune("target") then
  -- 目标处在免疫状态
end
```

## islootable

参数:

- **unit** `guid|token`

返回值: `boolean`

检查目标是否可以被拾取.

```lua
if ni.unit.islootable("target") then
  -- 目标可以拾取
end
```

## islooting

参数:

- **unit** `guid|token`

返回值: `boolean`

检查目标是否在拾取中.

```lua
if ni.unit.islooting("target") then
  -- 目标在拾取中
end
```

## ismounted

参数:

- **unit** `guid|token`

返回值: `boolean`

检查单位是否在骑乘状态.

```lua
if ni.unit.ismounted("target") then
  -- 目标在骑乘中
end
```

## ismoving

参数:

- **unit** `guid|token`

返回值: `boolean`

检查目标是否移动.

```lua
if ni.unit.ismoving("player") then
  -- 玩家正在移动中
end
```

## ispacified

参数:

- **unit** `guid|token`

返回值: `boolean`

检查单位是否被安抚.

```lua
if ni.unit.ispacified("target") then
  -- 目标处于安抚状态
end
```

## isplayer

参数:

- **unit** `guid|token`

返回值: `boolean`

检查目标是否是玩家类型.

```lua
if ni.unit.isplayer("target") then
  -- 目标是玩家类型
end
```

## isplayercontrolled

参数:

- **unit** `guid|token`

返回值: `boolean`

检查单位是否被玩家控制.

```lua
if ni.unit.isplayercontrolled("target") then
  -- 目标由玩家控制
end
```

## ispossessed

参数:

- **unit** `guid|token`

返回值: `boolean`

检查目标是否被控制.

```lua
if ni.unit.ispossessed("target") then
  -- 目标被控制
end
```

## ispreparation

参数:

- **unit** `guid|token`

返回值: `boolean`

检查单位是否处在准备状态.

```lua
if ni.unit.ispreparation("target") then
  -- 目标处于准备状态
end
```

## ispvpflagged

参数:

- **unit** `guid|token`

返回值: `boolean`

检查单位是否开启了PVP状态.

```lua
if ni.unit.ispvpflagged("target") then
  -- 目标处在PVP开启状态
end
```

## issilenced

参数:

- **unit** `guid|token`

返回值: `boolean`

检查单位是否处于沉默状态.

```lua
if ni.unit.issilenced("target") then
  -- 目标被沉默了
end
```

## isskinnable

参数:

- **unit** `guid|token`

返回值: `boolean`

检查单位是否可以被采集（拆解、剥皮、采矿等）.

```lua
if ni.unit.isskinnable("target") then
  -- 目标可以被采集
end
```

## isstunned

参数:

- **unit** `guid|token`

返回值: `boolean`

检查单位是否处于眩晕状态.

```lua
if ni.unit.isstunned("target") then
  -- 目标被眩晕了
end
```

## istaggedbyme

参数:

- **unit** `guid|token`

返回值: `boolean`

检查单位是否被玩家标记了.

```lua
if ni.unit.istaggedbyme("target") then
  -- 目标被我标记了
end
```

## istaggedbyother

参数:

- **unit** `guid|token`

返回值: `boolean`

检查单位是否被其他人标记了.

```lua
if ni.unit.istaggedbyother("target") then
  -- 目标被其他人标记了
end
```

## istotem

参数:

- **target** `guid|token`

返回值: `boolean`

检查生物是否为图腾.是[creaturetype](api/unit.md#creaturetype)的简写函数.

```lua
if ni.unit.istotem("target") then
  
end
```

## los

参数:

- **targetfrom** `guid|token|x,y,z`
- **targetto** `guid|token|x,y,z`
- **hitflags** `number` _可选参数_

返回值: `boolean, x, y, z`

检查单位之间是否有视线,有返回trun,无返回false,并返回碰撞的击中点.

```lua
if ni.unit.los("player", "target") then
 
end
local bool, x, y, z = ni.unit.los(100, 200, -10000, 100, 200, 10000);
if not bool then
	
end
```

## meleerange

参数:

- **unit1** `token|guid`
- **unit2** `token|guid`

返回值: `boolean`

计算 `unit1` 到 `unit2` 的近战范围. 如果你想检查单位是否在近战范围内请使用 [`inmelee`](api/unit.md#inmelee)

```lua
ni.unit.meleerange("player", "target")
```

## power

参数:

- **unit** `guid|token`
- **type** `string` _可选参数_

返回值: `number`

计算并返回单位当前能量的百分比（例如法力、能量、集中值等）.

```lua
if ni.unit.power("target") > 90 then
  -- 单位的能量超过了 90%
end
```

## powerraw

参数:

- **unit** `guid|token`
- **type** `string` _可选参数_

返回值: `number`

计算并返回单位当前的能量值（例如法力、能量、集中等）.

```lua
if ni.unit.powerraw("target") > 10000 then
  -- 单位的能量超过了 10000
end
```

## readablecreaturetype

参数:

- **target** `guid|token`

返回值: `string`

检查单位的类型返回类型名.

| 数值 | 字符串       |
| ---- | ------------ |
| 0    | 未知         |
| 1    | 野兽         |
| 2    | 龙类         |
| 3    | 恶魔         |
| 4    | 元素生物     |
| 5    | 巨人         |
| 6    | 亡灵         |
| 7    | 人型生物     |
| 8    | 小动物       |
| 9    | 机械         |
| 10   | 未指定       |
| 11   | 图腾         |
| 12   | 非战斗宠物   |
| 13   | 气体云团     |

```lua
local type = ni.unit.readablecreaturetype("playerpet")

if type == "Demon" then

end
```

## threat

参数:

- **unit** `guid|token`
- **unittargeted** `guid|token` _可选参数_

返回值: `number`

计算 `unit` 的威胁值.如果传递了第二个参数,则根据 `unittargeted` 来计算威胁值.

```lua
local threat = ni.unit.threat("player", "target")
```

## ttd

参数:

- **unit** `guid|token`

返回值: `number`

检索指定单位的死亡时间,单位为秒.如果单位不存在,则返回 `-2` ,如果单位是假人,或者单位以某种方式跳过了死亡时间计算,则返回 `99` .

```lua
if ni.unit.ttd("target") > 10 then
  
end
```

## unitstargeting

参数:

- **unit** `guid|token`
- **friendlies** `boolean` _默认值: false_

返回值: `table`

返回一个表格,包含所有在指定单位范围内的单位.每个单位都有 `guid` 、`name` 和 `distance` 属性. 

```lua
local units = ni.unit.unitstargeting("player")

for i = 1, #units do
  local target = units[i].guid
  local name = units[i].name
  local distance = units[i].distance
  -- 对定位玩家的单位执行某些操作
end
```

## location

参数:

- **unit** `guid|token`

返回值: `x, y, z`

返回值1是单位的x坐标,值2是单位的y坐标,值3是单位的z坐标.

```lua
local x, y, z = ni.unit.location("target");
--使用x、y和z的值执行一些操作
```

## transport

参数:

- **unit** `guid|token`

返回值: `string or nil`

如果单位有交通工具（比如在电梯或车辆上,或者一个单位在另一个单位上面）,则返回单位交通工具的GUID,否则返回nil.

```lua
local transport = ni.unit.transport("target")
if transport then
	--目标有交通工具
end
```

## facing

参数:

- **unit** `guid|token`

返回值: `number`

返回单位面向的弧度值.

```lua
if ni.unit.facing("target") == 0 then
	--该单位面朝正北
end
```

## LoS Bit Values

以下是可以传递给los函数的击中标志,如果你不想使用默认的HitTestGroundAndStructures值.

```lua
HitTestNothing = 0x0,
HitTestBoundingModels = 0x1,
HitTestWMO = 0x10,
HitTestUnknown = 0x40,
HitTestGround = 0x100,
HitTestLiquid = 0x10000,
HitTestUnknown2 = 0x20000,
HitTestMovableObjects = 0x100000,
HitTestLOS = HitTestWMO | HitTestBoundingModels | HitTestMovableObjects,
HitTestGroundAndStructures = HitTestLOS | HitTestGround
```

要计算你想要的位值,你可以使用wow的函数bit.bor或者简单地加上这些值.
```lua
local hit_ground_and_liquid = 0x100 + 0x10000;
if ni.unit.los("player", "target", hit_ground_and_liquid) then
	--之所以这样做是因为我们既没有击中地面也没有击中水面
end
```