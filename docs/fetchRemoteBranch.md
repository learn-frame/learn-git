# 拉取远端分支

## 查看远端分支

```git
git branch -r
```

## 方式一

在本地创建一个 feature-xxx 分支, 并拉取远端的 feature-xxx, 并在本地切换到 feature-xxx

```git
git checkout -b feature-xxx origin/feature-xxx
```

## 方式二

该方式会拉取远端的 feature-xxx, 但不会自动切换到该分支

```git
git fetch origin feature-xxx
```
