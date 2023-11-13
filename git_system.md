# git系统学习

## 1.配置用户信息

```
# 其中--global 表示全局配置对所有仓库生效  --system为系统配置，对所有用户生效
git config --global user.name "zlovety"
git config --global user.email zlovety@gmail.com
git config --global credential.helper store    # 保存用户名和密码，后续就不用输入了
git config --global --list    # 查看配置的用户名和邮箱
```

##  2.创建仓库

```
git init my-repo    # 在当前目录下新建my-repo文件夹作为我们的仓库
git clone
```

## 3.添加文件和删除

```
git status    # 查看当前目录下文件的状态
git add
git commit -m "注释"    # 也可以使用git commit -am "注释"   来直接完成添加和提交
git log    # 查看提交的记录
git log --oneline    # 只显示一行的简洁提交记录
git ls-files    #查看仓库状态
git rm other.log    # 将other.log从版本库和工作区都删除
git rm --cached other.log    # 将other.log从版本库中删除，但不删除工作区的文件
```

## 4.回退

<img src="C:/Users/Administrator/AppData/Roaming/Typora/typora-user-images/image-20231112095241057.png" width="600" height="300"/>

```
# 其中HEAD^ 表示上一个版本id
# 若在回退时不小心用了--hard导致东西都没了，则可使用git reflog 查看所有操作的id，之后再使用下面指令就可以了
git reset --hard 之前版本id
```

## 5. 查看两个文件之间的差异

```
git diff    # 默认比较工作区和暂存区差异
git diff HEAD    # 比较工作区和版本库的差异
git diff --cached    # 比较暂存区和版本库之间的差异
git diff HEAD~ HEAD    # 比较上一个版本和当前版本的差异 ~和^一样  HEAD~2表示HEAD之前的两个版本
git diff HEAD~ HEAD file3.txt    # 只查看file3.txt文件的版本差异
```

## 6. 忽略某个文件

```
vim .gitignore
# 在.gitignore文件中添加想忽略的文件，可以使用通配符如 *.log
# 若想忽略某个文件夹，在.gitignore文件中增加一行 文件夹名称/
```

## 7. 与远程github仓库关联

```
# 第一步在本地生成密钥
cd     # 回到本地根目录
cd .ssh
ssh-keygen -t rsa -b 4096    # 若第一次生成则可以直接回车，会自动生成id_rsa的密钥，若之前生成过，则输入个新名字test再回车
# 生成之后则有两个文件 test 和 test.pub  打开test.pub复制公钥，打开github的设置添加ssh密钥
# 若不是第一次生成密钥，则还需创建一个config文件,即访问github.com时用test密钥
tail -5 config
# github
Host github.com
HostName github.com
PreferredAuthentications publickey
IdentityFile ~/.ssh/test
```

```
# 若本地已有仓库，想直接关联到远程仓库中
git remote add origin git@github.com:zzzcccxx/myfirst.git
# 查看远程关联
git remote -v
# 也可以添加多个远程
git remote add gitlab git@gitlab.com:example/111.git
# 推到远程仓库 推到origin的仓库网址下 本地分支名称为main，远程分支为main
git push -u origin main:main
# push默认push到origin远程,想推到别的远程则需在push后添加
git push gitlab main
```

```
# 拉取 git pull <远程仓库名> <远程分支名>:<本地分支名>
git pull origin
```

## 分支

```
# 创建分支，只创建不切换
git branch 分支名

# 切换分支
git checkout 分支名
git switch 分支名

# 合并分支
git merge 分支名    # merge后的分支名表示即将被合并的分支，当前所在分支为合并到的分支。如想合并dev到main上，先切换到main分 # 支上再使用 git merge dev。分支合并后不手动删除还是存在的

# 查看分支图也可通过
git log --graph --oneline --decorate --all

# 删除分支
git branch -d 分支名
# 若没合并就要删除 则使用
git branch -D 分支名
```

## 解决冲突

```
# 若在合并时出现自动合并失败可以使用 git status 和git diff来查看冲突文件和冲突内容
vim 冲突的文件名    # 修改后在 git add 和git commit -m ""，注意commit后会直接合并，若不想继续合并，则可以使用
git merge --abort


# 第二种合并方法就是
git rebase dev  # 看geekhour哔哩哔哩
```



