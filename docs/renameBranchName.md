# 修改分支名

## 假设分支没有推到远端

直接重命名本地分支即可

```ts
git branch -m oldName newName
```

## 分支已经推到了远端

a. 先重命名本地分支

```ts
git branch -m oldName newName
```

b. 删除远程分支

```ts
git push --delete origin oldName
```

c. 推送新命名的本地分支

```ts
git push origin newName
```

d. 把修改后的本地分支与远程分支关联

```ts
git branch --set-upstream-to origin/newName
```
