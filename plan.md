# 一、整體三個月目標

## 總目標

完成一套可交接、可驗證、可追蹤的 OAI / Ariel cuBB / RU E2E 研究流程。

| 月份  | 月目標                                                                  | 月檢查點 |
| --- | -------------------------------------------------------------------- | ---- |
| 7 月 | 完成 OAI + Ariel cuBB + Pegatron RU E2E 建立與 OAI + Pegatron RU E2E baseline 比較表 | 7/31 |
| 8 月 | 完成 Metanoia MOSART 開源碼研究，建立 build / config / parameter / mapping 文件，留下可交接的研究文件  | 8/28 |
| 9 月 | 完成 OAI + Ariel cuBB + Metanoia RU 整合測試、驗證報告與最終交接文件                   | 9/26 |

---

# 二、每週里程碑總表

| 週次    | 日期        | 週五檢查點 | 週里程碑                                                   | 預期總進度 |
| ----- | --------- | ----- | ------------------------------------------------------ | ----: |
| W1    | 7/1–7/3   | 7/3   | 完成兩組已知成功設定檔的背景資料整理，建立後續比較與 Pegatron RU 對接 Ariel cuBB 的基礎                               | 8%   |
| W2    | 7/6–7/10  | 7/10  | 根據 W1 完成的 OAI + Pegatron RU 與 OAI + cuBB for WNC RU 設定檔整理，補齊參數意義、資料型態、範圍與 Need Confirm 項目，並整理出 Pegatron RU 對接 Ariel cuBB 時需要對齊或修改的參數清單。  |  16% |
| W3    | 7/13–7/17 | 7/17  | 根據 W1 / W2 的設定檔比較結果，整理 Pegatron RU 對接 Ariel cuBB 時需要修改或確認的參數，建立 OAI + Ariel cuBB + Pegatron RU 初版 config pack 與 launch readiness checklist。                           | 24%  |
| W4    | 7/20–7/24 | 7/24  | 根據 W1 / W2 / W3 的設定檔比較、mapping checklist 與 config pack，嘗試跑通 OAI L2/L3 + Ariel cuBB + Pegatron RU E2E，並留下完整 experiment log。                                    | 32%  |
| W5    | 7/27–7/31 | 7/31  | 整理 7 月兩階段比較結果：第一階段比較 OAI + Pegatron RU 與 OAI + cuBB for WNC RU 的成功設定檔差異；第二階段比較 OAI + Pegatron RU baseline 與 OAI + Ariel cuBB + Pegatron RU attempt 的設定、log、狀態與限制，完成 7 月月報。            | 40%  |
| W6    | 8/3–8/7   | 8/7   | 完成 Metanoia repo 初步研究，找出 source tree、README、build/config 入口                  |   48% |
| W7    | 8/10–8/14 | 8/14  | 完成 Metanoia build / run / config 初版研究，留下 build log 與 runtime notes             |   56% |
| W8    | 8/17–8/21 | 8/21  | 完成 Metanoia RU 參數與介面研究，建立 Pegatron RU vs Metanoia RU 比較                     |   64% |
| W9    | 8/24–8/28 | 8/28  | 完成 Metanoia 開源碼研究總結，產出 9 月整合可行性與計畫                                    |   72% |
| W10   | 8/31-9/4  | 9/4   |建立 OAI + Ariel cuBB + Metanoia RU 初版 config pack 與 launch flow                      | 78%  |
| W11   | 9/7–9/11  | 9/11  |完成第一次 OAI + Ariel cuBB + Metanoia RU launch attempt                                 | 84% |
| W12   | 9/14–9/18 | 9/18  |完成第二次測試 / debug / 狀態判定，建立與 Pegatron RU 版本比較初版                          | 92% |
| W13   | 9/21–9/25 | 9/25  |完成最終驗證報告、comparison、handover guide                                              | 98% |
| Final | 9/26      | 9/26  |最終檢查點                                                                               | 100% |


# 三、週計畫

## 工時估算原則

每日預估工時以 6–7 小時為基準；9 月因開學，預估工時以 4–6 小時為基準。

每一天通常安排一個主要工作，但實際工時包含資料查找、參數確認、文件整理、log / evidence 整理、Pending / Blocked 紀錄，以及隔天工作準備。

若主要工作提前完成，剩餘時間用於補齊本週其他產出；若主要工作無法完成，則保留目前進度、blocked reason 與 next step。

本計畫中的完成度代表文件與 evidence 完整度，不代表實驗、build 或 E2E 一定成功。


# W1：2026/7/1（三）–2026/7/3（五）

## 週里程碑

完成兩組已知成功設定檔的背景資料整理，建立後續比較與 Pegatron RU 對接 Ariel cuBB 的基礎。

本週重點不是先嘗試 E2E launch，而是先完成：

1. OAI + Pegatron RU 成功設定檔介紹
2. OAI + cuBB for WNC RU 成功設定檔介紹
3. OAI + Pegatron RU 與 OAI + cuBB for WNC RU 的初步差異比較

## 協作者與分工

| 協作者 | 角色 | 分工 |
|---|---|---|
| Kuan | Owner | 負責整理設定檔、建立參數表、補 hyperlink、完成 mapping、comparison 與 checkpoint |
| Ming | Supporter | 協助提供 OAI + Pegatron RU E2E 成功的 gNB / RU 設定檔位置、command、log 與成功條件 |
| Richard | Supporter | 協助提供 OAI + cuBB for WNC RU 設定檔位置、NVIDIA / Aerial 文件入口與 WNC RU 頻段、型號 |
| Professor | Reviewer | 檢查研究方向與產出是否符合「直接比較設定檔差異」的目標 |

## 每日工作

| 日期 | 主要工作 | 預估工時 | 補充工作 / 緩衝 | 截止日期 | 預期產出 |
|---|---|---:|---|---|---|
| 7/1（三） | 找出學長做 OAI + Pegatron RU E2E 成功的 gNB 與 RU 設定檔，並列出 Pegatron RU 頻段、型號 | 10min | 若路徑或型號不確定，直接問 Ming | 7/1 | [oai-pegatron-baseline.md][oai-pegatron-baseline] |
| 7/1（三） | 用表格介紹 OAI + Pegatron RU 的 gNB 設定檔參數 | 2h | 不知道的參數意義、資料型態或範圍先留白，Status 標記 Need Confirm，不硬猜 | 7/1 | [oai-gnb-parameter-table.md][oai-gnb-parameter-table] |
| 7/1（三） | 用表格介紹 Pegatron RU 設定檔參數 | 2h | 不知道的參數意義、資料型態或範圍先留白，Status 標記 Need Confirm，不硬猜 | 7/1 | [pegatron-ru-parameter-table.md][pegatron-ru-parameter-table] |
| 7/1（三） | 用第三個表格整理 OAI gNB 與 Pegatron RU 的相對對應參數 | 3h | 優先整理 frequency、bandwidth、SCS / numerology、TDD、IP / port、clock / sync、antenna、gain、fronthaul；找不到對應關係的項目標記 Need Confirm | 7/1 | [oai-gnb-to-pegatron-ru-parameter-mapping.md][oai-gnb-to-pegatron-ru-parameter-mapping] |
| 7/2（四） | LAB workshop | 6h | 無，該日以 workshop 為主；若有空檔，回填 7/1 文件中 Need Confirm 的欄位 | 7/2 | 無需技術產出，只列入行程 |
| 7/3（五） | 找出 OAI + cuBB for WNC RU 的 gNB 設定檔，例如 `xxWNC.html`，並查出 WNC RU 頻段、型號 | 30min | 若找不到設定檔或型號，直接問 Richard；若 NVIDIA 文件未寫清楚，標記 Need Confirm | 7/3 | [wnc-ru-config-index.md][wnc-ru-config-index] |
| 7/3（五） | 用一個表格介紹 OAI + cuBB for WNC RU 的 gNB 設定檔 | 3h | 將 `xxWNC.html` 中與 RU 對接相關的參數整理成表格；未知意義、範圍、型態先留白並標記 Need Confirm | 7/3 | [aerial-cubb-parameter-table.md][aerial-cubb-parameter-table] |
| 7/3（五） | 用一個表格比較 OAI + Pegatron RU 與 OAI + cuBB for WNC RU 的設定檔差異 | 3h | 只比較兩組已知成功設定檔，不延伸到 E2E launch；差異不確定的項目標記 Need Confirm | 7/3 | [oai-pegatron-vs-oai-aerial-pegatron-comparison.md][oai-pegatron-vs-oai-aerial-pegatron-comparison] |
| 7/3（五） | W1 checkpoint：檢查兩組設定檔資料是否已整理成可比較狀態 | 30min | 補齊文件連結、整理 Done / Pending / Blocked，列出下週要問 Ming / Johnson / Richard 的問題 | 7/3 | [week1-checkpoint.md][week1-checkpoint] |

## 本週產出與百分比

| 產出 | 完成度 | 截止日期 |
|---|---:|---|
| [oai-pegatron-baseline.md][oai-pegatron-baseline] | 60% | 7/1 |
| [oai-gnb-parameter-table.md][oai-gnb-parameter-table] | 50% | 7/1 |
| [pegatron-ru-parameter-table.md][pegatron-ru-parameter-table] | 50% | 7/1 |
| [oai-gnb-to-pegatron-ru-parameter-mapping.md][oai-gnb-to-pegatron-ru-parameter-mapping] | 50% | 7/1 |
| [wnc-ru-config-index.md][wnc-ru-config-index] | 60% | 7/3 |
| [aerial-cubb-parameter-table.md][aerial-cubb-parameter-table] | 60% | 7/3 |
| [oai-pegatron-vs-oai-aerial-pegatron-comparison.md][oai-pegatron-vs-oai-aerial-pegatron-comparison] | 40% | 7/3 |
| [week1-checkpoint.md][week1-checkpoint] | 100% | 7/3 |

## 7/3 通過標準

| 檢查項目 | 通過標準 |
|---|---|
| OAI + Pegatron RU 設定檔來源 | [oai-pegatron-baseline.md][oai-pegatron-baseline] 中有列出 gNB 設定檔路徑、RU 設定檔路徑、Pegatron RU 頻段、型號、資料來源；若不知道，需標記 Need Confirm 並寫明要問 Ming 或 Johnson |
| OAI gNB 參數表 | [oai-gnb-parameter-table.md][oai-gnb-parameter-table] 中已用表格列出 gNB 設定檔參數，至少包含 Parameter、Value、Meaning、Data Type、Range、Source、Status；不知道的欄位可留白，但 Status 必須標記 Need Confirm |
| Pegatron RU 參數表 | [pegatron-ru-parameter-table.md][pegatron-ru-parameter-table] 中已用表格列出 RU 設定檔參數，至少包含 Parameter、Value、Meaning、Data Type、Range、Source、Status；不知道的欄位可留白，但 Status 必須標記 Need Confirm |
| gNB 與 Pegatron RU 對應參數 | [oai-gnb-to-pegatron-ru-parameter-mapping.md][oai-gnb-to-pegatron-ru-parameter-mapping] 中已建立 gNB 與 RU 對應表，至少包含 frequency、bandwidth、SCS / numerology、TDD、IP / port、clock / sync、antenna、gain、fronthaul / eCPRI |
| OAI + cuBB for WNC RU 設定檔來源 | [wnc-ru-config-index.md][wnc-ru-config-index] 中有列出 `xxWNC.html` 或對應 gNB 設定檔位置、NVIDIA / Aerial 文件來源、WNC RU 頻段、型號；若不知道，需標記 Need Confirm 並寫明要問 Richard |
| OAI + cuBB for WNC RU 參數表 | [aerial-cubb-parameter-table.md][aerial-cubb-parameter-table] 中已用表格整理 OAI + cuBB for WNC RU 的 gNB 設定檔參數，並標示 Value、Meaning、Data Type、Range、Source、Status |
| 兩組成功設定檔比較 | [oai-pegatron-vs-oai-aerial-pegatron-comparison.md][oai-pegatron-vs-oai-aerial-pegatron-comparison] 中已比較 OAI + Pegatron RU 與 OAI + cuBB for WNC RU，至少包含 RU 類型、RU 頻段 / 型號、gNB config、frequency、bandwidth、SCS / numerology、TDD、IP / port、clock / sync、fronthaul、antenna / gain |
| Evidence / 超連結 | 每個產出表格中都要有 Source 或 Evidence 欄位，可放設定檔路徑、GitHub 連結、NVIDIA 文件連結、log path，不能只寫「已確認」 |
| Pending / Blocked | 不知道的地方不能亂補，必須標記 Need Confirm，並寫明要問誰：Ming、Johnson 或 Richard |
| Week 1 checkpoint | [week1-checkpoint.md][week1-checkpoint] 中有整理 W1 每個產出的 Done / Pending / Blocked 狀態、缺少的資料、下週要補的問題 |

---

# W2：2026/7/6（一）–2026/7/10（五）

## 週里程碑

根據 W1 完成的 OAI + Pegatron RU 與 OAI + cuBB for WNC RU 設定檔整理，補齊參數意義、資料型態、範圍與 Need Confirm 項目，並整理出 Pegatron RU 對接 Ariel cuBB 時需要對齊或修改的參數清單。

## 每日工作

| 日期 | 主要工作 | 預估工時 | 補充工作 / 緩衝 | 截止日期 | 預期產出 |
|---|---|---:|---|---|---|
| 7/6（一） | 補齊 OAI + Pegatron RU baseline 文件，確認 gNB / RU 設定檔來源、版本、成功條件與 evidence | 6h | 若設定檔來源或成功條件不完整，列 Pending 並詢問 Ming / Johnson；同時補齊 config-file-location-index | 7/6 | [oai-pegatron-baseline.md][oai-pegatron-baseline] 80%、[config-file-location-index.md][config-file-location-index] 50% |
| 7/7（二） | 補齊 OAI gNB 設定檔參數意義、資料型態、範圍與 Source | 6h | 不知道的參數不硬猜，Status 標記 Need Confirm；優先處理 E2E / RU 對接相關參數 | 7/7 | [oai-gnb-parameter-table.md][oai-gnb-parameter-table] 60% |
| 7/8（三） | 補齊 Pegatron RU 設定檔參數意義、資料型態、範圍，並對照 gNB 參數 | 6h | 將可能影響 cuBB 對接的 RU 參數標出，例如 frequency、bandwidth、sync、IP / port、fronthaul | 7/8 | [pegatron-ru-parameter-table.md][pegatron-ru-parameter-table] 60% |
| 7/9（四） | 整理 DGX Spark / Aerial L1 + OAI L2 安裝手冊與 OAI + cuBB for WNC RU 文件來源 | 7h | 若 NVIDIA / Aerial 文件中有 blocked issue 或版本限制，整理在文件中；不確定處標記 Need Confirm | 7/9 | [dgx-spark-aerial-oai-installation.md][dgx-spark-aerial-oai-installation] 70% |
| 7/10（五） | 週檢查點：根據 W1 / W2 的兩組設定檔差異，整理 Pegatron RU 對接 Ariel cuBB 前必須確認的問題 | 6h | 補齊本週文件、整理 Pending / Blocked、列出 W3 config pack 與 readiness checklist 需要的輸入 | 7/10 | [week2-checkpoint.md][week2-checkpoint]、[ru-to-cubb-alignment-questions.md][ru-to-cubb-alignment-questions] |

## 本週產出與百分比

| 產出 | 完成度 | 截止日期 |
|---|---:|---|
| [oai-pegatron-baseline.md][oai-pegatron-baseline] | 80% | 7/10 |
| [oai-gnb-parameter-table.md][oai-gnb-parameter-table] | 60% | 7/10 |
| [pegatron-ru-parameter-table.md][pegatron-ru-parameter-table] | 60% | 7/10 |
| [dgx-spark-aerial-oai-installation.md][dgx-spark-aerial-oai-installation] | 70% | 7/10 |
| [config-file-location-index.md][config-file-location-index] | 80% | 7/10 |
| [ru-to-cubb-alignment-questions.md][ru-to-cubb-alignment-questions] | 100% | 7/10 |
| [week2-checkpoint.md][week2-checkpoint] | 100% | 7/10 |

## 7/10 通過標準

| 檢查項目 | 通過標準 |
|---|---|
| OAI + Pegatron baseline | [oai-pegatron-baseline.md][oai-pegatron-baseline] 有 gNB config、RU config、command、log、成功條件與 Source / Evidence，不只是寫「已跑通」 |
| OAI gNB 參數表 | [oai-gnb-parameter-table.md][oai-gnb-parameter-table] 至少整理 10 個與 E2E / RU 對接有關的參數，並包含 Meaning、Data Type、Range、Source、Status |
| Pegatron RU 參數表 | [pegatron-ru-parameter-table.md][pegatron-ru-parameter-table] 至少整理 10 個 RU 端參數，並標示哪些可能要對齊 Ariel cuBB |
| DGX / Aerial 安裝手冊 | [dgx-spark-aerial-oai-installation.md][dgx-spark-aerial-oai-installation] 至少整理環境需求、安裝步驟、啟動入口、文件來源與 blocked issue |
| Config location | [config-file-location-index.md][config-file-location-index] 有整理 OAI、Pegatron RU、WNC RU、Aerial / cuBB 相關設定檔位置或待確認位置 |
| W3 準備 | [ru-to-cubb-alignment-questions.md][ru-to-cubb-alignment-questions] 有列出 Pegatron RU 要對齊 Ariel cuBB 前必須確認的問題，並標示要問 Ming / Johnson / Richard 的項目 |

---

# W3：2026/7/13（一）–2026/7/17（五）

## 週里程碑

根據 W1 / W2 的設定檔比較結果，整理 Pegatron RU 對接 Ariel cuBB 時需要修改或確認的參數，建立 OAI + Ariel cuBB + Pegatron RU 初版 config pack 與 launch readiness checklist。

## 每日工作

| 日期 | 主要工作 | 預估工時 | 補充工作 / 緩衝 | 截止日期 | 預期產出 |
|---|---|---:|---|---|---|
| 7/13（一） | 根據 W1 / W2 文件，補齊 OAI gNB 與 Pegatron RU 的參數對應關係 | 6h | 對照 gNB、RU 設定檔與 W1 comparison，找不到對應關係的項目標記 Need Confirm | 7/13 | [oai-gnb-to-pegatron-ru-parameter-mapping.md][oai-gnb-to-pegatron-ru-parameter-mapping] 70% |
| 7/14（二） | 整理 Ariel cuBB / Ariel RAN 所需設定，確認 cuBB 需要哪些 RU 端資訊 | 6h | 以 OAI + cuBB for WNC RU 成功設定檔為參考，整理對 Pegatron RU 的要求 | 7/14 | [aerial-cubb-parameter-table.md][aerial-cubb-parameter-table] 70% |
| 7/15（三） | 建立 Pegatron RU 對齊 Ariel cuBB 的 mapping checklist | 6h | 將 frequency、bandwidth、numerology、TDD、IP / port、sync、antenna、gain、fronthaul 分成 Match / Need Modify / Need Confirm | 7/15 | [pegatron-ru-to-aerial-cubb-mapping-checklist.md][pegatron-ru-to-aerial-cubb-mapping-checklist] 80% |
| 7/16（四） | 依據 mapping checklist 整理 OAI + Ariel cuBB + Pegatron RU 測試用 config pack | 7h | 集中 config、標註來源、記錄修改原因；不確定不直接修改，先保留 original vs modified note | 7/16 | `oai-aerial-pegatron-config-pack/` 60% |
| 7/17（五） | 週檢查點：確認 W4 launch attempt 所需 config、command、log path、環境需求是否 ready | 6h | 補齊 launch sequence、log location、readiness checklist，整理 W4 測試風險 | 7/17 | [e2e-readiness-checklist.md][e2e-readiness-checklist]、[week3-checkpoint.md][week3-checkpoint] |

## 本週產出與百分比

| 產出 | 完成度 | 截止日期 |
|---|---:|---|
| [oai-gnb-to-pegatron-ru-parameter-mapping.md][oai-gnb-to-pegatron-ru-parameter-mapping] | 70% | 7/17 |
| [aerial-cubb-parameter-table.md][aerial-cubb-parameter-table] | 70% | 7/17 |
| [pegatron-ru-to-aerial-cubb-mapping-checklist.md][pegatron-ru-to-aerial-cubb-mapping-checklist] | 80% | 7/17 |
| `oai-aerial-pegatron-config-pack/` | 60% | 7/17 |
| [e2e-readiness-checklist.md][e2e-readiness-checklist] | 90% | 7/17 |
| [e2e-launch-sequence.md][e2e-launch-sequence] | 70% | 7/17 |
| [log-location-and-debug-guide.md][log-location-and-debug-guide] | 70% | 7/17 |
| [week3-checkpoint.md][week3-checkpoint] | 100% | 7/17 |

## 7/17 通過標準

| 檢查項目 | 通過標準 |
|---|---|
| OAI baseline mapping | [oai-gnb-to-pegatron-ru-parameter-mapping.md][oai-gnb-to-pegatron-ru-parameter-mapping] 能說明 OAI gNB 與 Pegatron RU 哪些參數需要一致，未知項目標記 Need Confirm |
| Ariel cuBB 需求 | [aerial-cubb-parameter-table.md][aerial-cubb-parameter-table] 能列出 Ariel cuBB 需要從 config 或環境取得哪些 RU 資訊 |
| RU-to-cuBB alignment | [pegatron-ru-to-aerial-cubb-mapping-checklist.md][pegatron-ru-to-aerial-cubb-mapping-checklist] 至少包含 frequency、bandwidth、numerology、TDD、IP / port、sync、antenna、gain、fronthaul |
| Config pack | `oai-aerial-pegatron-config-pack/` 中的 config 來源、修改原因與尚未確認項目有被記錄 |
| W4 readiness | [e2e-readiness-checklist.md][e2e-readiness-checklist] 已列出 W4 launch attempt 的 command、config、log path、expected result |
| Traceability | W3 的 config pack 與 readiness checklist 必須能追溯到 W1 / W2 的設定檔比較與參數表 |

---

# W4：2026/7/20（一）–2026/7/24（五）

## 週里程碑

根據 W1 / W2 / W3 的設定檔比較、mapping checklist 與 config pack，嘗試跑通 OAI L2/L3 + Ariel cuBB + Pegatron RU E2E，並留下完整 experiment log。

## 每日工作

| 日期 | 主要工作 | 預估工時 | 補充工作 / 緩衝 | 截止日期 | 預期產出 |
|---|---|---:|---|---|---|
| 7/20（一） | 根據 W3 readiness checklist 進行 launch 前檢查：版本、config、network、clock / sync、log path | 6h | 確認每個 config 都能追溯到 W1 / W2 / W3 文件；若有缺口，標成 Partial / Blocked | 7/20 | [pre-launch-checklist.md][pre-launch-checklist] 100% |
| 7/21（二） | 執行 OAI L2/L3 + Ariel cuBB + Pegatron RU launch attempt，保存 command、config、log、result | 7h | 不論成功或失敗，都保存完整 command、config、log、actual result；不要只寫「failed」 | 7/21 | [oai-aerial-pegatron-first-attempt-log.md][oai-aerial-pegatron-first-attempt-log] 100% |
| 7/22（三） | 分析第一次 attempt log；若失敗，整理 reproduction steps、error、環境、推測原因 | 6h | 分類問題來源，補 error report；若 log 不足，補 log path 與重現方式 | 7/22 | [oai-aerial-pegatron-error-report.md][oai-aerial-pegatron-error-report] 70% |
| 7/23（四） | 根據 7/22 分析修正設定，進行 launch attempt 或補測關鍵步驟 | 7h | 進行第二次 attempt 或針對 blocked step 補測，保存完整紀錄 | 7/23 | [oai-aerial-pegatron-second-attempt-log.md][oai-aerial-pegatron-second-attempt-log] 100% |
| 7/24（五） | 週檢查點：整理本週 E2E 狀態，確認是 Pass / Partial / Blocked，列出 W5 比較所需 evidence | 6h | 完成 E2E status、common error list、week checkpoint，整理 W5 比較資料 | 7/24 | [week4-checkpoint.md][week4-checkpoint]、[oai-aerial-pegatron-e2e-status.md][oai-aerial-pegatron-e2e-status] |

## 本週產出與百分比

| 產出 | 完成度 | 截止日期 |
|---|---:|---|
| [pre-launch-checklist.md][pre-launch-checklist] | 100% | 7/20 |
| [oai-aerial-pegatron-first-attempt-log.md][oai-aerial-pegatron-first-attempt-log] | 100% | 7/21 |
| [oai-aerial-pegatron-second-attempt-log.md][oai-aerial-pegatron-second-attempt-log] | 100% | 7/23 |
| [oai-aerial-pegatron-error-report.md][oai-aerial-pegatron-error-report] | 80% | 7/24 |
| [oai-aerial-pegatron-e2e-status.md][oai-aerial-pegatron-e2e-status] | 100% | 7/24 |
| [common-error-list.md][common-error-list] | 80% | 7/24 |
| [week4-checkpoint.md][week4-checkpoint] | 100% | 7/24 |

## 7/24 通過標準

| 檢查項目 | 通過標準 |
|---|---|
| Launch attempt | 至少完成 1–2 次 OAI + Ariel cuBB + Pegatron RU launch attempt，或清楚說明無法執行的 blocking reason |
| Experiment log | 每次 attempt 都有 command、config、environment、log、actual result |
| Config traceability | Launch attempt 使用的 config 必須能追溯到 W1 / W2 的設定檔比較與 W3 的 config pack |
| E2E status | [oai-aerial-pegatron-e2e-status.md][oai-aerial-pegatron-e2e-status] 明確標示 Pass / Partial / Blocked / Fail |
| Error report | 若失敗，[oai-aerial-pegatron-error-report.md][oai-aerial-pegatron-error-report] 必須有 reproduction steps、logs、environment、推測原因 |
| Evidence | 有足夠資料支撐 W5 與 OAI + Pegatron baseline 比較 |
| Action Items | 若本週有正式開會，Action Items 留在該次 meeting note；若沒開會，不新增 action items |

---

# W5：2026/7/27（一）–2026/7/31（五）

## 月里程碑

整理 7 月兩階段比較結果：第一階段比較 OAI + Pegatron RU 與 OAI + cuBB for WNC RU 的成功設定檔差異；第二階段比較 OAI + Pegatron RU baseline 與 OAI + Ariel cuBB + Pegatron RU attempt 的設定、log、狀態與限制，完成 7 月月報。

## 每日工作

| 日期 | 主要工作 | 預估工時 | 補充工作 / 緩衝 | 截止日期 | 預期產出 |
|---|---|---:|---|---|---|
| 7/27（一） | 整理 OAI + Pegatron RU baseline 的最終版本：config、command、參數、log、成功條件 | 6h | 補齊 W1 / W2 baseline 文件缺漏，確認可支撐後續比較 | 7/27 | [oai-pegatron-baseline.md][oai-pegatron-baseline] 100% |
| 7/28（二） | 整理 OAI + Ariel cuBB + Pegatron RU 的最終狀態：config、command、log、成功 / 失敗 / blocked 原因 | 6h | 將 W4 attempt log 收斂成 E2E status，明確標示 Pass / Partial / Blocked / Fail | 7/28 | [oai-aerial-pegatron-e2e-status.md][oai-aerial-pegatron-e2e-status] 100% |
| 7/29（三） | 完成第一階段比較：OAI + Pegatron RU vs OAI + cuBB for WNC RU 的成功設定檔差異 | 7h | 比較 gNB config、RU 類型、頻段 / 型號、frequency、bandwidth、SCS、TDD、IP / port、sync、fronthaul、antenna / gain | 7/29 | [oai-pegatron-vs-oai-aerial-pegatron-comparison.md][oai-pegatron-vs-oai-aerial-pegatron-comparison] 80% |
| 7/30（四） | 完成第二階段比較：OAI + Pegatron RU baseline vs OAI + Ariel cuBB + Pegatron RU attempt | 6h | 把 W4 launch attempt 的 command、config、log、status、error type 與 baseline 做比較 | 7/30 | [oai-pegatron-vs-oai-aerial-pegatron-comparison.md][oai-pegatron-vs-oai-aerial-pegatron-comparison] 100%、[month1-open-issues.md][month1-open-issues] |
| 7/31（五） | 月檢查點：完成 7 月月報，列出 8 月 Metanoia 研究入口 | 6h | 完成 month1 summary、week5 checkpoint、8 月研究入口計畫；整理未完成原因與下一步 | 7/31 | [month1-summary.md][month1-summary]、[month2-metanoia-entry-plan.md][month2-metanoia-entry-plan]、[week5-checkpoint.md][week5-checkpoint] |

## 本週產出與百分比

| 產出 | 完成度 | 截止日期 |
|---|---:|---|
| [oai-pegatron-baseline.md][oai-pegatron-baseline] | 100% | 7/27 |
| [oai-aerial-pegatron-e2e-status.md][oai-aerial-pegatron-e2e-status] | 100% | 7/28 |
| [oai-pegatron-vs-oai-aerial-pegatron-comparison.md][oai-pegatron-vs-oai-aerial-pegatron-comparison] | 100% | 7/31 |
| [oai-gnb-parameter-table.md][oai-gnb-parameter-table] | 90% | 7/31 |
| [aerial-cubb-parameter-table.md][aerial-cubb-parameter-table] | 90% | 7/31 |
| [pegatron-ru-parameter-table.md][pegatron-ru-parameter-table] | 90% | 7/31 |
| [dgx-spark-aerial-oai-installation.md][dgx-spark-aerial-oai-installation] | 100% | 7/31 |
| [month1-open-issues.md][month1-open-issues] | 100% | 7/31 |
| [month1-summary.md][month1-summary] | 100% | 7/31 |
| [month2-metanoia-entry-plan.md][month2-metanoia-entry-plan] | 100% | 7/31 |
| [week5-checkpoint.md][week5-checkpoint] | 100% | 7/31 |

## 7/31 月檢查通過標準

| 檢查項目 | 通過標準 |
|---|---|
| OAI + Pegatron baseline | [oai-pegatron-baseline.md][oai-pegatron-baseline] 已整理成可比較 baseline，不只是「已跑通」 |
| 第一階段比較 | [oai-pegatron-vs-oai-aerial-pegatron-comparison.md][oai-pegatron-vs-oai-aerial-pegatron-comparison] 有比較 OAI + Pegatron RU 與 OAI + cuBB for WNC RU 的成功設定檔差異 |
| 第二階段比較 | [oai-pegatron-vs-oai-aerial-pegatron-comparison.md][oai-pegatron-vs-oai-aerial-pegatron-comparison] 有比較 OAI + Pegatron RU baseline 與 OAI + Ariel cuBB + Pegatron RU attempt 的 config、command、log、status、error type |
| OAI + Ariel + Pegatron attempt | [oai-aerial-pegatron-e2e-status.md][oai-aerial-pegatron-e2e-status] 有 launch attempt / E2E result / blocked reason 的完整紀錄 |
| Parameter understanding | OAI、Ariel cuBB、Pegatron RU 的關鍵參數表已整理，未知項目標記 Need Confirm |
| DGX / Aerial installation | [dgx-spark-aerial-oai-installation.md][dgx-spark-aerial-oai-installation] 整理到可交接程度，包含文件來源、環境需求、啟動入口與 blocked issue |
| Open issues | [month1-open-issues.md][month1-open-issues] 中所有未完成項目有原因、狀態、下一步與要詢問的協作者 |
| 8 月銜接 | [month2-metanoia-entry-plan.md][month2-metanoia-entry-plan] 明確知道 Metanoia 研究第一週要從哪裡開始 |
| Week 5 checkpoint | [week5-checkpoint.md][week5-checkpoint] 中已回顧 W1–W5 的 Done / Pending / Blocked、主要 evidence 與下月工作入口 |

---

# 7 月最終比較表比較項目

| 比較項目 | OAI + Pegatron RU baseline | OAI + cuBB for WNC RU | OAI + Ariel cuBB + Pegatron RU attempt | 為什麼要比 |
|---|---|---|---|---|
| 系統架構 | OAI L2/L3 + OAI L1 + Pegatron RU | OAI L2/L3 + Ariel cuBB + WNC RU | OAI L2/L3 + Ariel cuBB + Pegatron RU | 確認 Ariel cuBB 替代了哪一段，以及 RU 從 WNC 換成 Pegatron 後的差異 |
| L1 / cuBB 角色 | OAI L1 | Ariel cuBB | Ariel cuBB | 這是兩套系統核心差異 |
| RU 類型 | Pegatron RU | WNC RU | Pegatron RU | 確認 cuBB 成功案例與目標 RU 的差異 |
| RU 頻段 / 型號 | baseline value | WNC value | Pegatron value | 頻段與型號會影響設定檔與 fronthaul 對接 |
| gNB config | OAI baseline 使用的 gNB config | OAI + cuBB for WNC 使用的 gNB config，例如 `xxWNC.html` | Ariel 版本使用的 OAI config | 確認 L2/L3 設定是否需要改 |
| RU config | Pegatron RU baseline config | WNC RU 對應 config | Pegatron RU 對齊 cuBB 後的 config | 確認 RU 端是否需要重設 |
| frequency / bandwidth | baseline value | WNC value | Ariel + Pegatron value | 必須對齊 |
| numerology / SCS | baseline value | WNC value | Ariel + Pegatron value | 必須對齊 |
| TDD pattern | baseline value | WNC value | Ariel + Pegatron value | 影響 frame timing |
| fronthaul / eCPRI | baseline 設定 | cuBB + WNC 成功設定 | cuBB + Pegatron 設定 | RU 對接 cuBB 的重點 |
| IP / port | baseline 設定 | WNC 設定 | Ariel + Pegatron 設定 | 對接必須一致 |
| clock / sync | baseline 設定 | WNC 設定 | Ariel + Pegatron 設定 | 常見 E2E 問題來源 |
| antenna / gain | baseline 設定 | WNC 設定 | Ariel + Pegatron 設定 | 影響 RF / RU 行為 |
| 啟動順序 | OAI + Pegatron 啟動流程 | OAI + cuBB + WNC 啟動流程 | OAI + cuBB + Pegatron 啟動流程 | 確認流程差異 |
| log 位置 | OAI gNB log、RU log | OAI log、cuBB log、WNC RU log | OAI log、cuBB log、Pegatron RU log | Debug 需要 |
| 成功條件 | baseline 如何判斷成功 | WNC 成功案例如何判斷成功 | Ariel + Pegatron 如何判斷成功 / blocked | 避免只看「有沒有跑起來」 |
| 錯誤訊息 | baseline 是否有 error | WNC 成功案例是否有 warning / limitation | Ariel + Pegatron error | 用來定位問題 |
| 可重現性 | 是否能照文件重跑 | 是否能照文件重跑 | 是否能照文件重跑 | 符合可驗證與交接概念 |

[oai-pegatron-baseline]: https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/07-oai-aerial-pegatron/baseline-and-config/oai-pegatron-baseline.md
[oai-gnb-parameter-table]: https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/07-oai-aerial-pegatron/baseline-and-config/oai-gnb-parameter-table.md
[pegatron-ru-parameter-table]: https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/07-oai-aerial-pegatron/baseline-and-config/pegatron-ru-parameter-table.md
[wnc-ru-config-index]: https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/07-oai-aerial-pegatron/baseline-and-config/wnc-ru-config-index.md
[aerial-cubb-parameter-table]: https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/07-oai-aerial-pegatron/baseline-and-config/aerial-cubb-parameter-table.md
[config-file-location-index]: https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/07-oai-aerial-pegatron/baseline-and-config/config-file-location-index.md
[dgx-spark-aerial-oai-installation]: https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/07-oai-aerial-pegatron/baseline-and-config/dgx-spark-aerial-oai-installation.md
[ru-to-cubb-alignment-questions]: https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/07-oai-aerial-pegatron/baseline-and-config/ru-to-cubb-alignment-questions.md
[oai-gnb-to-pegatron-ru-parameter-mapping]: https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/07-oai-aerial-pegatron/mapping-and-readiness/oai-gnb-to-pegatron-ru-parameter-mapping.md
[pegatron-ru-to-aerial-cubb-mapping-checklist]: https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/07-oai-aerial-pegatron/mapping-and-readiness/pegatron-ru-to-aerial-cubb-mapping-checklist.md
[e2e-readiness-checklist]: https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/07-oai-aerial-pegatron/mapping-and-readiness/e2e-readiness-checklist.md
[e2e-launch-sequence]: https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/07-oai-aerial-pegatron/mapping-and-readiness/e2e-launch-sequence.md
[log-location-and-debug-guide]: https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/07-oai-aerial-pegatron/mapping-and-readiness/log-location-and-debug-guide.md
[pre-launch-checklist]: https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/07-oai-aerial-pegatron/experiments/pre-launch-checklist.md
[oai-aerial-pegatron-first-attempt-log]: https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/07-oai-aerial-pegatron/experiments/oai-aerial-pegatron-first-attempt-log.md
[oai-aerial-pegatron-second-attempt-log]: https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/07-oai-aerial-pegatron/experiments/oai-aerial-pegatron-second-attempt-log.md
[oai-aerial-pegatron-error-report]: https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/07-oai-aerial-pegatron/experiments/oai-aerial-pegatron-error-report.md
[oai-aerial-pegatron-e2e-status]: https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/07-oai-aerial-pegatron/experiments/oai-aerial-pegatron-e2e-status.md
[common-error-list]: https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/07-oai-aerial-pegatron/experiments/common-error-list.md
[oai-pegatron-vs-oai-aerial-pegatron-comparison]: https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/07-oai-aerial-pegatron/comparison-and-summary/oai-pegatron-vs-oai-aerial-pegatron-comparison.md
[month1-open-issues]: https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/07-oai-aerial-pegatron/comparison-and-summary/month1-open-issues.md
[month1-summary]: https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/07-oai-aerial-pegatron/comparison-and-summary/month1-summary.md
[month2-metanoia-entry-plan]: https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/07-oai-aerial-pegatron/comparison-and-summary/month2-metanoia-entry-plan.md
[week1-checkpoint]: https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/checkpoints/week1-checkpoint.md
[week2-checkpoint]: https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/checkpoints/week2-checkpoint.md
[week3-checkpoint]: https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/checkpoints/week3-checkpoint.md
[week4-checkpoint]: https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/checkpoints/week4-checkpoint.md
[week5-checkpoint]: https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/checkpoints/week5-checkpoint.md
# 8 月總目標

## Month Goal：2026/8/3–2026/8/28

完成：

> **Metanoia RU 開源碼研究。**

8 月的成果不是只說「看過程式碼」，而是要留下可交接的研究文件，讓 9 月可以根據這些文件把 Metanoia RU 接到 OAI L2/L3 + Ariel cuBB。

# W6：2026/8/3（一）–2026/8/7（五）

## 週里程碑

完成 Metanoia repo 初步研究，找出 source tree、README、build/config 入口。

本週的重點：

> Metanoia MOSART repo 裡面有哪些資料夾？
> 哪些部分可能跟 RU、PHY、fronthaul、config、build、runtime 有關？
> 9 月整合時應該從哪幾個檔案或資料夾開始看？

## 每日工作

| 日期     | 工作                                                                 | 截止日期 | 預期產出                                                                     |
| ------ | ------------------------------------------------------------------ | ---- | ------------------------------------------------------------------------ |
| 8/3（一） | 進入 Metanoia MOSART repo，整理 README、官方說明、主要資料夾名稱                     | 8/3  | [`metanoia-repo-overview.md`](https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/08-metanoia-source-study/repo-and-build/metanoia-repo-overview.md) 40%                                          |
| 8/4（二） | 建立 source tree，標出 build、config、runtime、RU / PHY / fronthaul 可能相關位置 | 8/4  | [`metanoia-source-tree.md`](https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/08-metanoia-source-study/repo-and-build/metanoia-source-tree.md) 50%                                            |
| 8/5（三） | 找出 build system、dependency、安裝說明、可能的 build command                  | 8/5  | [`metanoia-build-requirements.md`](https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/08-metanoia-source-study/repo-and-build/metanoia-build-requirements.md) 50%                                     |
| 8/6（四） | 找出 config 檔、example、script、啟動入口或執行說明                               | 8/6  | [`metanoia-config-location-index.md`](https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/08-metanoia-source-study/repo-and-build/metanoia-config-location-index.md) 40%、[`metanoia-run-entrypoint.md`](https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/08-metanoia-source-study/repo-and-build/metanoia-run-entrypoint.md) 30% |
| 8/7（五） | 週檢查點：整理本週不確定處，形成下週 build / run / config 研究問題清單                     | 8/7  | [`week6-checkpoint.md`](https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/checkpoints/week6-checkpoint.md)、[`metanoia-open-questions.md`](https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/08-metanoia-source-study/summary-and-plan/metanoia-open-questions.md)                       |

## 本週產出與百分比

| 產出                                  |  完成度 | 截止日期 |
| ----------------------------------- | ---: | ---- |
| [`metanoia-repo-overview.md`](https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/08-metanoia-source-study/repo-and-build/metanoia-repo-overview.md)         |  70% | 8/7  |
| [`metanoia-source-tree.md`](https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/08-metanoia-source-study/repo-and-build/metanoia-source-tree.md)           |  70% | 8/7  |
| [`metanoia-build-requirements.md`](https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/08-metanoia-source-study/repo-and-build/metanoia-build-requirements.md)    |  50% | 8/7  |
| [`metanoia-config-location-index.md`](https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/08-metanoia-source-study/repo-and-build/metanoia-config-location-index.md) |  40% | 8/7  |
| [`metanoia-run-entrypoint.md`](https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/08-metanoia-source-study/repo-and-build/metanoia-run-entrypoint.md)        |  30% | 8/7  |
| [`metanoia-open-questions.md`](https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/08-metanoia-source-study/summary-and-plan/metanoia-open-questions.md)        | 100% | 8/7  |
| [`week6-checkpoint.md`](https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/checkpoints/week6-checkpoint.md)               | 100% | 8/7  |

## 8/7 通過標準

| 檢查項目            | 通過標準                                                    |
| --------------- | ------------------------------------------------------- |
| Repo overview   | 能說明 Metanoia repo 的主要資料夾與用途                             |
| Source tree     | 至少標出 build、config、runtime、RU / PHY / fronthaul 相關位置     |
| Build entrance  | 找到 build 說明、build script、CMake/Makefile 或標出尚未找到         |
| Config entrance | 找到可能的 config/example/script，或標出尚未找到                     |
| Open questions  | 至少列出 8 個需要下週釐清的問題                                       |
| Daily Notes     | 8/3–8/7 每天都有 plan、review、evidence、next working day plan |

---

# W7：2026/8/10（一）–2026/8/14（五）

## 週里程碑

完成 Metanoia build / run / config 初版研究，留下 build log 與 runtime notes。

這週要留下可重現證據：

> 如果 build 成功，要知道成功條件。
> 如果 build 失敗，要知道錯在哪、怎麼重現、下一步要補什麼。

## 每日工作

| 日期      | 工作                                                                   | 截止日期 | 預期產出                                                                    |
| ------- | -------------------------------------------------------------------- | ---- | ----------------------------------------------------------------------- |
| 8/10（一） | 依 W6 找到的 build 說明整理建置環境：OS、dependency、toolchain、driver、library       | 8/10 | [`metanoia-build-guide.md`](https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/08-metanoia-source-study/repo-and-build/metanoia-build-guide.md) 40%                                           |
| 8/11（二） | 執行第一次 build attempt，保存 command、environment、terminal output、error log | 8/11 | [`metanoia-build-log.md`](https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/08-metanoia-source-study/repo-and-build/metanoia-build-log.md) 100%                                            |
| 8/12（三） | 分析 build 結果，整理成功條件或失敗原因，更新 build guide                               | 8/12 | [`metanoia-build-guide.md`](https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/08-metanoia-source-study/repo-and-build/metanoia-build-guide.md) 70%、[`metanoia-build-error-report.md`](https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/08-metanoia-source-study/repo-and-build/metanoia-build-error-report.md) 50%      |
| 8/13（四） | 整理 runtime 入口：執行檔、script、config、啟動參數、預期 log                          | 8/13 | [`metanoia-run-entrypoint.md`](https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/08-metanoia-source-study/repo-and-build/metanoia-run-entrypoint.md) 70%、[`metanoia-runtime-config-notes.md`](https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/08-metanoia-source-study/repo-and-build/metanoia-runtime-config-notes.md) 50% |
| 8/14（五） | 週檢查點：確認 W8 能開始整理 RU 參數與 interface mapping                            | 8/14 | [`week7-checkpoint.md`](https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/checkpoints/week7-checkpoint.md)、[`metanoia-parameter-table.md`](https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/08-metanoia-source-study/ru-study/metanoia-parameter-table.md) 初版                  |

## 本週產出與百分比

| 產出                                 |  完成度 | 截止日期 |
| ---------------------------------- | ---: | ---- |
| [`metanoia-build-guide.md`](https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/08-metanoia-source-study/repo-and-build/metanoia-build-guide.md)          |  80% | 8/14 |
| [`metanoia-build-log.md`](https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/08-metanoia-source-study/repo-and-build/metanoia-build-log.md)            | 100% | 8/11 |
| [`metanoia-build-error-report.md`](https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/08-metanoia-source-study/repo-and-build/metanoia-build-error-report.md)   |  70% | 8/14 |
| [`metanoia-run-entrypoint.md`](https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/08-metanoia-source-study/repo-and-build/metanoia-run-entrypoint.md)       |  80% | 8/14 |
| [`metanoia-runtime-config-notes.md`](https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/08-metanoia-source-study/repo-and-build/metanoia-runtime-config-notes.md) |  60% | 8/14 |
| [`metanoia-parameter-table.md`](https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/08-metanoia-source-study/ru-study/metanoia-parameter-table.md)      |  40% | 8/14 |
| [`week7-checkpoint.md`](https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/checkpoints/week7-checkpoint.md)              | 100% | 8/14 |

## 8/14 通過標準

| 檢查項目             | 通過標準                                                           |
| ---------------- | -------------------------------------------------------------- |
| Build guide      | 有 environment、dependency、command、expected result               |
| Build log        | 至少有 1 次 build attempt log                                      |
| Error report     | 若 build 失敗，有 reproduction steps、environment、error message、推測原因 |
| Runtime entrance | 找到可能的執行入口、script、binary 或標出尚未找到                                |
| Config notes     | 找到 runtime config 或標出目前缺口                                      |
| W8 準備            | 可以開始整理 Metanoia RU 端參數與介面需求                                    |

---

# W8：2026/8/17（一）–2026/8/21（五）

## 週里程碑

完成 Metanoia RU 參數與介面研究，建立 Pegatron RU vs Metanoia RU 比較。

這週的目標是回答：

> Metanoia RU 和 Pegatron RU 在設定檔、啟動方式、fronthaul、clock/sync、RF 參數上有哪些差異？
> 9 月如果要把 Metanoia RU 接到 OAI + Ariel cuBB，哪些參數一定要對齊？

## 每日工作

| 日期      | 工作                                                                          | 截止日期 | 預期產出                                                      |
| ------- | --------------------------------------------------------------------------- | ---- | --------------------------------------------------------- |
| 8/17（一） | 深入整理 Metanoia RU 相關參數：frequency、bandwidth、SCS、TDD、IP/port、sync、antenna、gain | 8/17 | [`metanoia-parameter-table.md`](https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/08-metanoia-source-study/ru-study/metanoia-parameter-table.md) 70%                         |
| 8/18（二） | 整理 Metanoia RU 介面：與 L1/cuBB/fronthaul 相關的 config、API、script、log             | 8/18 | [`metanoia-ru-interface-notes.md`](https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/08-metanoia-source-study/ru-study/metanoia-ru-interface-notes.md) 60%                      |
| 8/19（三） | 將 7 月 Pegatron RU baseline 參數與 Metanoia RU 參數對照                             | 8/19 | [`pegatron-vs-metanoia-ru-comparison.md`](https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/08-metanoia-source-study/ru-study/pegatron-vs-metanoia-ru-comparison.md) 60%               |
| 8/20（四） | 建立 Metanoia RU 對齊 Ariel cuBB 的 mapping checklist                            | 8/20 | [`metanoia-ru-to-aerial-cubb-mapping-checklist.md`](https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/08-metanoia-source-study/ru-study/metanoia-ru-to-aerial-cubb-mapping-checklist.md) 70%     |
| 8/21（五） | 週檢查點：整理 W9 feasibility report 需要的證據與風險清單                                    | 8/21 | [`week8-checkpoint.md`](https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/checkpoints/week8-checkpoint.md)、[`metanoia-integration-risk-list.md`](https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/08-metanoia-source-study/ru-study/metanoia-integration-risk-list.md) |

## 本週產出與百分比

| 產出                                                |  完成度 | 截止日期 |
| ------------------------------------------------- | ---: | ---- |
| [`metanoia-parameter-table.md`](https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/08-metanoia-source-study/ru-study/metanoia-parameter-table.md)                     |  90% | 8/21 |
| [`metanoia-ru-interface-notes.md`](https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/08-metanoia-source-study/ru-study/metanoia-ru-interface-notes.md)                  |  80% | 8/21 |
| [`pegatron-vs-metanoia-ru-comparison.md`](https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/08-metanoia-source-study/ru-study/pegatron-vs-metanoia-ru-comparison.md)           |  80% | 8/21 |
| [`metanoia-ru-to-aerial-cubb-mapping-checklist.md`](https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/08-metanoia-source-study/ru-study/metanoia-ru-to-aerial-cubb-mapping-checklist.md) |  80% | 8/21 |
| [`metanoia-integration-risk-list.md`](https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/08-metanoia-source-study/ru-study/metanoia-integration-risk-list.md)               | 100% | 8/21 |
| [`week8-checkpoint.md`](https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/checkpoints/week8-checkpoint.md)                             | 100% | 8/21 |

## 8/21 通過標準

| 檢查項目                | 通過標準                                                                 |
| ------------------- | -------------------------------------------------------------------- |
| Metanoia parameters | 至少整理 15 個 Metanoia RU 相關參數                                           |
| Interface notes     | 能說明 Metanoia RU 與 L1/cuBB/fronthaul 可能的對接位置                          |
| Pegatron comparison | 至少比較 Pegatron RU 與 Metanoia RU 的 8 個項目                               |
| Mapping checklist   | 至少包含 frequency、bandwidth、SCS、TDD、IP/port、sync、antenna、gain、fronthaul |
| Risk list           | 至少列出 5 個 9 月整合風險與驗證方法                                                |

---

# W9：2026/8/24（一）–2026/8/28（五）

## 週里程碑

完成 Metanoia 開源碼研究總結，產出 9 月整合可行性與計畫。

這週要把 8 月研究收斂成 9 月可以直接用的資料。

## 每日工作

| 日期      | 工作                                                                    | 截止日期 | 預期產出                                                 |
| ------- | --------------------------------------------------------------------- | ---- | ---------------------------------------------------- |
| 8/24（一） | 補齊 Metanoia repo overview、source tree、build guide、run entrypoint      | 8/24 | W6/W7 文件更新到 90% 以上                                   |
| 8/25（二） | 補齊 Metanoia parameter table、interface notes、mapping checklist         | 8/25 | W8 文件更新到 90% 以上                                      |
| 8/26（三） | 撰寫 OAI + Ariel cuBB + Metanoia RU 整合可行性報告                             | 8/26 | [`metanoia-oai-aerial-integration-feasibility.md`](https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/08-metanoia-source-study/summary-and-plan/metanoia-oai-aerial-integration-feasibility.md) 70% |
| 8/27（四） | 建立 9 月整合計畫：config pack、launch sequence、log collection、risk mitigation | 8/27 | [`month3-integration-plan.md`](https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/08-metanoia-source-study/summary-and-plan/month3-integration-plan.md) 80%                     |
| 8/28（五） | 月檢查點：完成 8 月總結，明確列出 9 月第一週要做什麼                                         | 8/28 | [`month2-summary.md`](https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/08-metanoia-source-study/summary-and-plan/month2-summary.md)、[`week9-checkpoint.md`](https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/checkpoints/week9-checkpoint.md)            |

## 本週產出與百分比

| 產出                                                |  完成度 | 截止日期 |
| ------------------------------------------------- | ---: | ---- |
| [`metanoia-repo-overview.md`](https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/08-metanoia-source-study/repo-and-build/metanoia-repo-overview.md)                       | 100% | 8/28 |
| [`metanoia-source-tree.md`](https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/08-metanoia-source-study/repo-and-build/metanoia-source-tree.md)                         | 100% | 8/28 |
| [`metanoia-build-guide.md`](https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/08-metanoia-source-study/repo-and-build/metanoia-build-guide.md)                         | 100% | 8/28 |
| [`metanoia-build-log.md`](https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/08-metanoia-source-study/repo-and-build/metanoia-build-log.md)                           | 100% | 8/28 |
| [`metanoia-run-entrypoint.md`](https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/08-metanoia-source-study/repo-and-build/metanoia-run-entrypoint.md)                      | 100% | 8/28 |
| [`metanoia-config-location-index.md`](https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/08-metanoia-source-study/repo-and-build/metanoia-config-location-index.md)               | 100% | 8/28 |
| [`metanoia-parameter-table.md`](https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/08-metanoia-source-study/ru-study/metanoia-parameter-table.md)                     | 100% | 8/28 |
| [`metanoia-ru-interface-notes.md`](https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/08-metanoia-source-study/ru-study/metanoia-ru-interface-notes.md)                  | 100% | 8/28 |
| [`pegatron-vs-metanoia-ru-comparison.md`](https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/08-metanoia-source-study/ru-study/pegatron-vs-metanoia-ru-comparison.md)           | 100% | 8/28 |
| [`metanoia-ru-to-aerial-cubb-mapping-checklist.md`](https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/08-metanoia-source-study/ru-study/metanoia-ru-to-aerial-cubb-mapping-checklist.md) | 100% | 8/28 |
| [`metanoia-oai-aerial-integration-feasibility.md`](https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/08-metanoia-source-study/summary-and-plan/metanoia-oai-aerial-integration-feasibility.md)  | 100% | 8/28 |
| [`month3-integration-plan.md`](https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/08-metanoia-source-study/summary-and-plan/month3-integration-plan.md)                      | 100% | 8/28 |
| [`month2-summary.md`](https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/08-metanoia-source-study/summary-and-plan/month2-summary.md)                               | 100% | 8/28 |

## 8/28 月檢查通過標準

| 檢查項目            | 通過標準                                             |
| --------------- | ------------------------------------------------ |
| Source study    | Metanoia repo 架構、build、run、config、interface 都有整理 |
| Build evidence  | 有 build guide 與 build log；失敗也要有 error report     |
| RU parameters   | Metanoia RU 參數表完成                                |
| Comparison      | 有 Pegatron RU vs Metanoia RU 比較                  |
| Feasibility     | 明確判斷 9 月整合是 Pass / Partial / Blocked 哪一種準備狀態     |
| Risk            | 主要整合風險都有驗證方法                                     |
| September entry | 明確知道 9 月第一週要建立哪些 config 與 launch flow            |

---

# 9 月總目標

## Month Goal：2026/8/31–2026/9/26

完成：

> **結合 OAI L2/L3 + Ariel cuBB + Metanoia RU E2E。**

9 月的重點不是再做大量 source code 研究，而是：

1. 根據 8 月研究成果建立初版 config
2. 嘗試 launch / E2E
3. 保存 log、error report、status
4. 與 7 月 Pegatron RU 版本比較
5. 完成最終交接文件
---

# W10：2026/8/31（一）–2026/9/4（五）

## 週里程碑

建立 OAI + Ariel cuBB + Metanoia RU 初版 config pack 與 launch flow。

## 每日工作

| 日期      | 工作                                                                              | 截止日期 | 預期產出                                                      |
| ------- | ------------------------------------------------------------------------------- | ---- | --------------------------------------------------------- |
| 8/31（一） | Review 8 月 feasibility report，確認哪些 Metanoia 參數能對齊 Ariel cuBB                    | 8/31 | [`metanoia-integration-start-review.md`](https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/09-oai-aerial-metanoia/preparation/metanoia-integration-start-review.md) 100%               |
| 9/1（二）  | 建立 OAI + Ariel cuBB + Metanoia RU 初版 config pack                                | 9/1  | `oai-aerial-metanoia-config-pack/` 50%                    |
| 9/2（三）  | 建立 launch sequence：啟動順序、command、expected log、failure checkpoint                 | 9/2  | [`oai-aerial-metanoia-launch-sequence.md`](https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/09-oai-aerial-metanoia/preparation/oai-aerial-metanoia-launch-sequence.md) 60%              |
| 9/3（四）  | 建立 pre-launch checklist：network、sync、fronthaul、frequency、bandwidth、TDD、log path | 9/3  | [`oai-aerial-metanoia-pre-launch-checklist.md`](https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/09-oai-aerial-metanoia/preparation/oai-aerial-metanoia-pre-launch-checklist.md) 80%         |
| 9/4（五）  | 週檢查點：確認 W11 first attempt 是否 ready                                              | 9/4  | [`week10-checkpoint.md`](https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/checkpoints/week10-checkpoint.md)、[`oai-aerial-metanoia-readiness.md`](https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/09-oai-aerial-metanoia/preparation/oai-aerial-metanoia-readiness.md) |

## 本週產出與百分比

| 產出                                            |  完成度 | 截止日期 |
| --------------------------------------------- | ---: | ---- |
| [`metanoia-integration-start-review.md`](https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/09-oai-aerial-metanoia/preparation/metanoia-integration-start-review.md)        | 100% | 8/31 |
| `oai-aerial-metanoia-config-pack/`            |  70% | 9/4  |
| [`oai-aerial-metanoia-launch-sequence.md`](https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/09-oai-aerial-metanoia/preparation/oai-aerial-metanoia-launch-sequence.md)      |  80% | 9/4  |
| [`oai-aerial-metanoia-pre-launch-checklist.md`](https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/09-oai-aerial-metanoia/preparation/oai-aerial-metanoia-pre-launch-checklist.md) | 100% | 9/4  |
| [`oai-aerial-metanoia-readiness.md`](https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/09-oai-aerial-metanoia/preparation/oai-aerial-metanoia-readiness.md)            | 100% | 9/4  |
| [`week10-checkpoint.md`](https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/checkpoints/week10-checkpoint.md)                        | 100% | 9/4  |

## 9/4 通過標準

| 檢查項目                 | 通過標準                                                        |
| -------------------- | ----------------------------------------------------------- |
| Config pack          | OAI、Ariel cuBB、Metanoia RU config 已集中整理                     |
| Launch sequence      | 有明確啟動順序、command、expected log                                |
| Pre-launch checklist | 已確認 network、sync、fronthaul、frequency、bandwidth、TDD、log path |
| Readiness            | 明確標示 Ready / Partial / Blocked                              |
| Pending              | 若有 blocked item，要寫清原因與下一步                                   |

---

# W11：2026/9/7（一）–2026/9/11（五）

## 週里程碑

完成第一次 OAI + Ariel cuBB + Metanoia RU launch attempt，留下完整 experiment log。

## 每日工作

| 日期      | 工作                                                                          | 截止日期 | 預期產出                                                           |
| ------- | --------------------------------------------------------------------------- | ---- | -------------------------------------------------------------- |
| 9/7（一）  | Launch 前最後檢查，確認 config、command、log path、環境狀態                                | 9/7  | [`first-attempt-precheck.md`](https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/09-oai-aerial-metanoia/experiments/first-attempt-precheck.md) 100%                               |
| 9/8（二）  | 執行第一次 OAI + Ariel cuBB + Metanoia RU launch attempt                         | 9/8  | [`oai-aerial-metanoia-first-attempt-log.md`](https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/09-oai-aerial-metanoia/experiments/oai-aerial-metanoia-first-attempt-log.md) 100%                |
| 9/9（三）  | 分析 first attempt log，分類問題屬於 OAI / Ariel cuBB / Metanoia RU / network / sync | 9/9  | [`oai-aerial-metanoia-error-report.md`](https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/09-oai-aerial-metanoia/experiments/oai-aerial-metanoia-error-report.md) 50%                      |
| 9/10（四） | 根據錯誤整理修正方向，補齊 config difference notes                                       | 9/10 | [`oai-aerial-metanoia-debug-notes.md`](https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/09-oai-aerial-metanoia/experiments/oai-aerial-metanoia-debug-notes.md) 60%                       |
| 9/11（五） | 週檢查點：確認 W12 second attempt 或補測方向                                            | 9/11 | [`week11-checkpoint.md`](https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/checkpoints/week11-checkpoint.md)、[`oai-aerial-metanoia-e2e-status.md`](https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/09-oai-aerial-metanoia/experiments/oai-aerial-metanoia-e2e-status.md) 50% |

## 本週產出與百分比

| 產出                                         |  完成度 | 截止日期 |
| ------------------------------------------ | ---: | ---- |
| [`first-attempt-precheck.md`](https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/09-oai-aerial-metanoia/experiments/first-attempt-precheck.md)                | 100% | 9/7  |
| [`oai-aerial-metanoia-first-attempt-log.md`](https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/09-oai-aerial-metanoia/experiments/oai-aerial-metanoia-first-attempt-log.md) | 100% | 9/8  |
| [`oai-aerial-metanoia-error-report.md`](https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/09-oai-aerial-metanoia/experiments/oai-aerial-metanoia-error-report.md)      |  70% | 9/11 |
| [`oai-aerial-metanoia-debug-notes.md`](https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/09-oai-aerial-metanoia/experiments/oai-aerial-metanoia-debug-notes.md)       |  70% | 9/11 |
| [`oai-aerial-metanoia-e2e-status.md`](https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/09-oai-aerial-metanoia/experiments/oai-aerial-metanoia-e2e-status.md)        |  50% | 9/11 |
| [`week11-checkpoint.md`](https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/checkpoints/week11-checkpoint.md)                     | 100% | 9/11 |

## 9/11 通過標準

| 檢查項目           | 通過標準                                            |
| -------------- | ----------------------------------------------- |
| First attempt  | 至少完成 1 次 launch attempt                         |
| Experiment log | 有 command、config、environment、logs、actual result |
| Error report   | 若失敗，有 reproduction steps、logs、environment、推測原因  |
| Debug notes    | 能初步分類問題來源                                       |
| E2E status     | 明確標示 Pass / Partial / Blocked                   |
| Next step      | W12 要修正或補測的方向明確                                 |

---

# W12：2026/9/14（一）–2026/9/18（五）

## 週里程碑

完成第二次測試 / debug / 狀態判定，建立與 Pegatron RU 版本比較初版。

## 每日工作

| 日期      | 工作                                                                   | 截止日期 | 預期產出                                                           |
| ------- | -------------------------------------------------------------------- | ---- | -------------------------------------------------------------- |
| 9/14（一） | 根據 W11 error report 修正 config、launch sequence 或環境設定                  | 9/14 | `oai-aerial-metanoia-config-pack/` 90%                         |
| 9/15（二） | 執行第二次 OAI + Ariel cuBB + Metanoia RU launch attempt 或補測 blocked step | 9/15 | [`oai-aerial-metanoia-second-attempt-log.md`](https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/09-oai-aerial-metanoia/experiments/oai-aerial-metanoia-second-attempt-log.md) 100%               |
| 9/16（三） | 分析第二次測試結果，更新 error report 與 debug notes                              | 9/16 | [`oai-aerial-metanoia-error-report.md`](https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/09-oai-aerial-metanoia/experiments/oai-aerial-metanoia-error-report.md) 100%                     |
| 9/17（四） | 建立 Pegatron RU 版本 vs Metanoia RU 版本比較初版                              | 9/17 | [`pegatron-vs-metanoia-e2e-comparison.md`](https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/09-oai-aerial-metanoia/final-report/pegatron-vs-metanoia-e2e-comparison.md) 70%                   |
| 9/18（五） | 週檢查點：確認最終狀態與 W13 要收斂的內容                                              | 9/18 | [`week12-checkpoint.md`](https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/checkpoints/week12-checkpoint.md)、[`oai-aerial-metanoia-e2e-status.md`](https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/09-oai-aerial-metanoia/experiments/oai-aerial-metanoia-e2e-status.md) 90% |

## 本週產出與百分比

| 產出                                          |  完成度 | 截止日期 |
| ------------------------------------------- | ---: | ---- |
| `oai-aerial-metanoia-config-pack/`          |  90% | 9/18 |
| [`oai-aerial-metanoia-second-attempt-log.md`](https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/09-oai-aerial-metanoia/experiments/oai-aerial-metanoia-second-attempt-log.md) | 100% | 9/15 |
| [`oai-aerial-metanoia-error-report.md`](https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/09-oai-aerial-metanoia/experiments/oai-aerial-metanoia-error-report.md)       | 100% | 9/16 |
| [`oai-aerial-metanoia-debug-notes.md`](https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/09-oai-aerial-metanoia/experiments/oai-aerial-metanoia-debug-notes.md)        | 100% | 9/18 |
| [`pegatron-vs-metanoia-e2e-comparison.md`](https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/09-oai-aerial-metanoia/final-report/pegatron-vs-metanoia-e2e-comparison.md)    |  80% | 9/18 |
| [`oai-aerial-metanoia-e2e-status.md`](https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/09-oai-aerial-metanoia/experiments/oai-aerial-metanoia-e2e-status.md)         |  90% | 9/18 |
| [`week12-checkpoint.md`](https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/checkpoints/week12-checkpoint.md)                      | 100% | 9/18 |

## 9/18 通過標準

| 檢查項目             | 通過標準                                        |
| ---------------- | ------------------------------------------- |
| Second attempt   | 有第二次 attempt log，或清楚說明無法執行的 blocking reason |
| Error report     | 錯誤分析完整，能支援後續接手                              |
| E2E status       | 明確判定 Pass / Partial / Blocked / Fail        |
| Comparison draft | 至少比較 Pegatron RU 版本與 Metanoia RU 版本的 8 個項目  |
| Final scope      | W13 只做收斂、補文件、最終報告，不再大改方向                    |

---

# W13：2026/9/21（一）–2026/9/25（五）

## 週里程碑

完成最終驗證報告、comparison、handover guide。

## 每日工作

| 日期      | 工作                                                          | 截止日期 | 預期產出                                              |
| ------- | ----------------------------------------------------------- | ---- | ------------------------------------------------- |
| 9/21（一） | 補齊 final E2E status、config pack、attempt logs                | 9/21 | [`oai-aerial-metanoia-final-verification.md`](https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/09-oai-aerial-metanoia/final-report/oai-aerial-metanoia-final-verification.md) 70%   |
| 9/22（二） | 完成 Pegatron RU 版本 vs Metanoia RU 版本比較                       | 9/22 | [`pegatron-vs-metanoia-e2e-comparison.md`](https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/09-oai-aerial-metanoia/final-report/pegatron-vs-metanoia-e2e-comparison.md) 100%     |
| 9/23（三） | 撰寫 final handover guide：repo、config、build、launch、logs、debug | 9/23 | [`final-handover-guide.md`](https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/09-oai-aerial-metanoia/final-report/final-handover-guide.md) 80%                     |
| 9/24（四） | 整理所有 meeting notes 產生的 Action Items 狀態與 open issues         | 9/24 | [`final-open-issues.md`](https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/09-oai-aerial-metanoia/final-report/final-open-issues.md)、meeting notes 更新           |
| 9/25（五） | 週檢查點：完成最終文件與 9/26 檢查準備                                      | 9/25 | [`final-3-month-summary.md`](https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/09-oai-aerial-metanoia/final-report/final-3-month-summary.md)、[`week13-checkpoint.md`](https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/checkpoints/week13-checkpoint.md) |

## 本週產出與百分比

| 產出                                          |  完成度 | 截止日期 |
| ------------------------------------------- | ---: | ---- |
| [`oai-aerial-metanoia-final-verification.md`](https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/09-oai-aerial-metanoia/final-report/oai-aerial-metanoia-final-verification.md) | 100% | 9/25 |
| [`pegatron-vs-metanoia-e2e-comparison.md`](https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/09-oai-aerial-metanoia/final-report/pegatron-vs-metanoia-e2e-comparison.md)    | 100% | 9/22 |
| [`final-handover-guide.md`](https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/09-oai-aerial-metanoia/final-report/final-handover-guide.md)                   | 100% | 9/25 |
| [`final-open-issues.md`](https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/09-oai-aerial-metanoia/final-report/final-open-issues.md)                      | 100% | 9/25 |
| [`final-3-month-summary.md`](https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/09-oai-aerial-metanoia/final-report/final-3-month-summary.md)                  | 100% | 9/25 |
| [`week13-checkpoint.md`](https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/checkpoints/week13-checkpoint.md)                      | 100% | 9/25 |

## 9/25 通過標準

| 檢查項目               | 通過標準                                             |
| ------------------ | ------------------------------------------------ |
| Final verification | 有 OAI + Ariel cuBB + Metanoia RU 最終狀態報告          |
| Comparison         | 有 Pegatron RU 版本 vs Metanoia RU 版本比較             |
| Handover           | 下一位接手者能找到 repo、config、build、launch、logs、debug 文件 |
| Open issues        | 所有未完成項目有原因、狀態、下一步                                |
| Meeting KPI        | Meeting Notes 中 Action Items 的狀態有回收              |
| Final summary      | 能清楚說明 7–9 月完成了什麼、未完成什麼、下一步是什麼                    |

---

# Final Checkpoint：2026/9/26（六）

## 最終檢查點，不安排新技術工作

| 檢查項目                                        | 通過標準                                                |
| ------------------------------------------- | --------------------------------------------------- |
| [`month2-summary.md`](https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/08-metanoia-source-study/summary-and-plan/month2-summary.md)                         | 100%                                                |
| [`month3-integration-plan.md`](https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/08-metanoia-source-study/summary-and-plan/month3-integration-plan.md)                | 100%                                                |
| [`oai-aerial-metanoia-final-verification.md`](https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/09-oai-aerial-metanoia/final-report/oai-aerial-metanoia-final-verification.md) | 100%                                                |
| [`pegatron-vs-metanoia-e2e-comparison.md`](https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/09-oai-aerial-metanoia/final-report/pegatron-vs-metanoia-e2e-comparison.md)    | 100%                                                |
| [`final-handover-guide.md`](https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/09-oai-aerial-metanoia/final-report/final-handover-guide.md)                   | 100%                                                |
| [`final-open-issues.md`](https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/09-oai-aerial-metanoia/final-report/final-open-issues.md)                      | 100%                                                |
| [`final-3-month-summary.md`](https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/09-oai-aerial-metanoia/final-report/final-3-month-summary.md)                  | 100%                                                |
| [`final-checkpoint.md`](https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/checkpoints/final-checkpoint.md)                       | 100%                                                |
| Meeting Notes                               | 所有會議都有 Action Items 或註明無新增 Action Items             |
| Daily Notes                                 | 每個工作日都有 plan、review、evidence、next working day plan  |
| Evidence                                    | 每個實驗結果都有 command、config、log、result 或 blocked reason |

---

# 9 月最終比較項目

9 月要比較的是：

> **7 月：OAI L2/L3 + Ariel cuBB + Pegatron RU**
> **9 月：OAI L2/L3 + Ariel cuBB + Metanoia RU**

建議比較：

| 比較項目                  | Pegatron RU 版本           | Metanoia RU 版本           | 為什麼要比                |
| --------------------- | ------------------------ | ------------------------ | -------------------- |
| RU 類型                 | Pegatron RU              | Metanoia RU              | 主要替換對象               |
| OAI L2/L3             | OAI                      | OAI                      | 確認上層是否一致             |
| L1 / cuBB             | Ariel cuBB               | Ariel cuBB               | 確認 L1/cuBB 是否一致      |
| RU config             | Pegatron RU config       | Metanoia RU config       | RU 對接差異              |
| Frequency / bandwidth | 7 月設定                    | 9 月設定                    | 需要對齊                 |
| Numerology / SCS      | 7 月設定                    | 9 月設定                    | 需要對齊                 |
| TDD pattern           | 7 月設定                    | 9 月設定                    | 影響 timing            |
| IP / port             | Pegatron 設定              | Metanoia 設定              | 對接必要條件               |
| fronthaul / eCPRI     | Pegatron 行為              | Metanoia 行為              | cuBB 對 RU 連線核心       |
| clock / sync          | Pegatron 設定              | Metanoia 設定              | 常見 blocking point    |
| antenna / gain        | Pegatron 設定              | Metanoia 設定              | RF 行為差異              |
| launch sequence       | 7 月流程                    | 9 月流程                    | 操作差異                 |
| log location          | Pegatron logs            | Metanoia logs            | debug 可行性            |
| E2E status            | Pass / Partial / Blocked | Pass / Partial / Blocked | 最終驗證                 |
| error type            | 7 月錯誤                    | 9 月錯誤                    | 找出 Metanoia 特有問題     |
| reproducibility       | 是否能照文件重跑                 | 是否能照文件重跑                 | 符合 Playbook 可驗證與交接概念 |

---
