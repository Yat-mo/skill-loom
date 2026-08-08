# Skill Loom

> 把散落的工作流、規則、Prompt 和踩坑經驗，織成真正會觸發、能驗證、可維護、可安全發布的 Agent Skill。

[![Release](https://img.shields.io/github/v/release/Yat-mo/skill-loom?display_name=tag&sort=semver)](https://github.com/Yat-mo/skill-loom/releases)
[![Tests](https://img.shields.io/badge/tests-38%2F38-brightgreen)](#驗證證據)
[![Trigger eval](https://img.shields.io/badge/trigger_eval-27%2F27-brightgreen)](#驗證證據)
[![License](https://img.shields.io/github/license/Yat-mo/skill-loom)](LICENSE)

## 一行安裝

```bash
npx skills add Yat-mo/skill-loom --skill skill-loom
```

確認遠端能找到 Skill：

```bash
npx skills add Yat-mo/skill-loom --list
```

## 你會得到什麼

Skill Loom 不是只生成一份很長的 `SKILL.md`。它會替一個可重複工作建立完整但不臃腫的生命週期：

```text
理解意圖 → 研究同類 → 設計觸發邊界 → 選最小結構
        → 建立 Skill → 執行評測 → 審查證據 → 安裝或發布
```

- 會先判斷任務是否真的值得做成 Skill。
- 會研究 skills.sh、SkillsMP 與 GitHub 的同類方案，再做 `keep / adapt / reject / invent`。
- 會先測 `description` 是否該觸發、是否誤觸發，再增加文件與流程。
- 只在內容真的需要時加入 `references/`、`workflows/`、`scripts/` 或完整路由。
- 公開發布必須經功能分支、PR、Release、遠端發現與隔離安裝驗證。

## 你可以直接这样说

- 「把這套 SOP 做成團隊可重用的 Skill，先研究同類方案。」
- 「改善這個 Skill 的觸發率，補正例、反例和相鄰意圖測試。」
- 「把專案規則整理成可路由的 Codex Skill，不要預製空目錄。」
- 「只審計這個 Skill 的結構與發布風險，先不要改檔。」
- 「發布到 GitHub，必須走 PR、Release 和乾淨安裝驗證。」

不適合用在一次性摘要、普通翻譯、臨時 Prompt、一般 npm/Python 套件發布，或明確不應成為 Skill 的任務。

## 為什麼叫 Skill Loom

`Loom` 是織布機。這個名字對應它真正做的事：

- 原料是規則、流程、文件、腳本和實戰教訓。
- 經線是穩定約束，緯線是不同任務流程。
- 測試與發布門禁負責檢查成品是否牢固。

名稱很新，方法並非憑空出現。Skill Loom 前身是 `qiaomu-meta-skill`，並保留完整上游歸因；`v3.0.0` 是品牌、Skill ID 與倉庫身份的正式切換。

## 三種結構，按壓力升級

```text
Single-file              Folder-light                 Full
└── SKILL.md              ├── SKILL.md                 ├── SKILL.md
                          ├── references/              ├── routing.yaml
                          ├── workflows/               ├── rules/ / gotchas/
                          └── scripts/                 ├── workflows/ / evals/
                                                       └── scripts/ / reports/
```

| 層級 | 何時使用 |
|---|---|
| Single-file | 主題少、沒有任務分流、不需要累積教訓 |
| Folder-light | 有少量獨立參考、流程或可重複腳本 |
| Full | 多條路由、跨工具入口、高代價陷阱或長期治理 |

行數只是提醒，不是拆檔命令。幾個文件如果永遠一起讀，就應該合併。

## 四種使用模式

| 模式 | 適用情況 | 最低證據 |
|---|---|---|
| Scaffold | 個人試驗、低風險 | 有效 frontmatter、自然觸發、明確排除 |
| Production | 團隊重用 | interface、trigger eval、輸出契約、安裝驗證 |
| Library | 跨專案基礎能力 | Skill IR、可攜性、信任邊界、維護節奏 |
| Governed | 公開或高信任流程 | secrets、rollback、PR、Release、乾淨安裝與聲明門禁 |

## 典型輸出

Skill Loom 只建立任務真正需要的資源；完整模式可能包含：

```text
your-skill/
├── SKILL.md
├── agents/
│   ├── interface.yaml
│   └── openai.yaml
├── references/
├── workflows/
├── scripts/
├── evals/trigger_cases.json
├── reports/
├── manifest.json
├── README.md
└── LICENSE
```

`SKILL.md` 是 Agent 的導航入口；README 是給人的產品頁。兩者不互相複製。

## 本地驗證

```bash
python3 scripts/validate_skill.py .
python3 scripts/export_skill_ir.py . --output reports/skill-ir.json
python3 scripts/trigger_eval.py . \
  --cases evals/trigger_cases.json \
  --output reports/trigger-eval.json
python3 scripts/release_check.py . --phase local --run-tests
```

## 驗證證據

`v3.0.0` 的品牌遷移重新執行完整測試；以下數字只證明目前倉庫的結構、觸發、發布與安裝流程，不代表所有下游 Skill 的內容品質：

- 單元測試：`38/38`
- Trigger eval：`27/27`
- Package validation：`0 failures / 0 warnings`
- Published gate：發布後記錄；未發布前視為 `missing evidence`
- 人工長期品質與跨模型表現：`missing evidence`

歷史建立案例與證據邊界見 [Codex Skill History Catalog](reports/codex-skill-catalog.md)。

## 前置條件

- [ ] Node.js 18+：`node --version`
- [ ] npx：`npx --version`
- [ ] Python 3.9+：`python3 --version`
- [ ] 發布時需要 GitHub CLI：`gh auth status`
- [ ] 研究或發布時允許連線至 skills.sh、SkillsMP 與 GitHub

## 權限與安全

- 審計任務保持只讀；只有建立、修改、安裝或發布要求才寫檔。
- 公開研究只讀候選目錄與源碼，不為了研究而執行未審查的第三方腳本。
- Token、Cookie、API key、私有附件與使用者本機路徑不得進入公開產物。
- 發布不直推 `main/master`，也不覆蓋已發布的同版本 Release。
- 公開 Skill 必須有明確 owner；第三方署名與 Profile 不會被自動冒用。

## 從舊名稱遷移

舊 Skill ID `qiaomu-meta-skill` 已由 `skill-loom` 取代：

```bash
npx skills add Yat-mo/skill-loom --skill skill-loom
```

GitHub 會把舊倉庫網址轉到新倉庫；本機路由、指令與自動觸發應改用 `skill-loom`。舊名稱仍保留在 `description` 作遷移別名，避免既有自然語句立即失效。

## Troubleshooting

| 問題 | 常見原因 | 處理方式 |
|---|---|---|
| `No valid skills found` | `SKILL.md` frontmatter 無效 | 執行 `scripts/validate_skill.py` 並修正 name/description |
| Skill 沒有觸發 | description 沒覆蓋使用者自然說法 | 補 trigger case，再跑 `trigger_eval.py` |
| Skill 到處誤觸發 | 缺少排除語句或 near-neighbor | 收窄 description並增加負面案例 |
| `gh: not authenticated` | GitHub CLI 未登入 | 執行 `gh auth login` |
| Release 被拒絕 | 版本已存在或分支不合規 | 提升版本並使用 `codex/` 功能分支 |
| 本機仍看到舊名稱 | 舊安裝目錄仍在 Skill 搜尋路徑 | 備份舊目錄後重新安裝 `skill-loom` |

## 方法來源與致謝

- 直接上游：[joeseesun/qiaomu-meta-skill](https://github.com/joeseesun/qiaomu-meta-skill)
- 方法來源：[yaojingang/yao-meta-skill](https://github.com/yaojingang/yao-meta-skill)
- 發布能力：[joeseesun/qiaomu-skill-publisher](https://github.com/joeseesun/qiaomu-skill-publisher)
- 漸進架構：[WoJiSama/skill-based-architecture](https://github.com/WoJiSama/skill-based-architecture)

同步原則是語義吸收而非整份鏡像：保留來源歸因，也保留 Skill Loom 對 Codex、所有權、漸進架構與證據門禁的獨立判斷。

Upstream inspiration: https://github.com/joeseesun/qiaomu-meta-skill; https://github.com/yaojingang/yao-meta-skill; https://github.com/joeseesun/qiaomu-skill-publisher; https://github.com/WoJiSama/skill-based-architecture

## License

MIT。保留上游作者的授權與歸因；Skill Loom 的新增內容同樣依 MIT 發布。
