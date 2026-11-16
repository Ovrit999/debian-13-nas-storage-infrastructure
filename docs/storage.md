# Hardware and storage notes

## Hardware record

| Item | Record |
|---|---|
| System | Dell OptiPlex 3090 Tower (reported) |
| Storage controller | PCIe SATA expansion card (reported; model/chipset unknown) |
| Drives | Mixed drives (reported; count, model, capacity, and role unknown) |
| Memory / CPU | Unknown |
| Boot device | Unknown |

Record drive role and stable identifiers using sanitized labels such as `data-a`, `data-b`, and `parity-a`. Do not publish serial numbers. Prefer filesystem UUIDs in private configuration; redact them from public examples unless there is a reason to disclose them.

## Mounts and pools

Configured mount points and storage pools are reported, but their paths and membership were not included in the available history. Add an inventory table only after checking the live system:

| Public label | Mount point | Filesystem | Capacity | Role | Verified |
|---|---|---|---:|---|---|
| data-a | `<PRIVATE_MOUNT_PATH>` | `<FILESYSTEM>` | `<SIZE>` | SnapRAID data / mergerfs branch | No |
| data-b | `<PRIVATE_MOUNT_PATH>` | `<FILESYSTEM>` | `<SIZE>` | SnapRAID data / mergerfs branch | No |
| parity-a | `<PRIVATE_MOUNT_PATH>` | `<FILESYSTEM>` | `<SIZE>` | SnapRAID parity, if configured | No |

## SnapRAID and mergerfs considerations

- SnapRAID protects only the files and disks included in its configuration and only to the extent that parity/content data is current and readable.
- SnapRAID sync is generally appropriate after reviewing changes; sync does not substitute for a separate backup.
- Do not run sync or recovery operations until disk mapping and configuration have been checked. A wrong mapping can make recovery harder.
- mergerfs is a union/pooled view of directories. It is not RAID, parity, a backup, or a guarantee that files are balanced across drives.
- Confirm each filesystem is mounted before exposing the pool. A missing mount can cause writes to land on the underlying root filesystem path.
- Document the chosen mergerfs create policy and branch order from the actual configuration rather than assuming defaults.

## Recovery planning

Before a real recovery event, identify the failed device by stable ID and confirm the remaining data and parity are readable. Keep a copy of configuration and a separate backup of irreplaceable data. Document tested recovery steps only after a controlled validation; no recovery test is evidenced in the supplied context.
