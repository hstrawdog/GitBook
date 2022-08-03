# Git常用命令

## 克隆

```
git clone 
```

## 关联Git地址

```
git remote add origin https://xxxxxxx/wangdong/helloworld.git
```

## 移除关联

```
git remote remove origin
```

## 添加

```
git add .
```

## 提交

```
git commit -m "xxx"
```

## 推送

```
git push origin master 
```

## 拉取

```
git  pull 
```
## 添加tag

```
git tag -a xxx
```

```
git tag -a xxx -m "xxx"
```

## 查看tag 

在 Git 中列出已有的标

```
git tag 
```

你也可以使用特定的模式查找标签。 例如，Git 自身的源代码仓库包含标签的数量超过 500 个。 如果只对 1.8.5 系列感兴趣，可以运行

```
git tag -l '1.5.8*'
```