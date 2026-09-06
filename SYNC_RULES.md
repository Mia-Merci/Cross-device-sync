# 同帐号跨设备同步规则

这个项目使用 GitHub 作为两台设备之间的唯一代码源。两台设备都应该从同一个远端仓库拉取、提交和推送。

## 适用触发语

当用户说“同步给 Mac mini”“同步给另一台设备”“同步到另一台电脑”或类似表达时，Codex 应执行本文件定义的同步流程。

## 同步前检查

1. 读取 `PROJECT_LOG.md`、`TODO.md`、`DECISIONS.md`，了解当前进度。
2. 运行 `git status --short --branch`，确认本机是否有未提交修改。
3. 如果存在未提交修改，先总结这些修改，并更新进度文档。
4. 不提交 `.env`、密钥、令牌、私密配置或日志中可能含有敏感信息的文件。

## 标准同步流程

1. 拉取远端最新内容：

   ```bash
   git pull --rebase
   ```

2. 更新项目记忆：
   - `PROJECT_LOG.md`：记录本次完成内容、重要变化、验证结果。
   - `TODO.md`：更新下一步任务。
   - `DECISIONS.md`：只记录影响后续开发的技术或产品决策。

3. 检查修改：

   ```bash
   git status --short
   git diff --check
   ```

4. 提交：

   ```bash
   git add .
   git commit -m "Sync project progress"
   ```

5. 推送：

   ```bash
   git push
   ```

## 冲突处理

如果 `git pull --rebase` 发生冲突：

1. 不要强推。
2. 先说明冲突文件和冲突原因。
3. 只解决与当前同步直接相关的冲突。
4. 解决后运行必要检查，再继续 `git rebase --continue`。

## 每日收尾

每天结束前至少保证：

- 工作代码已提交或明确记录为未完成。
- `PROJECT_LOG.md` 写明今天完成了什么。
- `TODO.md` 写明下一步优先级。
- 本机分支已推送到 GitHub。
