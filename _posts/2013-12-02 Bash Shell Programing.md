
# misc
To run a script, we need the excuatable permission

chmod u+x shellScript

chmod a+x shellScript

shebang the first line: #!/bin/bash 

PATH=PATH:~/bin

Use `type` command to verify a command.

`type cp`

# variables

变量名是大小写敏感的；Predfined的变量都是大写的。

filename="sometext" touch $filename
注意=号两遍不能有空格

在双引号里可以有变量名，如果要输出变量内容，一定要使用echo，不能直接输入变量名敲回车

date=$(date)
read -p "your note: " note

topic=$1

filename=“${topic}notes.txt”

echo $date: $note >> ~/$filename

use $HOME instead of tidle

调试技巧，shebang调整成：#!/bin/base -x

或者在某一行使用set -x，然后再通过 set +x来释放调试功能

set -e 如果有一行命令有问题就退出

if mkdir a;then echo "ok";else echo "error";fi

0 means success

注意空格很重要

[[ expression ]] 验证是否为空

[[ ! expression ]]

[[ $str = "something" ]] str equal "something"

[[ $str="something" ]] 如果等号两遍没有空格的话总是返回true

[[ -e $filename ]] 判断是否存在

[[-d $dirname]] 判断是否为目录

exit 0


if [[]]; then

fi

也可以使用 test command

[[ arg1 -eq arg2 ]],[[ arg1 -gt arg2 ]],[[ arg1 -lt arg2 ]],[[ arg1 -ne arg2 ]]
And,Or,Not

[[ $# -eq 1 && $1="foo"]]
[[ $a||$b ]]

$# 脚本参数的数量

$? 最后一行命令的退出状态

${#var}

"help test" 和 "help [[" 用来查询帮助文档


output: echo,printf，printf（默认不会输出新行，并且可以对输出内容做format）

input :read

设置空： answer=

IFS=: read a b,IFS指的是设置参数的间隔


0：标准输入 /dev/stdin
1：标准输出 /dev/stdout
2：错误 /dev/stderr

/dev/null 回收不用的变量

cmd 2>/dev/null 丢弃所有的ucow

for var in WORDS; do 
	
;; code to be repeated

done



while read -r; do

echo $REPLY

done


declear -i p 将p定义为整形变量 $((++x)) 
((..))可以在if语句中使用
Read-only attribute: declear -r constant = "some value"


sum(){
	
	return $(($1+$2))

}

start_with_a(){
	[[ $1 ==[aA]* ]];
	return $？
}

if start_with_a ax; then
	echo "yup"
else
	echo "nope"
fi

declear -A array

fun(){...}

${#var}:length of $var

${}

touch {a..c}.txt

[[ hello = h*o ]] ->true

[[ hello = "h*o" ]] -> false

=~匹配正则表达式

nice scriptname

退出session的时候也在script继续保持运行状态

nohup stillhere > log &
