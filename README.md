# fakego

[<img src="https://img.shields.io/github/license/esrrhs/fakego">](https://github.com/esrrhs/fakego)
[<img src="https://img.shields.io/github/languages/top/esrrhs/fakego">](https://github.com/esrrhs/fakego)
[![Go Report Card](https://goreportcard.com/badge/github.com/esrrhs/fakego)](https://goreportcard.com/report/github.com/esrrhs/fakego)
[<img src="https://img.shields.io/github/v/release/esrrhs/fakego">](https://github.com/esrrhs/fakego/releases)
[<img src="https://img.shields.io/github/actions/workflow/status/esrrhs/fakego/go.yml?branch=master">](https://github.com/esrrhs/fakego/actions)

轻量级嵌入式脚本语言

[README_EN](./README_EN.md)

## 简介
**fakego**是一款轻量级的嵌入式脚本语言，使用Golang语言编写，语法吸取自lua、golang、erlang，基于nex、goyacc生成语法树，编译成字节码解释执行。

[C++版本fake](https://github.com/esrrhs/fake)

[Java版本fake](https://github.com/esrrhs/fakejava)


## 脚本特性
* 语法类似lua
* 全部为函数
* 支持array，map，可以无限嵌套
* 支持函数绑定
* 自带解释器
* 支持多返回值
* 自带profile，可获取脚本各个函数运行时间
* 支持热更新
* 支持Int64
* 支持const定义
* 支持包
* 支持struct

## 示例

```

-- 当前包名
package mypackage.test

-- 引入的文件
include "common.fk"

-- 结构体定义
struct teststruct
	sample_a
	sample_b
	sample_c
end

-- 常量值
const hellostring = "hello"
const helloint = 1234
const hellomap = {1 : "a" 2 : "b" 3 : [1 2 3]}

-- func1 comment
func myfunc1(arg1, arg2)

	-- Java静态函数和类成员函数的调用
	arg3 := cfunc1(helloint) + arg2:memfunc1(arg1)

	-- 分支
	if arg1 < arg2 then
		-- 创建一个协程
		fake myfunc2(arg1, arg2)
	elseif arg1 == arg2 then
		print("elseif")
	else
		print("else")
	end

	-- for循环
	for var i = 0, i < arg2, i++ then
		print("i = ", i)
	end

	-- 数组
	var a = array()
	a[1] = 3

	-- 集合
	var b = map()
	b[a] = 1
	b[1] = a

	-- Int64
	var uid = 1241515236123614u
	log("uid = ", uid)

	-- 子函数调用
	var ret1, var ret2 = myfunc2()

	-- 其他包的函数调用
	ret1 = otherpackage.test.myfunc1(arg1, arg2)

	-- 结构体
	var tt = teststruct()
	tt->sample_a = 1
	tt->sample_b = teststruct()
	tt->sample_b->sample_a = 10

	-- 分支
	switch arg1
		case 1 then
			print("1")
		case "a" then
			print("a")
		default
			print("default")
	end

	-- 多返回值
	return arg1, arg3

end
```

## 使用
```
fakego.Parse("test.fk")
ret, err := fakego.Run("mypackage.test_return_value", 1, "2")
fmt.Println(ret)
```
