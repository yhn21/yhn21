# Debug

> 所有功能在使用时需要加上 `ni.debug` 前缀.

---

## print

参数:

- **message** `string`

返回值: `void`

如果 `ni.vars.debug` 设置为 true ,则打印出相应的消息.

```lua
ni.vars.debug = false
ni.debug.print("测试") -- 如果设置为 true,则不打印消息
ni.vars.debug = true
ni.debug.print("测试") -- 如果设置为 true,则打印消息
```

## log

参数:

- **message** `string`
- **error** `布尔型` _可选参数_

返回值: `无`

将消息打印到ni应用程序的控制台.错误参数是可选的,使用true表示错误消息,使用空值、false或normal表示普通消息.

```lua
ni.debug.log("测试")
```
