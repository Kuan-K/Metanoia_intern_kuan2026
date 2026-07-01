# Pegatron RU Parameter Table

## Purpose

說明本文件要交付的可驗證成果，並讓後續接手者可以依照 Source、Evidence、Status 與 Next Step 追蹤進度。

## Plan Alignment

| Related Week | Planned Completion | Due Date | Planned Deliverable |
|---|---:|---|---|
| W1 | 50% | 7/1 | `pegatron-ru-parameter-table.md` |
| W2 | 60% | 7/10 | `pegatron-ru-parameter-table.md` |
| W5 | 90% | 7/31 | `pegatron-ru-parameter-table.md` |

## Open Research Playbook Checklist

| Requirement | Check |
|---|---|
| Deliverable is measurable and verifiable | ☐ |
| Evidence path / hyperlink is recorded | ☐ |
| Unknown items are marked as Need Confirm | ☐ |
| Pending / Blocked reason is recorded | ☐ |
| Next step is clear | ☐ |

## Scope

- System / Component: Pegatron RU
- Config file path:
- Source owner:
- Related setup:
- Related RU model / band:

## Parameter Table

| 類別 | conf 中名稱 | 目前值 | 參數可能範圍 | 備註 |
|---|---|---|---|---|
| Radio / Carrier | center-of-channel-bandwidth | 3750000000 |  | RU 實際使用的載波中心頻率 |
| Radio / Carrier | channel-bandwidth | 100000000 |  | RU 使用的通道頻寬 |
| Radio / Carrier | scs | KHZ_30 |  | SCS = 30kHz |
| Radio / Carrier | number-of-prb | 273 |  | 可使用的 PRB 數量 |
| Radio / Carrier | cp-type | NORMAL |  |cp-type = NORMAL； Cyclic Prefix:在Symbol前面加上的一小段保護時間，用來降低多路徑造成的干擾；需與 gNB numerology / CP type 設定一致。 |
| Radio / Carrier | cp-length | 88 |  | symbol 前面保護區間的長度 |
| Radio / Carrier | cp-length-other | 72 |  | cp-length = 主要或特定 symbol 的 CP 長度<br>cp-length-other = 其他 symbol 的 CP 長度 |
| Radio / Carrier | offset-to-absolute-frequency-center | -3276 |  | 頻率 offset，需與 gNB 的 PointA / ARFCN / center frequency 對齊 |
| Radio / Carrier | frame-structure | 193 |  | 這個 endpoint 使用哪一種 frame / slot / symbol 結構 |

## 設定 RU 的 TX Carrier / RX Carrier
TX Carrier 是 RU 往 UE 發射訊號用的 carrier
RX Carrier 是 RU 從 UE 接收訊號用的 carrier
載波頻率與頻寬都與上表的值相同並且啟用
| 類別 | conf 中名稱 | 目前值 | 參數可能範圍 | 備註 |
|---|---|---|---|---|
| TX Carrier | tx-carr0 center-of-channel-bandwidth | 3750000000 |  |  |
| TX Carrier | tx-carr0 channel-bandwidth | 100000000 |  |  |
| TX Carrier | tx-carr0 gain | 14.0 |  | 增益 |
| TX Carrier | tx-carr0 active | ACTIVE |  |  |
| TX Carrier | tx-carr1 center-of-channel-bandwidth | 3750000000 |  |  |
| TX Carrier | tx-carr1 channel-bandwidth | 100000000 |  |  |
| TX Carrier | tx-carr1 gain | 14.0 |  |  |
| TX Carrier | tx-carr1 active | ACTIVE |  |  |
| RX Carrier | rx-carr0 center-of-channel-bandwidth | 3750000000 |  |  |
| RX Carrier | rx-carr0 channel-bandwidth | 100000000 |  |  |
| RX Carrier | rx-carr0 gain-correction | 0.0 |  |  |
| RX Carrier | rx-carr0 active | ACTIVE |  |  |
| RX Carrier | rx-carr1 center-of-channel-bandwidth | 3750000000 |  |  |
| RX Carrier | rx-carr1 channel-bandwidth | 100000000 |  |  |
| RX Carrier | rx-carr1 gain-correction | 0.0 |  |  |
| RX Carrier | rx-carr1 active | ACTIVE |  |  |
| TX Endpoint | tx-ep0 eaxc-id | 0 |  | Downlink 的 4 條資料流 |
| TX Endpoint | tx-ep1 eaxc-id | 1 |  |  |
| TX Endpoint | tx-ep2 eaxc-id | 2 |  |  |
| TX Endpoint | tx-ep3 eaxc-id | 3 |  |  |
| RX Endpoint | rx-ep0 eaxc-id | 0 |  | Uplink 的 4 條資料流 |
| RX Endpoint | rx-ep1 eaxc-id | 1 |  |  |
| RX Endpoint | rx-ep2 eaxc-id | 2 |  |  |
| RX Endpoint | rx-ep3 eaxc-id | 3 |  |  |
| PRACH Endpoint | prach-ep0 eaxc-id | 4 |  | Random Access 專用資料，一般 UL data 使用 rx-ep0 ~ rx-ep3，但是 UE 隨機接入用的 PRACH 另外使用 prach-ep0 ~ prach-ep3，eAxC ID 是 4～7 |
| PRACH Endpoint | prach-ep1 eaxc-id | 5 |  |  |
| PRACH Endpoint | prach-ep2 eaxc-id | 6 |  |  |
| PRACH Endpoint | prach-ep3 eaxc-id | 7 |  |  |
| eAxC bitmask | o-du-port-bitmask | 49152 |  | eAxC bitmask是決定 eAxC ID 怎麼被拆解，待確定 |
| eAxC bitmask | band-sector-bitmask | 16128 |  |  |
| eAxC bitmask | ccid-bitmask | 240 |  |  |
| eAxC bitmask | ru-port-bitmask | 15 |  |  |
| Compression | iq-bitwidth | 9 |  | IQ sample 使用 9-bit 壓縮 |
| Compression | compression-type | STATIC |  | 使用固定壓縮設定 |
| Compression | compression-method | BLOCK_FLOATING_POINT |  | 使用 BFP 壓縮方式 |
| Compression | fs-offset | TX = 0, RX/PRACH = 8 |  |  |

## Timing 類：時間 / 同步設定
| 類別 | conf 中名稱 | 目前值 | 參數可能範圍 | 備註 |
|---|---|---|---|---|
| UL Timing | ul-fft-sampling-offset | 21 |  | 上行 FFT 取樣位置 offset，RU 要從哪個時間點開始取樣做 FFT |
| Timing | downlink-radio-frame-offset | 2394880 |  | RU 要知道「什麼時間點開始算一個 radio frame」。
downlink-radio-frame-offset 就是在設定 DL radio frame 相對於參考時間的偏移量  |
| Timing | downlink-sfn-offset | 360 |  | 待確認 |
| Timing | n-ta-offset | 25600 |  | Timing Advance offset |
| Endpoint option | non-time-managed-delay-enabled | false |  | 沒有啟用 non-time-managed delay |

## Network Interface / Transport Flow：網路怎麼連
| 類別 | conf 中名稱 | 目前值 | 參數可能範圍 | 備註 |
|---|---|---|---|---|
| Network Interface | fm1-mac9 mac-address | 48:21:0b:4b:93:8e |  | RU 這邊的 mac-address 需對照gNB config |
| Network Interface | cuplane mac-address | 48:21:0b:4b:93:8e |  | RU 的 C-plane / U-plane Ethernet flow 使用這個 MAC address |
| Network Interface | cuplane vlan-id | 103 |  | C/U-plane 封包要走 VLAN 103 |
| Processing Element | ru-elements name | pse3 |  |  |
| Transport Flow | interface-name | cuplane |  |  |
| Transport Flow | ru-mac-address | 48:21:0b:4b:93:8e |  |  |
| Transport Flow | vlan-id | 103 |  |  |
| Transport Flow | o-du-mac-address | 00:11:22:33:44:66 |  |  |

##  TX Link Mapping、RX Link Mapping
將線路設定好，把 TX carrier 接到 TX endpoint，RX carrier 接到 RX endpoint
| 類別 | conf 中名稱 | 目前值 | 參數可能範圍 | 備註 |
|---|---|---|---|---|
| TX Link Mapping | tx-link0 | pse3 / tx-carr0 / tx-ep0 |  |  |
| TX Link Mapping | tx-link1 | pse3 / tx-carr0 / tx-ep1 |  |  |
| TX Link Mapping | tx-link2 | pse3 / tx-carr1 / tx-ep2 |  |  |
| TX Link Mapping | tx-link3 | pse3 / tx-carr1 / tx-ep3 |  |  |
| RX Link Mapping | rx-link0 | pse3 / rx-carr0 / rx-ep0 |  |  |
| RX Link Mapping | rx-link1 | pse3 / rx-carr0 / rx-ep1 |  |  |
| RX Link Mapping | rx-link2 | pse3 / rx-carr1 / rx-ep2 |  |  |
| RX Link Mapping | rx-link3 | pse3 / rx-carr1 / rx-ep3 |  |  |
| PRACH Link Mapping | rx-link4 | pse3 / rx-carr0 / prach-ep0 |  |  |
| PRACH Link Mapping | rx-link5 | pse3 / rx-carr0 / prach-ep1 |  |  |
| PRACH Link Mapping | rx-link6 | pse3 / rx-carr1 / prach-ep2 |  |  |
| PRACH Link Mapping | rx-link7 | pse3 / rx-carr1 / prach-ep3 |  |  |

## Parameters Related to RU / cuBB Alignment

| Parameter | gNB Side | RU / cuBB Side | Must Match? | Current Status | Evidence |
|---|---|---|---|---|---|
| frequency |  |  | ☐ Yes ☐ No ☐ Need Confirm |  |  |
| bandwidth |  |  | ☐ Yes ☐ No ☐ Need Confirm |  |  |
| numerology / SCS |  |  | ☐ Yes ☐ No ☐ Need Confirm |  |  |
| TDD pattern |  |  | ☐ Yes ☐ No ☐ Need Confirm |  |  |
| IP / port |  |  | ☐ Yes ☐ No ☐ Need Confirm |  |  |
| clock / sync |  |  | ☐ Yes ☐ No ☐ Need Confirm |  |  |
| antenna / gain |  |  | ☐ Yes ☐ No ☐ Need Confirm |  |  |
| fronthaul / eCPRI |  |  | ☐ Yes ☐ No ☐ Need Confirm |  |  |

## Evidence

| Evidence Type | Path / Link | Note |
|---|---|---|
| Source config / source file |  |  |
| Command / script |  |  |
| Log / screenshot / output |  |  |
| Related plan / checkpoint |  |  |

## Need Confirm / Open Questions

| Question | Owner / Ask Who | Due Date | Status | Evidence / Answer |
|---|---|---|---|---|
|  |  |  | ☐ Need Confirm ☐ Confirmed |  |

## Status

| Item | Status | Evidence / Note |
|---|---|---|
| Current status | ☐ Done ☐ Pending ☐ Blocked |  |
| If Pending / Blocked | Reason |  |
| Next step | Action |  |
