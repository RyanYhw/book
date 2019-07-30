# git


## 设置

设置用户名

``` shell
    git config --global user.name "Your name"
    git config --global user.email "email"
```

保存密码
```shell
 git config --global credential.helper store
```

## 使用

1.  如何查看特定分支的提交记录

```
git log <branch>
```

2.  如何回退到特定的版本

本地之前提交的数据会被删除, 需要做好备份
```
// HEAD 指向最新的提交, HEAD^ 上一次提交, 
// HEAD^^ 上上次提交(以此类推), 也可以写为 HEAD~2
git reset --hard HEAD^
git push -f origin <branch>
```



3. 将分支（A）merge 到 （B），然后 revert 这次的merge，那么 A 当前的提交将不能再次被merge到 B，如何处理

需要将这次revert提交再次revert

```
git revert <commit>
```

[force merge after reverting merge commit int git](https://stackoverflow.com/questions/19379034/force-merge-after-reverting-merge-commit-int-git)
