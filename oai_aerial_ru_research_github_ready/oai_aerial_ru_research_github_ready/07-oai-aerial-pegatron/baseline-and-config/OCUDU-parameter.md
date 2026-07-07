# OCUDU Parameter Table

> Reference :
>   https://docs.ocudu.org/integrations/radio_units/pegatron/
>

## Purpose

This note introduces the main parameters and organizes the RU config for the OCUDU.

## Parameter Table

## configuration
| Category | Parameter | OCUDU Value | Notes |
|---|---|---|---|
| Document Scope | Target RU family | Pegatron PR1450 / PR2850 |  |
| Document Scope | Tested RU model | PR1450-78I |  |
| Document Scope | Tested firmware version | v1.0.2.4p1 |  |
| DU Configuration | Sample configuration file | gnb_ru_pegatron_tdd_n78_100mhz_4x4.yml |  |

## RF Freq and MIMO Layer
| Category | Parameter | OCUDU Value | Notes |
|---|---|---|---|
| RF / Cell | NR band | n78 |  |
| RF / Cell | MIMO configuration | 4x4 MIMO / 4T4R |  |
| RF / Cell | Channel bandwidth | 100 MHz |  |
| RF / Cell | PRB count | 273 PRBs |  |
| RF / Cell | DL ARFCN | 650000 |  |
| RF / Cell | Center frequency | 3750.0 MHz |  |
| RF / Cell | UL frequency | 3750.0 MHz |  |

## TDD setting
| Category | Parameter | OCUDU Value | Notes |
|---|---|---|---|
| TDD | TDD pattern | DDDDDDDSUUU |  |
| TDD | TDD period | 10 slots |  |
| TDD | DL slots | 7 |  |
| TDD | Special slot DL symbols | 6 |  |
| TDD | UL slots | 2 |  |
| TDD | Special slot UL symbols | 4 |  |

## FH windows
| Category | Parameter | OCUDU Value | Notes |
|---|---|---|---|
| OFH Timing | t1a_max_cp_dl | 470 |  |
| OFH Timing | t1a_min_cp_dl | 285 |  |
| OFH Timing | t1a_max_cp_ul | 429 |  |
| OFH Timing | t1a_min_cp_ul | 285 |  |
| OFH Timing | t1a_max_up | 350 |  |
| OFH Timing | t1a_min_up | 125 |  |
| OFH Timing | ta4_max | 180 |  |
| OFH Timing | ta4_min | 110 |  |

## compression
| Category | Parameter | OCUDU Value | Notes |
|---|---|---|---|
| Compression | UL compression method | bfp |  |
| Compression | UL compression bitwidth | 9 |  |
| Compression | DL compression method | bfp |  |
| Compression | DL compression bitwidth | 9 |  |
| Compression | PRACH compression method | bfp |  |
| Compression | PRACH compression bitwidth | 9 |  |
| Compression | enable_ul_static_compr_hdr | true |  |
| Compression | enable_dl_static_compr_hdr | true |  |
| Power / Level | ru_reference_level_dBFS | -12 |  |
| Power / Level | subcarrier_rms_backoff_dB | 0 |  |

## network setting
| Category | Parameter | OCUDU Value | Notes |
|---|---|---|---|
| Network | network_interface | 0000:ca:01.3 |  |
| Network | ru_mac_addr | 48:21:0b:xx:xx:xx |  |
| Network | du_mac_addr | 00:11:22:33:44:55 |  |
| Network | vlan_tag_cp | 5 |  |
| Network | vlan_tag_up | 5 |  |
| Network | enable_promiscuous | true |  |
| Network | check_link_status | false |  |

## eAxC/DPDK setting CPU allocation
| Category | Parameter | OCUDU Value | Notes |
|---|---|---|---|
| eAxC Mapping | DL port IDs | [0, 1, 2, 3] |  |
| eAxC Mapping | UL port IDs | [0, 1, 2, 3] |  |
| eAxC Mapping | PRACH port IDs | [4, 5, 6, 7] |  |
| Synchronization | PTP synchronization | Required |  |
| DPDK / SR-IOV | DPDK mode | Enabled |  |
| DPDK / SR-IOV | DPDK PCI device flag | -a 0000:ca:01.3 |  |
| DPDK / SR-IOV | PMD drivers | iavf |  |
| CPU / Threading | OFH timing CPU | 3 |  |
| CPU / Threading | Main pool threads | 12 |  |
| CPU / Threading | Task queue size | 2048 |  |
| CPU / Threading | Backoff period | 10 |  |
