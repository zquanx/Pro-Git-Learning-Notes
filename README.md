# Git
## 起步
### 关于版本控制
* 集中化的版本控制系统
    * 英文
        * Centralized Version Control Systems，简称 CVCS
    * 代表产品
        * CVS
        * Subversion
        * Perforce
    * 缺点
        * 中央服务器单点故障
            * 无法提交更新
            * 丢失数据（主要是整个变更历史）
* 分布式版本控制系统
    * 英文
        * Distributed Version Control System，简称 DVCS
    * 代表产品
        * Git
        * Mercurial
        * Bazaar
        * Darcs
    * 解决问题
        * 客户端保留代码仓库完整镜像
        * 即使无法联网也可以提交更新
### 三个工作区域
* Git仓库
    * .git directory (Repository)
* 工作目录
    * Working Directory
* 暂存区域
    * Staging Area
* 关系图示
    * 
### 为什么推荐使用命令行
* 只有在命令行模式下你才能执行 Git 的 所有 命令，而大多数的 GUI 软件只实现了 Git 所有功能的一个子集以降低操作难度
* 如果你学会了在命令行下如何操作，那么你在操作 GUI 软件时应该也不会遇到什么困难，但是，反之则不成立
* 由于每个人的想法与侧重点不同，不同的人常常会安装不同的 GUI 软件，但 所有 人一定会有命令行工具
### 安装
* https://git-scm.com/book/zh/v2/%E8%B5%B7%E6%AD%A5-%E5%AE%89%E8%A3%85-Git
### 初次运行前的配置
* git config
    * 三个级别
        * --system
            * /etc/gitconfig
        * --global
            * ~/.gitconfig
            * ~/.config/git/config
        * 当前使用仓库的Git目录中的config文件
            * .git/config
    * 设置用户名称和邮件地址
        * git config --global user.name "Blue"
        * git config --global user.email blue@example.com
    * 查看配置信息
        * git config --list
        * git config <key>
## Git基础
### 获取Git仓库
* 在现有目录中初始化仓库
    * git init
    * git add .
    * git commit  -m 'init'
* 克隆现有仓库
    * git clone [url]
### 记录每次更新到仓库
* 检查当前文件状态
    * 命令
        * git status
        * git status -s
            * M（右边）
                * 修改了，未放入暂存区
            * M（左边）
                * 修改了，已放入暂存区
            * MM
                * 修改了并添加到暂存区后，又修改了
            * A
                * 新添加到暂存区的文件
            * ??
                * 新添加、未跟踪文件
    * 状态
        * nothing to commit , working directory clean
            * 说明
                * 当前工作目录相当（干净）
                * 所有已跟踪文件在上次提交后都（未更改过）
                * 当前目录下没有出现任何处于（未跟踪）状态的新文件
        * Untracked files
            * 未跟踪的文件
                * 意味着Git在之前的快照（提交）中没有这些文件
        * Changes to be committed
            * 已暂存状态
        * Changes not staged for commit
            * 已跟踪文件的内容发生了变化，但还没有放到【暂存区】
        * Unmerged paths
            * 包含合并冲突而处于未合并 (unmerged)状态的文件
* git add
    * 功能
        * 1、开始跟踪新文件
        * 2、把已跟踪的文件放到暂存区
        * 3、合并时把有冲突的文件标记问已解决状态
    * 理解为
        * 添加内容到下一次提交中
* 忽略文件
    * 格式规范
        * 所有空行或者以#开头的行都会被Git忽略
        * 可以使用标准的glob模式匹配
            * glob模式
                * 指shell所使用的简化了的正则表达式
                    * 星号 (*) 匹配0个或多个任意字符
                    * [abc] 匹配任何一个列在方括号中的字符
                    * 问号 (?) 只匹配一个任意字符
                    * [0-9] 匹配0到9之间的数字
                    * 两个星号 (**) 匹配任意中间目录
        * 匹配模式可以以 (/) 开头防止递归
        * 匹配模式可以以 (/) 结尾指定目录
        * 加上惊叹号 (!) 取反，可以忽略指定模式以外的文件或目录
    * tip
        * GitHub 有一个十分详细的针对数十种项目及语言的 .gitignore 文件列表，你可以在 https://github.com/github/gitignore 找到它.
* 查看已暂存和文暂存的【修改】
    * 命令
        * git diff
            * 查看【未暂存】的文件（更新部分）
        * git diff --cached/staged
            * 查看【已暂存】的文件（更新部分）
    * 工具
        * git difftool --tool-help
            * 查看系统支持哪些Git Diff插件
* 提交(git commit)
    * git commit
        * 这种方式会启动文本编辑器以便输入本次提交的说明
        * 默认会启用 shell 的环境变量 $EDITOR 所指定的软 件
        * 使用git config --global core.editor 命令设定你喜欢的编辑软件
    * -v
        * 这会将你所做的改变的 diff 输出放到编辑 器中从而使你知道本次提交具体做了哪些修改
    * -m
        * 将提交信息与命令放在同一行
    * -a
        * 【跳过】使用暂存区域
            * Git 就会自动把所有已经跟踪过的文件暂存 起来一并提交
* 移除文件
    * git rm
    * git rm -f
        * 如果删除之前修改过并且已经放到暂存区域的话
    * git rm --cached
        * 让文件保留在磁盘，但是并不想让 Git 继续跟踪
* 移动文件/【重命名】
    * git mv <file>
### 查看提交历史
* git log
    * -p
        * 显示每次提交的内容差异
    * -2
        * 仅显示最近2次提交
    * --stat
        * 看到每次提交的简略的统计信息
    * --pretty
        * =onelie
            * 将每个提交放在一行显示
        * =short
        * =full
        * =fuller
            * 查看每次提交详细信息
        * =format
            * =format:"%h -  %an,%ad : %s"
                * 常用选项
                    * %h
                        * 提交对象的简短哈希字串
                    * %an
                        * 作者的名字
                    * %ad
                        * 作者修订日期
                    * %cd
                        * 提交日期
                    * %s
                        * 提交说明
    * --graph
        * 形象展示
    * --since/after
        * 查出最近两周的提交
            * --since=2.weeks
        * 具体的某一天"2008-01-15"
    * --until/before
        * 某个日期之前的提交
    * --author
        * 指定作者的提交
    * --committer
        * 指定提交者的提交
    * --grep
        * 包含指定关键字的提交
    * --no-merges
### 撤销操作
* 重新提交
    * git commit --amend
        * 漏掉了文件没有添加
        * 修改提交信息
* 取消暂存的文件
    * git reset HEAD <file>...
* 撤销对文件的修改
    * git checkout -- <file>
### 远程仓库的使用
* 查看远程仓库
    * git remote
        * -v
            * 【读写】远程仓库使用的 Git 保存的简写与其对应的 URL
* 添加远程仓库
    * git remote add <shortname> <url>
* 从远程仓库拉取
    * git pull
* 推送到远程仓库
    * git push [remote-name] [branch-name]
* 查看某个远程仓库
    * git remote show [remote-name]
### 打标签
* 列出标签
    * git tag
* 创建标签
    * 轻量标签
        * git tag [tag-name]
    * 附注标签
        * git tag -a [tag-name] -m "comment"
* 标签详情
    * git show V1.4
* 后期打标签
    * git tag -a [tag-name] [commit-id]
* 共享标签
    * git push origin [tag-name]
* 删除标签
    * 本地
        * git tag -d [tag-name]
    * 远程
        * git push <remote> :refs/tags/[tag-name]
### Git别名
* 命令样例
    * git config --global alias.unstage 'reset HEAD --'
## Git分支
### 分支新建与合并
* 查看所有分支
    * git branch
        * -v
            * 查看每一个分支的最后一次提 交
        * --merged
            * 查看已经合并到当前分支的分支
        * --no-merged
            * 查看未合并到当前分支的分支
* 分支创建
    * git branch [branch-name]
* 分支切换
    * git checkout [branch-name]
* 合并分支
    * git merge
        * 例子 : 将test分支合并到master
            * 1、git checkout master
            * 2、git merge test
* 删除分支
    * git branch -d [branch-name]
### 分支开发工作流
* 长期分支
* 特性分支
* 远程分支
### 远程分支
* 推送
    
    * git push [remote] [branch]
* 新建远程分支
    * 1、git checkout -b [branch]
    * 2、git push [remote] [branch]
* 跟踪分支
    * 本地分支名和远程分支名保持一致
        
        * git checkout --track [remotename]/[branch]
    * 将本地分支与远程分支设置为不同名字
        
        * git checkout -b [branch] [remotename]/[branch]
    * 修改正在跟踪的上游分支
        
    * -u 或 --set-upstream-to
    * 上游快捷方式
     * > 当设置好跟踪分支后，可以通过 @{upstream} 或 @{u} 快捷方式来引用它。 所以在 master 分支时并且它正在跟踪origin/master时，如果愿意的话可以使用git merge @{u}来取 代git merge origin/master
    
* 查看设置的所有跟踪分支
        * git branch -vv
         * > 需要重点注意的一点是这些数字的值来自于你从每个服务器上最后一次抓取的数据。 这个命令并没有连接服务 器，它只会告诉你关于本地缓存的服务器数据。 如果想要统计最新的领先与落后数字，需要在运行此命令前抓 取所有的远程仓库。可以像这样做:$ git fetch --all; git branch -vv
    
* 拉取
    * git fetch
        * 从服务器上【抓取】本地没有的数据时，它并【不会修改】工作目录中的内容
    * git pull
        * 查找当前分支所跟踪的服务器与分支，从服务器上【抓取数据】然后尝试【合并】入那个远程分支
* 删除远程分支
    
    * git push [remote] --delete [branch]
### 变基
## 服务器上的Git
### 协议
* 本地协议
    * 本质
        * 远程版本库就是硬盘内的一个目录
    * 命令
        * git clone /opt/git/project.git
        * git clone file:///opt/git/project.git
    * 增加一个本地版本库到现有的 Git 项目
        * git remote add local_proj /opt/git/project.git
* HTTP协议
    * 命令 
        * git clone https://example.com/gitproject.git
* SSH协议
    * 命令
        * git clone user@server:project.git
*  Git协议
### 生成SSH公钥
* 存放目录
    * ~/.ssh/id_rsa.pub
* 生成命令
    * ssh-keygen
### GitWeb
* what?
    
    * 一个基于网页的简易查看器
* 命令
    * 打开
        * git instaweb --httpd=webrick
         * > 这个命令启动了一个监听 1234 端口的 HTTP 服务器，并且自动打开了浏览器

    * 停止
        
        * git instaweb --httpd=webrick --stop
## 分布式Git
### 分布式工作流程
* 集成管理者工作流
* > Git 允许多个远程仓库存在，使得这样一种工作流成为可能:每个开发者拥有自己仓库的写权限和其他所有人仓 库的读权限。 这种情形下通常会有个代表“官方”项目的权威的仓库。 要为这个项目做贡献，你需要从该项目 克隆出一个自己的公开仓库，然后将自己的修改推送上去。 接着你可以请求官方仓库的维护者拉取更新合并到 主项目。 维护者可以将你的仓库作为远程仓库添加进来，在本地测试你的变更，将其合并入他们的分支并推送 回官方仓库。

    * 1. 项目维护者推送到主仓库。
    * 2. 贡献者克隆此仓库，做出修改。
    * 3. 贡献者将数据推送到自己的公开仓库。
    * 4. 贡献者给维护者发送邮件，请求拉取自己的更新。
    * 5. 维护者在自己本地的仓库中，将贡献者的仓库加为远程仓库并合并修改。
    * 6. 维护者将合并后的修改推送到主仓库。
* 司令官与副官工作流
* > 这其实是多仓库工作流程的变种。 一般拥有数百位协作开发者的超大型项目才会用到这样的工作方式，例如著 名的 Linux 内核项目。 被称为副官(lieutenant)的各个集成管理者分别负责集成项目中的特定部分。 所有这 些副官头上还有一位称为司令官(dictator)的总集成管理者负责统筹。 司令官维护的仓库作为参考仓库，为所有协作者提供他们需要拉取的项目代码。

    * 1. 普通开发者在自己的特性分支上工作，并根据 master 分支进行变基。 这里是司令官的 master 分支。
    * 2. 副官将普通开发者的特性分支合并到自己的 master 分支中。
    * 3. 司令官将所有副官的 master 分支并入自己的 master 分支中。
    * 4. 司令官将集成后的 master 分支推送到参考仓库中，以便所有其他开发者以此为基础进行变基。
### 向一个项目贡献
* 提交准则
* > 在我们开始查看特定的用例前，这里有一个关于提交信息的快速说明。 有一个好的创建提交的准则并且坚持使 用会让与 Git 工作和与其他人协作更容易。 Git 项目提供了一个文档，其中列举了关于创建提交到提交补丁的若 干好的提示——可以在 Git 源代码中的 Documentation/SubmittingPatches 文件中阅读它

    * git diff --check
        * 检查空白错误
         * > 根据 git help diff 的描述，结合下面给出的图片，空白错误是指行尾的空 格、Tab 制表符，和行首空格后跟 Tab 制表符的行为


*XMind: ZEN - Trial Version*
