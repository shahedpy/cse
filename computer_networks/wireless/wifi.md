# Wi-Fi (802.11)

## Overview

Wi-Fi is a family of wireless networking protocols based on IEEE 802.11 standards. It enables devices to connect to local networks and the Internet without physical cables.

## 802.11 Standards Evolution

| Standard | Year | Frequency | Max Speed | Range | Notes |
|----------|------|-----------|-----------|-------|-------|
| 802.11 | 1997 | 2.4 GHz | 2 Mbps | ~20m | Original |
| 802.11b | 1999 | 2.4 GHz | 11 Mbps | ~35m | First popular |
| 802.11a | 1999 | 5 GHz | 54 Mbps | ~35m | Less interference |
| 802.11g | 2003 | 2.4 GHz | 54 Mbps | ~38m | Backward compatible with b |
| 802.11n (Wi-Fi 4) | 2009 | 2.4/5 GHz | 600 Mbps | ~70m | MIMO, dual-band |
| 802.11ac (Wi-Fi 5) | 2013 | 5 GHz | 3.5 Gbps | ~35m | MU-MIMO, wider channels |
| 802.11ax (Wi-Fi 6) | 2019 | 2.4/5 GHz | 9.6 Gbps | ~30m | OFDMA, better efficiency |
| 802.11ax (Wi-Fi 6E) | 2020 | 6 GHz | 9.6 Gbps | ~30m | 6 GHz band added |
| 802.11be (Wi-Fi 7) | 2024 | 2.4/5/6 GHz | 46 Gbps | ~30m | 320 MHz channels |

## Architecture

### Components

#### 1. Station (STA)
- End-user device (laptop, phone, IoT)
- Has wireless network interface card (NIC)

#### 2. Access Point (AP)
- Bridge between wireless and wired network
- Broadcasts SSID (network name)
- Manages connections

#### 3. Basic Service Set (BSS)
- One AP + associated stations
- Coverage area = Basic Service Area (BSA)

#### 4. Extended Service Set (ESS)
- Multiple APs with same SSID
- Seamless roaming
- Connected via Distribution System (DS)

### Topology Modes

#### Infrastructure Mode
```
STA ←→ AP ←→ Wired Network
```
- Most common
- Centralized control
- Internet access

#### Ad-Hoc Mode (IBSS)
```
STA ←→ STA ←→ STA
```
- Peer-to-peer
- No AP needed
- Limited range

#### Mesh Mode
```
AP ←→ AP ←→ AP
```
- Self-healing
- Extended coverage
- Example: Wi-Fi mesh systems

## Frequency Bands

### 2.4 GHz Band
- **Channels**: 1-14 (varies by country)
- **Non-overlapping**: 1, 6, 11 (in US)
- **Pros**: Better range, penetration
- **Cons**: Crowded, interference (Bluetooth, microwaves)

### 5 GHz Band
- **Channels**: 36-165 (many non-overlapping)
- **Pros**: Less interference, more channels, higher speeds
- **Cons**: Shorter range, worse penetration

### 6 GHz Band (Wi-Fi 6E)
- **Channels**: 1-233
- **Pros**: No legacy devices, cleaner spectrum
- **Cons**: Requires new hardware, shortest range

## Technologies

### MIMO (Multiple Input Multiple Output)
- Multiple antennas on AP and client
- Simultaneous data streams
- Example: 4×4 MIMO = 4 transmit, 4 receive antennas

### MU-MIMO (Multi-User MIMO)
- AP can transmit to multiple clients simultaneously
- Wi-Fi 5: Downlink only
- Wi-Fi 6: Uplink + downlink

### OFDMA (Orthogonal Frequency Division Multiple Access)
- Divides channels into smaller sub-channels
- Multiple users share channel efficiently
- Reduces latency

### Beamforming
- Focuses signal toward specific client
- Improves range and speed
- Reduces interference

### Channel Bonding
- Combines adjacent channels for higher throughput
- 20 MHz → 40 MHz → 80 MHz → 160 MHz
- Trade-off: fewer available channels

## Security

### Encryption Standards

| Protocol | Year | Security | Status |
|----------|------|----------|--------|
| WEP | 1997 | RC4 | **Broken** |
| WPA | 2003 | TKIP | **Deprecated** |
| WPA2 | 2004 | AES-CCMP | **Standard** |
| WPA3 | 2018 | AES-GCMP | **Recommended** |

### WPA2-PSK (Pre-Shared Key)
- Home/small office use
- Same password for all users
- 4-way handshake for authentication

### WPA2-Enterprise (802.1X)
- Corporate environments
- RADIUS server authentication
- Unique credentials per user

### WPA3 Improvements
- **SAE (Simultaneous Authentication of Equals)**
  - Replaces PSK handshake
  - Protects against offline dictionary attacks
- **Forward secrecy**
- **128-bit encryption minimum** (192-bit for Enterprise)
- **Protection on open networks** (OWE - Opportunistic Wireless Encryption)

## MAC Layer

### Carrier Sense Multiple Access (CSMA/CA)
1. Listen before transmit
2. If busy, wait random time (backoff)
3. Send data
4. Wait for ACK

**Why CA (Collision Avoidance)?**
- Wireless can't detect collisions while transmitting
- Unlike Ethernet's Collision Detection (CSMA/CD)

### RTS/CTS (Request to Send / Clear to Send)
- Solves hidden node problem
- See [RTS-CTS](rts-cts.md)

### Frames
- **Management**: Beacons, probe requests/responses, authentication
- **Control**: RTS, CTS, ACK
- **Data**: Actual payload

## Performance Factors

### Signal Strength (RSSI)
```
Excellent: > -50 dBm
Good:      -50 to -60 dBm
Fair:      -60 to -70 dBm
Poor:      < -70 dBm
```

### Interference
- **Co-channel**: Same channel, different networks
- **Adjacent channel**: Overlapping channels
- **Non-Wi-Fi**: Bluetooth, microwaves, baby monitors

### Obstacles
- **Least impact**: Air, wood, drywall
- **Moderate**: Glass, water, humans
- **High impact**: Metal, concrete, brick

## Roaming

### BSS Transition
1. Client monitors signal strength
2. When weak, scans for better AP
3. Authenticates with new AP
4. Switches association

### Fast Roaming (802.11r)
- Pre-authentication with neighboring APs
- Reduces handoff time
- Critical for VoIP, video calls

## Channel Selection

### 2.4 GHz Best Practices
- Use channels 1, 6, or 11 only
- Avoid auto-channel on all APs (can cause overlap)
- Site survey to minimize interference

### 5 GHz Best Practices
- Use DFS (Dynamic Frequency Selection) channels
- Wider channels (80 MHz) for fewer clients
- Narrower channels (20-40 MHz) for crowded areas

## Troubleshooting

### Poor Performance
1. Check signal strength (RSSI)
2. Scan for interference
3. Verify channel overlap
4. Update firmware
5. Check client capabilities

### Connection Drops
- AP overload (too many clients)
- Interference spikes
- Roaming threshold too aggressive
- Faulty hardware

### Tools
- **Windows**: `netsh wlan show networks mode=bssid`
- **macOS**: Option+Click Wi-Fi icon
- **Linux**: `iwconfig`, `iw`, `nmcli`
- **Apps**: WiFi Analyzer, NetSpot

## Best Practices

1. **Separate SSIDs for 2.4/5 GHz** (or band steering)
2. **Disable legacy rates** (802.11b) for better performance
3. **Enable WPA3** (fallback to WPA2)
4. **Use enterprise authentication** for businesses
5. **Regular firmware updates**
6. **Proper AP placement** (ceiling mount, central location)
7. **Enable 802.11k/v/r** for roaming

## See Also

- [Wireless Basics](basics.md)
- [RTS-CTS](rts-cts.md)
- [WiMAX](wimax.md)
- [Mobile Networks](mobile-networks.md)

## Course Materials

- [Lecture on wireless.pdf](../Lecture on wireless.pdf)
