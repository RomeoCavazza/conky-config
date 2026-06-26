# Conky Rails

Transparent Conky side rails for the Hyprland desktop. The layout keeps live
system telemetry on the edges of the workspace while leaving the center free
for windows.

The launcher starts both rails and prefers the repository copy when available:

```sh
/etc/nixos/config/conky/start_edex_conky_compact.sh
```

From Hyprland, the configured toggle is:

```sh
/etc/nixos/config/bin/edex-conky-toggle
```

The toggle makes Conky, Rofi, and the Hyprspace overview mutually exclusive. It
also adjusts workspace gaps while the rails are visible, then restores the
previous gap state when Conky exits.

| Path | Role |
| --- | --- |
| [`conky-left.txt`](conky-left.txt) | Desktop information and resource rail |
| [`conky-right.txt`](conky-right.txt) | GPU, thermals, network health, and NixOS rail |
| [`start_edex_conky_compact.sh`](start_edex_conky_compact.sh) | Starts both rails and warms script caches |
| [`scripts/`](scripts/) | Metric helpers for GPU, CPU temp, network, disk, ping, and Nix store |
| [`assets/`](assets/) | README screenshots |

## Previews

### Empty Workspace

No window is open; the rails sit directly on the desktop.

![Empty workspace](assets/empty.png)

### Active Workspace

The same rails with an editor window open in the center.

![Active workspace](assets/full.png)

## Panels

### Desktop Info

The left rail focuses on local desktop state and host resources:

- time, timezone, battery, host, user, kernel, uptime, and external IP
- network interface, packet counters, upload and download graphs
- CPU load, per-core bars, top CPU processes
- RAM, swap, cache, top memory processes
- root, home, and disk I/O usage

### Ops Panel

The right rail keeps operational signals visible:

- NVIDIA GPU name, utilization, VRAM, temperature, power, and clocks
- CPU and GPU thermals
- ping, established connections, and TIME-WAIT sockets
- system load, failed units, user count, and running processes
- Nix store size, current system generation, and retained generations
