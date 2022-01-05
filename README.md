## 版本管理

    使用 npm 的 version 命令来进行版本管理，常用命令

- `npm version major` : 更新主版本（大更新），`v1.0.0 -> v2.0.0`
- `npm version minor` : 更新次版本（中等级别的更新） `v1.0.0 -> v1.1.0`
- `npm version patch` : 更新修订版本（小修改） `v1.0.0 -> v1.0.1`
- `npm version prerelease` : 准备预发布版本 `v1.0.0 -> v1.0.0-1`

执行 npm version xxx 命令的时候，都会自动在 git 上打个 `tag`

    注意

- master 分支和 dev 分支是一直存在的；pre 分支只在项目提测阶段才存在；
- fix 分支只需要 master 分支出现 bug 的情况下才存在
- 有些更新不影响程序功能的，没有必要更新版本，例如修改 README.md 文件之类的

### master 线上分支

- 正式版分支，由预发布版本无 bug 时合并 master 分支和 pre 分支

### dev 开发版分支

- 在添加新功能时拉取最新 master 分支`git merge master`下来进行添加，添加完成需要测试就`提交到pre预发布分支`

### pre 预发布分支

- 在 dev 上创建 pre 分支，执行 `npm version prerelease` 命令
- 测试过程中出现的 bug，全部在 pre 分支上修复，测试完成提交到 master 分支后删除该 pre 分支
- 先到 master 分支进行合并 `git merge pre` 后再删除
- `git branch -D pre` 删除本地
- `git push origin --delete pre` 删除远程

### fix 紧急修复 bug 分支

- 当线上版本出现 bug 后，需要紧急修复的，就需要在 master 分支上切出 fix 分支来修复线上 bug，并且修复完成后合并到 master 分支 `git merge fix`，以及 dev 分支，并且删除 fix 分支
- `npm version major/minor/patch` 更新版本号
- `git branch -D fix` 删除本地
- `git push origin --delete fix` 删除远程


## 例子：

- 步骤一：在 dev 分支 commit 若干次
- 步骤二：准备预发布版本，在 dev 上创建 pre 分支，执行 npm version prerelease 命令
- 步骤三：预发布版本发现 bug，直接在 pre 分支上修复，提交 commit
- 步骤四：dev 分支继续开发新功能，提交 commit
- 步骤五：预发布版本完成了测试，可以直接发布了，切换到 master 分支，合并 pre 分支内容 git merge pre，删除 pre 分支，git branch -d pre
- 步骤六：在 master 分支上执行版本修改命令，根据版本更新的内容判断更新主次小版本，npm version major/minor/patch
- 步骤七：完成 master 分支发布，切换回 dev 分支，dev 分支合并 master 分支的内容 git merge master （这时候可能需要做人工合并冲突）
- 步骤八：继续在 dev 分支上进行新功能开发。提交若干个 commit
- 步骤九：此时 master 分支上出现 bug，需要紧急修复，在 master 分支上创建 fix 分支
- 步骤十：在 fix 分支上修复了 bug 后，执行 npm version prerelease 命令，准备预发布
- 步骤十一：测试无 bug 后，将 fix 分支的内容合并到 master 分支，git merge fix，更新版本后发布，删除 fix 分支，git branch -d fix ,并且更新本版 npm version major/minor/patch
- 步骤十二：回到 dev 分支，合并 master 分支的内容，继续开发，git merge master （这时候可能需要做人工合并冲突）