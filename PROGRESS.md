# 进度交接单

> 新对话第一句：读 `D:\第一个项目\PROGRESS.md`，我们继续。
> 最后更新：2026-10-10

## 新对话接手须知（先看这几条）

1. `AGENTS.md` 会自动加载，工作方式、教学要求、技术约定都在里面，不用重新交代。
2. 用户是编程新手。**不要一次倒一大段代码**，先讲思路、再动手，一次只推进一小步。
3. **沙箱对 `.git` 是只读的**：`git add` / `git commit` / `git push` 这类写操作必须先向用户申请授权。
4. **推送 GitHub 依赖本机 Clash 处于开启状态**（git 已单独配好 github.com 的代理，见下方"踩过的坑"）。
5. 数据库口令放在 `.env.local`（已被 `.gitignore` 忽略、不会上传），阶段 2 连库时读它，**不要写进任何进 git 的文件**。
6. **有一个问题等用户拍板**：阶段 1 的代码是由 AI 先写（边写边讲），还是用户自己敲、AI 在旁边指路？开新对话时**先问这一句再动手**。

## 一句话现状

环境全部就绪并验证通过，项目骨架已建好并完成首次 git 提交，可以开始写第一行业务代码了。

## 当前阶段

阶段 0：工程地基 —— 已完成，下一步进入阶段 1

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

## 未完成 / 待办

- 阶段 1 还没开始：让后端起服务、写出第一个接口
- 阶段 1 的代码由 AI 写还是用户写 —— 等用户决定

## 下一步

阶段 1：让后端跑起来，写出第一个接口，用浏览器就能访问到。建议的起手式：

1. 用 Spring Initializr 生成后端骨架（Spring Boot 3.x + Java 17 + Maven，包名 `com.jaychou`），放在 `backend\`
2. 跑起来，确认 8080 端口能访问
3. 写一个 `/api/hello`，浏览器打开就能看到返回
4. 顺手讲清 pom 依赖、启动类、内嵌 Tomcat 这几件事是干嘛的
5. 收尾：更新 PROGRESS.md + git 提交推送

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
| Ollama | 本地模型 deepseek-r1:1.5b | 模型在 C 盘（做阿 chou 时再搬 D 盘） |
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
├─ docs\              架构图与设计文档
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

