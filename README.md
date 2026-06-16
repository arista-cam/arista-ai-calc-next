# AI Backend Network Calculator

A browser-based tool for sizing AI backend network fabrics. Enter your GPU cluster parameters and get switch counts, optics requirements, cabling breakdowns, and topology diagrams — all based on real Arista 800G switch platforms.

## Features

- **Three fabric tiers** — single-tier (collapsed spine), two-tier (leaf-spine Clos), and three-tier (hyperscale Clos)
- **Arista platform auto-selection** — automatically picks the smallest balanced switch combination (7060X6, 7700R4, 7800R4) based on cluster size
- **Full optics breakdown** — transceiver counts per tier with breakout support (1:1, 1:2, 1:4)
- **Topology diagrams** — logical data path visualization showing switch models, port counts, and link bundles
- **Built-in validation** — hard errors for invalid topologies and warnings for unbalanced fabrics, with minimum platform suggestions
- **Light/dark theme** — follows system preference automatically
- **Print-friendly** — clean output for reports and proposals

## Supported Arista Platforms

| Platform | Ports | Type |
|----------|-------|------|
| 7060X6 | 32 / 64 | Fixed 800G |
| 7700R4 | 38 / 128 | Fixed 800G |
| 7800R4 | 144 / 288 / 432 / 576 | Chassis (4/8/12/16-slot × 36-port line cards) |

## Usage

Open `index.html` in any modern browser. No build step, no dependencies, no server required.

1. Enter your GPU count (or node count + GPUs per node)
2. Select a fabric tier
3. Adjust switch configuration (planes, downlink:uplink ratio, breakout)
4. Click **Calculate Network Requirements**

The tool auto-selects the optimal switch platforms. Override manually via the dropdowns or select "Other (custom)" for arbitrary port counts.

## Configuration Options

| Input | Description |
|-------|-------------|
| Total GPUs / Nodes | Cluster size — syncs bidirectionally |
| GPUs per node | Typically 8 for modern GPU servers |
| Links per GPU | Backend NIC links (1 standard, 2 for dual-rail) |
| Fabric tier | Single, two, or three-tier Clos topology |
| Leaf / Spine switch | Arista platform or custom port count |
| Planes | Redundant parallel fabrics (1–8) |
| Downlink:Uplink ratio | Port allocation ratio (1 = non-blocking, <1 = more uplinks) |
| Host port breakout | Switch-to-host port splitting (1:1, 1:2, 1:4) |
| Spine / Host link speed | 400G or 800G spine links, 100G–800G host links |

## Output

- **Metrics grid** — total GPUs, backend links, spine/leaf/total switch counts
- **Switch breakdown** — per-tier tables with platform names, switch counts per plane, port utilization, and bundle sizes
- **Topology diagram** — vertical data path from compute node through leaf/spine layers with link counts
- **Optics breakdown** — transceiver counts by tier and type (QSFP28, QSFP-DD, OSFP) with grand total
