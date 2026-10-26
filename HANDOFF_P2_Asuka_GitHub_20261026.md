# HANDOFF P2｜明日香桌宠 GitHub 私有迁移 · 本地 Git 基线

**状态：PASS（P2-B 已完成；未创建远程、未推送）**

- 日期：2026-10-26（Asia/Shanghai）
- 执行者：DeepSeek Harness（DSH）会话，受用户第 2 轮指令委托执行 P2
- 项目根：`D:\HuaweiMoveData\Users\86191\Desktop\Codex_Asuka_交付包_v2`
- 上游：`HANDOFF_P1_Asuka_GitHub_20261026.md`、`TASK_P2`（`asuka_p2_task.md`）、`HANDOFF P2 BASELINE`（`asuka_p2_baseline.md`）
- 未来远程（**本轮未创建**）：`waynewayne893/asuka-desktop-pet`（Private）

---

## 0. 结论摘要

| 项 | 结果 |
|---|---|
| Git 初始化 | 已执行 `git init -b main`（项目根） |
| 首提交 | **`c4c075d2b7ae81329cf90310c8639cca2e881925`**（root commit，无父提交） |
| 分支 / 提交数 | `main` / **1** |
| 入库文件 | **23 个 / 8,316,614 字节（7.93 MiB）** |
| 远程 | **无**（`git remote -v` 为空） |
| 推送 | **未执行**（无远程可推） |
| `.git` 占用 | 55 文件 / 8,295,525 字节 |
| 已安装宠物 | 3 只哈希**未变**（见 §8） |
| 母版 | 2 张 SHA-256 **未变**（见 §8） |
| 交付包自校验 | `SHA256SUMS.txt` **5/5 通过** |
| 工作树 | 干净；仅本交接文档 1 个文件未跟踪（见 §11） |

---

## 1. 项目根与最新快照

| 项 | 实测 |
|---|---|
| 当前目录 / `git rev-parse --show-toplevel` | `D:/HuaweiMoveData/Users/86191/Desktop/Codex_Asuka_交付包_v2`（两者一致） |
| 初始化前快照（14:35:16） | 1,130 文件 / 251,197,740 字节 / 239.56 MB |
| 初始化前 `.git` | **不存在**；祖先目录亦无 `.git` |
| 完成后（含 `.git` 与本交接文档） | **1,188 文件 / 259,514,850 字节**（其中 `.git` 55 文件 / 8,295,525 字节） |
| 与 P1 时点差异 | P1 为 1,128 文件 / 251,165,108 字节；增量 = `HANDOFF_P1`（30,806）、`mixed-test/qa/runtime-observation.json`、`AGENTS.md`/`docs/06`/`docs/08` 更新 |
| 最后一次并发写入 | 2026-10-26 **14:26:43**（`AGENTS.md`、`docs/08`、`runtime-observation.json`） |

---

## 2. 五道闸门的解除证据

| 闸门 | 状态 | 证据 |
|---|---|---|
| 1. 其他会话冻结（B1） | **已解除** | 用户于本轮回复「已冻结」；执行前 14:35:16 复检：`NEW_WRITES_SINCE_FREEZE=0`（自 14:26:44 起 8.5 分钟无新写入） |
| 2. 上传范围（B5） | **已解除** | 用户选择「优先采用约 8 MB 核心档案方案」+ 本轮确认「两套图集 + 两张母版都同意」 |
| 3. 第三方衍生素材入 Private（B2） | **已解除（限 Private）** | 用户勾选「两套图集 + 两张母版都同意（完整 7.93 MB 核心档案）」 |
| 4. Git 身份（B4） | **已解除** | 用户选择 `waynewayne893 <waynewayne893@users.noreply.github.com>`；**仅本仓库**配置，全局未改 |
| 5. 隐私处理（B6） | **已解除** | 用户选择「原样入库，不改任何文件」 |
| 6. 根路径 / 完整性 / 权利异常 | **无新异常** | `.git` 原本不存在；交付包 5/5、安装态 3 只、母版 2 张哈希均与 P1 一致 |

> 任务书要求「仅凭 mtime 静止几秒不能视为冻结」。本轮取得的是**用户显式冻结指令**，mtime 仅作事后一致性证据。

---

## 3. Git 操作日志（实际执行）

```text
# 1) 初始化（项目根，未加 -C 到父目录）
git init -b main
#   → Initialized empty Git repository in .../Codex_Asuka_交付包_v2/.git/

# 2) 身份（仅本仓库；未使用 --global）
git config user.name  "waynewayne893"
git config user.email "waynewayne893@users.noreply.github.com"

# 3) 新增规则文件（新建，不覆盖既有文件）
.gitignore      (668 B)
.gitattributes  (246 B)

# 4) README 追加「仓库说明（Git 私有归档）」小节（原 39 行内容未改动，2320 → 3949 B）

# 5) 精确列名暂存（23 个路径逐一列出，未使用 git add . / -A）
git add -- README.md AGENTS.md .gitignore .gitattributes HANDOFF_P1_Asuka_GitHub_20261026.md \
          docs/…（10 个） delivery/asuka-v2_20261026/…（6 个） references/approved_baselines/…（2 个）

# 6) 提交前复核（详见 §7）
git -c core.quotepath=false diff --cached --name-status
git diff-files --quiet                     # exit 0 → 索引与工作区逐字节一致
git ls-files -s / hash-object              # 二进制 blob 与工作区 blob 一致
git ls-files | Measure-Object -Line        # 23
git status --short                         # 空

# 7) 唯一首提交
git commit -m "chore: archive initial Asuka Codex Pets baseline"
```

未执行：`git remote add`、`git push`、`git clone`、`gh repo create`、任何 `--global` 配置、任何历史改写。

---

## 4. 提交事实

```text
SHA          c4c075d2b7ae81329cf90310c8639cca2e881925
短 SHA        c4c075d
TREE         f62ea413671c56072de5c89fcfac148bb474989d
PARENT       （空，root commit）
分支          main（commit 数 = 1）
AUTHOR       waynewayne893 <waynewayne893@users.noreply.github.com>
COMMITTER    waynewayne893 <waynewayne893@users.noreply.github.com>
DATE         2026-10-26 14:36:13 +0800
SUBJECT      chore: archive initial Asuka Codex Pets baseline
```

- `git remote -v` → **空输出**（无远程）。
- `git branch --show-current` → `main`。
- `git rev-list --count HEAD` → `1`。
- 提交后 `git status --short` → 空（除本交接文档，见 §11）。

---

## 5. 实际入库文件（23 个 / 8,316,614 B）

| # | 路径 | 字节 | blob（前 12） |
|---|---|---|---|
| 1 | `.gitattributes` | 246 | `b8ad8a79fa93` |
| 2 | `.gitignore` | 668 | `8a9de5e38312` |
| 3 | `AGENTS.md` | 2,868 | `afe8d798adba` |
| 4 | `HANDOFF_P1_Asuka_GitHub_20261026.md` | 30,806 | `0c3d0fb5c0a3` |
| 5 | `README.md` | 3,949 | `4fde9dff122d` |
| 6 | `delivery/asuka-v2_20261026/SHA256SUMS.txt` | 455 | `1b1d0f7f9a18` |
| 7 | `delivery/asuka-v2_20261026/asuka-school/pet.json` | 248 | `60c68bffc783` |
| 8 | `delivery/asuka-v2_20261026/asuka-school/spritesheet.webp` | 1,971,788 | `c5af54689761` |
| 9 | `delivery/asuka-v2_20261026/asuka-work/pet.json` | 258 | `8759e55285f4` |
| 10 | `delivery/asuka-v2_20261026/asuka-work/spritesheet.webp` | 2,017,070 | `9a2b9b235780` |
| 11 | `delivery/asuka-v2_20261026/使用与切换说明.md` | 1,798 | `18c6201e800e` |
| 12 | `docs/00-文件清单.md` | 412 | `c174dd09a265` |
| 13 | `docs/01-工程实施说明书.md` | 2,074 | `e6d011490a94` |
| 14 | `docs/02-美术规格书.md` | 1,587 | `d1d1ad3ce082` |
| 15 | `docs/03-状态与台词设计表.md` | 1,626 | `64b0cbb32782` |
| 16 | `docs/04-交给Codex的首轮提示词.txt` | 1,558 | `04362e5d7336` |
| 17 | `docs/05-第二阶段实施与验收_工作稿.md` | 5,039 | `85ed9cadb98a` |
| 18 | `docs/06-第三阶段续作状态_工作稿.md` | 5,811 | `e93c193d8e5c` |
| 19 | `docs/07-最终接入与验收报告_工作稿.md` | 5,695 | `1494d6977328` |
| 20 | `docs/08-混合双形态最小测试_工作稿.md` | 3,345 | `188c372bb4e5` |
| 21 | `docs/README_项目综述.md` | 1,703 | `154b340ada5d` |
| 22 | `references/approved_baselines/asuka_school_mode_baseline_v2.png` | 2,272,395 | `0fae8dd4af4a` |
| 23 | `references/approved_baselines/asuka_white_plugsuit_baseline_v2.png` | 1,985,215 | `5a29793c0312` |

二进制度量：`blob` 与工作区文件哈希一致（`diff-files --quiet` exit 0；两个 WebP 与两张 PNG 的 `ls-files -s` 与 `hash-object` 逐项 MATCH）。因 `.gitattributes` 声明 `* -text`，**未发生任何换行符或编码转换**，blob 字节 = 磁盘字节。

---

## 6. 明确排除范围（本地保留，未删除）

| 排除项 | 体积/数量 | 排除依据 | 验证 |
|---|---|---|---|
| `work/` 全部 | **1,098 文件 / 230.58 MB** | 过程素材、失败候选、QA、脚本、`mixed-test/`；用户指令「排除过程素材」 | `git check-ignore` 命中 `.gitignore:6:/work/` |
| `references/source_refs/` | 11 文件 / 1.05 MB | `说明.md` 明示「未核实转授权，不要公开分发」 | `git check-ignore` 命中 `.gitignore:9:/references/source_refs/` |
| `C:\Users\86191\.codex\**` | 不在项目内 | 用户私有数据（`auth.json`、sqlite、sessions） | 仓库根为项目根，非主目录；`.gitignore` 另设 `/.codex/`、`/auth.json`、`/installation_id` |
| `mixed-test/` 测试包 | 67 文件 / 3.91 MB | 未验收素材不自动入库（TASK §1.3） | 位于 `work/` 下，被整体忽略 |

`git status --porcelain --ignored=matching` 仅显示两条：`!! references/source_refs/`、`!! work/`。

> 说明：`docs/08` **作为记录**已入库（描述第三只混合测试及其运行观察），但**测试包本体（图集、QA JSON）未入库**。这是刻意的区分，不是遗漏。

---

## 7. 安全与隐私复核

### 7.1 密钥/凭据扫描（提交前，针对暂存内容）

- 模式：`sk-…`、`ghp_…`、`github_pat_`、`AKIA…`、`BEGIN … PRIVATE KEY`、`api_key[:=]`、`password[:=]`。
- 结果：**1 处命中，经定位为误报**。命中位于 `HANDOFF_P1_Asuka_GitHub_20261026.md` §5.1，内容是本报告自身列出的扫描模式清单：
  `模式含 api[_-]?key、secret、passw、bearer、sk-…、ghp_、github_pat_、AKIA…`
  → 命中 token 为字面量 `github_pat_`，其后无任何凭据串。**非泄露，未修改该文件**（用户选择"不改任何文件"）。
- 真实凭据：**0**。

### 7.2 个人绝对路径（按用户决定原样保留）

| 文件 | `C:\Users\86191` 出现次数 | 是否可脱敏 | 处理 |
|---|---|---|---|
| `HANDOFF_P1_Asuka_GitHub_20261026.md` | 14 | 可（未被哈希锁定） | **保留原样** |
| `docs/07-最终接入与验收报告_工作稿.md` | 2 | 可 | **保留原样** |
| `delivery/asuka-v2_20261026/使用与切换说明.md` | 2 | **不可**（被 `SHA256SUMS.txt` 锁定） | **保留原样** |
| `docs/06-第三阶段续作状态_工作稿.md` | 1 | 可 | **保留原样** |
| `docs/08-混合双形态最小测试_工作稿.md` | 1 | 可 | **保留原样** |
| 合计 | **20** | — | 用户选择「原样入库，不改任何文件」 |

- 未对任何入选文件做内容改写；`delivery` 校验链**未被破坏**（5/5 通过）。
- 新增的 `README.md` 小节只写占位形式 `C:\Users\<用户名>\...`，**未新增**真实路径。
- 残余风险：这些路径暴露本机用户名与目录结构。因仓库为 **Private**，本轮按用户决定接受；若日后改 Public，须先脱敏并重建提交（届时会改变 SHA）。

### 7.3 二进制元数据

沿用 P1 结论：两张母版 PNG 无 `tEXt/iTXt/EXIF`；`source_refs` 未入库；两张交付 WebP 仅 `loop`/`background` 容器字段。本轮未对入库二进制做二次改写。

---

## 8. 完整性证据（提交后复测）

### 8.1 交付包

`delivery/asuka-v2_20261026/SHA256SUMS.txt` 自校验：**5/5 通过，0 失败**。

```
51ecce0097b08e17308cbc90bb4dbf8c7353cabb90e33caf970b8d9a8fe80c29  asuka-school/spritesheet.webp
0d4024945ca4d5f757eff9afa6c0eb9f1892eadb93f8fdef5ae317c23de45049  asuka-work/spritesheet.webp
8f22978ed8105d6b6e023377a5d550406fd220f3cdaeb59dbd429393366e7091  asuka-school/pet.json
0dc5f4aa2a1c4accb0e0fc63ba0ca2cc5fa289f5195b0cf0885ae8454a43aa25  asuka-work/pet.json
f86bfb12d306a86597991ed122f3f5bb6a36495b04ffe21e0c2f988a241b1609  使用与切换说明.md
```

### 8.2 已安装宠物（只读访问，未改动）

| 宠物 | 安装目录 | spritesheet SHA-256 | 与 P1 相比 |
|---|---|---|---|
| `asuka-school` | `%USERPROFILE%\.codex\pets\asuka-school\` | `51ecce00…fe80c29` | 未变 |
| `asuka-work` | `%USERPROFILE%\.codex\pets\asuka-work\` | `0d402494…e45049` | 未变 |
| `asuka-mixed-test` | `%USERPROFILE%\.codex\pets\asuka-mixed-test\` | `83aba659…865fcb` | 未变 |

### 8.3 已批准母版（入库内容 = 磁盘原文件）

```
3f3062bc338ac9c9fbb7bbb319b1b7abdab5f8d756dd469ab6838963cbd42524  asuka_school_mode_baseline_v2.png
91f3ddc8ba6171178f222dc5d5532d4c6b46f750be393b69d91792051b6d7747  asuka_white_plugsuit_baseline_v2.png
```

与 P1 记录的哈希完全一致；`preservation-final.json` 的锁定关系仍成立。

---

## 9. P1 阻断项 B1–B7 处置

| ID | P1 描述 | P2 处置 | 状态 |
|---|---|---|---|
| B1 | 并发写入未冻结 | 用户显式「已冻结」；执行前后两次复检无新写入 | **关闭** |
| B2 | 角色 IP / 参考图授权未决 | 参考图排除；两套图集 + 两张母版经用户逐项同意入 **Private**；README 写明"Private 不等于授权" | **按 Private 关闭**（改 Public 前须重议） |
| B3 | 无 LICENSE | 用户决定不添加开源许可证；README 声明"不提供开源许可证、不声称版权归仓库所有者" | **关闭** |
| B4 | Git 身份缺失 | 仓库级 `user.name`/`user.email` 配置；全局仍为空 | **关闭** |
| B5 | 上传范围未定 | 采用 7.93 MiB 核心档案（23 文件） | **关闭** |
| B6 | 个人路径暴露 | 用户选择原样保留；README 说明并记录残余风险 | **关闭（接受风险）** |
| B7 | "上线"定义 | 沿 P2 BASELINE 认定：本项目为资产工程，"成功"= 三只本地包已安装且用户确认可用 | **关闭** |

---

## 10. 相对 P1 快照的文件改动（仅 3 项，均为本阶段必要写入）

| 文件 | 变化 | 说明 |
|---|---|---|
| `.gitignore` | 新增 668 B | `/work/`、`/references/source_refs/`、`/.codex/`、`/auth.json`、`/installation_id`、系统/编辑器临时文件、`__pycache__/`、`.venv/`、`node_modules/` |
| `.gitattributes` | 新增 246 B | `* -text` + `*.webp/*.png/*.gif/*.jpg/*.mp4 binary`，保证 blob 与磁盘字节一致 |
| `README.md` | 2320 → 3949 B（39 → 55 行，追加 16 行） | 追加「仓库说明（Git 私有归档）」，上文 39 行原文未改 |

未改动：`AGENTS.md`、`docs/` 全部、`delivery/` 全部、`references/approved_baselines/`、`work/` 全部、已安装 Pets、任何 Git 全局配置。

---

## 11. 唯一未跟踪项（预期状态，需 P3 决定）

**本文件 `HANDOFF_P2_Asuka_GitHub_20261026.md` 未入库。**

原因（结构性，非遗漏）：本文件必须记录首提交的完整 SHA，而若把它纳入该提交，SHA 会随其内容改变，形成自指矛盾。任务书同时要求"唯一首次本地 commit"，因此本轮**不再追加第二个提交**。后果：`git status --short` 会显示 1 个 `?? HANDOFF_P2_Asuka_GitHub_20261026.md`。

三种处理方式（P3 或用户选择）：

1. 在推送前作为**第二个提交**（如 `docs: add P2 handoff`）—— 最简单，但会使提交数变 2，需任务书放宽"唯一首提交"。
2. `git commit --amend` 纳入本文件 —— 提交数仍为 1，但**SHA 会改变**（不再是 `c4c075d…`），且本文件内的 SHA 字段将失效，需改为指向 amend 后的新 SHA 并由审核方接受。
3. 保持未跟踪，随 P3 建仓后单独提交或永不入库。

默认建议：**方式 1**，并在 P3 一并推送。

---

## 12. 风险与遗留

| # | 风险 | 影响 | 建议 |
|---|---|---|---|
| R1 | 仓库含第三方角色（EVA/明日香）同人衍生素材，无再分发许可 | 若改 Public 或对外分发将构成侵权风险 | 保持 Private；不得改可见性；不公开发布素材 |
| R2 | 20 处本机绝对路径（含用户名）已入库 | 隐私轻度暴露 | 改 Public 前必须清理并重建历史 |
| R3 | 无 LICENSE 且未声明权利归属 | 可能被误认为开源 | README 已声明；后续不添加开源许可 |
| R4 | 本交接文档未跟踪（§11） | `git status` 非全空 | P3 决定并入方式 |
| R5 | 仓库位于 `D:\HuaweiMoveData\…`（中文 + 空格路径，疑同步目录） | 克隆/推送可能出现同步冲突或长路径问题 | P3 推送前确认目录未被同步工具占用；必要时在新路径克隆验证 |
| R6 | `work/` 230 MB 仅存于单机 | 单点丢失风险 | 建议另行离线备份（不在本阶段范围） |
| R7 | 尚无远程，未验证 GitHub 端可达性 | P3 可能遇账号/权限/配额问题 | P3 前确认 `waynewayne893` 登录状态与 Private 权限 |

---

## 13. 已执行 / 未执行 / 待批准

### 13.1 已执行

- 只读复核：快照、`.git` 不存在性、交付包 5/5、安装态 3 只、母版 2 张。
- 新增 `.gitignore`、`.gitattributes`；`README.md` 追加仓库说明（不改原文）。
- `git init -b main`；仓库级 `user.name`/`user.email`。
- 精确列名暂存 23 个路径；提交前 6 项复核（名单、排除断言、`diff-files`、blob 一致性、计数、`status`）。
- 创建唯一首提交 `c4c075d2b7ae81329cf90310c8639cca2e881925`。
- 提交后复测：`git cat-file -p HEAD`、`ls-tree -r -l`、`count-objects -vH`、交付包与安装态哈希。
- 生成本交接文档。

### 13.2 未执行

- 未创建远程、未 `git remote add`、未 `push`、未创建 GitHub 仓库、未设置可见性。
- 未修改 `.codex`、未重装/切换 Pets、未运行任何制作或渲染脚本。
- 未修改母版、未改动 `delivery` 任一字节、未删除 `work/` 任何文件。
- 未修改 Git 全局配置（`git config --global --list` 仍只有 `safe.directory`）。
- 未安装任何依赖（未使用 `gh`、未装 LFS 钩子之外的组件）。

### 13.3 待批准（P3 前置）

1. 确认 `waynewayne893` 已在 GitHub 登录且具备建 Private 仓库权限。
2. 在网页创建**空**仓库 `asuka-desktop-pet`（Private，**不勾选** README/.gitignore/LICENSE）。
3. 决定 `HANDOFF_P2` 并入方式（§11，建议方式 1）。
4. 授权 `git remote add origin` 与首次 `push`（HTTPS + Git Credential Manager）。
5. 确认推送前再次冻结其他会话，并在推送后核对远端 23 文件 / 7.93 MiB。

---

## 14. 复核方法（供审核方复算）

```powershell
cd "D:\HuaweiMoveData\Users\86191\Desktop\Codex_Asuka_交付包_v2"

git rev-parse HEAD                 # c4c075d2b7ae81329cf90310c8639cca2e881925
git cat-file -p HEAD               # tree f62ea41… / author / subject
git rev-list --count HEAD          # 1
git branch --show-current          # main
git remote -v                      # 空
git ls-files | Measure-Object -Line        # 23
git ls-tree -r -l HEAD                      # 逐文件字节数，合计 8,316,614
git count-objects -vH                       # size 7.88 MiB
git status --short --ignored=matching       # !! work/ ; !! references/source_refs/ ; ?? HANDOFF_P2…

# 交付链复算
Get-Content delivery\asuka-v2_20261026\SHA256SUMS.txt |
  Select-String -Pattern '^([0-9a-f]{64})\s+(.+)$' |
  ForEach-Object { (Get-FileHash -Algorithm SHA256 ("delivery\asuka-v2_20261026\" + $_.Matches[0].Groups[2].Value.Trim())).Hash.ToLower() -eq $_.Matches[0].Groups[1].Value }
# → 5 个 True

# 二进制 blob 与磁盘一致（以战斗服为例）
(git ls-files -s -- delivery/asuka-v2_20261026/asuka-work/spritesheet.webp).Split()[1]   # 9a2b9b235780…
git hash-object -- delivery/asuka-v2_20261026/asuka-work/spritesheet.webp                # 同上
```

---

**P2 到此完成并停止。未创建远程、未推送、未公开任何内容。等待 ChatGPT 审核与 P3 授权。**
