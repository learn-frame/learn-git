# 删除 git 中的所有提交历史记录

## 期待效果

删除现存的所有 commit 记录，但代码保持最新，并且不会因为删除记录而影响 GitHub 的 contribution.

## 实现方式

```bash
git checkout --orphan latest_branch # 随便起名，别叫 master 就行
git add -A
git commit -am "比如可以写成 initial repo"
git branch -D master
git branch -m master
git push -f origin master
```
