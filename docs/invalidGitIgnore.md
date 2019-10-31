# 无效的 .gitignore

有时候在 .gitignore 正确地添加了要忽略的目录或文件，但这些文件仍然会被提交到远端。
原因是 .gitignore 只能忽略那些原来没有被 track 的文件，如果某些文件已经被纳入了版本管理中，则修改 .gitignore 文件时无效的。
因此我们需要将本地缓存删除掉，也就是将这些文件改变成未 track 状态，然后再提交。

```shell
git rm -r --cached .
git add .
git commit -m "YOUR_COMMITS"
```
