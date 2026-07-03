# Aerial cuBB Parameter Table

## Purpose

說明本文件要交付的可驗證成果，並讓後續接手者可以依照 Source、Evidence、Status 與 Next Step 追蹤進度。

## Plan Alignment

| Related Week | Planned Completion | Due Date | Planned Deliverable |
|---|---:|---|---|
| W1 | 60% | 7/3 | `aerial-cubb-parameter-table.md` |
| W3 | 70% | 7/14 | `aerial-cubb-parameter-table.md` |
| W3 | 70% | 7/17 | `aerial-cubb-parameter-table.md` |
| W5 | 100% | 7/31 | `aerial-cubb-parameter-table.md` |

## Parameter Table (compare to [pegatron RU gNB config](https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/doc/gnb.sa.band78.273prb.fhi72.4x4-pega-1G.conf))

因為大部分的參數都與[pegatron RU 的config檔](https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/oai_aerial_ru_research_github_ready/oai_aerial_ru_research_github_ready/07-oai-aerial-pegatron/baseline-and-config/oai-gnb-parameter-table.md)一樣所以只拉出布一樣的部分

| 類別               |                                   參數 |   Pegatron  |          Aerial  | note                                                                                                    |
| ---------------- | -----------------------------------: | -------------: | ------------------: | ---------------------------------------------------------------------------------------------------------------- |
| Cell identity    |                          `nr_cellid` |            `1` |         `12345678L` | NR Cell ID 不同，UE 看到的是不同 cell identity。通常不影響 RF 頻率，但會影響 cell 識別、核心網/UE 註冊觀察。                                      |
| UL antenna       |                 `pusch_AntennaPorts` |            `4` |                 `2` | 跟 RU 天線數、L1 支援層數、UL MIMO 能力有關。                                   |
| SRS              |                             `do_SRS` |            `0` |        `"periodic"` | pegatron關閉 SRS； Aerial啟用 periodic SRS。 |
| CORESET0         | `initialDLBWPcontrolResourceSetZero` |           `10` |                `12` | 影響初始 PDCCH / SIB1 搜尋位置。UE 要能解 SIB1，這個設定不能亂改，要跟 SSB、PointA、bandwidth 搭配。                                          |
| UE power         |                               `pMax` |           `23` |                `20` | 廣播給 UE 的最大發射功率限制                                      |
| PRACH            |          `zeroCorrelationZoneConfig` |           `15` |                `12` | X                                |
| PRACH power      |        `preambleReceivedTargetPower` |         `-104` |               `-96` | UE 發 PRACH 時的目標接收功率。。                                                                |
| PRACH retry      |                   `preambleTransMax` |            `7` |                 `6` | PRACH 最大重傳次數 index 不同。pegatron允許較多次 RA preamble 嘗試。                                                                   |
| PRACH ramping    |                   `powerRampingStep` |            `2` |                 `1` | PRACH 每次重傳功率增加幅度不同。                                                                  |
| Msg3 power       |                 `msg3_DeltaPreamble` |            `2` |                 `1` | PRACH preamble 到 Msg3 PUSCH 的功率 offset。會影響隨機接入後 Msg3 的發射功率。                                                      |
| UL power control |                `p0_NominalWithGrant` |          `-96` |               `-90` |                                                      |
| PUCCH hopping    |                          `hoppingId` |            `0` |                `40` |                                                      |
| PUCCH power      |                         `p0_nominal` |          `-96` |               `-90` |                                                               |
| TDD period       |      `dl_UL_TransmissionPeriodicity` |            `5` |                 `6` | `5 = ms2p5`，`6 = ms5`pegatron是 2.5 ms TDD pattern， Aerial是 5 ms TDD pattern。                                   |
| TDD DL slots     |                  `nrofDownlinkSlots` |            `3` |                 `6` | pegatron是 3 個完整 DL slot； Aerial是 6 個完整 DL slot。                                                                           |
| TDD DL symbols   |                `nrofDownlinkSymbols` |            `6` |                `10` | pegatron mixed slot 有 6 個 DL symbol； Aerial有 10 個 DL symbol。                                 |
| TDD UL slots     |                    `nrofUplinkSlots` |            `1` |                 `3` | pegatron 1 個完整 UL slot； Aerial 3 個完整 UL slot。                                                                             |
| TDD UL symbols   |                  `nrofUplinkSymbols` |            `4` |                 `0` | pegatron mixed slot 有 4 個 UL symbols； Aerial mixed slot 沒有 UL symbols。                                                    |
| SSB power        |                  `ssPBCH_BlockPower` |            `0` |               `-34` | SSB/PBCH block power 設定不同。值要跟實際 RU 發射功率、gain、校準一致。                                |
| L2-L1 transport  |            `MACRLCs.tr_s_preference` |   `"local_L1"` |          `"aerial"` | pegatron MAC/RLC 直接接 OAI local L1； Aerial MAC/RLC 走 Aerial transport 接外部 cuBB L1。                               |
| Scheduler        |                 `pusch_TargetSNRx10` |          `200` |               `280` | pegatron 20 dB， Aerial 28 dB。 Aerial對 PUSCH 目標 SNR 要求更高，會影響 UL MCS / link adaptation。                                   |
| Scheduler        |                 `pucch_TargetSNRx10` |          `200` |               `100` | pegatron 20 dB， Aerial 10 dB。PUCCH 目標 SNR 不同，會影響控制訊號接收門檻。                                                                 |

