## 1. 初始化

```
git init
```

## 2. 提交

```
git add .
git commit -m "xxxxx"
```

## 3. 创建分支

```
git branch dev01
```

## 4. 切换分支

```
git checkout dev01
```

## 5. 合并分支

```
# 若想将dev01分支合并到master上，则需先git checkout master再下列指令
git merge dev01
```

## 6. 删除分支dev01

```
git branch -d dev01
```

## 7. 创建公钥

```
ssh-keygen -t rsa
```

## 8. 添加远程仓库

```
git remote add <自己起个名字，一般用origin> <仓库ssh网站>
```

## 9. 查看和远程仓库的关联

```
git branch -vv
```

## 10. 将远程仓库的master和本地的master分支进行链接

```
# 第一次push执行下面指令后，后续就可以直接git push了
git push --set-upstream <自己起的名，origin> master:master
```



































