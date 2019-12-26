# Tags

## 本地新建 tag

```ts
git tag v1.0.0
```

对于 npm 包管理, 还可以使用如下命令:

```ts
npm version major
npm version minor
npm version patch
```

## 推送本地 tag 到远端

新建好的 tag 当然是要推送到远端了:

```ts
git push origin v1.0.0
```

如果有多个分支, 可以一并推送:

```ts
git push origin --tags

git push --follow-tags origin master
```

## 删除本地 tag

```ts
git tag -d v1.0.0
```

## 删除远端 tag

上面的方式只会删除本地分支, 如果已推到线上, 需要用下面的方式.

如下方式中第一种肯定是最靠谱的, 因为你无法保证哪个 SB 把分支名命名成了 v1.0.0 .......

```ts
git push origin :refs/tags/v1.0.0

git push origin :v1.0.0

git push --delete origin v1.0.0
```

## 查看某个 tag 的细节

```ts
git show v1.0.0
```

![git show tagname](../images/showTag.jpg)

## 根据 tag 进行版本回退

tag 最重要的目的就是控制版本节点, 因此可以用来进行版本会回退(至于为什么回退自行脑补).

通过上一步可以拿到 tag 的 hash, 所以老样子:

```ts
git reset --hard ee8c46
```

## 根据 tag 创建分支

有时我们根据旧 tag 进行版本回退了, 但新的 tag 未来还要用(比如复盘鞭尸...), 因此这个 tag 应该转成分支, 接下来 checkout 就好了.

```ts
git branch feature/xxx v1.0.1
```
