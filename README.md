# claude-network-skills

A collection of Claude Code skills and agents for network engineers and homelab enthusiasts.

**9 skills + 3 agents** covering BGP diagnostics, Cisco IOS patterns, interface health, SSH automation, config validation, and a full homelab track (VLANs, Pi-hole, WireGuard, and more).

These are compatible with [Claude Code](https://claude.ai/code) and any Claude Code-compatible harness (Cursor, OpenCode, etc).

---

## Skills

### Network Engineering

| Skill | What it covers |
|---|---|
| `network-bgp-diagnostics` | BGP neighbor states, stuck sessions (Active/Idle), AS path analysis, route filtering |
| `cisco-ios-patterns` | IOS/IOS-XE config syntax, show commands, wildcard masks, privilege levels, common gotchas |
| `network-interface-health` | CRC errors, input/output drops, duplex mismatches, flap detection, Python counter parsing |
| `netmiko-ssh-automation` | Multi-vendor SSH automation in Python — connect, send commands, batch ops, TextFSM parsing |
| `network-config-validation` | Pre-deployment checks — dangerous commands, syntax validation, subnet overlaps, duplicate IPs |

### Homelab

| Skill | What it covers |
|---|---|
| `homelab-network-setup` | Home network architecture from scratch — IP scheme design, DHCP, hardware selection |
| `homelab-vlan-segmentation` | IoT/guest/trusted VLAN segmentation on UniFi, pfSense, OPNsense, and MikroTik |
| `homelab-pihole-dns` | Pi-hole install, blocklists, DNS-over-HTTPS with cloudflared, local DNS records |
| `homelab-wireguard-vpn` | WireGuard server setup, peer config, split tunneling, DDNS, key generation in Python |

## Agents

| Agent | What it does |
|---|---|
| `network-troubleshooter` | Takes a symptom, walks layer-by-layer diagnosis, produces root cause + next steps |
| `network-config-reviewer` | Audits router/switch configs for security gaps, missing best practices, inconsistencies |
| `homelab-architect` | Takes your hardware + goals, outputs a complete network plan with IP scheme, VLANs, firewall rules |

---

## Installation

### Skills

```bash
# Copy all skills at once
cp -r skills/. ~/.claude/skills/

# Or copy individual skills
cp -r skills/network-bgp-diagnostics ~/.claude/skills/
cp -r skills/homelab-pihole-dns ~/.claude/skills/
```

Skills are loaded automatically by Claude Code when the context matches the "When to Activate" conditions in each skill.

### Agents

```bash
# Copy all agents
cp agents/network-troubleshooter.md ~/.claude/agents/
cp agents/network-config-reviewer.md ~/.claude/agents/
cp agents/homelab-architect.md ~/.claude/agents/
```

Invoke agents directly in Claude Code:
```
use the network-troubleshooter agent — BGP neighbor 10.0.0.2 is showing Active state
use the homelab-architect agent — I have a UDM Pro, 24-port UniFi switch, and a Raspberry Pi 4
```

---

## What these are

These skills package **knowledge** — how to read BGP output, what commands to run, troubleshooting patterns, config best practices. They work in Claude Code, Cursor, or any tool that supports Claude Code skills.

They're also contributed to [everything-claude-code](https://github.com/affaan-m/everything-claude-code).

---

## Built on top of

The technical content in these skills is informed by [NetNerd](https://github.com/arsallls/NetNerd) — a self-hosted AI copilot that connects Claude to real network devices over SSH for live diagnostics, config changes, and topology mapping. If you want Claude to actually SSH into your devices (not just advise you), that's what NetNerd does.

---

## Batch 2 (coming soon)

- `network-ospf-troubleshooting`
- `network-spanning-tree`
- `juniper-junos-patterns`
- `arista-eos-patterns`
- `network-topology-mapping`
- `homelab-proxmox-networking`
- `homelab-prometheus-monitoring`
- `homelab-docker-networking`
- Agents: `network-migration-planner`, `cli-translator`, `homelab-pihole-setup`, `homelab-nas-setup`

---

## License

MIT
