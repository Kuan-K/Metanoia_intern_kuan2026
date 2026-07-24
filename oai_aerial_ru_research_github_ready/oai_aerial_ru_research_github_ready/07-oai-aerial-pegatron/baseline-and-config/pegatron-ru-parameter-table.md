# Pegatron RU Parameter Table

## Purpose

This note introduces the main parameters used in the Pegatron RU configuration, including carrier settings, TX/RX carrier settings, endpoint mapping, timing configuration, network interface settings, and fronthaul link mapping.

## reference

> https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/doc/ietf-interface-processing-element.xml
>
> https://github.com/Kuan-K/Metanoia_intern_kuan2026/blob/main/doc/o-ran-uplane-conf_100M_4x4.xml
> 

## Parameter Table

| Category        | Name in Conf                          | Current Value | Possible Range | Notes                                                                                                                                                                                                           |
| --------------- | ------------------------------------- | ------------- | -------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Radio / Carrier | `center-of-channel-bandwidth`         | `3750000000`  |                | The actual carrier center frequency used by the RU.                                                                                                                                                             |
| Radio / Carrier | `channel-bandwidth`                   | `100000000`   |                | The channel bandwidth used by the RU.                                                                                                                                                                           |
| Radio / Carrier | `scs`                                 | `KHZ_30`      |                | SCS = 30 kHz.                                                                                                                                                                                                   |
| Radio / Carrier | `number-of-prb`                       | `273`         |                | Number of available PRBs.                                                                                                                                                                                       |
| Radio / Carrier | `cp-type`                             | `NORMAL`      |                | `cp-type = NORMAL`. Cyclic Prefix is a short guard interval added before each symbol to reduce interference caused by multipath propagation. This must be consistent with the gNB numerology / CP type setting. |
| Radio / Carrier | `cp-length`                           | `88`          |                | Length of the guard interval before the symbol.                                                                                                                                                                 |
| Radio / Carrier | `cp-length-other`                     | `72`          |                | `cp-length` refers to the CP length of the main or specific symbol.<br>`cp-length-other` refers to the CP length of the other symbols.                                                                          |
| Radio / Carrier | `offset-to-absolute-frequency-center` | `-3276`       |                | Frequency offset. This must be aligned with the gNB Point A / ARFCN / center frequency.                                                                                                                         |
| Radio / Carrier | `frame-structure`                     | `193`         |                | Defines which frame / slot / symbol structure is used by this endpoint.                                                                                                                                         |

## RU TX Carrier / RX Carrier Configuration

TX Carrier is used by the RU to transmit signals to the UE.
RX Carrier is used by the RU to receive signals from the UE.

The carrier frequency and bandwidth are the same as the values in the table above, and the carriers are enabled.

| Category       | Name in Conf                           | Current Value            | Possible Range | Notes                                                                                                                                                                             |
| -------------- | -------------------------------------- | ------------------------ | -------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| TX Carrier     | `tx-carr0 center-of-channel-bandwidth` | `3750000000`             |                |                                                                                                                                                                                   |
| TX Carrier     | `tx-carr0 channel-bandwidth`           | `100000000`              |                |                                                                                                                                                                                   |
| TX Carrier     | `tx-carr0 gain`                        | `14.0`                   |                | Gain.                                                                                                                                                                             |
| TX Carrier     | `tx-carr0 active`                      | `ACTIVE`                 |                |                                                                                                                                                                                   |
| TX Carrier     | `tx-carr1 center-of-channel-bandwidth` | `3750000000`             |                |                                                                                                                                                                                   |
| TX Carrier     | `tx-carr1 channel-bandwidth`           | `100000000`              |                |                                                                                                                                                                                   |
| TX Carrier     | `tx-carr1 gain`                        | `14.0`                   |                | Gain.                                                                                                                                                                             |
| TX Carrier     | `tx-carr1 active`                      | `ACTIVE`                 |                |                                                                                                                                                                                   |
| RX Carrier     | `rx-carr0 center-of-channel-bandwidth` | `3750000000`             |                |                                                                                                                                                                                   |
| RX Carrier     | `rx-carr0 channel-bandwidth`           | `100000000`              |                |                                                                                                                                                                                   |
| RX Carrier     | `rx-carr0 gain-correction`             | `0.0`                    |                |                                                                                                                                                                                   |
| RX Carrier     | `rx-carr0 active`                      | `ACTIVE`                 |                |                                                                                                                                                                                   |
| RX Carrier     | `rx-carr1 center-of-channel-bandwidth` | `3750000000`             |                |                                                                                                                                                                                   |
| RX Carrier     | `rx-carr1 channel-bandwidth`           | `100000000`              |                |                                                                                                                                                                                   |
| RX Carrier     | `rx-carr1 gain-correction`             | `0.0`                    |                |                                                                                                                                                                                   |
| RX Carrier     | `rx-carr1 active`                      | `ACTIVE`                 |                |                                                                                                                                                                                   |
| TX Endpoint    | `tx-ep0 eaxc-id`                       | `0`                      |                | Four downlink data streams.                                                                                                                                                       |
| TX Endpoint    | `tx-ep1 eaxc-id`                       | `1`                      |                |                                                                                                                                                                                   |
| TX Endpoint    | `tx-ep2 eaxc-id`                       | `2`                      |                |                                                                                                                                                                                   |
| TX Endpoint    | `tx-ep3 eaxc-id`                       | `3`                      |                |                                                                                                                                                                                   |
| RX Endpoint    | `rx-ep0 eaxc-id`                       | `0`                      |                | Four uplink data streams.                                                                                                                                                         |
| RX Endpoint    | `rx-ep1 eaxc-id`                       | `1`                      |                |                                                                                                                                                                                   |
| RX Endpoint    | `rx-ep2 eaxc-id`                       | `2`                      |                |                                                                                                                                                                                   |
| RX Endpoint    | `rx-ep3 eaxc-id`                       | `3`                      |                |                                                                                                                                                                                   |
| PRACH Endpoint | `prach-ep0 eaxc-id`                    | `4`                      |                | Data stream dedicated to Random Access. General UL data uses `rx-ep0` to `rx-ep3`, while PRACH for UE random access uses `prach-ep0` to `prach-ep3`. The eAxC IDs are `4` to `7`. |
| PRACH Endpoint | `prach-ep1 eaxc-id`                    | `5`                      |                |                                                                                                                                                                                   |
| PRACH Endpoint | `prach-ep2 eaxc-id`                    | `6`                      |                |                                                                                                                                                                                   |
| PRACH Endpoint | `prach-ep3 eaxc-id`                    | `7`                      |                |                                                                                                                                                                                   |
| eAxC bitmask   | `o-du-port-bitmask`                    | `49152`                  |                | The eAxC bitmask determines how the eAxC ID is decoded. To be confirmed.                                                                                                          |
| eAxC bitmask   | `band-sector-bitmask`                  | `16128`                  |                |                                                                                                                                                                                   |
| eAxC bitmask   | `ccid-bitmask`                         | `240`                    |                |                                                                                                                                                                                   |
| eAxC bitmask   | `ru-port-bitmask`                      | `15`                     |                |                                                                                                                                                                                   |
| Compression    | `iq-bitwidth`                          | `9`                      |                | IQ samples use 9-bit compression.                                                                                                                                                 |
| Compression    | `compression-type`                     | `STATIC`                 |                | Uses a fixed compression configuration.                                                                                                                                           |
| Compression    | `compression-method`                   | `BLOCK_FLOATING_POINT`   |                | Uses BFP compression.                                                                                                                                                             |
| Compression    | `fs-offset`                            | `TX = 0`, `RX/PRACH = 8` |                |                                                                                                                                                                                   |

## Timing Configuration

| Category        | Name in Conf                     | Current Value | Possible Range | Notes                                                                                                                                                     |
| --------------- | -------------------------------- | ------------- | -------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------- |
| UL Timing       | `ul-fft-sampling-offset`         | `21`          |                | Uplink FFT sampling position offset. This defines the time point from which the RU starts sampling for FFT processing.                                    |
| Timing          | `downlink-radio-frame-offset`    | `2394880`     |                | The RU needs to know when a radio frame starts.<br>`downlink-radio-frame-offset` defines the offset of the DL radio frame relative to the reference time. |
| Timing          | `downlink-sfn-offset`            | `360`         |                | To be confirmed.                                                                                                                                          |
| Timing          | `n-ta-offset`                    | `25600`       |                | Timing Advance offset.                                                                                                                                    |
| Endpoint option | `non-time-managed-delay-enabled` | `false`       |                | Non-time-managed delay is not enabled.                                                                                                                    |

## Network Interface / Transport Flow Configuration

| Category           | Name in Conf           | Current Value       | Possible Range | Notes                                                           |
| ------------------ | ---------------------- | ------------------- | -------------- | --------------------------------------------------------------- |
| Network Interface  | `fm1-mac9 mac-address` | `48:21:0b:4b:93:8e` |                | The MAC address on the RU side. This must match the gNB config. |
| Network Interface  | `cuplane mac-address`  | `48:21:0b:4b:93:8e` |                | The RU C-plane / U-plane Ethernet flow uses this MAC address.   |
| Network Interface  | `cuplane vlan-id`      | `103`               |                | C/U-plane packets use VLAN 103.                                 |
| Processing Element | `ru-elements name`     | `pse3`              |                |                                                                 |
| Transport Flow     | `interface-name`       | `cuplane`           |                |                                                                 |
| Transport Flow     | `ru-mac-address`       | `48:21:0b:4b:93:8e` |                |                                                                 |
| Transport Flow     | `vlan-id`              | `103`               |                |                                                                 |
| Transport Flow     | `o-du-mac-address`     | `00:11:22:33:44:66` |                |                                                                 |

## TX Link Mapping / RX Link Mapping

This section configures the connection between carriers and endpoints.
The TX carrier is mapped to the TX endpoint, and the RX carrier is mapped to the RX endpoint.

| Category           | Name in Conf | Current Value                 | Possible Range | Notes |
| ------------------ | ------------ | ----------------------------- | -------------- | ----- |
| TX Link Mapping    | `tx-link0`   | `pse3 / tx-carr0 / tx-ep0`    |                |       |
| TX Link Mapping    | `tx-link1`   | `pse3 / tx-carr0 / tx-ep1`    |                |       |
| TX Link Mapping    | `tx-link2`   | `pse3 / tx-carr1 / tx-ep2`    |                |       |
| TX Link Mapping    | `tx-link3`   | `pse3 / tx-carr1 / tx-ep3`    |                |       |
| RX Link Mapping    | `rx-link0`   | `pse3 / rx-carr0 / rx-ep0`    |                |       |
| RX Link Mapping    | `rx-link1`   | `pse3 / rx-carr0 / rx-ep1`    |                |       |
| RX Link Mapping    | `rx-link2`   | `pse3 / rx-carr1 / rx-ep2`    |                |       |
| RX Link Mapping    | `rx-link3`   | `pse3 / rx-carr1 / rx-ep3`    |                |       |
| PRACH Link Mapping | `rx-link4`   | `pse3 / rx-carr0 / prach-ep0` |                |       |
| PRACH Link Mapping | `rx-link5`   | `pse3 / rx-carr0 / prach-ep1` |                |       |
| PRACH Link Mapping | `rx-link6`   | `pse3 / rx-carr1 / prach-ep2` |                |       |
| PRACH Link Mapping | `rx-link7`   | `pse3 / rx-carr1 / prach-ep3` |                |       |
