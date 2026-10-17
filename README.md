# presentation-builder

給 Claude Code 用的簡報製作 SKILL：先根據你的資料產出一份「簡報版 Markdown」讓你確認架構，確認後才生成 pptx。適用週報、進度報告、成果報告、研究報告等各種報告。

## 安裝

用 git 直接 clone 到 Claude Code 的 skills 資料夾，資料夾名稱要叫 `presentation-builder`：

```bash
# macOS／Linux
git clone https://github.com/npruxjco/presentation-builder-skill ~/.claude/skills/presentation-builder

# Windows（PowerShell）
git clone https://github.com/npruxjco/presentation-builder-skill $env:USERPROFILE\.claude\skills\presentation-builder
```

或下載 zip，解壓後把內容放進上述路徑的 `presentation-builder` 資料夾，使 `SKILL.md` 位於 `skills\presentation-builder\SKILL.md`。

重新開啟 Claude Code 後生效。資料夾裡只有 `SKILL.md` 會被 Claude 當成指令載入；本檔只是給人看的說明。

## 怎麼用

在 Claude Code 裡直接說，例如：

> 幫我把 `report.md` 做成簡報，對象是主管，15 分鐘

或輸入 `/presentation-builder`。

## 它會怎麼做

1. **問清楚欄位**：主題、目的、受眾、時間長度、資料來源。缺的會問你，不會猜。
2. **判斷報告類型**：專案進度或研究報告；看不出來會問你。
3. **產出簡報版 MD**：檔名 `<來源檔名>-slides.md`，放在來源檔旁邊。裡面有簡報架構總覽、每頁的目的、投影片文字、講者備註，開頭還有「需要你先回答的問題」（來源資料有缺漏或矛盾時列在這裡）。
4. **停下來等你確認**：你可以直接改 MD，或回答問題請它修改。想只要大綱的話，到這裡就可以停。
5. **生成 pptx**：確認後才做，內容只依 MD；要改內容就先改 MD，再重新生成。
6. **逐頁檢查並回報**：做了什麼、驗證結果、沒做什麼、需要你決定的事。

## 需要的環境

- Python 與 `python-pptx`（缺少時 Claude 會先問你，並裝在專案外的暫存環境）
- 逐頁轉圖檢查需要 PowerPoint 或 LibreOffice；沒有時 Claude 會在回報中說明沒有檢查到版面

## 簡報的外觀

- 你在專案裡提供一份舊簡報（pptx 或 pdf），Claude 會讀取並沿用它的版型、字型與章節頁寫法。
- 沒有提供時，Claude 會問你要不要給範例簡報；仍沒有就用中性版型（白底、單一字型、清楚層級、頁碼）。
- 想固定自己的風格：在 `references/` 放 `style-default.md`（文字描述版型、字型、配色）與選用的 `style-default-lib.py`（python-pptx 版面函式庫），SKILL 會自動使用。本 repo 不附作者的個人風格。

## 檔案說明

| 檔案 | 用途 |
|---|---|
| `SKILL.md` | 入口：流程與風格解析規則 |
| `references/narrative-core.md` | 通用敘事規則：標題、誠實性、章節與頁面串接、講者備註 |
| `references/prompts-6-steps.md` | 六步驟提示詞與回報格式 |
| `references/report-project.md` | 專案進度報告的檢查項目 |
| `references/report-research.md` | 研究報告的檢查項目（核心問題對照、不能成立的推論） |
| `references/slides-md-format.md` | 簡報版 MD 的格式 |
| `references/style-default.md`、`style-default-lib.py` | 可選，本 repo 不含：你自己的預設風格與版面函式庫，放進來即生效 |

## 想改成自己的規則

直接編輯 `references/` 底下的檔案即可，例如在 `narrative-core.md` 調整標題規範，或新增 `report-xxx.md` 當作新的報告類型（再到 `SKILL.md` 的「確認報告類型」加一行）。
