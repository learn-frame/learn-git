# 删除 git 所有历史提交记录, 但保留 contributions

## 期待效果

删除现存的所有 commit 记录, 但代码保持最新, 并且不会因为删除记录而影响 GitHub 的 contribution.

## 实现方式

```bash
git checkout --orphan latest_branch # 随便起名, 别叫 master 就行
git add -A
git commit -am "比如可以写成 initial repo"
git branch -D master
git branch -m master
git push -f origin master
```
