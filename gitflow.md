# Git 规范
我们使用 Gitflow 工作流，具体请参考 [Gitflow](https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow)。

## 分支
### 主分支

- main
- develop

![img](https://raw.githubusercontent.com/pan-team/spec/main/img/gitflow/01-How-it-works.svg)

### 功能分支
- feature/xxx

![img](https://raw.githubusercontent.com/pan-team/spec/main/img/gitflow/02-Feature-branches.svg)

### 发布分支
- release/xxx

![img](https://raw.githubusercontent.com/pan-team/spec/main/img/gitflow/03-Release-branches.svg)

### 热修复分支
- hotfix/xxx

![img](https://raw.githubusercontent.com/pan-team/spec/main/img/gitflow/04-Hotfix-branches.svg)

### 版本标签
- v1.0.0

## 提交规范
### 提交类型
- feat: 新功能
- fix: 修复 bug
- docs: 文档
- style: 代码格式
- refactor: 重构
- perf: 性能优化
- test: 测试
- build: 构建
- ci: CI
- chore: 其他

### 提交内容
- 以动词开头，使用第一人称现在时，比如 change，而不是 changed 或 changes
- 第一个字母小写
- 结尾不加句号（.）

### 提交示例
- feat: add login page
- fix: fix login bug

## 提交流程
### 开发新功能
1. 从 develop 分支创建新的功能分支
2. 开发新功能
3. 提交新功能
4. 合并新功能分支到 develop 分支

#### 开始 Feature
```bash
# 通过 develop 分支创建新的功能分支
git checkout -b feature/xxx develop

# 修改代码
git status
git add .
git commit -m "feat: add xxx page"
```

#### 提交 Feature
```bash
# 切换到 develop 分支
git checkout develop
git pull

#--no-ff：不使用fast-forward方式合并，保留分支的commit历史
#--squash：使用squash方式合并，把多次分支commit历史压缩为一次
git merge --no-ff feature/xxx

# 推送到远程仓库
git push origin develop

# 删除功能分支
git branch -d feature/xxx

# 删除远程仓库的功能分支
git push origin --delete feature/xxx
```

### 发布新版本
1. 从 develop 分支创建新的发布分支
2. 发布新版本
3. 合并发布分支到 main 分支
4. 合并发布分支到 develop 分支

#### 发布新版本的注意事项
- 发布新版本时，需要将 main 分支的代码合并到 develop 分支，以保证 develop 分支的代码是最新的
- 发布新版本时，需要将 develop 分支的代码合并到 main 分支，以保证 main 分支的代码是最新的

#### 开始 Release
```bash
# 通过 develop 分支创建新的发布分支
git checkout -b release/xxx develop
```

#### 完成 Release
```bash
# 切换到 main 分支
git checkout main

# 合并发布分支到 main 分支
git merge --no-ff release/xxx

# 打标签
git tag -a v1.0.0 -m "v1.0.0"

# 推送到远程仓库
git push origin main
git push origin v1.0.0

# 切换到 develop 分支
git checkout develop

# 合并发布分支到 develop 分支
git merge --no-ff release/xxx

# 推送到远程仓库
git push origin develop

# 删除发布分支
git branch -d release/xxx

# 删除远程仓库的发布分支
git push origin --delete release/xxx
```

### 修复线上 bug
1. 从 main 分支创建新的热修复分支
2. 修复线上 bug
3. 合并热修复分支到 main 分支
4. 合并热修复分支到 develop 分支

#### 开始 Hotfix
```bash
# 通过 main 分支创建新的热修复分支
git checkout -b hotfix/xxx main
```

#### 完成 Hotfix
```bash
# 切换到 main 分支
git checkout main

# 合并热修复分支到 main 分支
git merge --no-ff hotfix/xxx

# 打标签
git tag -a v1.0.1 -m "v1.0.1"

# 推送到远程仓库
git push origin main
git push origin v1.0.1

# 切换到 develop 分支
git checkout develop

# 合并热修复分支到 develop 分支
git merge --no-ff hotfix/xxx

# 推送到远程仓库
git push origin develop

# 删除热修复分支
git branch -d hotfix/xxx

# 删除远程仓库的热修复分支
git push origin --delete hotfix/xxx
```

## 版本号
### 主版本号
- 当你做了不兼容的 API 修改
### 次版本号
- 当你做了向下兼容的功能性新增
### 修订号
- 当你做了向下兼容的问题修正

## 参考
- [Gitflow](https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow)
- [AngularJS Git Commit Message Conventions](
https://gist.github.com/stephenparish/9941e89d80e2bc58a153)
- [Semantic Versioning 2.0.0](
https://semver.org/lang/zh-CN/)
- [Git Commit Message Conventions](
https://gist.github.com/stephenparish/9941e89d80e2bc58a153)

## 作者
- [icy37785](https://github.com/icy37785)
