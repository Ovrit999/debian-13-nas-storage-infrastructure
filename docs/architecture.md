# Architecture and project status

## Purpose

Provide centralized file storage from a headless Debian 13 host, with an aggregated filesystem view, parity protection for selected data, SMB access, remote connectivity, and drive health monitoring. These are the documented design goals and project components; their current operational state has not been verified.

## Component roles

| Component | Intended role | Evidence still needed |
|---|---|---|
| Debian 13 | Base server operating system | `cat /etc/os-release`, update cadence |
| mergerfs | Presents configured directories as a pooled namespace | Mount source, options, branch order, write policy, mount persistence |
| SnapRAID | Parity and recovery for selected data disks | Config, parity/content files, disk mapping, last sync/scrub status |
| Samba | SMB file sharing to authorized clients | Share definitions, users/groups, protocol and access policy |
| Tailscale | Private remote network path | Device approval, ACL/grants, route and DNS settings |
| smartmontools | Drive health visibility | Enabled services, tests, alert destination and latest results |
| PCIe SATA card | Adds storage connectivity | Exact controller/chipset, driver, attached drive mapping |

## Data path (conceptual)

1. Local or authorized remote clients reach Samba over the applicable network path.
2. Samba exposes only intended paths and permissions.
3. mergerfs presents selected mounted data directories as one namespace.
4. SnapRAID tracks configured data disks and parity separately; it is not a live mirror.
5. SMART monitoring can surface device health changes but cannot prevent every failure.

No routing, firewall, VLAN, port-forwarding, or LAN topology is asserted here. Confirm each from the host and network configuration before adding detail.

## Status labels for future edits

- **Verified:** captured from the live host and checked against expected behavior.
- **Reported:** described in project history but not independently confirmed in this documentation pass.
- **Planned:** intended but not yet implemented.
- **Unknown:** evidence is not available.

For portfolio credibility, add dated evidence such as sanitized command output, configuration excerpts, and test results. Do not mark a component verified based only on package installation.
