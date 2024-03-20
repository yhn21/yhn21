# Rune

> 所有使用的函数将以 `ni.rune` 作为前缀.

---

## available

参数:

返回值: `number`

计算可用的符文数量.

```lua
if ni.rune.available() == 6 then
  -- 玩家拥有所有6个符文
end
```

## deathrunes

参数:

返回值: `number`

计算死亡符文的数量.

```lua
if ni.rune.deathrunes() == 4 then
  -- 玩家有4个符文是死亡符文
end
```

## bloodrunecd

参数:

返回值: `number`, `number`

返回冷却中和非冷却中的鲜血符文数量.

```lua
local offcd, oncd = ni.rune.bloodrunecd()
  -- 1, 1 or 2, 0 or 0, 2
```

## deathrunecd

参数:

返回值: `number`, `number`

返回冷却中和非冷却中的死亡符文数量.

```lua
local offcd, oncd = ni.rune.deathrunecd()
  -- 1, 1 or 2, 0 or 0, 2
```

## frostrunecd

参数:

返回值: `number`, `number`

返回冷却中和非冷却中的冰霜符文数量.

```lua
local offcd, oncd = ni.rune.frostrunecd()
  -- 1, 1 or 2, 0 or 0, 2
```

## unholyrunecd

参数:

返回值: `number`, `number`

返回冷却中和非冷却中的邪恶符文数量.

```lua
local offcd, oncd = ni.rune.unholyrunecd()
  -- 1, 1 or 2, 0 or 0, 2
```
