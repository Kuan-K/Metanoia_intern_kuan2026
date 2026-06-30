# 一、整體三個月目標

## 總目標

完成一套可交接、可驗證、可追蹤的 OAI / Ariel cuBB / RU E2E 研究流程。

| 月份  | 月目標                                                                  | 月檢查點 |
| --- | -------------------------------------------------------------------- | ---- |
| 7 月 | 完成 Richard / Ming 交接，建立 OAI + Ariel cuBB + Pegatron RU baseline 與比較表 | 7/31 |
| 8 月 | 完成 Metanoia MOSART 開源碼研究，建立 build / config / parameter / mapping 文件  | 8/28 |
| 9 月 | 完成 OAI + Ariel cuBB + Metanoia RU 整合測試、驗證報告與最終交接文件                   | 9/26 |

---

# 二、每週里程碑總表

| 週次    | 日期        | 週五檢查點 | 週里程碑                                                   | 預期總進度 |
| ----- | --------- | ----- | ------------------------------------------------------ | ----: |
| W1    | 7/1–7/3   | 7/3   | 與 Ming / Richard 完成交接，確認 action items 與資料入口          | 8%   |
| W2    | 7/6–7/10  | 7/10  | 完成 OAI + Pegatron RU baseline 深入整理，並整理 DGX Spark / Aerial L1 + OAI L2 安裝手冊  |  16% |
| W3    | 7/13–7/17 | 7/17  | 完成 Pegatron RU 設定檔理解，嘗試讓 RU 參數對齊 Ariel cuBB 需求             | 24%  |
| W4    | 7/20–7/24 | 7/24  | 嘗試跑通 OAI L2/L3 + Ariel cuBB + Pegatron RU E2E       | 32%  |
| W5    | 7/27–7/31 | 7/31  | 完成 OAI + Pegatron baseline 與 OAI + Ariel cuBB + Pegatron 的差異比較與月報       | 40%  |
| W6    | 8/3–8/7   | 8/7   | 完成 Metanoia MOSART repo 架構與 README / source tree 初版      |   48% |
| W7    | 8/10–8/14 | 8/14  | 完成 Metanoia build / run / config 初版驗證                     |   56% |
| W8    | 8/17–8/21 | 8/21  | 完成 Pegatron vs Metanoia config mapping 與整合可行性初版        |   64% |
| W9    | 8/24–8/28 | 8/28  | 完成 8 月月檢查：Metanoia source study 與 9 月整合計畫           |   72% |
| W10   | 8/31–9/4  | 9/4   | 完成 OAI + Ariel + Metanoia 初版 config pack 與 launch flow    |   80% |
| W11   | 9/7–9/11  | 9/11  | 完成第一次 Metanoia E2E run log 與 error report                 |   86% |
| W12   | 9/14–9/18 | 9/18  | 完成第二次測試、debug tree、Pegatron vs Metanoia E2E 比較         |   92% |
| W13   | 9/21–9/25 | 9/25  | 完成最終報告、handover guide、config pack、experiment logs      |   98% |
| Final | 9/26      | 9/26  | 最終檢查，不新增工作，只確認提交完整性                            |  100% |


# 三、週計畫

# W1：2026/7/1（三）–2026/7/3（五）

## 週里程碑

完成 Ming / Richard 初次交接，確認 7 月工作入口與 meeting action items。

## 每日工作

| 日期     | 工作                                                                                                           | 截止日期 | 預期產出                                                                       |
| ------ | ------------------------------------------------------------------------------------------------------------ | ---- | -------------------------------------------------------------------------- |
| 7/1（三） | 準備 Ming / Richard 交接問題清單；與 Ming 開會，交接已跑通的 OAI L2/L3 + OAI L1 + Pegatron RU E2E，確認 gNB 與 RU 設定檔位置、主要參數、成功條件   | 7/1  | `2026-07-01-ming-handover.md`                                              |
| 7/2（四） | LAB workshop                                                                                                 | 7/2  | 無需技術產出，只列入行程                                                               |
| 7/3（五） | 嘗試安裝 DGX Spark；與 Richard 開會交接 DGX Spark 安裝手冊、Aerial L1 + OAI L2 安裝手冊、WNC RU config 位置、OAI / Ariel RAN 參數設定方式 | 7/3  | `2026-07-03-richard-handover.md`、`dgx-spark-aerial-oai-installation.md` 初版 |

## 本週產出與百分比

| 產出                                     |  完成度 | 截止日期 |
| -------------------------------------- | ---: | ---- |  |
| `2026-07-01-ming-meeting note.md`      | 100% | 7/1  |
| `2026-07-03-richard-meeting note.md`   | 100% | 7/3  |
| `oai-pegatron-baseline.md`             |  40% | 7/3  |
| `dgx-spark-aerial-oai-installation.md` |  30% | 7/3  |
| `wnc-ru-config-index.md`               |  30% | 7/3  |
| `pegatron-ru-config-index.md`          |  30% | 7/3  |

## 7/3 通過標準

| 檢查項目                  | 通過標準                                                                          |
| --------------------- | ----------------------------------------------------------------------------- |
| Ming meeting notes    | 有記錄 OAI + Pegatron RU E2E 已跑通的 config、command、log、成功條件                        |
| Richard meeting notes | 有記錄 DGX Spark / Aerial L1 + OAI L2 安裝手冊來源、WNC RU config 位置、OAI / Ariel 參數設定入口 |
| Action Items          | 只放在 meeting notes 裡，每個 action item 有 owner、deliverable、due date、evidence      |
| 下週工作入口           | 明確知道 W2 要整理哪幾份 config、哪份安裝手冊、哪個 baseline log                                  |

---

# W2：2026/7/6（一）–2026/7/10（五）

## 週里程碑

完成 **OAI + Pegatron RU baseline 的深入整理**，並完成 **DGX Spark / Aerial L1 + OAI L2 安裝手冊整理到可照著做的程度**。

## 每日工作

| 日期      | 工作                                                                                                 | 截止日期 | 預期產出                                                      |
| ------- | -------------------------------------------------------------------------------------------------- | ---- | --------------------------------------------------------- |
| 7/6（一）  | 整理已跑通的 OAI L2/L3 + OAI L1 + Pegatron RU E2E baseline：使用版本、config、command、log、成功條件                  | 7/6  | `oai-pegatron-baseline-summary.md` 60%                    |
| 7/7（二）  | 深入整理 OAI gNB 設定檔參數：頻段、bandwidth、numerology、TDD pattern、RU/fronthaul 相關設定                           | 7/7  | `oai-gnb-parameter-table.md` 50%                          |
| 7/8（三）  | 深入整理 Pegatron RU 設定檔參數：RU IP、port、clock/sync、frequency、bandwidth、gain、antenna、eCPRI/fronthaul 相關設定 | 7/8  | `pegatron-ru-parameter-table.md` 50%                      |
| 7/9（四）  | 整理 DGX Spark / Aerial L1 + OAI L2 安裝手冊：環境需求、安裝步驟、依賴套件、啟動方式、可能錯誤                                    | 7/9  | `dgx-spark-aerial-oai-installation.md` 70%                |
| 7/10（五） | 週檢查點：整理 baseline、參數表、安裝手冊；確認 W3 要把 Pegatron RU 哪些參數對齊 Ariel cuBB                                   | 7/10 | `week2-checkpoint.md`、`ru-to-cubb-alignment-questions.md` |

## 本週產出與百分比

| 產出                                     |  完成度 | 截止日期 |
| -------------------------------------- | ---: | ---- |
| `oai-pegatron-baseline.md`             |  80% | 7/10 |
| `oai-gnb-parameter-table.md`           |  60% | 7/10 |
| `pegatron-ru-parameter-table.md`       |  60% | 7/10 |
| `dgx-spark-aerial-oai-installation.md` |  70% | 7/10 |
| `config-file-location-index.md`        |  80% | 7/10 |
| `ru-to-cubb-alignment-questions.md`    | 100% | 7/10 |
| `week2-checkpoint.md`                  | 100% | 7/10 |

## 7/10 通過標準

| 檢查項目                    | 通過標準                                  |
| ----------------------- | ------------------------------------- |
| OAI + Pegatron baseline | 有 config、command、log、成功條件，不只是寫「已跑通」   |
| OAI gNB 參數              | 至少整理 10 個與 E2E / RU 對接有關的參數           |
| Pegatron RU 參數          | 至少整理 10 個 RU 端參數，並標示哪些可能要對齊 cuBB      |
| DGX / Aerial 安裝手冊       | 至少整理環境需求、安裝步驟、啟動入口、blocked issue      |
| W3 準備                   | 有列出「Pegatron RU 要對齊 Ariel cuBB」的待確認問題 |

---

# W3：2026/7/13（一）–2026/7/17（五）

## 週里程碑

完成 Pegatron RU 設定檔理解，並嘗試將 RU 設定對齊 Ariel cuBB 需求。

重點是回答：
> Pegatron RU 原本是怎麼跟 OAI L1 對接的？
> 若要改成 Ariel cuBB，RU 端哪些參數必須一致？

## 每日工作

| 日期      | 工作                                                                                                            | 截止日期 | 預期產出                                                  |
| ------- | ------------------------------------------------------------------------------------------------------------- | ---- | ----------------------------------------------------- |
| 7/13（一） | 整理 OAI L1 baseline 中 gNB 與 Pegatron RU 的參數對應關係                                                                | 7/13 | `oai-gnb-to-pegatron-ru-parameter-mapping.md` 50%     |
| 7/14（二） | 整理 Ariel cuBB / Ariel RAN 所需設定：cuBB 需要哪些 RU 端資訊、啟動時讀哪些 config                                                 | 7/14 | `aerial-cubb-parameter-table.md` 60%                  |
| 7/15（三） | 建立 Pegatron RU 對齊 Ariel cuBB 的 mapping checklist：frequency、bandwidth、numerology、TDD、IP/port、sync、antenna、gain | 7/15 | `pegatron-ru-to-aerial-cubb-mapping-checklist.md` 70% |
| 7/16（四） | 依據 mapping checklist 調整或整理 OAI + Ariel cuBB + Pegatron RU 測試用 config pack                                     | 7/16 | `oai-aerial-pegatron-config-pack/` 60%                |
| 7/17（五） | 週檢查點：確認 W4 launch attempt 所需 config、command、log path、環境需求是否 ready                                             | 7/17 | `e2e-readiness-checklist.md`、`week3-checkpoint.md`    |

## 本週產出與百分比

| 產出                                                |  完成度 | 截止日期 |
| ------------------------------------------------- | ---: | ---- |
| `oai-gnb-to-pegatron-ru-parameter-mapping.md`     |  70% | 7/17 |
| `aerial-cubb-parameter-table.md`                  |  70% | 7/17 |
| `pegatron-ru-to-aerial-cubb-mapping-checklist.md` |  80% | 7/17 |
| `oai-aerial-pegatron-config-pack/`                |  60% | 7/17 |
| `e2e-readiness-checklist.md`                      |  90% | 7/17 |
| `e2e-launch-sequence.md`                          |  70% | 7/17 |
| `log-location-and-debug-guide.md`                 |  70% | 7/17 |
| `week3-checkpoint.md`                             | 100% | 7/17 |

## 7/17 通過標準

| 檢查項目                 | 通過標準                                                                        |
| -------------------- | --------------------------------------------------------------------------- |
| OAI baseline mapping | 能說明 OAI gNB 與 Pegatron RU 哪些參數需要一致                                          |
| Ariel cuBB 需求        | 能列出 Ariel cuBB 需要從 config 或環境取得哪些 RU 資訊                                     |
| RU-to-cuBB alignment | checklist 至少包含 frequency、bandwidth、numerology、TDD、IP/port、sync、antenna、gain |
| Config pack          | OAI、Ariel cuBB、Pegatron RU 測試用 config 已集中整理                                 |
| W4 readiness         | 已列出 W4 launch attempt 的 command、config、log path、expected result             |

---

# W4：2026/7/20（一）–2026/7/24（五）

## 週里程碑

嘗試跑通 **OAI L2/L3 + Ariel cuBB + Pegatron RU E2E**，並留下完整 experiment log。

## 每日工作

| 日期      | 工作                                                                                     | 截止日期 | 預期產出                                                      |
| ------- | -------------------------------------------------------------------------------------- | ---- | --------------------------------------------------------- |
| 7/20（一） | 根據 W3 readiness checklist 進行 launch 前檢查：版本、config、network、clock/sync、log path          | 7/20 | `pre-launch-checklist.md` 100%                            |
| 7/21（二） | 執行 OAI L2/L3 + Ariel cuBB + Pegatron RU launch attempt，保存 command、config、log、result | 7/21 | `oai-aerial-pegatron-first-attempt-log.md` 100%           |
| 7/22（三） | 分析第一次 attempt log；若失敗，整理 reproduction steps、error、環境、推測原因                              | 7/22 | `oai-aerial-pegatron-error-report.md` 70%                 |
| 7/23（四） | 根據 7/22 分析修正設定，進行 launch attempt 或補測關鍵步驟                                            | 7/23 | `oai-aerial-pegatron-second-attempt-log.md` 100%          |
| 7/24（五） | 週檢查點：整理本週 E2E 狀態，確認是 Pass / Partial / Blocked，列出 W5 比較所需 evidence                      | 7/24 | `week4-checkpoint.md`、`oai-aerial-pegatron-e2e-status.md` |

## 本週產出與百分比

| 產出                                          |  完成度 | 截止日期 |
| ------------------------------------------- | ---: | ---- |
| `pre-launch-checklist.md`                   | 100% | 7/20 |
| `oai-aerial-pegatron-first-attempt-log.md`  | 100% | 7/21 |
| `oai-aerial-pegatron-second-attempt-log.md` | 100% | 7/23 |
| `oai-aerial-pegatron-error-report.md`       |  80% | 7/24 |
| `oai-aerial-pegatron-e2e-status.md`         | 100% | 7/24 |
| `common-error-list.md`                      |  80% | 7/24 |
| `week4-checkpoint.md`                       | 100% | 7/24 |

## 7/24 通過標準

| 檢查項目           | 通過標準                                                         |
| -------------- | ------------------------------------------------------------ |
| Launch attempt | 至少完成 1–2 次 OAI + Ariel cuBB + Pegatron RU launch attempt     |
| Experiment log | 每次 attempt 都有 command、config、log、result                      |
| E2E status     | 明確標示 Pass / Partial / Blocked                                |
| Error report   | 若失敗，必須有 reproduction steps、logs、environment、推測原因             |
| Evidence       | 有足夠資料支撐 W5 與 OAI + Pegatron baseline 比較                      |
| Action Items   | 若本週有再開會，Action Items 留在該次 meeting note；若沒開會，不新增 action items |

---

# W5：2026/7/27（一）–2026/7/31（五）

## 月里程碑

整理 OAI + Pegatron RU baseline 與 OAI + Ariel cuBB + Pegatron RU 的差異，完成 7 月月報。

## 每日工作

| 日期      | 工作                                                                              | 截止日期 | 預期產出                                                    |
| ------- | ------------------------------------------------------------------------------- | ---- | ------------------------------------------------------- |
| 7/27（一） | 整理 OAI + Pegatron baseline 的最終版本：config、command、參數、log、成功條件                     | 7/27 | `oai-pegatron-baseline-summary.md` 100%                 |
| 7/28（二） | 整理 OAI + Ariel cuBB + Pegatron RU 的最終狀態：config、command、log、成功 / 失敗 / blocked 原因 | 7/28 | `oai-aerial-pegatron-e2e-status.md` 100%                |
| 7/29（三） | 建立兩套系統的比較表：架構、參數、啟動流程、log、錯誤、限制、可重現性                                            | 7/29 | `oai-pegatron-vs-oai-aerial-pegatron-comparison.md` 80% |
| 7/30（四） | 整理 7 月 meeting notes 中 Action Items 的完成狀態；整理 open issues 與 8 月銜接方向              | 7/30 | `month1-open-issues.md`、meeting notes 更新                |
| 7/31（五） | 月檢查點：完成 7 月月報，列出 8 月 Metanoia 研究入口                                              | 7/31 | `month1-summary.md`、`month2-metanoia-entry-plan.md`     |

## 本週產出與百分比

| 產出                                                  |  完成度 | 截止日期 |
| --------------------------------------------------- | ---: | ---- |
| `oai-pegatron-baseline-summary.md`                  | 100% | 7/27 |
| `oai-aerial-pegatron-e2e-status.md`                 | 100% | 7/28 |
| `oai-pegatron-vs-oai-aerial-pegatron-comparison.md` | 100% | 7/31 |
| `oai-gnb-parameter-table.md`                        |  90% | 7/31 |
| `aerial-cubb-parameter-table.md`                    |  90% | 7/31 |
| `pegatron-ru-parameter-table.md`                    |  90% | 7/31 |
| `dgx-spark-aerial-oai-installation.md`              | 100% | 7/31 |
| `month1-open-issues.md`                             | 100% | 7/31 |
| `month1-summary.md`                                 | 100% | 7/31 |
| `month2-metanoia-entry-plan.md`                     | 100% | 7/31 |

## 7/31 月檢查通過標準

| 檢查項目                      | 通過標準                                                                     |
| ------------------------- | ------------------------------------------------------------------------ |
| OAI + Pegatron baseline   | 已整理成可比較 baseline，不只是「已跑通」                                                |
| OAI + Ariel + Pegatron    | 有 launch attempt / E2E result / blocked reason 的完整紀錄                     |
| Comparison                | 有兩套系統的差異比較表                                                              |
| Parameter understanding   | OAI、Ariel cuBB、Pegatron RU 的關鍵參數已整理                                      |
| DGX / Aerial installation | DGX Spark / Aerial L1 + OAI L2 安裝手冊整理完成                                  |
| Meeting KPI               | Ming / Richard meeting notes 有 Action Items；後續工作有 follow 這些 Action Items |
| Open issues               | 未完成項目有原因與下一步                                                             |
| 8 月銜接                   | 明確知道 Metanoia 研究第一週要從哪裡開始                                                |

---

7 月最終比較表比較項目：

| 比較項目              | OAI + Pegatron RU baseline       | OAI + Ariel cuBB + Pegatron RU       | 為什麼要比                |
| ----------------- | -------------------------------- | ------------------------------------ | -------------------- |
| 系統架構              | OAI L2/L3 + OAI L1 + Pegatron RU | OAI L2/L3 + Ariel cuBB + Pegatron RU | 確認 Ariel cuBB 替代了哪一段 |
| L1 / cuBB 角色      | OAI L1                           | Ariel cuBB                           | 這是兩套系統核心差異           |
| gNB config        | OAI baseline 使用的 gNB config      | Ariel 版本使用的 OAI config               | 確認 L2/L3 設定是否需要改     |
| RU config         | Pegatron RU baseline config      | Pegatron RU 對齊 cuBB 後的 config        | 確認 RU 端是否需要重設        |
| 頻率 / bandwidth    | baseline value                   | Ariel 版本 value                       | 必須對齊                 |
| numerology / SCS  | baseline value                   | Ariel 版本 value                       | 必須對齊                 |
| TDD pattern       | baseline value                   | Ariel 版本 value                       | 影響 frame timing      |
| fronthaul / eCPRI | baseline 設定                      | Ariel cuBB 需求                        | RU 對接 cuBB 的重點       |
| IP / port         | baseline 設定                      | Ariel 版本設定                           | 對接必須一致               |
| clock / sync      | baseline 設定                      | Ariel 版本設定                           | 常見 E2E 問題來源          |
| antenna / gain    | baseline 設定                      | Ariel 版本設定                           | 影響 RF / RU 行為        |
| 啟動順序              | OAI + Pegatron 啟動流程              | OAI + cuBB + Pegatron 啟動流程           | 確認流程差異               |
| log 位置            | OAI gNB log、RU log               | OAI log、cuBB log、RU log              | Debug 需要             |
| 成功條件              | baseline 如何判斷成功                  | Ariel 版本如何判斷成功                       | 避免只看「有沒有跑起來」         |
| 錯誤訊息              | baseline 是否有 error               | Ariel 版本 error                       | 用來定位問題               |
| 可重現性              | 是否能照文件重跑                         | 是否能照文件重跑                             | 符合 Playbook 可驗證概念    |

---

## W6：2026/8/3（一）–2026/8/7（五）

### 週里程碑

完成 Metanoia MOSART repo overview、source tree、README summary。

### 每日工作

| 日期     | 工作                                  |
| ------ | ----------------------------------- |
| 8/3（一） | clone / 瀏覽 MOSART repo，整理 README    |
| 8/4（二） | 建立 source tree，標出主要資料夾功能            |
| 8/5（三） | 找 build / install / dependency 文件   |
| 8/6（四） | 找 config、script、example、entry point |
| 8/7（五） | 週檢查點：完成 repo overview 初版            |

### 本週產出與百分比

| 產出                                  |  百分比 |
| ----------------------------------- | ---: |
| `metanoia-mosart-repo-overview.md`  |  80% |
| `metanoia-mosart-source-tree.md`    |  80% |
| `metanoia-readme-summary.md`        | 100% |
| `metanoia-build-requirements.md`    |  50% |
| `metanoia-config-location-index.md` |  50% |
| `metanoia-open-questions.md`        | 100% |
| `week6-meeting-notes.md`            | 100% |
| `week6-daily-notes/`                | 100% |

### 8/7 通過標準

| 檢查項目           | 通過標準                                       |
| -------------- | ------------------------------------------ |
| Repo overview  | 說得出 MOSART repo 的主要資料夾與用途                  |
| Source tree    | 至少標出 build、config、runtime、radio / PHY 相關位置 |
| README summary | 整理官方說明、限制、執行提示                             |
| Open questions | 至少 10 個需要問學長或教授的具體問題                       |
| Evidence       | 附 repo path、檔案位置或截圖                        |

---

## W7：2026/8/10（一）–2026/8/14（五）

### 週里程碑

完成 Metanoia build / run / config 初版驗證。

### 每日工作

| 日期      | 工作                                    |
| ------- | ------------------------------------- |
| 8/10（一） | 整理 build system 與 dependencies        |
| 8/11（二） | 嘗試 build，保存成功或失敗 log                  |
| 8/12（三） | 找 runtime config 與執行參數                |
| 8/13（四） | 找 log / debug / error handling 方法     |
| 8/14（五） | 週檢查點：完成 build guide 與 config notes 初版 |

### 本週產出與百分比

| 產出                                  |  百分比 |
| ----------------------------------- | ---: |
| `metanoia-build-guide.md`           |  80% |
| `metanoia-build-log.md`             | 100% |
| `metanoia-runtime-config-notes.md`  |  70% |
| `metanoia-parameter-table.md`       |  60% |
| `metanoia-log-and-debug-guide.md`   |  60% |
| `metanoia-error-report-template.md` | 100% |
| `week7-meeting-notes.md`            | 100% |
| `week7-daily-notes/`                | 100% |

### 8/14 通過標準

| 檢查項目            | 通過標準                                      |
| --------------- | ----------------------------------------- |
| Build guide     | 有環境需求、build command、expected output       |
| Build log       | 成功或失敗都要保存完整 log                           |
| Runtime notes   | 找到主要執行入口或說明沒有找到的證據                        |
| Parameter table | 至少 15 個 Metanoia 相關參數或設定欄位                |
| Error template  | 可用來記錄 reproduction steps、logs、environment |

---

## W8：2026/8/17（一）–2026/8/21（五）

### 週里程碑

完成 Pegatron RU vs Metanoia RU config mapping 與 OAI + Ariel 整合可行性初版。

### 每日工作

| 日期      | 工作                                     |
| ------- | -------------------------------------- |
| 8/17（一） | 深入整理 Metanoia 參數表                      |
| 8/18（二） | 對照 Pegatron RU config                  |
| 8/19（三） | 建立 Pegatron vs Metanoia config mapping |
| 8/20（四） | 分析接 OAI + Ariel cuBB 的可行性與風險           |
| 8/21（五） | 週檢查點：完成 feasibility report 初版          |

### 本週產出與百分比

| 產出                                          |  百分比 |
| ------------------------------------------- | ---: |
| `metanoia-parameter-table.md`               |  90% |
| `pegatron-vs-metanoia-config-mapping.md`    |  80% |
| `pegatron-vs-metanoia-ru-comparison.md`     |  80% |
| `metanoia-oai-aerial-feasibility-report.md` |  70% |
| `metanoia-integration-risk-list.md`         |  90% |
| `metanoia-interface-notes.md`               |  70% |
| `week8-meeting-notes.md`                    | 100% |
| `week8-daily-notes/`                        | 100% |

### 8/21 通過標準

| 檢查項目               | 通過標準                                     |
| ------------------ | ---------------------------------------- |
| Config mapping     | 至少 15 個 Pegatron config 欄位對應 Metanoia 欄位 |
| RU comparison      | 至少比較架構、config、啟動方式、log、限制、風險             |
| Feasibility report | 明確判斷可行 / 部分可行 / 目前不可行，並說明原因              |
| Risk list          | 至少列出 5 個整合風險與對應驗證方式                      |
| Evidence           | 每個 mapping 欄位都要有來源位置或註明待確認               |

---

## W9：2026/8/24（一）–2026/8/28（五）

### 月里程碑

完成 8 月月檢查：Metanoia MOSART source study、build guide、config mapping、9 月整合計畫。

### 每日工作

| 日期      | 工作                         |
| ------- | -------------------------- |
| 8/24（一） | 補齊 Metanoia source study   |
| 8/25（二） | 補齊 build / run / config 文件 |
| 8/26（三） | 完成 Pegatron vs Metanoia 比較 |
| 8/27（四） | 完成 9 月整合測試計畫               |
| 8/28（五） | 月檢查點：完成 Month 2 summary    |

### 本週產出與百分比

| 產出                                          |  百分比 |
| ------------------------------------------- | ---: |
| `month2-summary.md`                         | 100% |
| `metanoia-mosart-repo-overview.md`          | 100% |
| `metanoia-mosart-source-tree.md`            | 100% |
| `metanoia-build-guide.md`                   | 100% |
| `metanoia-runtime-config-notes.md`          | 100% |
| `metanoia-parameter-table.md`               | 100% |
| `metanoia-log-and-debug-guide.md`           |  90% |
| `pegatron-vs-metanoia-config-mapping.md`    | 100% |
| `pegatron-vs-metanoia-ru-comparison.md`     | 100% |
| `metanoia-oai-aerial-feasibility-report.md` | 100% |
| `month3-integration-plan.md`                | 100% |
| `month2-action-item-status.md`              | 100% |

### 8/28 月檢查通過標準

| 檢查項目         | 通過標準                                             |
| ------------ | ------------------------------------------------ |
| Source study | repo 架構、build、run、config、log 都有整理                |
| Mapping      | Pegatron vs Metanoia config mapping 完成           |
| Feasibility  | 9 月整合方向明確                                        |
| Risk         | 每個主要風險都有驗證方式                                     |
| Action item  | 所有 8 月 action item 有狀態與 evidence                 |
| 9 月計畫        | 已列出 first run config、command、log collection plan |

---

# 六、9 月：整合與收斂，工作量降低

9 月不再安排大量開源碼研究，主要是：

1. 建立初版整合設定
2. 跑第一次測試
3. 修正後跑第二次
4. 整理最終文件

---

## W10：2026/8/31（一）–2026/9/4（五）

### 週里程碑

完成 OAI + Ariel cuBB + Metanoia 初版 config pack 與 launch flow。

### 每日工作

| 日期      | 工作                                     |
| ------- | -------------------------------------- |
| 8/31（一） | Review 8 月 feasibility report          |
| 9/1（二）  | 建立 OAI + Ariel + Metanoia 初版 config    |
| 9/2（三）  | 與 Richard / Ming 確認整合方向                |
| 9/3（四）  | 補齊 config pack、launch flow、risk review |
| 9/4（五）  | 週檢查點：確認可以進入 first run                  |

### 本週產出與百分比

| 產出                                      |  百分比 |
| --------------------------------------- | ---: |
| `oai-aerial-metanoia-initial-config.md` |  80% |
| `oai-aerial-metanoia-config-pack/`      |  70% |
| `metanoia-config-mapping-checklist.md`  |  90% |
| `oai-aerial-metanoia-launch-flow.md`    |  80% |
| `month3-risk-review.md`                 |  90% |
| `week10-meeting-notes.md`               | 100% |
| `week10-daily-notes/`                   | 100% |

### 9/4 通過標準

| 檢查項目        | 通過標準                                |
| ----------- | ----------------------------------- |
| Config pack | OAI、Ariel、Metanoia config 都集中整理     |
| Launch flow | 有明確 command order                   |
| Checklist   | Pegatron-to-Metanoia mapping 已逐項確認  |
| Risk review | 已知風險都有觀察 log 與驗證方式                  |
| Meeting     | 整合方向已經問過 Richard / Ming 或列為 pending |

---

## W11：2026/9/7（一）–2026/9/11（五）

### 週里程碑

完成第一次 OAI + Ariel cuBB + Metanoia E2E 測試紀錄與 error report。

### 每日工作

| 日期      | 工作                             |
| ------- | ------------------------------ |
| 9/7（一）  | First run 前檢查 config           |
| 9/8（二）  | 執行第一次測試                        |
| 9/9（三）  | 整理 gNB / Ariel / Metanoia logs |
| 9/10（四） | 分類錯誤，建立 error report           |
| 9/11（五） | 週檢查點：確認 second run 修正方向        |

### 本週產出與百分比

| 產出                                   |  百分比 |
| ------------------------------------ | ---: |
| `metanoia-e2e-first-run-log.md`      | 100% |
| `metanoia-e2e-error-report.md`       |  90% |
| `debug-decision-tree.md`             |  80% |
| `oai-aerial-metanoia-config-pack/`   |  85% |
| `oai-aerial-metanoia-launch-flow.md` |  90% |
| `week11-meeting-notes.md`            | 100% |
| `week11-action-items.md`             | 100% |

### 9/11 通過標準

| 檢查項目          | 通過標準                                          |
| ------------- | --------------------------------------------- |
| First run log | 有 command、config、result、log                   |
| Error report  | 若失敗，有 reproduction steps、environment、logs     |
| Debug tree    | 能判斷問題偏向 OAI / Ariel / Metanoia / network / RF |
| Next action   | 每個 blocking issue 都有 owner、due date、evidence  |
| Evidence      | 所有 log 都有保存路徑                                 |

---

## W12：2026/9/14（一）–2026/9/18（五）

### 週里程碑

完成第二次測試、debug decision tree、Pegatron vs Metanoia E2E 比較。

### 每日工作

| 日期      | 工作                                     |
| ------- | -------------------------------------- |
| 9/14（一） | 修正 W11 blocking issue                  |
| 9/15（二） | 執行第二次 E2E 測試                           |
| 9/16（三） | 整理 second run log                      |
| 9/17（四） | 完成 Pegatron vs Metanoia E2E comparison |
| 9/18（五） | 週檢查點：確認 final verification 狀態          |

### 本週產出與百分比

| 產出                                         |  百分比 |
| ------------------------------------------ | ---: |
| `metanoia-e2e-second-run-log.md`           | 100% |
| `metanoia-e2e-error-report.md`             | 100% |
| `debug-decision-tree.md`                   | 100% |
| `oai-aerial-metanoia-config-pack/`         |  95% |
| `pegatron-vs-metanoia-e2e-result-table.md` |  90% |
| `metanoia-e2e-troubleshooting.md`          |  90% |
| `updated-runbook.md`                       |  90% |
| `week12-meeting-notes.md`                  | 100% |

### 9/18 通過標準

| 檢查項目            | 通過標準                                |
| --------------- | ----------------------------------- |
| Second run      | 有完整 second run log                  |
| 狀態判定            | 明確標示成功 / 部分成功 / 未成功但可解釋             |
| Comparison      | Pegatron vs Metanoia E2E 至少比較 8 個項目 |
| Troubleshooting | 常見錯誤有對應排查步驟                         |
| Final plan      | 下週只剩補測、整理、交接，不再大改方向                 |

---

## W13：2026/9/21（一）–2026/9/25（五）

### 週里程碑

完成最終報告、handover guide、config pack、experiment logs、meeting notes index。

### 每日工作

| 日期      | 工作                                                 |
| ------- | -------------------------------------------------- |
| 9/21（一） | 最後補測或補 log                                         |
| 9/22（二） | 完成 final comparison tables                         |
| 9/23（三） | 完成 final report draft                              |
| 9/24（四） | 補齊 meeting notes、action item status、handover guide |
| 9/25（五） | 週檢查點：完成 final deliverables                         |

### 本週產出與百分比

| 產出                                          |  百分比 |
| ------------------------------------------- | ---: |
| `metanoia-e2e-final-verification-report.md` | 100% |
| `final-3-month-report.md`                   |  95% |
| `final-handover-guide.md`                   |  95% |
| `final-config-pack/`                        | 100% |
| `final-experiment-logs/`                    | 100% |
| `final-comparison-tables.md`                | 100% |
| `final-action-item-status.md`               | 100% |
| `all-meeting-notes-index.md`                | 100% |
| `updated-runbook.md`                        | 100% |
| `metanoia-e2e-troubleshooting.md`           | 100% |

### 9/25 通過標準

| 檢查項目           | 通過標準                                       |
| -------------- | ------------------------------------------ |
| Final report   | 三個月成果、限制、問題、下一步都寫清楚                        |
| Handover guide | 下一位接手者能照文件找到 config、run command、logs       |
| Config pack    | OAI / Ariel / Pegatron / Metanoia 都整理好     |
| Logs           | 所有實驗 log 都集中保存                             |
| Meeting notes  | 所有 meeting notes 有 index                   |
| Action items   | 所有 action item 都有 Done / Pending / Blocked |

---

## Final：2026/9/26（六）

### 最終檢查點，不安排新工作

| 檢查項目                          | 通過標準 |
| ----------------------------- | ---- |
| `final-3-month-report.md`     | 100% |
| `final-handover-guide.md`     | 100% |
| `final-config-pack/`          | 100% |
| `final-experiment-logs/`      | 100% |
| `final-comparison-tables.md`  | 100% |
| `final-action-item-status.md` | 100% |
| `all-meeting-notes-index.md`  | 100% |
| 每週檢查點紀錄                      | 100% |
| 7/31、8/28 月檢查紀錄               | 100% |

