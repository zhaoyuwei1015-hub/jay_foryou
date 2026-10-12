# 进度交接单

> 新对话第一句：读 `D:\第一个项目\PROGRESS.md`，我们继续。
> 最后更新：2026-10-12

## 新对话接手须知（先看这几条）

1. `AGENTS.md` 会自动加载，工作方式、教学要求、技术约定都在里面，不用重新交代。
2. 用户是编程新手。**不要一次倒一大段代码**，先讲思路、再动手，一次只推进一小步。
3. **沙箱对 `.git` 是只读的**：`git add` / `git commit` / `git push` 这类写操作必须先向用户申请授权。
4. **推送 GitHub 依赖本机 Clash 处于开启状态**（git 已单独配好 github.com 的代理，见下方"踩过的坑"）。
5. 数据库口令放在 `.env.local`（已被 `.gitignore` 忽略、不会上传），阶段 2 连库时读它，**不要写进任何进 git 的文件**。
6. **阶段 1 采用"AI 实操演示 + 用户在 VS Code 里实时观察"的方式**（2026-10-10 已定）。
   用户已会在 VS Code 里打开 `D:\第一个项目`，并用左侧「源代码管理」面板观察改动 / 暂存 / 提交。
7. **阶段 1 的完整过程记录在 `docs\第二段-版本控制与GitHub-过程记录.md`**（58 轮对话的浓缩版：
   时间线、敲过的每条命令、当前仓库状态、下一步、还没练到的点）。需要细节时读它，不用翻旧对话。
8. **从 2026-10-11 15:37 起，git 命令一律由用户自己敲**，AI 只给命令 + 解释。
   用户自己练习改文件的那些操作**不要记进本文件**。

## 一句话现状

环境全部就绪，项目骨架、本地仓库、GitHub 远端都已打通。阶段 1（Git 版本控制实操）接近完成：
四站流程（改 → 暂存 → 提交 → 推送）练熟，三招"回来"的命令（restore / reset / revert）分清，
分支课走到第 6 步——**分叉已经造出来，只差把它合回一根**。

## 当前阶段

阶段 1：Git 版本控制实操 —— 进行中（只差"把 practice2 合回 main"这最后一步）

## 已完成

- 环境盘点与安装（清单见下方"环境清单"）
- 建立项目仓库骨架：`AGENTS.md`、`PROGRESS.md`、`.gitignore`、`README.md`、`docs\`、`docs\architecture.html`
- 装好数据库可视化客户端 DBeaver 26.2.2（免安装版，全在 D 盘），桌面快捷方式已加
- DBeaver 的配置目录（原本偷偷生成在 C 盘）已迁移到 `D:\dev\dbeaver-home`，并用目录联接指回原位
- 设置好 git 全局身份：`zhaoyuwei1015-hub` / `zhaoyuwei1015@gmail.com`
- 卸载 GitHub Desktop（界面纯英文、只能连 GitHub，改用网页版 + 命令行）
- 修复 DBeaver 每次启动先显示英文再自己重启成中文的问题（`dbeaver.ini` 里加了 `-nl zh`）
- 确认 MySQL root 密码可用，能正常连上 8.0.42（明文不记录在 git 跟踪的文件里）
- 完成首次 git 提交
- 建立 GitHub 远程仓库 `zhaoyuwei1015-hub/jay_foryou`（Public）并完成首次推送
- 阶段 1 第一次完整走通：改 `README.md` → 暂存 → 提交（`b2a99cb`）→ 推送，GitHub 上已可见
- 确认了 git 写操作（add / commit / push）在沙箱里需要单独授权，已加好免重复询问的规则
- 练完"后悔药一号"（改动还没提交）：用「放弃更改」或 `git restore <文件>`，把文件还原成上一次提交的样子
- 练完"后悔药二号"（改动已经提交）：用 `git revert` 追加一条反向提交抵消它，历史完整保留
- 演示用的两条本地提交（`4f0f3c5`、`7a62c5a`）已用 `git reset --hard 885f0c7` 清掉，仓库与 GitHub 完全一致
- 讲清了"改了 / 提交了 / 推送了"三站的区别，以及"已推送的历史不可改写"这条纪律
- 名词对齐成**四站**：改了没暂存 → 暂存了 → 提交了（本地）→ 推送了（云端）。GitHub 到第④站才知道
- 练完 `git reset` 三档的用法，用户自己敲 `git reset --hard HEAD~2` 清掉了两条练习用的垃圾提交（`162a861`、`3fc81ae`），历史回到 `1f920ae`
- 认清 `git reflog` 是安全网（以为抹掉的提交其实还能找回）；也认清 `git restore` 的基准是**暂存区**而不是最后一次提交（这是他当时"敲了没反应"的真正原因）
- 搞清工具关系：**git 是独立程序，VS Code 的「源代码管理」只是它的遥控器**；终端是第二个遥控器
- 学会读 VS Code 图表（一行 = 一次提交，不等于一个文件）、学会分批 add + commit 让不同文件带不同说明
- 分清 `restore` / `reset` / `revert`：`--soft/--mixed/--hard` 三档**只属于 reset**；`revert` 是推送之后唯一正确的撤回方式
- 分支课第 1–6 步：`git branch` 看分支 → `git switch -c practice` 开分支 → 在 practice 上改 README 提交（`81a2c3c`）→ 切换分支看"平行世界" → `git merge practice` 完成第一次**快进合并** → 造出真分叉（`main` 的 `4ab8559` 与 `practice2` 的 `e502143`）

## 未完成 / 待办

- 阶段 1 最后一步：把 `practice2` 合回 `main`（预期产生一个"合并提交"，这是分支课最值得看的一幕）
- 阶段 1 收尾：清理 README 里的练习痕迹 → 更新 PROGRESS.md → 提交推送
- 阶段 2 及之后的后端搭建尚未开始
- 阿 chou 的 AI 方案待定：不用 Ollama，后期可能尝试扣子（Coze）

## 下一步

阶段 1 收尾。按顺序做：

1. **把 `practice2` 合回 `main`**：`git switch main` → `git merge practice2`。
   两边改的位置离得远（main 改第 8 行附近、practice2 改文件末尾），所以应该**自动合并、不冲突**，
   并在图表里多出一个**有两个父亲的合并提交**（它本身不代表内容改动，只代表"把两条线缝在一起"）。
2. 看一眼 `git log --oneline --graph --all`：分叉会收敛回一根。
3. 顺手确认那个未结问题：VS Code「图表」把显示范围切到所有分支，看能不能看见 `practice2` 那条线。
4. 清理 README 里的练习痕迹（含第 8 行 `## 技术栈main 分支加的：分支练习用` 黏在一行的问题）。
5. 更新 PROGRESS.md + 提交推送，然后进入**阶段 2：后端搭建**。

（后端搭建顺延到阶段 2。先把 Git 练熟，后面每一步代码改动才有安全网。）

## 关键决策（及原因）

| 决策 | 内容 | 原因 |
|---|---|---|
| JDK | Eclipse Temurin 17，装在 `D:\dev\jdk-17` | JDK 17 是 Spring Boot 3 的主流版本；装在 D 盘，不占 C 盘 |
| Maven | 3.9.16，装在 `D:\dev\apache-maven-3.9.16` | 本地仓库改到 `D:\dev\maven-repo`，并配阿里云镜像，下载快 |
| 数据库 | MySQL 8.0.42（电脑上已有的） | Java 岗位最常用；不用换，只补一个好用的客户端 |
| 数据库客户端 | DBeaver（免费开源，可替代 Navicat） | 免费正版不会被杀毒软件误删；免安装可放 D 盘；导出 CSV/Excel/JSON 都支持 |
| Git 身份 | `zhaoyuwei1015-hub` / `zhaoyuwei1015@gmail.com` | GitHub Desktop 安装时已自动写入全局配置，沿用即可 |
| Git 客户端 | 不用桌面客户端，用网页版 + 命令行 | GitHub Desktop 没有中文界面，网页版有中文 |
| 云端仓库 | GitHub：`zhaoyuwei1015-hub/jay_foryou`（Public、无许可证） | 账号已有、面试官看得多；Public 方便给人看 |
| GitHub 访问 | 只对 github.com 单独配置走本机 Clash 代理（127.0.0.1:7897） | 直连 github.com:443 不通；只作用于 GitHub，Clash 关掉时不影响其他站点 |
| AI 方案 | 待定：不用 Ollama，后期可能尝试扣子（Coze） | 用户决定；到阶段 11 再做具体选型 |

## 环境清单

| 组件 | 版本 | 位置 |
|---|---|---|
| JDK | Temurin 17.0.20.1 | `D:\dev\jdk-17` |
| Maven | 3.9.16（仓库 `D:\dev\maven-repo`） | `D:\dev\apache-maven-3.9.16` |
| Git | 2.55.0 | `D:\Git` |
| Node / npm / pnpm | 22.17.0 / 10.9.2 / 11.25.0 | `D:\node` |
| VS Code | 1.131.0 | `D:\visul stdio code` |
| MySQL | 8.0.42（服务正在运行） | 程序在 C 盘，数据在 C 盘（待定是否搬 D 盘） |
| MySQL 客户端 | DBeaver 26.2.2（主力）+ Workbench 8.0 + VS Code 插件 | `D:\dev\dbeaver`，工作区 `D:\dev\dbeaver-data` |
| Ollama | 本地模型 deepseek-r1:1.5b（**本项目暂不使用**，AI 方案待定） | 模型在 C 盘；确认长期不用可以删掉腾空间 |
| 未安装 | Redis、Docker、WSL | 用到时再装，现在不影响 |

### MySQL 里已有的数据库（都是以前课程/练习留下的，别乱删）

`dxd20222122189`、`jyx20222122003`、`mydatabase`、`sakila`、`sty20222122001`、
`user_sql`、`zhaoyuwei`、`zyw`、`zyw20222122125`

本项目计划用的库名：`jay_foryou`（阶段 2 建库时创建，不会动上面这些）

## 文件清单

```
D:\第一个项目\
├─ AGENTS.md          工作说明书（自动加载）
├─ PROGRESS.md        这份进度单
├─ README.md          项目简介
├─ .gitignore         哪些文件不进 git
├─ .env.local         本地数据库口令（不进 git）
├─ docs\              架构图、设计文档、过程记录
└─ work\              临时试验（不进 git）
```

## 踩过的坑

- 沙箱里直接联网会被挡（提示连 127.0.0.1:9 被拒绝），需要单独申请授权才能下载东西。
- `pnpm config set store-dir` 在 Windows 上会报 `EXDEV cross-device link`，改配置要用项目里的 `.npmrc`。
- GitHub Desktop 界面**没有中文**，也没有语言切换开关；官方一直没做，网上汉化包是第三方改包，风险高。
- GitHub Desktop 只能连 GitHub，不支持 Gitee；安装位置写死在 C 盘用户目录，无法改路径。
- 沙箱对 `.git` 目录是只读的，所以 `git add` / `git commit` 这类写操作需要单独授权。
- DBeaver 冷启动会先按 Windows 系统语言判断界面语言（这台机器给的是 en），然后才读自己的"中文"设置并重启一次，所以会闪一下英文。已在 `D:\dev\dbeaver\dbeaver.ini` 加 `-nl zh` 固定为中文。
- `github.com:443` 在国内直连不通，而且 **Git 默认不读 Windows 的系统代理设置**，所以第一次 `git push` 直接超时报错。解决办法是给 git 单独配代理：`git config --global http.https://github.com.proxy http://127.0.0.1:7897`。注意这个配置依赖本机 Clash 处于开启状态。
- VS Code 打开一个新文件夹时会进入「受限模式」（顶部黄条），会限制终端等部分功能。点「管理」→「信任此文件夹」即可关闭。
- `git add` / `git commit` / `git push` 都需要写入 `.git` 目录，沙箱里是只读的，必须先申请用户授权。
- VS Code「图表」最上面那条「传出的更改」是**汇总节点**（把所有未推送提交的改动合起来显示），不是一次提交；真正的提交是下面带实心圆点和蓝色 `main` 标签的那条。只有一个未推送提交时，两者看起来会一模一样。
- 状态栏的 `↑n`、面板里的蓝色「同步更改 n 个」按钮、图表顶上的「传出的更改」，说的都是同一件事：本地有 n 条提交还没推送。
- **`git restore <文件>` 的基准是"暂存区"，不是"最后一次提交"。** 如果先 `git add` 再 `git restore`，
  等于是拿新版覆盖新版，什么都不会发生（用户当时就踩了这个坑）。要真正丢掉改动要用 `git restore --source=HEAD --staged --worktree <文件>`，
  或者直接用面板上那个 `↩` 按钮（按钮做的事比裸命令狠）。
- **VS Code 的「更改」列表偶尔不刷新**：图标上顶着角标 `1`、标签页带 `M`，但列表是空的。
  此时 `git status` 是正常的，属于界面层的毛病。修法：`Ctrl+Shift+P` → "重新加载窗口"，或整个关掉 VS Code 再开。
- **在文件里插入内容时如果忘了回车**，会和上一行黏成一行。README 第 8 行的 `## 技术栈main 分支加的：分支练习用` 就是这么来的。
- **`git commit` 不带 `-m` 会掉进 Vim**（这台机器上 `core.editor` 没设过，git 兜底用 `vi`，而 `D:\Git\Git\usr\bin\vi` 确实存在）。
  如果不小心进去了：按 `Esc`，再敲 `:q!` 回车就能安全退出。
- **PowerShell 的 Tab 补全不补 git 子命令**（它只补自己的命令和文件名），所以 `git re<Tab>` 没反应。
  Git Bash 开箱自带 git 补全，位置是 `D:\Git\Git\git-bash.exe`。
- **VS Code 的「图表」默认可能只显示当前分支的历史**，所以开了新分支后图表上看不到分叉（终端里 `git log --graph --all` 是能看见的）。
  这是显示范围问题，不是 git 数据有问题——把范围切到所有分支即可。

