# claude-network-skills

**Claude Code skills and agents for network engineers and homelab enthusiasts.**

Stop getting generic networking advice from AI. These skills load structured, practitioner-level knowledge directly into Claude Code — specific commands, ordered diagnostic sequences, real config patterns, and anti-patterns from production environments.

9 skills + 4 agents covering BGP, Cisco IOS, interface health, SSH automation, config validation, enterprise network design, and a full homelab track.

Compatible with [Claude Code](https://claude.ai/code), Cursor, and any Claude Code-compatible harness.

---

## What this actually does

Claude already knows networking. These skills make it work like a senior network engineer.

Without skills, Claude gives you textbook answers. With skills, it gives you the ordered diagnostic sequence an experienced engineer would follow, the exact IOS commands to run, what the output means, and the anti-patterns to avoid. The difference shows up immediately.

**Skills auto-activate** — you don't have to invoke them manually. Ask about a BGP Active state and the `network-bgp-diagnostics` skill loads automatically. Ask about setting up VLANs on UniFi and `homelab-vlan-segmentation` loads. The skill detection is based on context, not keywords.

**Agents are invoked explicitly** and do a full job, not just answer a question. Paste a router config into `network-config-reviewer` and get back a prioritized security audit. Describe your hardware to `homelab-architect` and get a complete network plan.

---

## Installation

### 1. Clone or download

```bash
git clone https://github.com/arsallls/claude-network-skills.git
cd claude-network-skills
```

### 2. Install skills

```bash
# Install all skills at once
cp -r skills/. ~/.claude/skills/

# Or pick individual skills
cp -r skills/network-bgp-diagnostics ~/.claude/skills/
cp -r skills/homelab-pihole-dns ~/.claude/skills/
```

### 3. Install agents

```bash
# Create the agents directory if it doesn't exist
mkdir -p ~/.claude/agents

# Install all agents
cp agents/network-troubleshooter.md ~/.claude/agents/
cp agents/network-config-reviewer.md ~/.claude/agents/
cp agents/homelab-architect.md ~/.claude/agents/
cp agents/network-architect.md ~/.claude/agents/
```

### 4. Verify

Open a new Claude Code session and run `/skills` — you should see the network skills listed. Or just ask a networking question and watch the skill auto-load.

---

## Skills

### Network Engineering

#### `network-bgp-diagnostics`
BGP neighbor state analysis and troubleshooting. Covers the full diagnostic sequence for Active/Idle/Connect states, AS path analysis, route filtering, and peering issues. Includes a Python parser for BGP summary output.

```
# Test prompt
my BGP neighbor 10.0.0.2 is showing Active state, how do I diagnose it?
```

#### `cisco-ios-patterns`
IOS and IOS-XE reference patterns — config mode hierarchy, essential show commands, wildcard mask calculation, ACL structure, privilege levels, and the operational gotchas that cause the most incidents (forgetting `wr mem`, wrong wildcard direction, implicit deny).

```
# Test prompt
what's the wildcard mask for a /27 and how do I use it in a named ACL?
```

#### `network-interface-health`
Interface error diagnosis — CRC errors, input/output drops, runts, giants, duplex mismatches, flapping, and speed negotiation failures. Includes a Python counter parser for automated health checks.

```
# Test prompt
my interface is showing CRC errors, walk me through diagnosing it
```

#### `netmiko-ssh-automation`
Python Netmiko patterns for multi-vendor SSH automation — single device connections, batch parallel operations, enable mode, TextFSM parsing, and production-grade error handling. Credentials from environment variables, never hardcoded.

```
# Test prompt
write a python script to collect show version from 20 cisco routers in parallel
```

#### `network-config-validation`
Pre-deployment config validation — dangerous command detection, IOS-XE syntax checking, subnet overlap detection, duplicate IP detection, and security/best-practice auditing. The check you run before every change window.

```
# Test prompt
validate this config block: [paste IOS config]
```

---

### Homelab

#### `homelab-network-setup`
Home network architecture from scratch. IP addressing scheme design, hardware selection, DHCP scoping, DNS setup, and the five mistakes that trip up every first-time homelab builder.

```
# Test prompt
I want to build a homelab network from scratch, where do I start?
```

#### `homelab-vlan-segmentation`
VLAN segmentation for IoT, guest, trusted, and server traffic. Covers UniFi, pfSense/OPNsense, and MikroTik — VLAN creation, trunk/access port config, SSID-to-VLAN mapping, and the firewall rules that actually enforce the segmentation.

```
# Test prompt
how do I isolate my IoT devices on a UniFi network?
```

#### `homelab-pihole-dns`
Pi-hole installation, blocklist management, DNS-over-HTTPS with cloudflared, local DNS records (nas.home.lan, pi.home.lan), and DHCP integration. Includes Docker Compose setup and troubleshooting commands.

```
# Test prompt
walk me through setting up Pi-hole on a Raspberry Pi
```

#### `homelab-wireguard-vpn`
WireGuard VPN server setup, peer configuration, split tunnel vs full tunnel routing, key generation in Python, DDNS setup for dynamic IPs, and QR code generation for mobile clients.

```
# Test prompt
set up a WireGuard server on my Pi for remote access to my home network
```

---

## Agents

Agents do a job, not just answer a question. Invoke them explicitly.

#### `network-troubleshooter`
Takes a symptom description and walks through a structured OSI-layer-by-layer diagnostic. Produces a ranked hypothesis table, specific diagnostic commands to run, and a root cause summary with fixes and verification steps.

```
use the network-troubleshooter agent — users on VLAN 20 can't reach the internet but VLAN 10 is fine
use the network-troubleshooter agent — BGP neighbor 10.0.0.2 dropped and won't come back up
```

#### `network-config-reviewer`
Security and correctness audit for router and switch configurations. Checks for open VTY lines, default SNMP communities, missing NTP/logging/banners, undefined ACL references, OSPF without authentication, and more. Returns prioritized findings with severity ratings and exact fix commands.

```
use the network-config-reviewer agent — [paste show running-config output]
```

#### `network-architect`
Enterprise network design from requirements. Takes site count, user scale, application requirements, compliance needs, and budget constraints — outputs a complete design with topology, routing architecture (IGP/BGP), segmentation model, redundancy approach, hardware recommendations, and phased implementation plan.

```
use the network-architect agent — we have 1 HQ, 2 data centers, 40 branches, 3000 users, dual ISP at HQ, PCI compliance required
use the network-architect agent — greenfield DC, 500 servers, 10G to server, 100G spine, tight budget
```

#### `homelab-architect`
Home network design from hardware inventory and goals. Takes your specific devices (UDM, Pi, NAS, switches) and what you want to achieve, and outputs a complete plan: IP scheme, VLAN layout, firewall rules, DNS setup, Wi-Fi SSIDs, static IP assignments, and a phased implementation order with time estimates.

```
use the homelab-architect agent — I have a UniFi Dream Machine, Raspberry Pi 4, and Synology NAS. I want VLANs, Pi-hole, and a guest network
```

---

## What's coming (Batch 2)

Skills:
- `network-ospf-troubleshooting`
- `network-spanning-tree`
- `juniper-junos-patterns`
- `arista-eos-patterns`
- `network-topology-mapping`
- `homelab-proxmox-networking`
- `homelab-prometheus-monitoring`
- `homelab-docker-networking`

Agents:
- `network-migration-planner` — step-by-step change plans with rollback steps and risk assessment
- `cli-translator` — translate commands between Cisco, Juniper, Arista, and VyOS
- `homelab-pihole-setup` — guided interactive Pi-hole installation walkthrough
- `homelab-nas-setup` — guided NAS setup for Synology, TrueNAS, and Linux

---

## These skills are also contributed to

[everything-claude-code](https://github.com/affaan-m/everything-claude-code) — a community collection of Claude Code skills with 140k+ stars.

---

## Built on top of

The technical content in these skills comes from [NetNerd](https://github.com/arsallls/NetNerd) — a self-hosted AI network copilot that connects Claude to real network devices over SSH. Diagnostics, config changes, and topology mapping from a browser. If you want Claude to actually run these commands on your devices instead of just advising you, that's what NetNerd does.

---

## License

MIT — use it, modify it, share it.
