# OAI gNB Parameter Table

## Purpose

說明本文件要交付的可驗證成果，並讓後續接手者可以依照 Source、Evidence、Status 與 Next Step 追蹤進度。

## Plan Alignment

| Related Week | Planned Completion | Due Date | Planned Deliverable |
|---|---:|---|---|
| W1 | 50% | 7/1 | `oai-gnb-parameter-table.md` |
| W2 | 60% | 7/7 | `oai-gnb-parameter-table.md` |
| W5 | 100% | 7/31 | `oai-gnb-parameter-table.md` |

## Open Research Playbook Checklist

| Requirement | Check |
|---|---|
| Deliverable is measurable and verifiable | ☐ |
| Evidence path / hyperlink is recorded | ☐ |
| Unknown items are marked as Need Confirm | ☐ |
| Pending / Blocked reason is recorded | ☐ |
| Next step is clear | ☐ |

## Scope

- System / Component: OAI gNB
- Config file path:
- Source owner:
- Related setup:
- Related RU model / band:

## Parameter Table

| 類別 | 參數名稱 | conf 中名稱 | 目前值 | 可能範圍 | 備註 |
|---|---|---|---|---|---|
| gNB 基本設定 | 啟用的 gNB 清單 | `Active_gNBs` | `"gNB-OAI"` | 字串清單，需對應 `gNB_name` |  |
| gNB 基本設定 | ASN.1 輸出詳細程度 | `Asn1_verbosity` | `"none"` | `none`, `info`, `annoying` | conf 註解 |
| gNB 基本設定 | gNB 識別碼 | `gNB_ID` | `0xe00` | 非負整數或 16 進位值；需符合 gNB ID 規劃 |  |
| gNB 基本設定 | gNB 名稱 | `gNB_name` | `"gNB-OAI"` | 字串 |  |
| gNB 基本設定 | Tracking Area Code | `tracking_area_code` | `1` | `0x0001`–`0xfffd`；conf 註解保留 `0x0000`, `0xfffe` | conf 註解 |
| gNB 基本設定 | NR Cell ID | `nr_cellid` | `1` | 非負整數；通常為 36-bit NR Cell Identity 範圍內 |  |
| PLMN / Slice | MCC / MNC / MNC 長度 | `mcc`, `mnc`, `mnc_length` | `001`, `01`, `2` | `mcc`: 3 位數；`mnc`: 2 或 3 位數；`mnc_length`: `2` 或 `3` | 需與 5GC / SIM 設定一致 |
| PLMN / Slice | Slice / Service Type | `sst` | `1` | 常見 `1`–`4`；3GPP SST 為 8-bit 欄位，實際支援依 OAI/核心網版本 | OAI issue 中曾顯示部分版本 authorized values 為 `1 2 3 4` |
| Antenna / MIMO | PDSCH antenna port 設定 | `pdsch_AntennaPorts_XP`, `pdsch_AntennaPorts_N1` | `2`, `2` | 正整數；乘積通常需對應 PDSCH port / MIMO 配置 | 本案 2×2 = 4 |
| Antenna / MIMO | 最大 MIMO layers | `maxMIMO_layers` | `4` | `1`–RU/UE 支援最大 layer；4T4R 常見為 `1`–`4` | 需與 RU/UE 能力一致 |
| Antenna / MIMO | PUSCH antenna ports | `pusch_AntennaPorts` | `4` | 正整數；常見 `1`, `2`, `4` | 需與 UL/MIMO/RU RX 能力一致 |
| Antenna / MIMO | CSI-RS 開關 | `do_CSIRS` | `1` | `0` 或 `1` | 0=關閉，1=啟用 |
| Antenna / MIMO | SRS 開關 | `do_SRS` | `0` | `0` 或 `1` | 0=關閉，1=啟用 |
| SIB / Cell Common | SIB1 TDA | `sib1_tda` | `15` | 整數；常見 `0`–`15` | 需依 OAI/NR TDA 設定確認 |
| RF / 頻率設定 | Physical Cell ID | `physCellId` | `0` | `0`–`1007` | NR PCI 範圍 |
| RF / 頻率設定 | SSB 絕對頻率 | `absoluteFrequencySSB` | `649920` | NR-ARFCN 整數；需落在對應 band 支援範圍 | 本檔註解寫 selected SSB frequency = 3349.92 MHz，但疑似舊註解 |
| RF / 頻率設定 | DL / UL 頻段 | `dl_frequencyBand`, `ul_frequencyBand` | `78`, `78` | 3GPP NR band 編號；需為 RU/UE/頻譜支援 band | 本案為 n78 |
| RF / 頻率設定 | DL Point A 絕對頻率 | `dl_absoluteFrequencyPointA` | `646724` | NR-ARFCN 整數；需配合 Band/SCS/PRB | conf 註解寫 frequency point A = 3700.86 MHz |
| RF / 頻率設定 | DL / UL carrier offset | `dl_offstToCarrier`, `ul_offstToCarrier` | `0`, `0` | 非負整數；依 carrier / BWP 配置 |  |
| RF / 頻率設定 | DL / UL subcarrier spacing | `dl_subcarrierSpacing`, `ul_subcarrierSpacing` | `1`, `1` | `0`=15 kHz, `1`=30 kHz, `2`=60 kHz, `3`=120 kHz | conf 註解 |
| RF / 頻率設定 | DL / UL carrier bandwidth / PRB | `dl_carrierBandwidth`, `ul_carrierBandwidth` | `273`, `273` | 依 3GPP NR channel bandwidth、SCS、band 決定；100 MHz @ 30 kHz 常見最大為 `273` PRB | 需與 RU `number-of-prb` 對應 |
| RF / 頻率設定 | UE 最大上行功率 | `pMax` | `23` | 常見 `-30`–`33` dBm | 依 UE capability / 法規 / RRC 設定 |
| BWP / PDCCH | Initial DL / UL BWP 位置與頻寬 | `initialDLBWPlocationAndBandwidth`, `initialULBWPlocationAndBandwidth` | `1099`, `1099` | RIV 編碼值；範圍依 carrier PRB 數決定 | conf 註解引用 38.101-1 Table 5.3.2-1 |
| BWP / PDCCH | Initial DL / UL BWP SCS | `initialDLBWPsubcarrierSpacing`, `initialULBWPsubcarrierSpacing` | `1`, `1` | `0`=15 kHz, `1`=30 kHz, `2`=60 kHz, `3`=120 kHz | conf 註解 |
| BWP / PDCCH | Initial DL BWP CORESET#0 | `initialDLBWPcontrolResourceSetZero` | `10` | 常見 `0`–`15` | 依 MIB / CORESET#0 table |
| BWP / PDCCH | Initial DL BWP SearchSpace#0 | `initialDLBWPsearchSpaceZero` | `0` | 常見 `0`–`15` | 依 SearchSpace#0 table |
| PRACH / RACH | PRACH configuration index | `prach_ConfigurationIndex` | `159` | 常見 `0`–`255`；實際依 FR1/FR2、FDD/TDD、SCS table |  |
| PRACH / RACH | PRACH Msg1 FDM | `prach_msg1_FDM` | `0` | `0`=one, `1`=two, `2`=four, `3`=eight | conf 註解 |
| PRACH / RACH | PRACH Msg1 frequency start | `prach_msg1_FrequencyStart` | `0` | 非負整數；不可超出 UL BWP / PRB 範圍 |  |
| PRACH / RACH | Zero correlation zone config | `zeroCorrelationZoneConfig` | `15` | 常見 `0`–`15` |  |
| PRACH / RACH | Preamble 接收目標功率 | `preambleReceivedTargetPower` | `-104` | 常見 `-202`–`-60` dBm，通常 2 dB step |  |
| PRACH / RACH | Preamble 最大重傳次數 | `preambleTransMax` | `7` | index `0`–`10` 對應 `3,4,5,6,7,8,10,20,50,100,200` | conf 註解 |
| PRACH / RACH | Power ramping step | `powerRampingStep` | `2` | `0`=dB0, `1`=dB2, `2`=dB4, `3`=dB6 | conf 註解 |
| PRACH / RACH | RA response window | `ra_ResponseWindow` | `5` | 常見 index `0`–`7` 對應 `1,2,4,8,10,20,40,80` slots | conf 註解列出可選 window |
| PRACH / RACH | SSB per RACH occasion 設定 | `ssb_perRACH_OccasionAndCB_PreamblesPerSSB_PR`, `ssb_perRACH_OccasionAndCB_PreamblesPerSSB` | `4`, `15` | PR: `1`=oneeighth, `2`=onefourth, `3`=half, `4`=one, `5`=two, `6`=four, `7`=eight, `8`=sixteen；Preambles: `0`–`15` 對應 `4,8,12,...,64` | conf 註解 |
| PRACH / RACH | RA contention resolution timer | `ra_ContentionResolutionTimer` | `7` | index `0`–`7` 對應 `8,16,24,32,40,48,56,64` | conf 註解 |
| PRACH / RACH | RSRP threshold SSB | `rsrp_ThresholdSSB` | `19` | 常見 `0`–`127` | RSRP threshold index |
| PRACH / RACH | PRACH root sequence index 設定 | `prach_RootSequenceIndex_PR`, `prach_RootSequenceIndex` | `2`, `1` | PR: `1`=839, `2`=139；index 範圍依 root sequence length，839 約 `0`–`837`，139 約 `0`–`137` | conf 註解 |
| PRACH / RACH | Msg1 subcarrier spacing | `msg1_SubcarrierSpacing` | `1` | `0`=15 kHz, `1`=30 kHz, `2`=60 kHz, `3`=120 kHz | conf 註解說此值會優先於 PRACH config index 推導值 |
| PRACH / RACH | Restricted set config | `restrictedSetConfig` | `0` | `0`=unrestricted, `1`=restricted type A, `2`=restricted type B | conf 註解 |
| PRACH / RACH | Msg3 delta preamble | `msg3_DeltaPreamble` | `2` | 常見非負整數；實際 dB offset = `2 × field value` | conf 註解說明換算方式 |
| PRACH / RACH | P0 nominal with grant | `p0_NominalWithGrant` | `-96` | 常見 `-202`–`24` dBm |  |
| PUCCH | PUCCH group hopping | `pucchGroupHopping` | `0` | `0`=neither, `1`=group hopping, `2`=sequence hopping | conf 註解 |
| PUCCH | Hopping ID | `hoppingId` | `0` | 常見 `0`–`1023` |  |
| PUCCH | PUCCH P0 nominal | `p0_nominal` | `-96` | 常見 `-202`–`24` dBm |  |
| SSB / PBCH | SSB positions in burst bitmap | `ssb_PositionsInBurst_Bitmap` | `0x1` | bitmask；長度依 FR1/FR2 與 SSB beams 數決定 |  |
| SSB / PBCH | SSB periodicity serving cell | `ssb_periodicityServingCell` | `2` | `0`=ms5, `1`=ms10, `2`=ms20, `3`=ms40, `4`=ms80, `5`=ms160, `6`=spare2, `7`=spare1 | conf 註解 |
| SSB / PBCH | SS/PBCH block power | `ssPBCH_BlockPower` | `0` | 常見 `-60`–`50` dBm |  |
| DMRS | DMRS Type A position | `dmrs_TypeA_Position` | `0` | `0`=pos2, `1`=pos3 | conf 註解 |
| Numerology | Cell common subcarrier spacing | `subcarrierSpacing` | `1` | `0`=15 kHz, `1`=30 kHz, `2`=60 kHz, `3`=120 kHz | conf 註解 |
| TDD Pattern | TDD reference subcarrier spacing | `referenceSubcarrierSpacing` | `1` | `0`=15 kHz, `1`=30 kHz, `2`=60 kHz, `3`=120 kHz | conf 註解 |
| TDD Pattern | DL / UL transmission periodicity | `dl_UL_TransmissionPeriodicity` | `5` | `0`=ms0p5, `1`=ms0p625, `2`=ms1, `3`=ms1p25, `4`=ms2, `5`=ms2p5, `6`=ms5, `7`=ms10 | conf 註解 |
| TDD Pattern | Downlink slots / symbols 數量 | `nrofDownlinkSlots`, `nrofDownlinkSymbols` | `3`, `6` | slots: `0`–週期內總 slot 數；symbols: `0`–`13` | 需符合 TDD period 與 numerology |
| TDD Pattern | Uplink slots / symbols 數量 | `nrofUplinkSlots`, `nrofUplinkSymbols` | `1`, `4` | slots: `0`–週期內總 slot 數；symbols: `0`–`13` | 需符合 TDD period 與 numerology |
| SCTP / 5GC | SCTP input / output streams | `SCTP_INSTREAMS`, `SCTP_OUTSTREAMS` | `2`, `2` | 正整數；常見 `1`–`65535` |  |
| SCTP / 5GC | AMF IP 設定 | `amf_ip_address`, `ipv4` | `"192.168.8.82"` | IPv4 address | 需對應 5GC AMF IP |
| Network Interface | gNB N2 / NG-AMF IPv4 address | `GNB_IPV4_ADDRESS_FOR_NG_AMF` | `"192.168.8.83"` | IPv4 address | gNB 對 AMF 的 N2/NGAP IP |
| Network Interface | gNB N3 / NG-U IPv4 address | `GNB_IPV4_ADDRESS_FOR_NGU` | `"192.168.8.83"` | IPv4 address | gNB 對 UPF 的 N3/GTP-U IP |
| Network Interface | GTP-U / S1-U port | `GNB_PORT_FOR_S1U` | `2152` | `0`–`65535`；標準 GTP-U port 為 `2152` | conf 註解 |
| MAC/RLC | MAC/RLC component carrier 數 | `num_cc` | `1` | 正整數；依 carrier 數量 | 在 `MACRLCs` 區塊 |
| MAC/RLC | MAC/RLC transport preference | `tr_s_preference`, `tr_n_preference` | `"local_L1"`, `"local_RRC"` | OAI transport 字串；常見 `local_L1`, `local_RRC` 等 | 依 OAI 架構 |
| MAC/RLC | PUSCH / PUCCH target SNR x10 | `pusch_TargetSNRx10`, `pucch_TargetSNRx10` | `200`, `200` | 整數；單位通常為 SNR ×10 | `200` 約代表 20.0 dB |
| MAC/RLC | DL BLER target upper / lower | `dl_bler_target_upper`, `dl_bler_target_lower` | `.35`, `.15` | `0.0`–`1.0` |  |
| MAC/RLC | UL BLER target upper / lower | `ul_bler_target_upper`, `ul_bler_target_lower` | `.35`, `.15` | `0.0`–`1.0` |  |
| MAC/RLC | PUSCH failure threshold | `pusch_FailureThres` | `100` | 非負整數 | OAI scheduler/PHY 判斷門檻 |
| MAC/RLC | DL minimum MCS | `dl_min_mcs` | `24` | 常見 `0`–`28`；部分 MCS table 可到 `31` | 依 NR MCS table / OAI 設定 |
| Security | Ciphering algorithms | `ciphering_algorithms` | `"nea0"` | `nea0`, `nea1`, `nea2`, `nea3` | conf 註解 |
| Security | Integrity algorithms | `integrity_algorithms` | `"nia2"`, `"nia0"` | `nia0`, `nia1`, `nia2`, `nia3` | conf 註解 |
| Security | DRB ciphering / integrity 開關 | `drb_ciphering`, `drb_integrity` | `"yes"`, `"no"` | `"yes"` 或 `"no"` | conf 註解 |
| L1 | L1 component carrier 數 | `num_cc` | `1` | 正整數；依 carrier 數量 | 在 `L1s` 區塊 |
| L1 | L1 northbound transport preference | `tr_n_preference` | `"local_mac"` | OAI transport 字串；常見 `"local_mac"` |  |
| L1 | PRACH / PUCCH0 / PUSCH DTX threshold | `prach_dtx_threshold`, `pucch0_dtx_threshold`, `pusch_dtx_threshold` | `130`, `80`, `10` | 整數；OAI PHY 偵測門檻，實際範圍依 implementation |  |
| L1 | TX amplitude backoff | `tx_amp_backoff_dB` | `20` | 非負數，單位 dB；需與 O-RU 設定一致 | conf 註解 |
| L1 | L1 RX / TX thread core | `L1_rx_thread_core`, `L1_tx_thread_core` | `18`, `19` | CPU core ID，非負整數；需小於系統 CPU core 數 |  |
| L1 | Phase compensation | `phase_compensation` | `0` | 常見 `0` 或 `1`；需與 O-RU 設定一致 | conf 註解 |
| RU | Local RF 開關 | `local_rf` | `"no"` | `"yes"` 或 `"no"` | `"no"` 代表使用外部 RU / fronthaul |
| RU | RU TX / RX 數量 | `nb_tx`, `nb_rx` | `4`, `4` | 正整數；需與 RU antenna / endpoint 數一致 | 本案 4T4R |
| RU | TX / RX attenuation | `att_tx`, `att_rx` | `0`, `0` | 非負數，單位通常 dB |  |
| RU | RU bands | `bands` | `[78]` | NR band 編號 list；需為 RU 支援 band | 本案 n78 |
| RU | Max PDSCH reference signal power | `max_pdschReferenceSignalPower` | `-27` | 常見 dBm 範圍；需依 RU 發射能力與法規 |  |
| RU | Max RX gain | `max_rxgain` | `75` | 非負數，單位通常 dB；依 RF/RU 硬體 |  |
| RU | Subframe extension | `sf_extension` | `0` | 非負整數；OAI/RU timing 相關 |  |
| RU | eNB / gNB instance mapping | `eNB_instances` | `[0]` | instance index list；通常從 `0` 開始 |  |
| RU | RU thread core | `ru_thread_core` | `12` | CPU core ID，非負整數；需小於系統 CPU core 數 |  |
| RU | Slot ahead | `sl_ahead` | `5` | 正整數；OAI scheduler / fronthaul look-ahead |  |
| RU | RU transport preference | `tr_preference` | `"raw_if4p5"` | OAI transport 字串；本案使用 `"raw_if4p5"` 啟用 FHI 7.2 | conf 註解 |
| RU | Precoding 開關 | `do_precoding` | `0` | `0` 或 `1`；需與 O-RU 設定一致 | conf 註解 |
| Logging | 各層 log level | `global_log_level`, `hw_log_level`, `phy_log_level`, `mac_log_level`, `rlc_log_level`, `pdcp_log_level`, `rrc_log_level`, `ngap_log_level`, `f1ap_log_level` | 全部 `"info"` | 常見 `error`, `warn`, `info`, `debug`, `trace`；實際依 OAI log 系統 |  |
| FHI 7.2 / Fronthaul | DPDK devices | `dpdk_devices` | `"0000:43:0a.0"`, `"0000:43:0a.1"` | PCI BDF 格式裝置清單，例如 `dddd:bb:ss.f` | 需對應 gNB server NIC/VF |
| FHI 7.2 / Fronthaul | FHI CPU core 設定 | `system_core`, `io_core`, `worker_cores` | `0`, `4`, `(2)` | CPU core ID，非負整數；需小於系統 CPU core 數且避免互相衝突 |  |
| FHI 7.2 / Fronthaul | RU fronthaul MAC address | `ru_addr` | `"48:21:0b:4b:93:8e"`, `"48:21:0b:4b:93:8e"` | MAC address list，格式 `xx:xx:xx:xx:xx:xx` | 需對應 RU C/U-plane MAC |
| FHI 7.2 / Fronthaul | Fronthaul MTU | `mtu` | `9000` | 常見 `1500` 或 jumbo frame `9000`/`9216`；需 NIC、switch、RU 都支援 | conf 註解說 `1500` 也可用 |
| FHI 7.2 / Fronthaul | T1a / Ta4 timing window | `T1a_cp_dl`, `T1a_cp_ul`, `T1a_up`, `Ta4` | `(285,429)`, `(285,429)`, `(96,196)`, `(110,180)` | 二元組 `(min,max)`；非負整數，實際範圍依 O-RAN FH timing、OAI、RU vendor 設定 | 需問 Ming 是否為 Pegatron 建議值或實測值 |
| FHI 7.2 / Fronthaul | IQ width / PRACH IQ width | `iq_width`, `iq_width_prach` | `9`, `9` | 常見 `8`–`16` bits；需與 O-RU endpoint `iq-bitwidth` 一致 | 本案 RU XML 也是 9 |
| FHI 7.2 / Fronthaul | PRACH eAxC offset | `eAxC_offset` | `4` | 非負整數；需與 RU PRACH endpoint eAxC ID 起點一致 | 本案 PRACH eAxC 預期 4–7 |
| FHI 7.2 / Fronthaul | PRACH kbar | `kbar` | `4` | 非負整數；PRACH frequency offset 相關，實際範圍依 PRACH/RU/OAI 設定 | 需問 Ming 確認 |

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
