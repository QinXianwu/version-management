## 版本管理
    使用 npm 的 version 命令来进行版本管理，常用命令
- `npm version major` : 更新主版本（大更新），`v1.0.0 -> v2.0.0`
- `npm version minor` : 更新次版本（中等级别的更新） `v1.0.0 -> v1.1.0`
- `npm version patch` : 更新修订版本（小修改） `v1.0.0 -> v1.0.1`
- `npm version prerelease` : 准备预发布版本 `v1.0.0 -> v1.0.0-1`

执行 npm version xxx 命令的时候，都会自动在 git 上打个 tag

### master 线上分支
 - 正式版分支，由预发布版本无bug时合并 master分支和pre分支
### dev 开发版分支
 - 在添加新功能时`拉取最新master分支`下来进行添加，添加完成需要测试就`提交到pre预发布分支`
### pre 预发布分支
 - 在 dev 上创建pre分支，执行 `npm version prerelease` 命令
 - 测试过程中出现的bug，全部在pre分支上修复，测试完成提交到master分支后删除该pre分支 
 - 先到 master 分支进行合并 `git merge pre` 后再删除
 - `git branch -D pre` 删除本地
 - `git push origin --delete pre` 删除远程
