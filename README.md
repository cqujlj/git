# git常用命令
##### 1、创建仓库、配置
     (1) mkdir dirName //创建空目录
     (2) git init // 初始化 在工作路径上创建主分支--> 把创建的空目录变成可管理的仓库
     (3) git config user.name "your name"  //配置用户名
     (4) git config user.eamil "youeamil@xxx.com.."  //配置用户邮箱
     (5) ssh-keygen -t rsa -C "youremail@example.com"  // 创建SSH Key
     (6) git config user.name //查看用户名
     (7) git config user.email //查看用户邮箱
##### 2、克隆远程仓库
     (1) git clone https://github.com/cqujlj/React.git // 克隆远程仓库
        将整个仓库复制下来，不需要本地文件夹设置为仓库，直接在本地生成远程仓库的拷贝；可以直接push
     (2) git pull // 将远程主机的最新内容拉下来后直接合并 git pull = git fetch + git merge
     (3) git fetch是将远程主机的最新内容拉到本地，用户在检查了以后决定是否合并到工作本机分支中
        需要先git init 将本地文件夹变成仓库；要先执行git remote add origin命令来指定源，才能push
##### 3、从工作区存入暂存区：git add 
    (1) git add fileName // 将某个文件存入暂存区
    (2) git add fileName1 fileName2 fileName3 //把多个文件存入暂存区
    (3) git add . // 将所有文件提交到暂存区
##### 4、从暂存区提交到仓库：git commit
    git commit -m "提交的备注信息"  // 提交到仓库
       若已经有若干文件放入仓库，再次提交可以不用git add和git commit -m "备注信息" 这2步， 直接用
    git commit -m "备注信息" // 将内容放至仓库 "备注信息"
    git status // 查看状态
##### 5、将本地仓库的文件推到远程仓库
    git push <远程主机名> <本地分支名>  <远程分支名>
    (1) git push origin master：refs/for/master    //将本地的master分支推送到远程主机origin上的对应master分支， 
        origin 是远程主机名，第一个master是本地分支名，第二个master是远程分支名
    (2) git push -u origin master     //如果当前分支与多个主机存在追踪关系，则可以使用 -u 参数指定一个默认主机
    (3) git push origin master    //将本地分支推送到与之存在追踪关系的远程分支（通常两者同名），如果该远程分支不存在，则会被新建
##### 6、删除/回退
    删除放入暂存区文件的方法（已commit后）
    git rm file  // 从git版本库中删除文件  从commit后撤回到add后
    git commit -m "delete file" // 提交删除
    
    git reset HEAD^ --hard    // 删除后 可以用git rm 文件名再回撤一步
    git reset HEAD~2 --hard     // 回撤2步
    git reset --files     // 从仓库回撤到暂存区
    git reset HEAD    // 回撤暂存区内容到工作目录
    git reset HEAD --soft     //回撤提交到暂存区
    git reset HEAD --hard     // 回撤提交 放弃变更 (慎用)
    git reset HEAD^      // 回撤仓库最后一次提交
    git reset --hard commitid     // 回撤到该次提交id的位置
    git push -f -u origin 分支名   //所有内容都回撤完了 将回撤后的操作强制推送到远程分支
##### 7、分支
    git branch 分支名   // 新建分支
    git branch    // 查看当前所有分支
    git branch -r // 列出远程分支(远程所有分支名)
    git branch -a // 查看远程分支(列出远程分支以及本地分支名)
    git branch -d 分支名 // 删除分支
    git branch -D 分支名 // 强制删除 若没有其他分支合并就删除 d会提示 D不会
    git branch -m 旧分支名 新分支名 // 修改分支名
    git checkout 分支名    // 切换分支
    git checkout -b 分支名  // 创建并切换分支
    git checkout commitId 文件名（文件路径下的文件名） 还原这个文件到对应的commitId的版本
    
    git merge 分支名 // 把该分支的内容合并到现有分支上
    git fetch // 更新remote索引
    git push -u origin 分支名 // 将本地分支推送到origin主机，同时指定origin为默认主机，
    后面就可以不加任何参数使用git push 也可解决 git建立远程分支关联时出现fatal ... upstram的问题
    关于分支的一些理解：
         (1) 在每次提交时，Git都把他们串成一条时间线，这条时间线就是一个分支； master：主分支；
          HEAD指针严格来说指向提交，而不是master； master指向提交，因此HEAD指向当前分支
         (2) 每有一次提交，master分支都会向前移动一步，因此master分支会越来越大
         例：
          创建分支：git branch dev 此时工作区没有任何变化
          切换到dev分支：git checkout dev,此时对工作区进行修改，然后进行一次新的commit；dev指针向前移动一步，master指针不变
          在dev上的工作完成了，就可以把dev合并到master上；git checkout master；git merge dev
          合并完分支后，可以删除dev分支，git branch -d dev
##### 8、查看暂存区，工作区，仓库的差异
    git diff    // 查看变更 工作区与暂存区的差异比对
    git diff --cached    // 暂存区与提交版本的差异
    git diff HEAD    // 工作区与仓库中最后一次提交版本的差别
##### 9、查看状态、信息 
    git status    // 查看状态
    git log -n    // 查看前n次的提交记录
##### 其他：
###### 文件相关指令
    touch a    // 创建一个a文件
    echo xxxx >> a    // 把xxxxx这个内容放入a文件
    cat a     // 打开a文件 读取出a文件中的内容
    rm 文件名    // 删除文件
###### 查看文件夹
    ls     // 查看当前路径下面的所有文件名
    ls 文件夹名      // 查看对应文件夹中的内容
    ls -l     // 拉出最近git提交记录以及对应修改的文件名
    ls -l -a    // 拉出最近git提交记录以及对应修改的文件名，隐藏的文件也会显示
###### 路径相关命令
    pwd     // 打印当前工作路径
    cd ~    // 将工作路径快速切换到root
    cd -    // 将工作路径切换到上一状态
    cd ..     // 切回到上一个工作路径
    cd 文件夹名     // 进入某个目录
    cd /    // 进入根目录
###### vim相关指令
    vim 文件名 // 新建一个文件
    i 插入内容
    按下esc :wq 保存并退出
    按下esc :q 直接退出
    vim 模式下 文件中#号开头的为注释
