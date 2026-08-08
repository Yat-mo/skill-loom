# Qiaomu Meta Skill — Yat-mo Fork

> 把零散的流程、規則、Prompt、SOP 或舊 Skill，變成能準確觸發、可驗證、可維護、可安全發布的 Agent Skill。

[![Release](https://img.shields.io/github/v/release/Yat-mo/qiaomu-meta-skill?display_name=tag&sort=semver)](https://github.com/Yat-mo/qiaomu-meta-skill/releases)
[![Last commit](https://img.shields.io/github/last-commit/Yat-mo/qiaomu-meta-skill)](https://github.com/Yat-mo/qiaomu-meta-skill/commits/main)
[![License](https://img.shields.io/github/license/Yat-mo/qiaomu-meta-skill)](LICENSE)

## 一行安裝

```bash
npx skills add Yat-mo/qiaomu-meta-skill --skill qiaomu-meta-skill
```

確認公開來源可被發現：

```bash
npx skills add Yat-mo/qiaomu-meta-skill --list
```

## 為什麼值得用

一般 Skill 產生器通常只幫你寫出一份 `SKILL.md`。這個 Fork 處理的是完整生命週期：

1. 判斷需求是否真的值得做成 Skill。
2. 搜尋 skills.sh、SkillsMP 與 GitHub 上的同類方案。
3. 用 `keep / adapt / reject / invent` 取長補短，不拼貼別人的文字。
4. 先測 `description` 的觸發與排除邊界。
5. 按實際壓力選擇最小結構，不先搭空架子。
6. 驗證格式、版本、所有權、秘密資訊與證據聲明。
7. 只有在明確授權時，才經功能分支、PR、Release 與乾淨安裝發布。

## Yat-mo Fork 改了什麼

| 項目 | 這個 Fork 的做法 |
|---|---|
| 預設用途 | Codex 的一般 Skill 建立、改良、遷移、評測與發布權威 |
| 結構 | `Single-file → Folder-light → Full`，按真實壓力逐級增加 |
| 核心原則 | 結構服務內容、激活優於存儲、結構可復用但內容不能預製 |
| 規則寫法 | 重要原則必須附可執行命令或具體檢驗句 |
| 多輪會話 | 每個新任務重新匹配路由，不沿用上一任務的 workflow |
| Codex 支援 | 內建並驗證 `agents/openai.yaml` |
| 所有權 | 發布時必須明確指定 owner，不替第三方產物強加喬木署名 |
| 相容性 | 修正內建 SkillsMP 搜尋在 Python 3.9 的 `datetime.UTC` 問題 |

詳細方法見 [Progressive Skill Architecture](references/progressive-skill-architecture.md)。

## 你可以直接这样说

- 「把這套 SOP 做成一個團隊可重用的 Skill，先研究同類方案。」
- 「改善這個 Skill 的觸發率，補 should-trigger、should-not-trigger 和 near-neighbor。」
- 「把專案規則整理成可路由、可維護的 Codex Skill，不要預製沒證據的內容。」
- 「只審計這個 Skill 的結構與發布風險，先不要改檔。」
- 「把這個 Skill 發布到 GitHub，必須走 PR、Release 和乾淨安裝驗證。」

不適合：

- 一次性的摘要、翻譯或普通文件整理
- 不打算重複使用的臨時 Prompt
- 一般 Python/npm 套件發布
- 明確要求「不要做成 Skill」的任務

## 三種結構層級

```text
Single-file
└── SKILL.md

Folder-light
├── SKILL.md
├── references/
├── workflows/
└── scripts/

Full
├── SKILL.md
├── routing.yaml
├── rules/ / gotchas/
├── workflows/ / references/
├── scripts/ / evals/ / reports/
└── 按目標平台生成的 adapters 或 hooks
```

只有在多條獨立任務路由、反覆出現的高代價陷阱、跨工具入口或真實 route drift 已出現時，才升級到 Full。

## 產出

依模式與風險，可能產生：

```text
your-skill/
├── SKILL.md
├── agents/
│   ├── interface.yaml
│   └── openai.yaml
├── references/
├── scripts/
├── evals/trigger_cases.json
├── reports/
├── manifest.json
├── README.md
└── LICENSE
```

個人試驗不會被迫擁有完整目錄；公開或高風險 Skill 才需要完整證據與發布門禁。

## 模式

| 模式 | 適用情況 | 最低要求 |
|---|---|---|
| Scaffold | 個人試驗、低風險 | 有效 frontmatter、自然觸發與明確排除 |
| Production | 團隊重用 | interface、trigger eval、輸出契約、安裝證據 |
| Library | 跨專案基礎能力 | Skill IR、可攜性、信任邊界、維護節奏 |
| Governed | 公開或高信任流程 | secrets、rollback、PR、Release、乾淨安裝與聲明門禁 |

## 驗證證據

Yat-mo Fork v2.9.1 沿用 v2.9.0 的行為，這次只重寫公開 README。最近一次完整行為驗證：

- 單元測試：`38/38`
- Trigger eval：`27/27`
- 包驗證：`0 failures / 0 warnings`
- 先例研究：skills.sh 與 SkillsMP 共 `2/2` 查詢成功，51 個去重候選家族
- Published gate：`10 pass / 0 block`
- 公開發現與隔離安裝：通過

這些證據只證明結構、觸發、發布與安裝流程；真實專案長期效果與人工品質比較仍是 `missing evidence`。
歷史建立案例保留在 [Codex Skill History Catalog](reports/codex-skill-catalog.md)，不再塞進首頁。

## 本地驗證

```bash
python3 scripts/validate_skill.py .
python3 scripts/trigger_eval.py . \
  --cases evals/trigger_cases.json \
  --output reports/trigger-eval.json
python3 scripts/release_check.py . --phase local --run-tests
```

## 前置條件

- [ ] Node.js 18+：`node --version`
- [ ] npx：`npx --version`
- [ ] Python 3.9+：`python3 --version`
- [ ] 發布時需要 GitHub CLI：`gh auth status`
- [ ] 搜尋或發布時允許連線至 skills.sh、SkillsMP 與 GitHub

## 權限與安全

- 審計任務保持只讀；只有建立、修改或發布要求才寫檔。
- 公開研究只讀取候選的目錄資料與源碼，不執行未審查的第三方腳本。
- Token、Cookie、API key、私有附件與本機絕對路徑不得進入公開產物。
- 發布不直推 `main/master`，不覆蓋已發布的同版本 Release。
- owner 必須明確；只有喬木本人所有的套件才會注入喬木 Profile。

## 更新與上游同步

此 Fork 追蹤：

- 直接上游：[joeseesun/qiaomu-meta-skill](https://github.com/joeseesun/qiaomu-meta-skill)
- 架構方法：[WoJiSama/skill-based-architecture](https://github.com/WoJiSama/skill-based-architecture)
- 方法來源：[yaojingang/yao-meta-skill](https://github.com/yaojingang/yao-meta-skill)
- 發布能力：[joeseesun/qiaomu-skill-publisher](https://github.com/joeseesun/qiaomu-skill-publisher)

同步原則：追蹤上游，但把 Yat-mo 的 Codex 路由、所有權、平台適配與漸進架構保留為經審查的客製 patch。

Upstream inspiration: https://github.com/joeseesun/qiaomu-meta-skill; https://github.com/yaojingang/yao-meta-skill; https://github.com/joeseesun/qiaomu-skill-publisher; https://github.com/WoJiSama/skill-based-architecture

## Troubleshooting

| 問題 | 常見原因 | 處理方式 |
|---|---|---|
| `No valid skills found` | `SKILL.md` frontmatter 無效 | 執行 `scripts/validate_skill.py` 並修正 name/description |
| Skill 沒有觸發 | description 沒覆蓋使用者自然說法 | 補 trigger case，再跑 `trigger_eval.py` |
| Skill 到處誤觸發 | 缺少排除語句或 near-neighbor | 收窄 description，增加負面案例 |
| `gh: not authenticated` | GitHub CLI 未登入 | 執行 `gh auth login` |
| Release 被拒絕 | 版本已存在或不是 `codex/` 分支 | 提升 patch 版本並使用合規功能分支 |
| 安裝副本跑 published gate 失敗 | 下載包沒有 `.git` remote | 在 Git checkout 執行 published gate；下載包只跑包與 trigger 驗證 |

## License

MIT。保留原上游作者的授權與歸因；Yat-mo Fork 的新增內容同樣依 MIT 發布。
