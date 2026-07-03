# OAI Pegatron Vs OAI Aerial Pegatron Comparison

## Purpose

## Comparison Scope

| Comparison Stage | Baseline | New / Target Setup | Purpose |
|---|---|---|---|
| Stage 1 | OAI + Pegatron RU | OAI + cuBB for WNC RU | Compare two known successful configurations |
| Stage 2 | OAI + Pegatron RU baseline | OAI + Ariel cuBB + Pegatron RU attempt | Compare target integration attempt against baseline |

## What cuPHYcontroller-_P5G_WNC_DGX.yaml is doing

| 類別                    | 這份 YAML 做的事                                         | 備註                                   |
| --------------------- | --------------------------------------------------- | ---------------------------------------- |
| Aerial/cuPHY 啟動設定     | 設定 SDK、L2 adapter config、                | 讓 cuPHY controller 能跟 OAI L2 adapter 接起來 |
| Host / DGX 硬體設定       | 設定 NIC PCIe BDF、MTU、GPU、CPU thread、DPDK queue       | 決定封包從哪張網卡送到 RU                           |
| O-RAN FH / RU cell 設定   | 設定每個 O-RU 的 MAC、VLAN、eAxC、IQ 格式、timing、PRB、RX ports | 換 RU 時最需要檢查                              |

## parameter table

### 版本與 OAI L2 adapter 連接

| 參數                               |                          目前值 | 意義                           | 備註                                |
| -------------------------------- | -------------------------------: | ---------------------------- | ------------------------------------------------- |
| `aerial_sdk_version`             |                      `26-1-cubb` | Aerial cuBB SDK 版本           |                                  |
| `l2adapter_filename`             | `l2_adapter_config_P5G_DGX.yaml` | cuPHY 要接哪份 L2 adapter config |  |
| `aerial_metrics_backend_address` |                 `127.0.0.1:8081` |             |                                             |
| `low_priority_core`              |                             `10` |      |                                              |
| `enable_ptp_svc_monitoring`      |                              `0` | 是否監控 PTP                     | 需先確認 PTP 真的有同步      |

### DPDK / NIC / GPU / Host 硬體設定

設定 Aerial cuPHY 這個 L1 程式要怎麼使用伺服器硬體資源

| 參數            |        目前值 | 意義                    | 備註          |
| ------------- | -------------: | --------------------- | --------------------------- |
| `nics[0].nic` | `0000:01:00.0` | 使用的 NIC PCIe BDF    | 如果換網卡或換 port 要改             |
| `nics[0].mtu` |         `8192` | Jumbo frame MTU       | **要跟 switch / RU / NIC 對齊** |
| `nics[0].gpu` |            `0` | 這張 NIC 搭配哪張 GPU  | 換 DGX 可能要改                 |
| `txq_size`    |         `8192` | TX queue size         |                       |
| `rxq_size`    |        `16384` | RX queue size         |                       |
| `cpu_mbufs`   |       `196608` | DPDK packet buffer 數量 |                       |
| `workers_ul`  |        `[5,6]` | UL worker CPU core    |                      |
| `workers_dl`  |      `[7,8,9]` | DL worker CPU core    |                       |
| `gpus`        |          `[0]` | 使用 GPU 0              |                      |

### cuPHY L1 runtime / GPU resource 設定

| 類別                 | 參數                             |  目前值 | 意義                   |
| ------------------ | ------------------------------ | ---: | -------------------- |
| PUSCH GPU resource | `mps_sm_pusch`                 | `40` | PUSCH 使用的 GPU SM 資源  |
| PUCCH GPU resource | `mps_sm_pucch`                 |  `4` | PUCCH GPU 資源         |
| PRACH GPU resource | `mps_sm_prach`                 |  `4` | PRACH GPU 資源         |
| PDSCH GPU resource | `mps_sm_pdsch`                 | `46` | PDSCH GPU 資源         |
| PDCCH GPU resource | `mps_sm_pdcch`                 | `12` | PDCCH GPU 資源         |
| SRS                | `enable_srs`                   |  `1` | 啟用 SRS               |
| Massive MIMO       | `mMIMO_enable`                 |  `0` | 目前不是 Massive MIMO 模式 |
| L1 sanity check    | `enable_l1_param_sanity_check` |  `0` | L1 參數檢查目前關掉          |

### O-RU 數量

數量需對應RU 數量，可能需要刪減
| O-RU   | `cell_id` | `dst_mac_addr`      | `vlan` | `fs_offset_dl` |
| ------ | --------: | ------------------- | -----: | -------------: |
| O-RU 0 |         1 | `e8:c7:cf:ac:58:20` |  `564` |            `7` |
| O-RU 1 |         2 | `22:04:9B:9E:27:A2` |    `2` |           `15` |
| O-RU 2 |         3 | `22:04:9B:9E:27:A3` |    `2` |           `15` |
| O-RU 3 |         4 | `22:04:9B:9E:27:A4` |    `2` |           `15` |
| O-RU 4 |         5 | `22:04:9B:9E:27:A5` |    `2` |           `15` |
| O-RU 5 |         6 | `22:04:9B:9E:27:A6` |    `2` |           `15` |
| O-RU 6 |         7 | `22:04:9B:9E:27:A7` |    `2` |           `15` |
| O-RU 7 |         8 | `22:04:9B:9E:27:A8` |    `2` |           `15` |

### RU 網路識別參數

| 參數                 | 目前值                 | 意義                                  | note                           |
| ------------------ | ------------------- | ----------------------------------- | ----------------------------------------- |
| `src_mac_addr`     | `00:00:00:00:00:00` | source MAC；註解說設成 0 會使用 NIC port MAC | 但要確認 Pegatron RU 是否限制來源 MAC         |
| `dst_mac_addr`     | 每個 O-RU 不同          | RU 的 MAC address                    | 需對應RU 的 MAC address     |
| `nic`              | `0000:01:00.0`      | 使用哪張 NIC                            | FH 接不同 port 要改                         |
| `vlan`             | O-RU0=`564`，其他=`2`  | eCPRI VLAN ID                       | 需要跟 Pegatron RU / switch VLAN 對齊     |
| `pcp`              | `7`                 | VLAN priority                       | 要確認 Pegatron 要求 |
| `txq_count_uplane` | `1`                 | U-plane TX queue 數                  | 需確認                                     |

### eAxC ID
| Channel            |  eAxC ID       |
| ------------------ | ---------------- |
| `eAxC_id_ssb_pbch` | `[0, 1, 2, 3]`   |
| `eAxC_id_pdcch`    | `[0, 1, 2, 3]`   |
| `eAxC_id_pdsch`    | `[0, 1, 2, 3]`   |
| `eAxC_id_csirs`    | `[0, 1, 2, 3]`   |
| `eAxC_id_pusch`    | `[0, 1, 2, 3]`   |
| `eAxC_id_pucch`    | `[0, 1, 2, 3]`   |
| `eAxC_id_prach`    | `[4, 5, 6, 7]`   |
| `eAxC_id_srs`      | `[8, 9, 10, 11]` |


### IQ compression / CUS-plane data format
需對齊
| 參數                         | 目前值 |
| -------------------------- | --- |
| `dl_iq_data_fmt.comp_meth` | `1` |
| `dl_iq_data_fmt.bit_width` | `9` |
| `ul_iq_data_fmt.comp_meth` | `1` |
| `ul_iq_data_fmt.bit_width` | `9` |

### numerology / PRB / bandwidth

| 參數                 |   目前值 | 意義                             |
| ------------------ | ----: | ------------------------------ |
| `mu`               |   `1` | numerology = 1， 30 kHz SCS |
| `pusch_prb_stride` | `273` | PUSCH PRB stride               |
| `srs_prb_stride`   | `273` | SRS PRB stride                 |
| `prach_prb_stride` |  `12` | PRACH PRB stride               |
| `pusch_nMaxPrb`    | `273` | PUSCH max PRB                   |
| `lower_guard_bw`   | `845` | lower guard bandwidth      |

### O-RAN FH timing window
可以根據 Ming 學長之前的參數下去做微調
| 參數                        |      目前值 |
| ------------------------- | -------: |
| `section_3_time_offset`   |    `484` |
| `T1a_min_cp_ul_ns`        |  `36000` |
| `T1a_max_cp_dl_ns`        | `464000` |
| `T1a_min_cp_dl_ns`        |   `7600` |
| `T1a_max_up_ns`           | `339000` |
| `Ta4_min_ns`              |  `84000` |
| `Ta4_max_ns`              | `280000` |
| `Tcp_adv_dl_ns`           | `125000` |
| `ul_u_plane_tx_offset_ns` | `280000` |

### gain / amplitude
| 參數                    |               目前值 | 意義                                |
| --------------------- | ----------------: | --------------------------------- |
| `fs_offset_dl`        | O-RU0=`7`，其他=`15` | DL full-scale offset / scaling 相關 |
| `fs_offset_ul`        |              `-5` | UL scaling offset                 |
| `exponent_dl`         |               `4` | DL exponent                       |
| `exponent_ul`         |               `4` | UL exponent                       |
| `max_amp_ul`          |           `65504` | UL 最大 amplitude                   |
| `ul_gain_calibration` |           `78.68` | UL gain calibration               |
| `lower_guard_bw`      |             `845` | guard bandwidth 相關                |
