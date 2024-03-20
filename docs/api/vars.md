# Vars

> 所有使用的函数将以 `ni.vars` 作为前缀.

---

## general

```lua
ni.vars.latency -- 在执行循环动作的间隔时间
ni.vars.interrupt -- could be `all` or `wl` or `bl`
ni.vars.build -- 这个变量可能存储的是当前运行的客户端的构建版本号
ni.vars.debug -- 一个布尔值,用于控制是否打印调试信息.当设置为 true 时,使用 ni.debug.print 函数的地方将会打印信息,以便调试
ni.vars.customtarget -- 这个变量可能用于存储一个自定义目标的 token 或 guid（全局唯一标识符）
```

## hotkeys

```lua
ni.vars.hotkeys.aoe
ni.vars.hotkeys.cd
ni.vars.hotkeys.pause
ni.vars.hotkeys.custom
```

## profiles

```lua
ni.vars.profiles.primary --主配置文件的名称
ni.vars.profiles.secondary --次配置文件的名称
ni.vars.profiles.active --当前活动配置文件的名称
ni.vars.profiles.generic --通用配置文件的名称
ni.vars.profiles.genericenabled --通用配置文件是否启用
ni.vars.profiles.interrupt --中断引擎是否启用
ni.vars.profiles.enabled --活动配置文件是否启用
ni.vars.profiles.useEngine --启用/禁用成员表
ni.vars.profiles.delay --延迟配置文件执行的时间（不应通过变量本身设置）
```

## units

```lua
ni.vars.units.follow
ni.vars.units.followEnabled
ni.vars.units.mainTank
ni.vars.units.mainTankEnabled
ni.vars.units.offTank
ni.vars.units.offTankEnabled
```

## combat

```lua
ni.vars.combat.started -- 玩家回复启用/禁用（战斗中）时为true/false
ni.vars.combat.time -- 自战斗开始以来的时间
ni.vars.combat.melee -- 使用跟随功能决定移动时为true/false
ni.vars.combat.cd -- 冷却切换启用时为true/false
ni.vars.combat.aoe -- AOE（区域效果）切换启用时为true/false
ni.vars.combat.casting -- 向服务器发送法术时为true/false

```
