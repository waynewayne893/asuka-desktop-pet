# HANDOFF P1｜明日香桌宠 GitHub 私有迁移 · 只读审查交接

- 阶段：**P1 只读审查（已完成）**，未进入 P2。
- 执行时间：2026-10-26 14:17–14:22（Asia/Shanghai）。
- 工作区（= 已确认项目根目录）：`D:\HuaweiMoveData\Users\86191\Desktop\Codex_Asuka_交付包_v2`。
- 本轮写入：仅本文件 `HANDOFF_P1_Asuka_GitHub_20261026.md`。未初始化 Git、未暂存、未提交、未创建远程、未推送、未构建、未安装依赖、未改动任何既有文件。

## 0. 结论摘要

**可以迁移，但现在不具备直接进入 P2 的条件。**

| 判定 | 内容 |
|---|---|
| 项目识别 | 已确认唯一根目录，但**它不是应用程序源码工程**，而是「官方 Pets 素材 + QA 记录 + 文档」资产工程 |
| "已上线"的实测含义 | 官方 hatch-pet 本地宠物包已安装到 `%USERPROFILE%\.codex\pets\`，用户确认可选择并播放；**没有**网页/服务端部署、安装包或更新通道 |
| Git 现状 | 工作区与所有祖先目录均**无 `.git`**，无历史、无远程、无子模块 |
| 敏感凭据 | 未发现任何密钥/令牌/证书/`.env`/数据库/日志；`C:\Users\86191` 个人路径出现在 11 个文本文件中 |
| 硬阻断 | **B1 并发写入未冻结**、**B2 素材授权未决**、**B3 无 LICENSE**、**B4 Git 身份缺失**、**B5 上传范围未定** |
| 建议仓库 | `waynewayne893/asuka-desktop-pet`，**Private**（角色 IP 未获授权前必须 Private） |

---

## 1. 项目识别与识别证据

### 1.1 定位过程（不猜测）

| 检查 | 结果 |
|---|---|
| 当前工作区顶层 | `README.md`、`AGENTS.md`、`docs/`、`delivery/`、`references/`、`work/` |
| 桌面及二级子目录中含 `asuka`/`明日香`/`pet`/`宠物` 的目录 | **只有本工作区一个** |
| 工作区内或祖先目录的 `.git` | **无**（逐级向上检查至驱动器根） |
| 桌面另外两个 Git 仓库 | `个人网页建立\personal-space`（独立网站工程：有 `.git`、**无 remote**，抽查 `.md/.json/.html/.ts/.tsx` 未命中 asuka/明日香）、`论文complete\两个二元建模博弈`；**均与桌宠无关，不得混淆** |
| 文档自述一致性 | `README.md`、`AGENTS.md`、`docs/00–08` 指向同一项目与同一交付包 |

### 1.2 项目画像

| 项 | 实测结论 |
|---|---|
| 根目录 | 本工作区（`Codex_Asuka_交付包_v2`） |
| 技术栈 | **无应用源码栈**：无 `package.json`、无 `pyproject.toml`、无 `*.sln/*.csproj`、无 `Cargo.toml`、无 Electron/Tauri 配置。实际构成 = 静态素材（PNG/WebP/GIF/MP4）+ 233 份 JSON（QA 报告与清单）+ 10 个 Python 脚本 + 1 个 Node 脚本 |
| 主要"程序入口" | 宠物包清单 `delivery\asuka-v2_20261026\asuka-{school,work}\pet.json`（`spriteVersionNumber: 2`，`spritesheetPath: spritesheet.webp`） |
| 运行平台 | 第三方桌面应用 Codex 的官方 Pets 能力；**未修改该应用任何安装文件** |
| 打包工具 | 无。所谓"打包"= 复制官方 hatch-pet 本地包结构（`pet.json` + `spritesheet.webp`）到用户目录 |
| 版本号 | 交付物命名 `asuka-v2_20261026`；图集声明 `spriteVersionNumber: 2`。无软件版本语义（无 commit/tag 体系） |
| 上线/发布方式 | 本地安装到 `C:\Users\86191\.codex\pets\`，应用内 Refresh 后选择。**无发布流水线、无自动更新、无分发服务器** |
| 源码与发行物是否分离 | 逻辑上分离（`work/` 过程 → `delivery/` 发行），物理上同目录、无构建产物目录 |

> 推论（影响 P2 范围）：把本项目上传 GitHub 属于**资产与档案的版本化归档**，不涉及 CI/CD、构建复现或自动更新发布。这降低了迁移风险，同时意味着仓库价值主要在"可追溯的验收证据"，而非"可运行的软件"。

### 1.3 体量快照（14:21:43 实测）

| 指标 | 数值 |
|---|---|
| 文件数 | 1,128 |
| 总大小 | 251,165,108 字节（239.53 MB） |
| 扩展名 | `.png` 673（221.07 MB）、`.json` 233（0.73 MB）、`.md` 137、`.gif` 55（6.24 MB）、`.py` 10、`.jpg` 9（1.2 MB）、`.webp` 5（9.5 MB）、`.txt` 3、`.mp4` 2（0.45 MB）、`.cjs` 1 |
| 区域分布 | `work/` 1,097 文件 / 230.58 MB；`references/` 13 / 5.11 MB；`delivery/` 6 / 3.81 MB；`docs/` 10 / 约 0.02 MB |
| 最大单文件 | 4.83 MB（`work\phase3_20261025\work\references\masters-and-standard-panel.png`） |
| 最长路径 | 相对 94 字符 / 绝对约 151 字符（未超 260，含中文与空格） |

---

## 2. 已上线运行态与保护约束

### 2.1 本机安装现状（只读核对，未改动）

| 宠物 ID | 安装目录 | 大小 | SHA256（前 12 位） | 状态 |
|---|---|---|---|---|
| `asuka-school` | `C:\Users\86191\.codex\pets\asuka-school\` | 1,971,788 | `51ecce0097b0` | 已安装，用户确认可选择并播放 |
| `asuka-work` | `C:\Users\86191\.codex\pets\asuka-work\` | 2,017,070 | `0d4024945ca4` | 已安装，用户确认可选择并播放 |
| `asuka-mixed-test` | `C:\Users\86191\.codex\pets\asuka-mixed-test\` | 1,988,930 | `83aba6599245` | 已安装（2026-10-26 14:20:27），**待用户选择观察，未验收** |

- 两套已验收包：安装副本与 `delivery/` 逐字节一致（`pet.json`、`spritesheet.webp` 共 4 文件全部 IDENTICAL）。
- `delivery\asuka-v2_20261026\SHA256SUMS.txt` 自校验：**5/5 通过，0 失败**。
- 旧宠物"白龙司书"不在本地目录，仅保留在 Pets 服务记录中（记录 ID 见 `docs/06`），本次未触碰。

### 2.2 P2/P3 必须遵守的保护约束

1. **禁止**任何 `git` 操作触及 `C:\Users\86191\.codex\`（该目录不在仓库范围，且含 `auth.json`、`installation_id`、多个 sqlite）。
2. **禁止**重跑安装/复制脚本；安装目录哈希当前与交付包一致，任何写入都会破坏"安装=交付"的可验证性。
3. **禁止**修改 `references/approved_baselines/` 两张母版（已被 `preservation-final.json` 以哈希锁定）。
4. **禁止**以"清理仓库"为由删除 `work/` 内的失败候选或被拒版本——它们是验收证据链的一部分。
5. 若日后仓库改 Public，须先解决 B2/B3；Private 状态下同样不得把仓库链接公开到协作渠道。

---

## 3. 审计窗口内的并发写入（阻断项 B1，最高优先级）

**这是本轮最重要的现场发现：工作区在审查期间是活动写入状态。**

| 时间 | 事件 | 证据 |
|---|---|---|
| 14:17:37 | 审查开始，全量盘点 | 1,059 文件 / 247,052,339 字节 |
| 14:19:48 | 新增脚本 `work\phase3_20261025\mix_rows_test.py` | 文件 CreationTime = 14:19:48 |
| 14:19:50–14:19:54 | 生成 `work\phase3_20261025\mixed-test\` 全套（67 文件，3.91 MB，含 `final/spritesheet.webp` 与 8 份 QA JSON） | 目录与文件 mtime |
| 14:20:27 | 第三只宠物被安装到 `C:\Users\86191\.codex\pets\asuka-mixed-test\` | 安装目录 mtime + 哈希与工作区一致 |
| 14:21:38 | `AGENTS.md`、`docs\06`、新增 `docs\08` 被更新 | mtime |
| 14:21:43 | 审查再次盘点 | 1,128 文件 / 251,165,108 字节（+69 文件 / +4.11 MB） |

判断与处置：

- 该批改动**已被授权**（`AGENTS.md` 新增条目 + `docs/08-混合双形态最小测试_工作稿.md`），不是失控写入；但其产生时间落在本次审查窗口内，属于"另一个 Agent/会话正在写入"的情形。
- 依 TASK P1 第 2 节要求：**记录并停止任何可能冲突的操作**。本轮因此未运行任何官方校验/安装脚本，也未把任何目录声明为"最终态"。
- 工作区内**没有** `.lock`/`.tmp`/`.partial` 残留；`.codex\thread-writer-locks` 最新为 14:02:46，与 14:19 的写入不对应，说明写入方未通过该锁登记。
- **P2 前置**：必须由用户明确一个冻结时刻（或在确认写入方空闲后）重新取基线；本文件第 1.3 节与第 12 节的所有数字/哈希都是 14:21–14:22 的**时点值**，不是终值。

---

## 4. Git 基线

| 项 | 实测 |
|---|---|
| 是否已初始化 | **否**（工作区与全部祖先目录无 `.git`） |
| 分支 / HEAD / 远程 / 提交历史 | 不存在 |
| 工作区状态 | 无 Git 概念；磁盘上有未版本化文件 1,128 个 |
| worktree / 子模块 | 无 |
| `git` 可执行文件 | `D:\Git\cmd\git.exe`，`git version 2.56.0.windows.2` |
| `git-lfs` | `git-lfs/3.8.0`（已装，但本项目不需要） |
| 全局身份 | `user.name`、`user.email` **均未配置**（`git config --global --list` 仅有 `safe.directory`） |
| 全局其他 | `credential.helper=manager`；`init.defaultbranch` 未设全局；system 级 `init.defaultbranch=master`、`core.autocrlf=false` |
| 凭据助手 | `git-credential-manager.exe` 存在于 `D:\Git\ucrt64\bin\`（可用，无需新增依赖） |
| `gh` CLI | **未安装**（P3 不能依赖 `gh repo create`，需网页创建或另行授权安装） |
| 并发风险 | 当前有活动写入方（见第 3 节）；另有两个无关仓库在桌面，勿 `git add` 越界 |

结论：P2 是一次**从零开始**的初始化，不存在"保留历史/改写历史"问题；但同样意味着没有 `git log` 可作证据，首个提交即基线，必须一次做对。

---

## 5. 敏感数据扫描：范围、结果、局限

### 5.1 范围与方法

| 方法 | 覆盖 |
|---|---|
| 内容正则（密钥/密码/令牌/私钥） | 全部 `.md,.txt,.json,.py,.cjs,.js`，模式含 `api[_-]?key`、`secret`、`passw`、`bearer`、`sk-…`、`ghp_`、`github_pat_`、`AKIA…`、`BEGIN … PRIVATE KEY`、`token[:=]` |
| 扩展名/文件名白名单 | `.env*`、`.pem`、`.key`、`.pfx`、`.p12`、`.crt`、`.cer`、`.jks`、`.zip/.7z/.rar/.tar/.gz`、`.exe/.dll/.msi`、`.db/.sqlite`、`.log`、`.csv/.xlsx/.docx`、`.ttf/.otf/.woff*` |
| 个人标识 | `C:\Users\86191`、邮箱正则、`waynewayne893`、`github.com`、`installation_id/device_id/machine_id` |
| 图像元数据 | 对 `references/`、`delivery/` 全部图像读取 PNG chunk / EXIF / WebP 容器信息 |

### 5.2 结果

| 类别 | 结果 |
|---|---|
| 密钥、令牌、密码、私钥 | **0**（无任何命中） |
| `.env`、证书、签名密钥 | **0** |
| 数据库、日志、崩溃转储、用户数据、设备标识 | **0** |
| 邮箱、GitHub 账号名、远程 URL | **0**（注意：`waynewayne893` 仅由用户口头提供，**磁盘上无任何证据**） |
| 个人绝对路径 `C:\Users\86191` | **11 个文件命中**（见下表） |
| 图像隐写风险 | 两张母版 PNG `info` 为空（无 `tEXt/iTXt/EXIF`）；`source_refs` 的 JPEG 仅 `JFIF` + 456 字节 ICC；两张交付 WebP 仅 `loop`/`background` 容器字段。**未发现提示词、生成软件署名、作者、GPS 或 C2PA 清单** |
| 工作区外的敏感物 | `C:\Users\86191\.codex\auth.json`、`installation_id`、`*.sqlite`、`sessions/`、`computer-use/` 等**均在仓库范围之外**，但一旦把仓库根误设为 `C:\Users\86191` 或桌面根目录就会纳入——P2 必须显式在项目根 `git init` |

命中个人路径的文件（供 P2 决定是否脱敏）：

```
delivery/asuka-v2_20261026/使用与切换说明.md        (2 处，安装路径说明)
docs/06-第三阶段续作状态_工作稿.md                    (1)
docs/07-最终接入与验收报告_工作稿.md                  (2)
work/phase3_20261025/mix_rows_test.py               (1)
work/phase3_20261025/finish_standard_rows.py        (1)
work/phase3_20261025/render_final_previews.py       (1)
work/phase3_20261025/school/qa/register-cardinals-v3.py (1)
work/phase3_20261025/school/qa/school_remaining.py  (1)
work/phase3_20261025/work/qa/diagnose-look-matte.py (1)
work/phase3_20261025/work/qa/finish_recovered_row.py (1)
work/phase3_20261025/work/qa/register-cardinals-recovered-v2.py (1)
```

另：`mixed-test\qa\validation.json`、`pet-quality.json` 内含完整绝对路径（`atlas` 字段），以及 `docs/08`、`docs/06` 新增段落中的安装路径。

### 5.3 局限（未做的事）

- 未联网核实 `waynewayne893` 账号、`asuka-desktop-pet` 仓库是否存在及权限（P1 不使用凭据、未安装 `gh`）。
- 未读取 `.codex` 下 sqlite/`auth.json`（越界且无必要），因此**云端 Pets 记录、活跃宠物 ID 未在本轮独立核验**，仅沿用 `docs/06/07/08` 的自述。
- 图像仅做容器/元数据层检查，未做 LSB 隐写分析或像素级内容复核（后者属 P0 已验收范围，本轮不重复）。
- 未对所有二进制做"逐块"扫描；`.webp/.gif/.mp4` 仅验证头部与主要元数据。
- 未运行官方 `validate_atlas` 等脚本，避免产生新写入文件（符合 P1 只读边界）。

---

## 6. 素材授权逐类结论

> P1 不判断权利归属，只按可核查证据分类。**任何"可上传"结论都以"仓库为 Private 且用户确认"为前提。**

| # | 类别 | 路径 / 文件 | 数量·体积 | 来源与证据 | 结论 |
|---|---|---|---|---|---|
| 1 | 角色本体 IP | 明日香（惣流/式波）×EVA | — | 角色版权归 khara；本项目为同人/个人用途的 AI 生成衍生形象，无授权文件 | **待确认（默认不得公开分发）** |
| 2 | 已批准母版 | `references/approved_baselines/*.png` | 2 · 4.06 MB | AI 生成，派生自第 4 类参考图；哈希已由 `preservation-final.json` 锁定 | **待确认**；Private 归档需用户明确同意 |
| 3 | 用户参考图 | `references/source_refs/*`（8 图 + 说明） | 11 · 1.05 MB | 同名 `说明.md` 原文：「仅用于个人设计核对；**未核实转授权，不要作为可公开分发的最终素材**」 | **不得上传**（建议排除；私有仓库亦建议排除） |
| 4 | 过程素材 | `work/phase2_*`、`work/phase3_*` 下 PNG/GIF/MP4 | ~1,097 · 230.58 MB | 由第 2 类母版衍生；含被拒候选、失败条带、逐帧拆解 | **待确认**；默认排除（体积+授权双风险） |
| 5 | 最终发行素材 | `delivery/asuka-v2_20261026/**`（2 WebP + 2 pet.json + 说明 + SHA256SUMS） | 6 · 3.81 MB | 已安装并交付；同上为角色衍生 | **待确认**（若上传，仅此一处作为唯一发行源） |
| 6 | 制作脚本 | `work/**/*.py`（10）、`render_mp4.cjs` | 11 · 约 0.03 MB | 用户/Agent 自写代码；但**硬编码**官方 skill 缓存绝对路径，`render_mp4.cjs` 还 `require` 了 Codex 运行时内的 Playwright | **可上传（代码权属归用户），但不可复现**；上传前须替换绝对路径 |
| 7 | 文档 | `README.md`、`AGENTS.md`、`docs/00–08`、`docs/04*.txt` | 12 · 约 0.3 MB | 用户自写；`docs/03` 台词为原创风格句（「我可没在等你。」等），**非逐字引用原作台词** | **可上传**（Private） |
| 8 | QA 证据 | `work/**/qa/*.json` 等 | 233 JSON（全仓）· 0.73 MB | 官方工具输出 + 人工审阅记录；含绝对路径 | **待确认**（建议脱敏后随仓库归档，是最有价值的可追溯部分） |
| 9 | 字体 / 语音 / 音乐 / Live2D·Spine / 第三方库 | — | **0** | 全量扩展名扫描：无 `.ttf/.otf/.woff`、无 `.mp3/.wav/.ogg`、无 `.moc3/.skel/.atlas`、无 `node_modules/`、无 `vendor/` | **不适用**（本项目未引入任何第三方资产，故无附加许可义务） |
| 10 | 官方工具链 | `C:\Users\86191\.codex\plugins\cache\openai-curated-remote\work-pets\0.1.6\skills\create-pet`（24 文件） | 不在工作区 | OpenAI 随应用分发的技能包 | **不得复制入库**（不属本项目资产，且未核实其再分发条款） |

**授权小结**：项目**没有**任何可证明的授权文件（无 LICENSE、无授权书、无许可声明）。在角色 IP 与参考图两项未决前，唯一安全的默认动作是：**Private 仓库 + 排除第 3 类 + 其余类别逐项由用户书面确认**。

---

## 7. 允许上传 / 禁止上传清单（P2 的操作依据，尚未执行）

### 7.1 最小可复现集（推荐，约 7.90 MB / 20 文件，另加本报告 1 文件）

| 纳入 | 理由 |
|---|---|
| `README.md`、`AGENTS.md` | 项目说明与协作规则；AGENTS 为内部 AI 规则，Private 下可入库 |
| `docs/00`–`docs/08`、`docs/README_项目综述.md` | 完整设计、实施、验收、混合测试记录 |
| `delivery/asuka-v2_20261026/**`（6 文件） | 唯一发行源 + 自校验清单 |
| `references/approved_baselines/**`（2 文件） | 母版锁定基线（**需 B2 授权确认**） |
| `HANDOFF_P1_Asuka_GitHub_20261026.md`（本文件） | 迁移审计记录本身 |
| 可选：`work/**/qa/*.json` 与 `work/**/README_工作稿.md`（约 1 MB） | 验收证据链；建议脱敏后纳入 |

核心集指纹（供 P2 复核差异）：`20 文件 / 8,282,270 字节 / 排序清单 SHA256 = 9c36d73ff42aab72e6b41a9f9be938fbd9816117cd2e0cb9f81420ed0f40fe2b`（14:22:06 时点，**不含本报告**；加入本报告后为 21 文件）。

### 7.2 排除清单

| 排除 | 理由 |
|---|---|
| `references/source_refs/**` | 说明.md 明示不可公开分发；且含 4 组重复文件 |
| `work/phase2_*/**`、`work/phase3_*/**` 的图像主体（约 230 MB） | 授权未定 + 体积 + 大量被拒候选，属"工作现场"而非交付物 |
| `work/phase3_20261025/mixed-test/**` | 新增未验收测试包；是否归档由用户在 B5 中决定 |
| 任何 `C:\Users\86191\.codex\**` | 应用私有数据，含凭据 |
| `*.tmp`、`Thumbs.db`、`.DS_Store`、编辑器目录 | 当前未发现，但 .gitignore 应预置 |

---

## 8. 发行文件、大文件与重复内容

| 检查 | 结果 | 处置建议 |
|---|---|---|
| > 100 MB 文件（GitHub 硬限） | 无 | — |
| > 45 MB 文件 | 无 | — |
| 最大文件 | 4.83 MB | 无需 LFS |
| 是否需要 Git LFS | **不需要**（git-lfs 3.8.0 已装但不必启用） | 明确不启用，避免引入 LFS 依赖 |
| 是否需要 GitHub Releases | 本轮不需要 | 若日后要分发 `.webp` 宠物包，可作附件，但会公开传播素材 → 先决 B2 |
| 重复内容 | **192 组哈希重复**（母版在 phase2/phase3 各留一份共 5 份；两套最终 WebP 与 `delivery/` 一致各 2 份；GIF 预览跨阶段重复） | 属**刻意留档**（不可变性证据），不建议去重；如担心体积，仅排除 `work/` 整体 |
| 二进制占比 | 99.6%（239 MB 中图像约 238 MB） | 仓库定位"资产归档"，接受二进制为主 |

---

## 9. 文档与可复现性

| 项 | 状态 |
|---|---|
| README | 有（`README.md`，偏"交付说明"，未描述 `work/`、`delivery/`、`docs/05–08`，已过期） |
| 文件清单 | `docs/00-文件清单.md` 仅列到 `docs/04` 与两张母版，**已过期** |
| LICENSE / NOTICE | **完全没有**（全量扫描 0 命中） |
| 依赖锁文件 | **没有**（无 `requirements.txt`、`package-lock.json`、`pnpm-lock.yaml`） |
| 构建说明 | 无构建；`work/*/README_工作稿.md` 提供产物说明 |
| 依赖 | Python + Pillow（运行时可见 12.3.0）；`render_mp4.cjs` 依赖 `C:/Users/86191/.cache/codex-runtimes/.../playwright`；脚本依赖官方 `create-pet/scripts/*.py`（绝对路径） |
| 私有仓库能否独立构建 | **不能**。缺少官方 skill 脚本，且脚本路径写死本机；只能"读得懂、可追溯"，无法"clone 即重制" |

结论：仓库适合作为**档案与决策记录**，不宜宣称"可复现构建"。若用户期望"换一台机器能重做图集"，需要在 P2 之后单列一个"环境与复现说明"任务（超出 P1 范围）。

---

## 10. 阻断项（进入 P2 前必须解决）

| ID | 阻断项 | 证据 | 解除条件 |
|---|---|---|---|
| **B1** | 工作区在审查期间被并发写入（+69 文件 / +4.11 MB），当前不是冻结态 | 第 3 节时间线 | 用户指定冻结时刻，或确认写入方空闲后重新盘点 |
| **B2** | 角色 IP 与用户参考图授权未决；`source_refs/说明.md` 明示不可公开分发 | 第 6 节 | 用户对第 2/4/5 类逐项书面确认；第 3 类保持排除 |
| **B3** | 无 LICENSE，未声明权利状态（默认"全部权利保留"不适用于非权利人） | 第 9 节 | 明确"不添加开源许可证"，并在 README 声明"含第三方角色形象，仅限私人归档，不构成授权" |
| **B4** | Git 身份未配置（`user.name`/`user.email` 为空） | 第 4 节 | 用户提供署名与邮箱（推荐 GitHub noreply 邮箱），在**仓库级**配置，不改全局 |
| **B5** | 上传范围未定（7.90 MB 核心集 vs 239.53 MB 全量） | 第 7 节 | 用户在最小集 / 加 QA JSON / 全量归档中选一 |
| **B6** | 个人绝对路径暴露（11 文件 + 新增 QA JSON 的 `atlas` 字段） | 第 5.2 节 | 决定"原样入库"或"脱敏为 `<USERPROFILE>` 后再入库"（脱敏属内容修改，需单独授权） |
| **B7** | "项目已经上线"的定义需澄清 | 本工作区无应用源码、无部署物 | 若用户所指为其他工程（如 `个人网页建立`），则 P1 目标错位，需重新下发任务书 |

---

## 11. 建议仓库命名与 Private 策略

| 项 | 建议 | 说明 |
|---|---|---|
| Owner | `waynewayne893` | 用户提供；**本轮未联网核实账号与权限** |
| 仓库名 | `asuka-desktop-pet` | 沿用基线建议；语义清楚，避免 `codex-` 前缀（易与官方混淆） |
| 可见性 | **Private** | 角色 IP 未授权 + 含个人路径 + 含内部 Agent 规则，三项均指向 Private |
| 描述 | `Asuka dual-form pet packages for Codex Pets (v2 atlas, local install) — personal archive` | 明示私人归档 |
| 初始化 | 空仓库（不勾选 README/.gitignore/LICENSE） | 避免与本地首提交冲突 |
| 分支 | `main` | 系统默认是 `master`，P2 用 `git init -b main` 指定 |
| 改 Public 的前置 | B2 解除 + 移除 `source_refs`/个人路径 + 更新 README 权利声明 | 否则不建议 |

---

## 12. P2 具体操作建议与验收条件（**本轮均未执行**）

### 12.1 步骤

**Step 0 — 冻结与复核（B1）**
1. 请用户确认写入方已停止（或指定冻结时刻）。
2. 重新执行盘点：文件数、总字节、`git` 不存在、核心集指纹是否等于 `9c36d73f…`（14:22:06 时点）。
3. 若指纹已变，以新快照为准，并更新本文件而非沿用旧数字。

**Step 1 — 用户决策（B2/B3/B4/B5/B6）**
1. 授权类别确认（母版/最终素材/过程素材/QA JSON）。
2. 是否脱敏个人路径。
3. Git 署名与邮箱。
4. 上传范围三选一。

**Step 2 — 本地准备（只写 `.git` 与新配置文件）**
```powershell
# 在项目根执行，绝不加 -C 到父目录
git init -b main
git config user.name  "<用户提供>"
git config user.email "<用户提供>"
git config core.autocrlf false      # 与 system 一致，避免二进制换行污染
```
- 新建 `.gitignore`（建议内容）：
```gitignore
# 工作现场（若选最小集）
/work/
/references/source_refs/
# 迁移审计（可选，按 B5 决定是否入库）
# HANDOFF_P1_Asuka_GitHub_20261026.md
# 系统与编辑器
Thumbs.db
desktop.ini
.DS_Store
*.tmp
```
- 可选 `.gitattributes`：
```gitattributes
* text=auto eol=lf
*.webp binary
*.png  binary
*.gif  binary
*.mp4  binary
```

**Step 3 — 精确暂存（禁止 `git add -A` / `git add .`）**
```powershell
git add README.md AGENTS.md docs delivery references/approved_baselines HANDOFF_P1_Asuka_GitHub_20261026.md
git status --short
git diff --cached --stat
```

**Step 4 — 提交前强制核验**
```powershell
git ls-files | Measure-Object -Line
git ls-files -z | ForEach-Object { ... }        # 逐文件确认无 source_refs / 无 .codex / 无 .env
git count-objects -vH
git diff --cached --numstat | Sort-Object -Descending | Select-Object -First 10
```
- 断言：暂存区不含 `references/source_refs/`、不含 `work/`（若选最小集）、不含任何 `C:\Users\86191\.codex`。

**Step 5 — 停止**
- 仅创建本地首次提交，**不创建远程、不推送**，回到用户与审核 AI 处获取 P3 授权。

### 12.2 P2 验收条件

| # | 验收项 | 通过标准 |
|---|---|---|
| 1 | 冻结一致性 | P2 开始时盘点与 Step 0 记录一致，无并发写入 |
| 2 | 仓库根正确 | `git rev-parse --show-toplevel` 输出恰为项目根，未包含父目录任何文件 |
| 3 | 范围正确 | `git ls-files` 文件数与实测一致；不含排除清单任一路径 |
| 4 | 无敏感物 | 暂存区密钥/证书扫描 0 命中；个人路径按用户决策处理完毕 |
| 5 | 二进制度量 | 用 `git cat-file blob :delivery/asuka-v2_20261026/asuka-school/spritesheet.webp` 取回暂存内容后计算 SHA-256，须等于 `51ecce00…`（同理战斗服 `0d402494…`）；**不可用 `git hash-object` 的 SHA-1 值与 SHA256SUMS 直接比较** |
| 6 | 体积 | 首提交 < 10 MB（最小集）或按用户选择的上限 |
| 7 | 分支与身份 | 分支 `main`；`git log -1 --format='%an <%ae>'` 为用户确认值；未改全局配置 |
| 8 | 未越界 | 无 `git remote`、无 push、`.codex\pets` 三个包哈希不变 |

---

## 13. 已执行 / 未执行 / 待授权

### 13.1 已执行（只读 + 本文件写入）

- 全量盘点：1,128 文件 / 251,165,108 字节；扩展名、目录、最大文件、最长路径、重复组（192）统计。
- 项目识别：桌面二级目录检索、祖先 `.git` 检查、文档交叉核对、排除 `personal-space` 等无关仓库。
- 交付完整性：`SHA256SUMS.txt` 自校验 5/5 通过；三只已安装包与工作区/交付包逐字节比对一致。
- Git 基线：`git --version`、`git lfs version`、全局/系统配置只读查询、凭据助手与 `gh` 存在性。
- 敏感扫描：正则内容扫描 + 扩展名白名单 + 个人路径定位 + 14 张图像元数据解析（母版 2、参考图 10、交付 WebP 2，Pillow 12.3.0）。
- 并发发现：捕获 14:19:48–14:21:38 的 69 文件写入与第三只宠物安装。
- 写入：仅 `HANDOFF_P1_Asuka_GitHub_20261026.md`。

### 13.2 未执行（P1 明令禁止或无需）

- 未 `git init/add/commit/remote/push`；未改任何 Git 配置（含全局）。
- 未创建/删除任何文件（除本报告）；未移动、重命名、压缩、去重。
- 未安装任何依赖；未运行 `pip install`、`npm/pnpm`。
- 未运行官方 `validate_atlas`/`prepare_pet_run`/预览脚本（会产生写入）。
- 未构建、未打包、未启动/重启桌宠、未操作应用 UI、未修改 `.codex\pets`。
- 未联网核实账号/仓库/云端 Pets 记录；未读取凭据文件。

### 13.3 待授权（按优先级）

| 优先级 | 待授权事项 | 归属 |
|---|---|---|
| P0 | 冻结工作区（B1）；确认"已上线"指本资产工程（B7） | 用户 |
| P0 | 素材授权逐类确认（B2）；决定是否添加权利声明而非 LICENSE（B3） | 用户 + 审核 AI |
| P1 | Git 署名/邮箱（B4）；上传范围（B5）；个人路径脱敏与否（B6） | 用户 |
| P1 | 是否允许 P2 新建 `.git`、`.gitignore`、`.gitattributes` | 用户 + 审核 AI |
| P2 | 是否创建 `waynewayne893/asuka-desktop-pet`（Private） | 用户（P3 前置） |
| P2 | 是否需要安装 `gh`（当前 P3 只能网页建仓 + HTTPS 推送） | 用户 |

---

## 14. 局限与未核实事项

1. **未联网**：GitHub 账号、仓库存在性、配额、分支保护、Private 计费均未核实。
2. **云端 Pets 记录未独立核验**：`docs/06` 提到的白龙司书记录 ID、Pets 服务状态，本轮仅沿用文档自述。
3. **时点性**：所有数字为 14:21–14:22 快照；14:19–14:21 已发生两次变更，后续仍可能变化。
4. **未做像素级/隐写级素材审查**：透明边缘、隐藏 RGB、方向语义等属 P0 已验收范围，本轮不重复判定，也不背书。
5. **未验证 Git 在该路径的实际行为**：路径含中文与空格、位于 `D:\HuaweiMoveData`（疑为迁移/同步目录）。P2 首次 `git init` 后应确认无同步冲突与长路径问题。
6. **未评估 192 组重复的取舍**：属 P2 决策；本报告只做记录，不建议在 P1 去重。
7. **第三方工具许可未逐条核对**：Pillow、Playwright、git-lfs 均作为**工具**使用而非打包分发，故未产生随仓库分发的许可义务；若日后 vendor 它们，需重新评估。

---

## 附录 A — 关键哈希

```
# 交付包（与 SHA256SUMS.txt 一致，且与已安装副本一致）
51ecce0097b08e17308cbc90bb4dbf8c7353cabb90e33caf970b8d9a8fe80c29  delivery/asuka-v2_20261026/asuka-school/spritesheet.webp
8f22978ed8105d6b6e023377a5d550406fd220f3cdaeb59dbd429393366e7091  delivery/asuka-v2_20261026/asuka-school/pet.json
0d4024945ca4d5f757eff9afa6c0eb9f1892eadb93f8fdef5ae317c23de45049  delivery/asuka-v2_20261026/asuka-work/spritesheet.webp
0dc5f4aa2a1c4accb0e0fc63ba0ca2cc5fa289f5195b0cf0885ae8454a43aa25  delivery/asuka-v2_20261026/asuka-work/pet.json
f86bfb12d306a86597991ed122f3f5bb6a36495b04ffe21e0c2f988a241b1609  delivery/asuka-v2_20261026/使用与切换说明.md
3bf1f7beb34e76d43b4c116b91d3e099eac481011e7828343313a523e99b97ab  delivery/asuka-v2_20261026/SHA256SUMS.txt

# 母版（preservation-final.json 锁定，未变）
3f3062bc338ac9c9fbb7bbb319b1b7abdab5f8d756dd469ab6838963cbd42524  references/approved_baselines/asuka_school_mode_baseline_v2.png
91f3ddc8ba6171178f222dc5d5532d4c6b46f750be393b69d91792051b6d7747  references/approved_baselines/asuka_white_plugsuit_baseline_v2.png

# 第三只（并发期间新增，未验收）
83aba65992452114a6a4156f6ec9655a3869b3a127b6ab0ce8edf15ccc865fcb  work/phase3_20261025/mixed-test/final/spritesheet.webp

# 核心集指纹（14:22:06 时点，P2 需重算比对）
9c36d73ff42aab72e6b41a9f9be938fbd9816117cd2e0cb9f81420ed0f40fe2b  (20 files, 8,282,270 bytes)
```

## 附录 B — 本轮执行的关键命令（只读）

```text
Get-Location; Get-ChildItem -Force
Get-ChildItem -Recurse -File | Measure-Object Length -Sum       # 盘点
Get-ChildItem -Directory -Filter .git -Recurse -Depth 3         # 无 .git
git --version; git lfs version
git config --global --list; git config --system --list
git config --global --get user.name / user.email                # 空
Get-Command gh                                                  # 未安装
Get-FileHash -Algorithm SHA256 <delivery files>                 # 5/5 通过
Get-FileHash -Algorithm SHA256 <installed files>                # 与交付一致
python -c "PIL.Image.open(...).info"                            # 图像元数据
Select-String -Pattern 'api[_-]?key|secret|passw|bearer|sk-|ghp_|BEGIN .*PRIVATE KEY|token[:=]'
Select-String -Pattern 'C:\\Users\\86191'                       # 11 文件
Get-ChildItem -Recurse -File | Get-FileHash | Group-Object      # 192 重复组
```

---

**P1 到此停止。等待用户与审核 AI 批准 P2；未获批准前不进行任何 Git 初始化、提交或仓库创建。**
