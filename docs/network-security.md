# Network and security

## Reported components

Tailscale remote access and Samba file sharing are part of the project context. No private IPs, subnet, DNS names, port-forwarding rules, firewall rules, share names, user names, or Tailscale ACLs were available to verify.

## Documentation checklist

- Record whether SMB is reachable only on the intended LAN and/or through the private Tailscale network.
- Use named users/groups and least-privilege filesystem permissions; avoid guest write access unless there is a documented need.
- Keep SMB credentials out of the repository. Store secrets in local protected files or a secrets manager.
- Review Tailscale device authorization and access policy; do not publish auth keys, node keys, recovery codes, or account identifiers.
- Do not expose SMB directly to the public internet. Document any firewall behavior from actual configuration.
- Apply Debian security updates through a defined maintenance process and record reboot requirements.
- Limit administrative access, use SSH keys where applicable, and document the actual SSH hardening state rather than assumed settings.
- Back up Samba, mount, mergerfs, and SnapRAID configuration separately from the storage pool.

## Sanitization before publishing

Replace real addresses with examples such as `192.0.2.0/24` or `<LAN_SUBNET>`. Remove host-specific identifiers, serials, usernames, domain names, keys, passwords, tokens, and Tailscale device details. Inspect commit history and screenshots too; removing a secret from the latest file does not remove it from old commits.

## Security status

The supplied history does not establish firewall policy, access control, encryption, update automation, backup coverage, or remote-access ACL posture. Mark these as unknown until verified.
