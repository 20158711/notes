# git
---
用户信息

	git config --global user.name "20158711"
	git config --global user.email "1280334378@qq.com"
	
	git config --list
	
	git config <key>	-->		git config user.name
	
	git init	//项目初始化
	git add .	
	git commit -m 'initial project version'
	
	git status
	git rm aa.md
	
	git log		//查看提交历史
	
	git clone https://github.com/20158711/aa.git
	
	git remote add [remote-name] git@github.com:20158711/blog.git
	git remote add origin git@github.com:20158711/blog.git
	
	git remote rename [oldname] [newname]
	git remote rm [remote-name]
	
	git fetch [remote-name]	//拉取
	git fetch origin
	
	git pull [remote-name] [branch]==git fetch + git merge
	
	git push [remote-name] [branch]
	git push origin master [-f]		//-f 强推
	git push [remote-name] [tagname]
	git push origin v1.4
	
	git tag
	git tag -a [version] [-m 'comment']
	git tag -a v1.4 -m 'my version 1.4'
	git show v1.4

回车
---

	core.autocrlf
	假如你正在 Windows 上写程序，而你的同伴用的是其他系统（或相反），你可能会遇到 CRLF 问题。 这是因为 Windows 使用回车（CR）和换行（LF）两个字符来结束一行，而 Mac 和 Linux 只使用换行（LF）一个字符。 虽然这是小问题，但它会极大地扰乱跨平台协作。许多 Windows 上的编辑器会悄悄把行尾的换行字符转换成回车和换行，或在用户按下 Enter 键时，插入回车和换行两个字符。
	Git 可以在你提交时自动地把回车和换行转换成换行，而在检出代码时把换行转换成回车和换行。 你可以用 core.autocrlf 来打开此项功能。 如果是在 Windows 系统上，把它设置成 true，这样在检出代码时，换行会被转换成回车和换行：
	
	$ git config --global core.autocrlf true
	
	如果使用以换行作为行结束符的 Linux 或 Mac，你不需要 Git 在检出文件时进行自动的转换；然而当一个以回车加换行作为行结束符的文件不小心被引入时，你肯定想让 Git 修正。 你可以把 core.autocrlf 设置成 input 来告诉 Git 在提交时把回车和换行转换成换行，检出时不转换：
	
	$ git config --global core.autocrlf input
	
	这样在 Windows 上的检出文件中会保留回车和换行，而在 Mac 和 Linux 上，以及版本库中会保留换行。
	如果你是 Windows 程序员，且正在开发仅运行在 Windows 上的项目，可以设置 false 取消此功能，把回车保留在版本库中：
	
	$ git config --global core.autocrlf false

​	
# github
---

	ssh-keygen.exe -t rsa -b 4096 -C '1280334378@qq.com'