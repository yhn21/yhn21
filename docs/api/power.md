# Power

> 所有函数在使用时将会在前面添加 `ni.power`.

如果你只需要获取单位当前的能量百分比,有两个简写函数,比如:

- [`ni.unit.power`](api/unit.md#power)
- [`ni.unit.powerraw`](api/unit.md#powerraw)
- [`ni.player.power`](api/player.md).
- [`ni.player.powerraw`](api/player.md).

默认情况下,能量类型将匹配专精的当前能量类型.

---

## current

参数:

- **unit** `guid|token`
- **type** `name|id`

返回值: `number`

计算单位当前的能量百分比.

```lua
local power = ni.power.current("player") 
```

## currentraw

参数:

- **unit** `guid|token`
- **type** `name|id`

返回值: `number`

计算单位当前的能量数值.

```lua
local power = ni.power.currentraw("player") 
```

## ismax

参数:

- **unit** `guid|token`
- **type** `name|id`

返回值: `boolean`

检查单位的能量是否处于最大值.

```lua
if ni.power.ismax("player") then
  -- 玩家的能量处于 100%
end
```

## max

参数:

- **unit** `guid|token`
- **type** `name|id`

返回值: `number`

计算单位的最大能量.

```lua
local maxpower = ni.power.max("target")
```
