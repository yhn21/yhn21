# Generic

> 适用于不符合特定分类的通用函数.

---

## delayfor

参数:

- **delay** `number`
- **func** `function`

返回值: `布尔值`

延迟指定时间对特定函数调用.

```lua
ni.delayfor(2, function()
  ni.spell.cast("暗影箭", "target")
end);
-- 暗影箭将延迟2秒施放.
```

## require

参数:

- **filename** `string`

返回值: `从加载的文件返回数据`

Ni的require函数.它用于将文件加载到另一个代码块中,使得可以在不重复加载的情况下访问其他函数,因为每次初始加载都会被缓存（重新加载将清除缓存）.传递给文件的字符串可以是不带.lua扩展名的文件名,也可以包含.lua扩展名.它会在Data文件夹中搜索该文件.此外,您还可以使用绝对路径（例如C:\Some Folder\file.lua）.

```lua
local data = ni.utils.require("Example"); --这将从data文件夹加载名为Example.lua的文件,并将其存储在本地变量data中

print(example.version()); --在示例文件中已经有一个名为"version"的函数,所以这里会打印版本号
```
