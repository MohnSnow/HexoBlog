---
title: git ignore 文件解析
date: 2018-08-30 17:42:04
tags:
---
在git中如果想忽略掉某个文件，不让这个文件提交到版本库中，可以使用修改根目录中 .gitignore 文件的方法（如无，则需自己手工建立此文件）。这个文件每一行保存了一个匹配的规则.
例如：
```
# 此为注释 – 将被 Git 忽略
*.a       # 忽略所有 .a 结尾的文件
!lib.a    # 但 lib.a 除外
/TODO     # 仅仅忽略项目根目录下的 TODO 文件，不包括 subdir/TODO
build/    # 忽略 build/ 目录下的所有文件
doc/*.txt # 会忽略 doc/notes.txt 但不包括 doc/server/arch.txt
```

规则很简单，不做过多解释，但是有时候在项目开发过程中，突然心血来潮想把某些目录或文件加入忽略规则，按照上述方法定义后发现并未生效，原因是.gitignore只能忽略那些原来没有被track的文件，如果某些文件已经被纳入了版本管理中，则修改.gitignore是无效的。那么解决方法就是先把本地缓存删除（改变成未track状态），然后再提交：
```
git rm -r --cached .
git add .
git commit -m 'update .gitignore'
```

新的项目需要配置一下,否则不会计入贡献
```
 这个是全局的：
 git config --global user.name "MohnSnow"
 git config --global user.email "mengdexin_work@163.com"
 非全局的：
 git config user.name "MohnSnow"
 git config user.email "mengdexin_work@163.com"
```