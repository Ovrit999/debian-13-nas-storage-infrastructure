# Setup and verification workflow

This is a documentation checklist, not a copy-paste installation recipe. The actual disk map, mount points, package state, and service settings are unknown. Never apply storage commands without adapting and reviewing them for the host.

## 1. Capture a sanitized baseline

On the server, collect operating system release, hostname, block-device model/size (without serials), filesystem types, mounts, enabled services, and relevant configuration. Redact identifiers and addresses before saving output in this public repository. Confirm whether the active hostname is `nasjason`; `nasjson` appears in earlier project context as an alternate spelling.

## 2. Confirm disks and filesystems

Map each physical disk to a stable device path, filesystem, UUID, mount point, and intended role. Verify expansion-card visibility and controller behavior after reboot. Never assume `/dev/sdX` letters remain stable.

## 3. Confirm persistent mounts

Review the real `/etc/fstab` and mount options. Verify each data and parity filesystem mounts correctly after a reboot before enabling services that use it. The example in `examples/fstab.example` is a placeholder only.

## 4. Review storage configuration

Review mergerfs branches and policy, then inspect SnapRAID data/parity/content mappings. Verify the pool does not hide an absent mount. Confirm sync/scrub schedule, logs, and alerting from the real setup. Do not invent a `snapraid sync` workflow or claim parity health without evidence.

## 5. Review sharing and remote access

Check Samba shares and filesystem ownership with a non-admin client. Confirm access from intended LAN devices and (if configured) authorized Tailscale devices. Check that unintended users cannot read or write shares.

## 6. Verify monitoring and recovery

Confirm smartmontools is active and reports the expected devices; document test cadence and alert destination. A SMART pass is not a backup. Document an independent backup and a tested restore/recovery procedure before claiming resilience.

## Evidence to add

- Sanitized inventory and mount table, with date and host identifiers removed.
- Sanitized SnapRAID/mergerfs/Samba excerpts, showing placeholders for secrets and identifiers.
- Results of client access checks, reboot/mount checks, and monitoring checks.
- A recovery exercise record and independent backup restore evidence.

Do not include credentials, private keys, Tailscale keys, serial numbers, or private network details.
