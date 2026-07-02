# OAI gNB To Pegatron RU Parameter Mapping

## Purpose

說明本文件要交付的可驗證成果，並讓後續接手者可以依照 Source、Evidence、Status 與 Next Step 追蹤進度。

## Plan Alignment

| Related Week | Planned Completion | Due Date | Planned Deliverable |
|---|---:|---|---|
| W1 | 50% | 7/1 | `oai-gnb-to-pegatron-ru-parameter-mapping.md` |
| W3 | 70% | 7/13 | `oai-gnb-to-pegatron-ru-parameter-mapping.md` |
| W4 | 100% | 7/17 | `oai-gnb-to-pegatron-ru-parameter-mapping.md` |

## Open Research Playbook Checklist

| Requirement | Check |
|---|---|
| Deliverable is measurable and verifiable | ☐ |
| Evidence path / hyperlink is recorded | ☐ |
| Unknown items are marked as Need Confirm | ☐ |
| Pending / Blocked reason is recorded | ☐ |
| Next step is clear | ☐ |

## file
OAI : [gNB config](https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/doc/gnb.sa.band78.273prb.fhi72.4x4-pega-1G.conf) 
pegatron RU : [ietf-interface-processing-element.xml](https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/doc/ietf-interface-processing-element.xml), [o-ran-uplane-conf_100M_4x4.xml](https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/doc/o-ran-uplane-conf_100M_4x4.xml)

## Mapping / Alignment Table

### Freq/bandwidth/SCS
| 項目                   |                                                       gNB conf |                                     RU XML | 判斷                     |
| -------------------- | -------------------------------------------------------------: | -----------------------------------------: | ---------------------- |
| NR band              | `dl_frequencyBand = 78`、`ul_frequencyBand = 78`、`bands = [78]` |                                       X    | need to match RU ability |
| SCS                  |                                                  `1`， 30 kHz    |                                    `KHZ_30` | match                    |
| DL PRB               |                                    `dl_carrierBandwidth = 273`   |                      `number-of-prb = 273` | match                     |
| UL PRB               |                                    `ul_carrierBandwidth = 273`   |                      `number-of-prb = 273` | match                     |
| RU center frequency  |                                absoluteFrequencyPointA= 646724   | `center-of-channel-bandwidth = 3750000000` | match                     |
| RU channel bandwidth |                            gNB  273 PRB @ 30 kHz，約 98.28 MHz   |             `channel-bandwidth = 100000000` | match                     |
| SSB frequency        |                   `absoluteFrequencySSB = 649920` → 3748.8 MHz   |                         RU center 3750 MHz | SSB iin the carrier,match  |

### antenna / MIMO Layer
| 項目               |                      gNB |                  RU XML | 判斷     |
| ---------------- | -----------------------: | ----------------------: | ------ |
| TX              |               `nb_tx = 4` | `tx-ep0 ~ tx-ep3`| match |
| RX              |               `nb_rx = 4` | `rx-ep0 ~ rx-ep3`| match |
| PRACH           | `eAxC_offset = 4`         |    prach-ep0 ~ prach-ep3 = eAxC 4~7 | match |
| DL MIMO layer    |     `maxMIMO_layers = 4` |    RU have 4 TX endpoint | match |
| UL antenna ports | `pusch_AntennaPorts = 4` |    RU have 4 RX endpoint | match |

### IQ data
| 項目                 |                      gNB |                           RU XML | 判斷                  |
| ------------------ | -----------------------: | -------------------------------: | ------------------- |
| IQ bitwidth        |           `iq_width = 9` |                `iq-bitwidth = 9` | match                  |
| PRACH IQ bitwidth  |     `iq_width_prach = 9` | PRACH endpoint `iq-bitwidth = 9` | match                  |

### Fronthaul MAC / VLAN

| 項目             |             gNB conf |              RU XML | 判斷                          |
| -------------- | -------------------: | ------------------: | --------------------------- |
| RU MAC         |  `48:21:0b:4b:93:8e` | `48:21:0b:4b:93:8e` | match                          |
| VLAN ID        |         X |               `103` | already corfirm with Ming         |
| O-DU MAC       |         X | `00:11:22:33:44:66` | already corfirm with Ming         |

[note] ARFCN = Absolute Radio Frequency Channel Number :是一個「頻率編號」。

3GPP TS 38.104 definition
```
Freq = Freq-Offs + ΔFGlobal × (Nref - Nref-Offs)

# in 3000 MHz - 24250 MHz this range
FREF-Offs = 3000 MHz
NREF-Offs = 600000
ΔFGlobal = 15 kHz = 0.015 MHz
Nref = correspond parameter
```
absoluteFrequencySSB = 649920 → Freq 3748.8 MHz , dl_absoluteFrequencyPointA = 646724  → Freq 3700.86 MHz

1 PRB = 12 subcarriers  ,  273 PRB × 12 subcarriers/PRB × 30 kHz = 98.28 MHz
```
3700.86 MHz                         3750 MHz                         3799.14 MHz
    |-----------------------------------|-----------------------------------|
  PointA                              Center                          右邊界附近
    <----------- 49.14 MHz -----------> <----------- 49.14 MHz ----------->
```
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
