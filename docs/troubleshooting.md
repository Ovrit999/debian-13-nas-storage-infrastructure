# Troubleshooting guide

These are safe diagnostic directions, not findings about the current host. Capture sanitized output before making changes.

| Symptom | Check | Caution |
|---|---|---|
| A drive is missing | Check controller/PCIe seating, kernel device discovery, and stable device identifiers | Do not identify a disk by `/dev/sdX` alone; never initialize or format an unknown device |
| A filesystem is absent from the pool | Check mount status and the configured source path | Stop writes to the pool until the intended filesystems are mounted |
| Pool appears empty or incomplete | Compare actual mergerfs branches with mounted filesystems and path permissions | Avoid changing branch paths before confirming where existing data resides |
| Samba share is inaccessible | Check service status, share path, account/group permissions, client network path, and logs | Do not solve access issues by making storage world-writable |
| Remote access fails | Confirm device authorization and Tailscale connectivity, then check the service path and policy | Never share auth keys or open SMB to the public internet as a shortcut |
| SnapRAID reports errors | Preserve logs and configuration; verify disk mapping and device health | Avoid sync, fix, or recovery commands until the reported condition is understood |
| SMART warning appears | Identify the physical drive carefully, review health attributes and backups | A failing disk may deteriorate during extended tests; prioritize data safety |

Record symptom, time, sanitized logs, root cause, resolution, and follow-up action. Do not publish IP addresses, serials, or credentials in incident examples.
