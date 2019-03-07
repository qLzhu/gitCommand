```
git help -a                                               # 显示Git全部命令
git help "xxx"                                            # 获取某个命令的帮助信息
git help config                                           


配置个人信息
=
--system                                                  # 系统级 etc/gitconfig
--global                                                  # 用户级 ~/.gitconfig 或 ~/.config/git/config
--local                                                   # 目录级 .git/config

git config --global user.name "xxx"                       # 设置提交代码时的用户名（用户级别）
git config --global user.email "xxx@xxx.com"              # 设置邮箱

git config --list                                         # 显示当前的Git配置
git config --list --global                                # 显示用户级Git配置

git config user.name                                      # 查看当前使用的用户名
git config --get user.name                                #
git config user.name "xxx"                                # 更改用户名(默认修改当前目录里的配置，即目录级)
git config --local user.name "xxx"
git config --global --unset user.name "xxx"               # 删除某个用户名

客户端基本配置
=
git config -e "--global"                                  # 编辑用户级Git配置文件
git config --global core.editor "vim"                     # 修改默认的编辑器
git config --global commit.template ~/.xxx.txt            # 设置提交时的信息模版
git config --global core.excludesfile ~/.gitignore_global # 设置全局忽略文件

Git 中的着色
=
git config --global color.ui true                         # git status 等命令自动着色
git config --global color.status auto
git config --global color.diff auto
git config --global color.branch auto
git config --global color.interactive auto


创建本地仓库
=
git init                                                  # 初始化此仓库
git init "xxx"                                            # 新建并初始化仓库

git clone "Remote SSH/HTTPS url"                          # 克隆远程仓库到本地
git clone "Remote SSH/HTTPS url" "Remote name"            # 克隆远程仓库到本地并更名

添加文件
=
git add .                                                 # 所有文件添加到 index (暂存区)
git add --all
git add "xxx"                                             # 单个文件添加到暂存区
git add "x... ..."                                        # 多个文件添加到暂存区
git reset HEAD "xxx"                                      # 取消这个文件的暂存
git checkout -- "xxx"                                     # 撤销对文件的修改 

移动/改名文件
=
git mv "xxx" "New xxx"                                    # 更改文件名
git mv "xxx" "New location"                               # 把该文件或目录移动到指定位置

删除文件
=
git rm "xxx"                                              # 删除工作区内的某个文件，并把此次删除操作添加到暂存区
git rm -r "xxx"                                           # 递归删除，一般用于删除目录
git rm --cached "xxx"                                     # 停止追踪此文件，不会删除
git checkout -- "xxx"                                     # 恢复误删文件的最新版本
git ls-files --deleted                                    # 查看删除的文件(git rm 删除的不显示)

提交暂存区的内容到历史区
=
git commit                                                # 使用默认的编辑器编辑提交内容，保存即可提交
git commit -m "message"                                   # 单行提交
git commit "file" -m "message"                            # 提交暂存区内的指定文件
git commit -am "message"                                  # 提交已追踪并有变化的文件
git commit -amend                                         # 使用这次的 message 替代上一次的提交
git commit -amend -m "message"                            # 此次提交替换上次的提交记录，暂存区有变化的文件也会随本次提交
git commit -amend "file" -m "message"                     # 暂存区内指定的文件随本次一起提交，替换上次提交记录

查看信息
=
git status                                                # 显示有变更的文件

查看历史提交记录
=
git log                                                   # 显示当前分支的版本历史
git log --stat                                            # 显示commit历史，以及每次commit发生变更的文件
git log --reverse                                         # 反着显示提交历史
git log --no-merges                                       # 显示除合并以外的提交
git log -5                                                # 显示最近五次的提交
git log --oneline                                         # 单行显示提交记录
git log -5 --oneline                                      # 单行显示最近5次的提交记录
git log --until={2019-01-03}                              # 显示2019年1月3日之前的提交记录，也可以使用 --before
git log --before=2.day --oneline                          # 显示两天前的提交
git log --since={2019-01-01}                              # 显示2019年1月1日之后的提交记录，--after (使用没反应)
git log --since={2019-01-01} --until={2019-01-03}         # 显示2019年1月1日到1月3日之间的提交记录
git log --abbrev-commit                                   # 以简短形式显示 SHA-1 
git log --author="xxx"                                    # 显示指定作者相关的提交
git log --committer="xxx"                                 # 显示指定提交者相关的提交
git shortlog -sn                                          # 显示所有提交过的用户，按提交次数的多少排序
git blame "xxx"                                           # 显示指定文件在什么时间修改过
git log --grep "xxx"                                      # 显示跟xxx关键词有关的提交
git log -S"function_name"                                 # 跟文件内某个函数有关的添加删除等提交记录
git log --pretty=format:"%cn %s" --graph                  # 以ASCII图形形式展现历史记录中的提交者和提交说明
-----------------------------------------
%H  提交对象（commit）的完整哈希字串
%h  提交对象的简短哈希字串
%T  树对象（tree）的完整哈希字串
%t  树对象的简短哈希字串
%P  父对象（parent）的完整哈希字串
%p  父对象的简短哈希字串
%an 作者（author）的名字
%ae 作者的电子邮件地址
%ad 作者修订日期（可以用 --date= 选项定制格式）
%ar 作者修订日期，按多久以前的方式显示
%cn 提交者（committer）的名字
%ce 提交者的电子邮件地址
%cd 提交日期
%cr 提交日期，按多久以前的方式显示
%s  提交说明
-----------------------------------------

远程仓库
=
git remote -v                                              # 查看此目录都连接了那些远程仓库
git remote show origin                                     # 查看 origin 远程仓库的详细信息
git remote add "xxx(origin)" "git@github.com:xxx/xxx.git"  # 添加远程仓库用于（push/pull/fetch）
git remote rename "origin" "xxx"                           # 重命名远程仓库的名称
git remote rm "origin"                                     # 删除远程仓库

git fetch                                                  # 下载远程仓库的所有变动（需要手动把变动的文件跟本地合并）
git fetch "xxx(origin)" "xxx"                              # 下载远程仓库指定分支的变动
git fetch --prune                                          # 获取所有原创分支并清除服务器上已删掉的分支
git pull                                                   # 下载远程仓库的所有变动并与本地合并

git push                                                   # 推送所有分支到远程仓库
git push origin master                                     # 把当前的分支推送到远程仓库指定分支上
git push origin master --force                             # 强行推送当前分支到远程仓库，即使有冲突
git push -u origin master                                  # git remote add 关联远程仓库后第一次提交使用
```