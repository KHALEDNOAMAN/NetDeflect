# NetDeflect - Deployment Guide

## Overview
Open-source DDoS mitigation for Linux with nftables, XDP, and 110+ attack signatures.

## Architecture
```
Incoming Traffic --> XDP (kernel) --> nftables --> Application
                       |                |
                  Fast Drop         Rule Engine
                  (wire-speed)      (110 signatures)
                       |                |
                  sFlow/NetFlow    Auto-Learning
                       |                |
                  BGP Blackhole    Discord Alerts
```

## Quick Install
```bash
curl -sSL https://raw.githubusercontent.com/0vm/NetDeflect/main/install.sh | bash
```

## Protection Capabilities
| Attack Type | Method | Throughput |
|-------------|--------|-----------|
| SYN Flood | XDP + SYN cookies | 100 Gbps |
| UDP Flood | Rate limiting + geo-block | 100 Gbps |
| DNS Amplification | Signature match | 50 Gbps |
| Game Server | Protocol validation | 40 Gbps |
| VPN/WireGuard | Allowlist + rate limit | 40 Gbps |

## Configuration
| Setting | Default | Description |
|---------|---------|-------------|
| auto_learn | true | Learn normal traffic patterns |
| discord_webhook | null | Alert webhook URL |
| bgp_enabled | false | BGP blackhole routing |
| threshold_pps | 100000 | Packets/sec trigger |