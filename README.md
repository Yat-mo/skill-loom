# Skill Loom

> 簡單說：這是一個「幫你製作和維護 Agent Skill 的 Skill」。

[![Release](https://img.shields.io/github/v/release/Yat-mo/skill-loom?display_name=tag&sort=semver)](https://github.com/Yat-mo/skill-loom/releases)
[![Tests](https://img.shields.io/badge/tests-39%2F39-brightgreen)](#給開發者的驗證資料)
[![License](https://img.shields.io/github/license/Yat-mo/skill-loom)](LICENSE)

## Agent Skill 是什麼？

Agent Skill 可以理解成一份給 AI 使用的工作手冊。

例如，你每次都要重新告訴 AI：

- 寫報告時要遵守什麼格式；
- 修 Bug 時要先檢查哪些地方；
- 發布內容前要做哪些確認；
- 哪些事情可以做，哪些事情不能做。

把這些規則、步驟和工具整理成一個資料夾後，AI 便能在遇到相同任務時主動讀取和使用。這個資料夾就是一個 Agent Skill。

## Skill Loom 能幫你做什麼？

你把現有的流程、筆記、Prompt、SOP、文件或舊 Skill 交給它，它會幫你：

1. 判斷這件事是否值得做成 Skill。
2. 整理真正需要保留的規則和步驟。
3. 建立或修改 Skill 文件。
4. 測試 AI 會不會在正確的時候使用它。
5. 檢查安裝後能否正常被 Codex、Claude Code 等工具找到。
6. 只有你明確要求時，才會發布到 GitHub。

它不只是把一段 Prompt 改名為 `SKILL.md`，也不會為了看起來完整而建立一堆空資料夾。

## 安裝

```bash
npx skills add Yat-mo/skill-loom --skill skill-loom
```

查看是否能找到這個 Skill：

```bash
npx skills add Yat-mo/skill-loom --list
```

## 你可以直接這樣說

- 「把這套客服處理流程做成一個 Skill。」
- 「把這份 SOP 和幾個腳本整理成團隊可以重複使用的 Skill。」
- 「這個 Skill 經常沒有被 AI 使用，幫我找出原因並改善。」
- 「只檢查這個 Skill 有什麼問題，先不要修改文件。」
- 「把這個 Skill 發布到 GitHub，並確認其他人可以正常安裝。」

你不需要先懂 Skill 的目錄結構，也不需要指定要建立哪些文件。先把你希望 AI 重複做好什麼說清楚即可。

## 一個實際例子

假設你每星期都要整理一次產品數據。你可以說：

> 我每星期都要讀取三份 CSV，找出異常數字，再按固定格式寫週報。請把這個流程做成 Skill。

Skill Loom 會先確認輸入、輸出和不能出錯的地方，再按需要建立：

```text
weekly-report/
├── SKILL.md              # 告訴 AI 何時使用，以及基本做法
├── references/           # 報告格式或欄位說明
├── scripts/              # 可以重複執行的檢查程式
├── evals/                # 測試 AI 會不會正確使用這個 Skill
└── README.md              # 給人看的安裝和使用說明
```

如果流程很簡單，它可能只建立一份 `SKILL.md`。只有內容真的需要時，才會加入其他文件。

## 哪些情況適合使用？

適合：

- 同一套指示已經向 AI 重複說過很多次。
- 團隊希望所有 AI 都遵守相同做法。
- 現有 Skill 太長、經常誤觸發或完全不觸發。
- 想檢查 Skill 是否能安裝、測試或安全發布。
- 想把專案規則整理成 AI 每次工作前會讀取的資料。

不適合：

- 只做一次的摘要、翻譯或普通文件整理。
- 只是想問一個問題，沒有重複使用的需要。
- 一般 npm、Python 套件或 App 的發布工作。
- 你已經明確說不要把內容做成 Skill。

## 它會不會擅自修改或發布？

不會。

- 你說「只檢查」時，它只會報告問題。
- 你說「建立」或「修改」時，它才會更改 Skill 文件。
- 你明確說「發布到 GitHub」時，它才會建立分支和 Pull Request。
- 它不會直接把內容推送到 `main`，也不會把 Token、Cookie 或 API key 寫進公開倉庫。

## 會產生哪些文件？

| 文件 | 白話說明 |
|---|---|
| `SKILL.md` | AI 的入口，說明何時使用和怎樣完成任務 |
| `README.md` | 給人看的安裝與使用說明 |
| `references/` | 需要時才讀取的背景資料 |
| `scripts/` | 重複工作使用的程式，不必每次由 AI 重寫 |
| `evals/` | 測試哪些說法應該觸發或不應觸發 Skill |
| `reports/` | 保存測試結果和已知限制 |

簡單 Skill 不需要擁有全部文件。

## 發布到 GitHub 時會做什麼？

只有在你明確要求發布時，Skill Loom 才會：

1. 檢查 Skill 名稱、版本和必要文件。
2. 檢查是否意外包含密碼或 Token。
3. 建立獨立分支和 Pull Request。
4. 測試通過後才合併。
5. 建立版本 Release。
6. 用全新臨時環境重新安裝一次，確認別人也能安裝。

## 前置條件

- [ ] Node.js 18 或以上：`node --version`
- [ ] npx：`npx --version`
- [ ] Python 3.9 或以上：`python3 --version`
- [ ] 只有發布到 GitHub 時才需要 GitHub CLI：`gh auth status`

## 配置

一般建立和修改 Skill 不需要 API key。

搜尋公開 Skill 時需要網絡連線；發布到 GitHub 時需要已登入的 `gh`。任何憑證都應保留在本機，不要寫進 Skill 文件。

## 給開發者的驗證資料

這一節是給維護者看的；一般使用者可以跳過。

```bash
python3 scripts/validate_skill.py .
python3 scripts/trigger_eval.py . \
  --cases evals/trigger_cases.json \
  --output reports/trigger-eval.json
python3 scripts/release_check.py . --phase local --run-tests
```

目前版本的自動檢查結果：

- 單元測試：`39/39`
- 觸發測試：`27/27`
- 套件檢查：`0 failures / 0 warnings`

這些結果證明安裝、觸發和發布流程通過檢查，不代表每一個由它建立的 Skill 都必然內容優秀。內容品質仍需要按實際用途驗收。

## Troubleshooting

| 遇到的問題 | 常見原因 | 解決方法 |
|---|---|---|
| 安裝後找不到 `skill-loom` | 安裝位置不是目前 Agent 使用的目錄 | 重新執行安裝命令，並指定正確 Agent |
| AI 沒有使用某個 Skill | `description` 沒有寫中使用者的自然說法 | 增加實際說法作為測試，再改善描述 |
| AI 在不相關任務也使用 Skill | 缺少「不適用情況」和反例 | 補上排除條件與不應觸發的測試 |
| `gh: not authenticated` | GitHub CLI 尚未登入 | 執行 `gh auth login` |
| Release 被拒絕 | 版本已存在，或發布分支不符合要求 | 提升版本並使用新的功能分支 |

## 舊名稱

Skill Loom 的舊名稱是 `qiaomu-meta-skill`。GitHub 舊網址會自動轉到目前倉庫；新的安裝、指令和路由應使用 `skill-loom`。

## 方法來源與致謝

- [joeseesun/qiaomu-meta-skill](https://github.com/joeseesun/qiaomu-meta-skill)
- [yaojingang/yao-meta-skill](https://github.com/yaojingang/yao-meta-skill)
- [joeseesun/qiaomu-skill-publisher](https://github.com/joeseesun/qiaomu-skill-publisher)
- [WoJiSama/skill-based-architecture](https://github.com/WoJiSama/skill-based-architecture)

Upstream inspiration: https://github.com/joeseesun/qiaomu-meta-skill; https://github.com/yaojingang/yao-meta-skill; https://github.com/joeseesun/qiaomu-skill-publisher; https://github.com/WoJiSama/skill-based-architecture

## License

MIT
