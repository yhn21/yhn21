# Memory

> 这是为了内存读取功能.每个函数前都加上了 `ni.memory`.

---

## baseaddress

参数:

返回值: `number, string`

返回客户端的基地址.返回值1是数值形式,返回值2是字符串格式化后的值.

```lua
local base = ni.memory.baseaddress();
if ni.memory.read("byte", base + 0x12345678) == 0xCC then
	--在基地址加上0x12345678处的值是0xCC
end
```

## objectpointer

参数:

- **object** `token|guid`

返回值: `number, string`

返回对象的指针.返回值1是数值形式,返回值2是字符串格式化后的值.

```lua
local ptr = ni.memory.objectpointer("player");
```

## read

参数:

- **readtype** `string (see below)`
- **address** `number`
- **...** `offsets to add to the address to read off of` _可选参数_

返回值: `readtype value`

根据第一个参数指定的类型返回内存中的值.

```lua
local ptr = ni.memory.objectpointer("player");
local height = ni.memory.read("float", ptr, 0x8F8); --获取玩家的高度（熊猫人之谜的偏移量）
```

---

> 以下字符串是 read 函数接受的读取类型参数.

## read types

```lua
"bool" --true/false 格式化
"byte" --number 格式化
"string" --string 格式化
"float" --number 格式化
"double" --number 格式化
"int16"/"short" --number 格式化
"int32"/"int" --number 格式化
"int64" --string 格式化 格式化
"uint16"/"ushort" --number 格式化
"uint"/"uint32" --number 格式化
"uint64"/"GUID" --string 格式化
```