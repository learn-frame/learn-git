# 同步 fork 过来的工程

在看 React 源码, 于是把源码 fork 到了自己的仓库, 这个期间 facebook/react 的 master 也一直被提交. 同步 fork 过来的工程, 需要这么做.

```bash
# 先切到 master
git checkout master

# 配置 remote, 指向源仓库
git remote add upstream https://github.com/facebook/react.git

# 获取远端的 upstream
git fetch upstream

# 把 upstream/master 合并到本地 master
git merge upstream/master
```
