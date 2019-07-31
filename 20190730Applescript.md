#Applescript简明教程

## 理论基础
> 数据类型
* Boolean
* Number(Integer,Real)
* Text, String, Unicode text(text, string, and Unicode text will all compare as equal)
* Date
* Constant(yes，no，ask)
* List({1,1.9, "text"})
* Record({firstName:"iDoraemon", lastName:"Nathan"})

> 运算符
* +
* -
* *
* ?
* /(return Real)*
* ÷*
* \^(指数运算,return Real)
* div(舍余数,return Integer)
* mod(取余数,return Integer)

> 比较运算符
>>
含义|语法|输出 
:--|:-:|:-:
是否相等|1 = 1.0| true
 |1 is equal to 1.0| true
是否不同| 1 ≠ 1.0| false
 | 1 is not 1.0 |false
 | 1 is not equal to 1.0 |false
左边是否数值大于<br>文本长于<br>时间晚于右边<br>* 支持类型: integer，real， date，text|1 is greater than or equal 2|false
 |1 comes after 2|false
 |1 is not less than or equal to 2|false
左边是否数值小于<br>文本短于<br>时间早于右边<br>* 支持类型: integer，real， date，text|1 is less than or equal 2|true
 |1 comes before 2|true
 |1 is not greater than or equal to 2|true
前者是否以后者为开始<br>* 支持类型:text，list|"abc" starts with "a"|true
 |[1,2] starts with 1|true
 |"abc" begins with 1|false
 |[1,2] begins with 1|true
 前者是否以后者为结束<br>* 支持类型:text，list|"abc" ends with "a"|true
 前者中是否包含后者这一元素<br>* 支持类型:text，list, record|"abc" contains "a"|true
 前者中是否不含后者这一元素<br>* 支持类型:text，list, record|"abc"  does not contains "a"|false
 后者中是否包含前者这一元素<br>* 支持类型:text，list, record|"a" is in "abc"|true
 后者中是否不含前者这一元素<br>* 支持类型:text，list, record|"a" is not in "abc"|false
> 逻辑运算符
and or not
Text & xx => Text e.g "Text" & 1 => "Text1"
Record & xx => Record e.g {name:"a"} & "b" => {name:"a", «class ktxt»:"b"}
xx & xx => List e.g 1 & "b"=>{1, "b"}

> 注释
1. 单行注释 --
2. 块注释  (* *)

# 实际操作
## 查看数据类型
```applescript
class of "string"
```
## 强制数据类型转换
```applescript
"text" as list      | show as {text}
"1.99" as integer   | show as 2
"1.49" as integer   | show as 1 小数点后16会默认roundup
```
## 循环
```java
tell application "Finder"
	make new folder at desktop with properties {name:"Test"}
	repeat with a from 1 to 100
		make new folder at folder "Test" of desktop with properties {name:a as string}
	end repeat
end tell
```
## 提取字符串中的字母或单词
```
characters of "A String" | show as {"A", " ", "S", "t", "r", "i", "n", "g"}
words of "A string" | show as {"A", "string"}
characters 3 through 5 of "A String" |取第3-5个字符 show as {"S", "t", "r"}
```
## 提取Finder文件列表
```
tell application "Finder"
    files of desktop
    folders of desktop
    
    files of desktop whose name begins with "31195"
end tell
```
## 变量
```
set myResult to the result of (make new folder at desktop)
```
```
set message to "最先定义的"
run aNewScript
displayA("作为形式参数定义的")

script aNewScript
	set message to "在脚本对象里定义的"
	display dialog message
end script

on displayA(message)
	display dialog message
end displayA
```
```
set a to 1
set b to a
display dialog "赋值的结果:a=" & a & "; b=" & b
set b to 0
display dialog "修改变量b之后:a=" & a & "; b=" & b
-- list 和 Record传引用, 可使用copy将两者分开
set a to {1, 2, 3, 4, 5}
set b to 1
copy a to b
```
## 属性
```
property countTimes : 0
set countTimes to countTimes + 1
display dialog "这是第" & countTimes & "次运行本脚本"
--脚本退出后属性保持不变
```
## 流程控制
1.tell:指明脚本要控制的程序对象

> ```
    --这是简单形式
    tell front window of application "Finder" to close 
    --这是复合形式
    tell application "Finder" 
        close front window
    end tell
```

2.if:依据条件跳转

>```
    if boolean1 then statement1
    else if boolean2 then statement2
    else statement3  end if
```
3.repeat:循环
>```
repeat n times
    --do something
end repeat
repeat until boolean
    --do something
end repeat
repeat while boolean
    --do something
end repeat
repeat with loopVariable from startValue to stopValue by    stepValue 
    --do something
end repeat
```
4.Considering/Ignoring:比较文本时，指定忽略或考虑某一属性
>``` 
considering attribute1 but ignoring attribute2 
    --compare texts
end considering
```
>attribute|含义 
:--|:-:
case|大小写
diacriticals|字母变调符号(如e和é)
hyphens|连字符(-)
numeric strings|数字化字符串(默认是忽略的)，用于比较版本号时启用它punctuation|标点符号(,.?!等等，包括中文标点)
white space|空格
## 交互
```
-- 普通对话框
display dialog "contents"
```
![-w431](media/15639481066564/15643815337876.jpg)
```
-- 对话框跟随button(max size = 3)
display dialog "contents" buttons ["sure","ok","need more time"]
```
![-w418](media/15639481066564/15643815046252.jpg)
```
-- 设定默认值
display dialog "contents" buttons ["sure","ok","need more time"] default button "ok"
```
![-w421](media/15639481066564/15643816988728.jpg)
```
-- 设定标题
display dialog "contents" buttons ["sure", "ok", "need more time"] default button "ok" with title "plz choose"
```
![-w447](media/15639481066564/15643817710247.jpg)
```
-- 设定icon
display dialog "contents" buttons ["sure", "ok", "need more time"] default button "ok" with title "plz choose" with icon note
display dialog "contents" buttons ["sure", "ok", "need more time"] default button "ok" with title "plz choose" with icon stop 
display dialog "contents" buttons ["sure", "ok", "need more time"] default button "ok" with title "plz choose" with icon caution 
```

```
-- 1秒后消失
display dialog "contents" buttons ["sure", "ok", "need more time"] default button "ok" with title "plz choose" with icon note giving up after 1
```
```
--带默认输入框
display dialog "带有输入框的对话框" default answer "默认回答"
```
```
--警告框
display alert "这是一个警告" message "警告的信息" as warning
```
```
--列表选择对话框
 choose from list {"备选一", "备选二", "备选三"} with title "这是一个列表选择框" with prompt "请做 出选择!" default items {"备选二"} with empty selection allowed and multiple selections allowed
```
```
try
    --do something at risk 做一些可能导致错误的事情 
on error errText number errNum
    -- do something to handle error 做一些处理错误的事情 
end try
```
```try
	display dialog "aaa"
	tell application "Finder"
		make new folder at desktop with properties {name:"AppleScript Folder"}
	end tell
on error eText number eNum
	if (eNum = -48) then
		display dialog "发生文件错误，错误内容为:" & eText
	else if (eNum = -128) then
		display dialog "您按下了取消按钮，错误内容为:" & eText
	end if
end try
```
```
--查找当前路径
path to documents folder --返回当前用户的“文档”文件夹绝对路径alias
path to library folder from system domain --返回系统的“资源库”绝对路径alias
```
```
--/和:转换
POSIX path of alias "Macintosh HD:System:Library:CoreServices:Finder.app:" 
--返回"/System/Library/CoreServices/Finder.app/"
POSIX file "/Users/Nathan/Desktop/example.txt"
--返回file "Macintosh HD:Users:Nathan:Desktop:example.txt"
```
##文件读取
```
set myFile to alias "Macintosh HD:Users:chenqi:projects:finance-price-center:pom.xml"
read myFile for (get eof myFile)
*
get eof myFile 用来获取读取文件长度
*
```
限定|含义
:-:|:-:
from 整数|指定从哪个位置开始读取(位置指字节数)
for 整数|指定读取多少个字节
to 整数|指定读取到哪个位置为止 
before 文本|指定读取到文本所指定的关键字为止(不含本身)
until 文本|同上，但含本身
using delimiter 文本|指定分隔符读取成list类型的数据，这里参数也可是由文本组成的list
as 类型|指定读取成何种数据类型，如text,list
##文件写入
```
set aFile to alias "Macintosh HD:Users:chenqi:projects:finance-price-center:example.text" 
set fp to open for access aFile with write permission 
--打开文件 
write "abc" to fp 
--写入数据
close access fp 
--关闭文件
```
## 事件处理器(Handle)
same as function in <b>javascript</b>
```
on add(x, y)
    set answer to (x + y)
    return answer end add
    
display dialog add(1, 2) 
```

* 特殊的事件处理器:run, open, quit和idle
使用语法:on run, end run

<br>run:</br>
* 默认的事件处理器,like java main method
* 如果显示声明了run方法, 不可以有任何其他方法在handle之外

<br>open:</br>
* Drag & Drop App

<br>idle:</br>
* 空闲时的后台任务,循环,默认时间间隔是30秒,通过return n(秒)修改间隔时间

<br>quit:</br>
* 处理用户手动退出保持运行的程序时要执行的任务。其中，必须包含 有“continue quit”命令，否则程序将不可能正常退出

## 文件夹操作
```
on adding folder items to theFolder after receiving theItemList 
    --发现文件添加文件就弹出对话框，显示有几个文件添加了
    display dialog ((count theItemList) & "个项目被添加到了该文件夹) 
    as text buttons {"好", "立即查看"}
    --选择立即查看则打开文件夹
    if button returned of result = "立即查看" then 
        tell application "Finder"
            open theFolder 
        end tell
    end if
    
end adding folder items to
```
## 关键字
me :
1. path to me
2. class of me

