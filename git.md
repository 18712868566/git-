###Welcome to use MarkDown
###本例详见 e/githubGlobal/gitTHT , e/githubGlobal/gitFZCT  (FZCT分支冲突)
###Git 基本命令

	ls -a   ----------------------   查看包含文件
	   
  	open <filename> ---------------  打开某某文件 mac版本支持, win7 不支持改命令
  	
  	git touch index.html ----------  创建一个文件 mac版本支持, win7 不支持改命令
  	
  	git diff ---------------------  比较文件用
  	
  	git log -p	-------------        比较提交用 
  	 
	git log --oneline	------------- oneline标记把每一个提交压缩到了一行中 它默认只显示提交ID和提交信息的第一行
	
	git log --stat ------------------  stat选项显示每次提交的文件增删数量  （注意：修改一行记作增加一行且删去一行），当你想要查看提交引入的变化时这会非常有用

	git log -p	--------------------- 如果你想知道每次提交删改的绝对数量，你可以将-p选项传入git log。这样提交所有的删改都会被输出
	
	git shortlog --------------------- 它把每个提交按作者分类，显示提交信息的第一行。这样可以容易地看到谁做了什么
	
		例如:
			git shortlog 
				lixuefeng (3):
			      log1
			      log2
			      log3

	git status -s		-----------------	add 之后 commit 之前 文件 的状态  
		M  1.txt
	
	
###回到过去
	git commit --amend --no-edit  ----------------  当文件更改或者有修改时,提交的时候, 不新增提交( change ),在上一次提交的基础上,再次提交 

	git reset <filename>		  ------------------  	当 add 操作之后, 没有 commit 之前 退回到 add 之前的操作
	
	git reset --hard HEAD/HEAD^/HEAD~100/(之前版本的id号) 0c54827		  ------------------  	当 add 操作之后, 也执行 commit 后 退回到  之前的版本
	
	
###单个文件回到过去
	
	git checkout (id号) -- <filename>  ----- git checkout 0c54827 -- index.html  	 


###去到未来	
	git reflog  ------  查看我的每一步操作 然后在 Git reset (id 号)
	
		0c54827 HEAD@{0}: reset: moving to 0c54827
		a4958f1 HEAD@{1}: reset: moving to HEAD^
		ad73b2a HEAD@{2}: commit (amend): log3
		3d7b612 HEAD@{3}: commit: log3
		a4958f1 HEAD@{4}: commit: log2
		0c54827 HEAD@{5}: commit (initial): log1


	$ git reset --hard ad73b2a              			穿越--回到这一步
	$ git reset --hard HEAD@{0}	  						穿越--回到这一步





###分支

	git log --oneline --graph	-------------------         分支视图
	
	git branch <name>  ----------------------               新建一个分支
	
	git checkout -b <name> 		-----------------------     创建一个分支,并且移动到新建分支  
	
	git checkout <name>  ----------------------             切换分支
	   
	git branch -d <name> 	------------------------        删除分支
	
	git commit -am 'log4 in dev'	------------------      add + commit 步骤合并写法(注意:这种写法只适用于 文件已存在git管理库中)
	
	git merge <name> 		-----------------------         合并某某分支到当前分支
	
	git merge --no-ff -m 'keep merge info' <name> 		-----------------------  合并某某分支到当前分支,并且显示提示文本
	
		git log --oneline --graph    //视图结构如下
			*   d54093d keep merge info
			|\									//在这里我们把 dev 分支合并到了主分支 
			| * e7ab9d1 log4 in dev			
			|/									//在这里我们建立了一个 dev 的分支
			* e61e6fa back to change 1 and add commit fot index.html
			* ad73b2a log3
			* a4958f1 log2
			* 0c54827 log1

	
###分支冲突

	CONFLICT  //冲突
		
		当 master 中的文件 所有修改
		并且 dev(分支) 中的文件也有所修改时	
		我们 在 master 上 merge dev 时 
		
			会出现冲突 
			
			这时需要人工合并  详见 修改文件本身
			
			<<<<<<< HEAD	//当前修改部分
			this is master
			=======
			this is dev
			>>>>>>> dev		// dev 分支修改部分
			
			人工合并冲突部分之后
			在 git commit -ad 'user tips'
			git log --oneline --graph    //查看分支视图
			
			*   412c6b5 solve conflict			合并之后记录信息
			|\
			| * 234e0e8 change this is dev   	--->合并这两个commit
			* | 4a485ef change master        	--->
			|/
			* 485cacd change 1

		  
	REBASE  //分支冲突
			
		
	
	
#log 高级用法
	参考链接: http://www.360doc.com/content/16/0519/10/10058718_560380335.shtml		