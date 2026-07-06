# OAI Pegatron vs. OAI Aerial Pegatron Comparison

## Purpose

This note compares the baseline OAI + Pegatron RU configuration with the OAI L2 + Aerial cuBB + Pegatron RU integration attempt.
The goal is to identify which parameters must be checked or modified when replacing the original OAI local L1 path with the Aerial cuBB / cuPHY L1 path.

## Comparison Scope

| Comparison Stage | Baseline                   | New / Target Setup                      | Purpose                                                      |
| ---------------- | -------------------------- | --------------------------------------- | ------------------------------------------------------------ |
| Stage 1          | OAI + Pegatron RU          | OAI + cuBB for WNC RU                   | Compare two known successful configurations.                 |
| Stage 2          | OAI + Pegatron RU baseline | OAI + Aerial cuBB + Pegatron RU attempt | Compare the target integration attempt against the baseline. |

## What `cuPHYcontroller-_P5G_WNC_DGX.yaml` Is Doing

| Category                             | What This YAML Does                                                                | Notes                                                             |
| ------------------------------------ | ---------------------------------------------------------------------------------- | ----------------------------------------------------------------- |
| Aerial / cuPHY startup configuration | Sets the SDK version and L2 adapter config.                                        | Allows the cuPHY controller to connect with the OAI L2 adapter.   |
| Host / DGX hardware configuration    | Sets NIC PCIe BDF, MTU, GPU, CPU threads, and DPDK queues.                         | Determines which NIC is used to send packets to the RU.           |
| O-RAN FH / RU cell configuration     | Sets each O-RU's MAC address, VLAN, eAxC ID, IQ format, timing, PRB, and RX ports. | These are the most important items to check when changing the RU. |

## Parameter Table

### Version and OAI L2 Adapter Connection

| Parameter                        |                    Current Value | Meaning                                                         | Notes                                                               |
| -------------------------------- | -------------------------------: | --------------------------------------------------------------- | ------------------------------------------------------------------- |
| `aerial_sdk_version`             |                      `26-1-cubb` | Aerial cuBB SDK version.                                        |                                                                     |
| `l2adapter_filename`             | `l2_adapter_config_P5G_DGX.yaml` | Specifies which L2 adapter config file cuPHY should connect to. |                                                                     |
| `aerial_metrics_backend_address` |                 `127.0.0.1:8081` | Aerial metrics backend address.                                 |                                                                     |
| `low_priority_core`              |                             `10` | CPU core used for low-priority tasks.                           |                                                                     |
| `enable_ptp_svc_monitoring`      |                              `0` | Whether to monitor the PTP service.                             | Need to confirm that PTP synchronization is actually working first. |

### DPDK / NIC / GPU / Host Hardware Configuration

This section configures how the Aerial cuPHY L1 program uses the server hardware resources.

| Parameter     |  Current Value | Meaning                                      | Notes                                                     |
| ------------- | -------------: | -------------------------------------------- | --------------------------------------------------------- |
| `nics[0].nic` | `0000:01:00.0` | NIC PCIe BDF used by cuPHY.                  | Must be modified if the NIC or port is changed.           |
| `nics[0].mtu` |         `8192` | Jumbo frame MTU.                             | **Must be aligned with the switch, RU, and NIC.**         |
| `nics[0].gpu` |            `0` | Specifies which GPU is paired with this NIC. | May need to be changed when using a different DGX server. |
| `txq_size`    |         `8192` | TX queue size.                               |                                                           |
| `rxq_size`    |        `16384` | RX queue size.                               |                                                           |
| `cpu_mbufs`   |       `196608` | Number of DPDK packet buffers.               |                                                           |
| `workers_ul`  |        `[5,6]` | UL worker CPU cores.                         |                                                           |
| `workers_dl`  |      `[7,8,9]` | DL worker CPU cores.                         |                                                           |
| `gpus`        |          `[0]` | Uses GPU 0.                                  |                                                           |

### cuPHY L1 Runtime / GPU Resource Configuration

| Category           | Parameter                      | Current Value | Meaning                                           |
| ------------------ | ------------------------------ | ------------: | ------------------------------------------------- |
| PUSCH GPU resource | `mps_sm_pusch`                 |          `40` | GPU SM resources used by PUSCH.                   |
| PUCCH GPU resource | `mps_sm_pucch`                 |           `4` | GPU SM resources used by PUCCH.                   |
| PRACH GPU resource | `mps_sm_prach`                 |           `4` | GPU SM resources used by PRACH.                   |
| PDSCH GPU resource | `mps_sm_pdsch`                 |          `46` | GPU SM resources used by PDSCH.                   |
| PDCCH GPU resource | `mps_sm_pdcch`                 |          `12` | GPU SM resources used by PDCCH.                   |
| SRS                | `enable_srs`                   |           `1` | Enables SRS.                                      |
| Massive MIMO       | `mMIMO_enable`                 |           `0` | The current setup is not using Massive MIMO mode. |
| L1 sanity check    | `enable_l1_param_sanity_check` |           `0` | L1 parameter sanity check is currently disabled.  |

### Number of O-RUs

The number of O-RUs must match the actual number of RUs in use.
Unused O-RU entries may need to be removed or disabled.

| O-RU   | `cell_id` | `dst_mac_addr`      | `vlan` | `fs_offset_dl` |
| ------ | --------: | ------------------- | -----: | -------------: |
| O-RU 0 |       `1` | `e8:c7:cf:ac:58:20` |  `564` |            `7` |
| O-RU 1 |       `2` | `22:04:9B:9E:27:A2` |    `2` |           `15` |
| O-RU 2 |       `3` | `22:04:9B:9E:27:A3` |    `2` |           `15` |
| O-RU 3 |       `4` | `22:04:9B:9E:27:A4` |    `2` |           `15` |
| O-RU 4 |       `5` | `22:04:9B:9E:27:A5` |    `2` |           `15` |
| O-RU 5 |       `6` | `22:04:9B:9E:27:A6` |    `2` |           `15` |
| O-RU 6 |       `7` | `22:04:9B:9E:27:A7` |    `2` |           `15` |
| O-RU 7 |       `8` | `22:04:9B:9E:27:A8` |    `2` |           `15` |

### RU Network Identification Parameters

| Parameter          | Current Value               | Meaning                                                                                        | Notes                                                                             |
| ------------------ | --------------------------- | ---------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------- |
| `src_mac_addr`     | `00:00:00:00:00:00`         | Source MAC address. The comment says that setting it to `0` will use the NIC port MAC address. | Need to confirm whether the Pegatron RU restricts the allowed source MAC address. |
| `dst_mac_addr`     | Different for each O-RU     | RU MAC address.                                                                                | Must match the RU MAC address.                                                    |
| `nic`              | `0000:01:00.0`              | Specifies which NIC is used.                                                                   | Must be modified if the fronthaul uses a different port.                          |
| `vlan`             | O-RU0 = `564`, others = `2` | eCPRI VLAN ID.                                                                                 | Must be aligned with the Pegatron RU and switch VLAN settings.                    |
| `pcp`              | `7`                         | VLAN priority.                                                                                 | Need to confirm the Pegatron RU requirement.                                      |
| `txq_count_uplane` | `1`                         | Number of U-plane TX queues.                                                                   | To be confirmed.                                                                  |

### eAxC ID

| Channel            | eAxC ID          |
| ------------------ | ---------------- |
| `eAxC_id_ssb_pbch` | `[0, 1, 2, 3]`   |
| `eAxC_id_pdcch`    | `[0, 1, 2, 3]`   |
| `eAxC_id_pdsch`    | `[0, 1, 2, 3]`   |
| `eAxC_id_csirs`    | `[0, 1, 2, 3]`   |
| `eAxC_id_pusch`    | `[0, 1, 2, 3]`   |
| `eAxC_id_pucch`    | `[0, 1, 2, 3]`   |
| `eAxC_id_prach`    | `[4, 5, 6, 7]`   |
| `eAxC_id_srs`      | `[8, 9, 10, 11]` |

### IQ Compression / CUS-Plane Data Format

These settings must be aligned with the RU compression configuration.

| Parameter                  | Current Value |
| -------------------------- | ------------- |
| `dl_iq_data_fmt.comp_meth` | `1`           |
| `dl_iq_data_fmt.bit_width` | `9`           |
| `ul_iq_data_fmt.comp_meth` | `1`           |
| `ul_iq_data_fmt.bit_width` | `9`           |

### Numerology / PRB / Bandwidth

| Parameter          | Current Value | Meaning                                 |
| ------------------ | ------------: | --------------------------------------- |
| `mu`               |           `1` | Numerology = 1, which means 30 kHz SCS. |
| `pusch_prb_stride` |         `273` | PUSCH PRB stride.                       |
| `srs_prb_stride`   |         `273` | SRS PRB stride.                         |
| `prach_prb_stride` |          `12` | PRACH PRB stride.                       |
| `pusch_nMaxPrb`    |         `273` | Maximum number of PUSCH PRBs.           |
| `lower_guard_bw`   |         `845` | Lower guard bandwidth.                  |

### O-RAN FH Timing Window

These values can be fine-tuned based on the parameters previously tested by Ming.

| Parameter                 | Current Value |
| ------------------------- | ------------: |
| `section_3_time_offset`   |         `484` |
| `T1a_min_cp_ul_ns`        |       `36000` |
| `T1a_max_cp_dl_ns`        |      `464000` |
| `T1a_min_cp_dl_ns`        |        `7600` |
| `T1a_max_up_ns`           |      `339000` |
| `Ta4_min_ns`              |       `84000` |
| `Ta4_max_ns`              |      `280000` |
| `Tcp_adv_dl_ns`           |      `125000` |
| `ul_u_plane_tx_offset_ns` |      `280000` |

### Gain / Amplitude

| Parameter             |              Current Value | Meaning                                    |
| --------------------- | -------------------------: | ------------------------------------------ |
| `fs_offset_dl`        | O-RU0 = `7`, others = `15` | Related to DL full-scale offset / scaling. |
| `fs_offset_ul`        |                       `-5` | UL scaling offset.                         |
| `exponent_dl`         |                        `4` | DL exponent.                               |
| `exponent_ul`         |                        `4` | UL exponent.                               |
| `max_amp_ul`          |                    `65504` | Maximum UL amplitude.                      |
| `ul_gain_calibration` |                    `78.68` | UL gain calibration.                       |
| `lower_guard_bw`      |                      `845` | Related to guard bandwidth.                |
