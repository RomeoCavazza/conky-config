# Conky

[![CI](https://github.com/RomeoCavazza/conky-config/actions/workflows/ci.yml/badge.svg)](https://github.com/RomeoCavazza/conky-config/actions/workflows/ci.yml)

<p align="left">
  <img src="assets/conky.png" alt="Conky" width="26" />
  <img src="assets/hyprland.png" alt="Hyprland" height="22" />
  <img src="https://raw.githubusercontent.com/RomeoCavazza/nixos-config/refs/heads/main/docs/assets/logo/nvidia.svg" alt="NVIDIA" width="26" />
</p>

Transparent Conky side rails for the Hyprland desktop. The layout keeps live
system telemetry on the edges of the workspace while leaving the center free
for windows.

The launcher starts both rails. When launched from Home Manager, it can resolve
the repository checkout through `NIXOS_CONFIG_REPO`; otherwise it falls back to
its own directory:

```sh
start_edex_conky_compact.sh
```

From Hyprland, the configured toggle is:

```sh
edex-conky-toggle
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

- **Session**: time, timezone, battery, host, user, kernel, uptime, and external
  IP.
- **Network**: interface detection via [`net_iface.sh`](scripts/net_iface.sh),
  packet counters via [`net_packets.sh`](scripts/net_packets.sh), throughput via
  [`net_rx_kib.sh`](scripts/net_rx_kib.sh) and
  [`net_tx_kib.sh`](scripts/net_tx_kib.sh), plus graph helpers
  [`net_rx_graph.sh`](scripts/net_rx_graph.sh) and
  [`net_tx_graph.sh`](scripts/net_tx_graph.sh).
- **CPU**: total load, per-core bars, process count, and top CPU processes.
- **Memory**: RAM, swap, cache, and top memory processes.
- **Storage**: root and home usage plus disk I/O via
  [`disk_io_kib.sh`](scripts/disk_io_kib.sh) and
  [`disk_io_graph.sh`](scripts/disk_io_graph.sh).

### Ops Panel

The right rail keeps operational signals visible:

- **GPU**: NVIDIA device name via [`gpu_name.sh`](scripts/gpu_name.sh), live
  metrics via [`gpu_info.sh`](scripts/gpu_info.sh), and graph helpers
  [`gpu_util_graph.sh`](scripts/gpu_util_graph.sh),
  [`gpu_mem_graph.sh`](scripts/gpu_mem_graph.sh), and
  [`gpu_power_graph.sh`](scripts/gpu_power_graph.sh).
- **Thermals**: CPU temperature via [`cpu_temp_c.sh`](scripts/cpu_temp_c.sh)
  and GPU temperature via [`gpu_info.sh`](scripts/gpu_info.sh).
- **Network Health**: ping latency via [`ping_ms.sh`](scripts/ping_ms.sh),
  established connections, and TIME-WAIT sockets.
- **System Health**: load average, failed units, user count, and running
  process count.
- **NixOS**: store size via [`nix_store_size.sh`](scripts/nix_store_size.sh),
  current system generation, and retained generations.
