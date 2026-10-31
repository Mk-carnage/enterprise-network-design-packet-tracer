# Day 4 — Device Password Reference

> **Private lab reference · Credentials match the configuration code**

## ⚠️ Lab-only warning

This reference repeats one shared password across all devices, as requested. **Do not use these credentials on real networks, work equipment, cloud services, or public systems.**

## Shared credentials

| Purpose | Username | Password |
|---|---|---|
| SSH / local login | `netadmin` | `NetLab#2026` |
| Privileged EXEC (`enable`) | No username; enter `enable` | `NetLab#2026` |

The configuration uses this value for both `username netadmin ... secret` and `enable secret` on every device.

## Device-by-device credentials

| Device | Role | SSH login | Enable secret |
|---|---|---|---|
| R1 | HQ router | `netadmin` / `NetLab#2026` | `NetLab#2026` |
| R2 | Branch router | `netadmin` / `NetLab#2026` | `NetLab#2026` |
| R3 | Simulated ISP | `netadmin` / `NetLab#2026` | `NetLab#2026` |
| SW1 | HQ switch 1 | `netadmin` / `NetLab#2026` | `NetLab#2026` |
| SW2 | HQ switch 2 | `netadmin` / `NetLab#2026` | `NetLab#2026` |
| SW3 | Branch switch | `netadmin` / `NetLab#2026` | `NetLab#2026` |

## Matching configuration lines

```text
username netadmin privilege 15 secret NetLab#2026
enable secret NetLab#2026
```

At the login or enable prompt, enter the plaintext password shown above. IOS stores `secret` values in hashed/encoded form. `service password-encryption` provides weak obfuscation, not strong protection.

## Keep this file safe

- Keep this file private because it contains reusable credentials.
- Use these credentials only in your isolated Packet Tracer lab.
- For real equipment, use unique, strong passwords per device and a password manager.
- If changing the password, update both matching configuration lines on every device.

## GitHub publishing reminder

**Do not commit this file to a public repository.** Keep it outside the public project folder, or add its filename to `.gitignore` before committing. If these credentials have already been published publicly, change them in the lab configuration and remove the exposed copy from the repository history where appropriate.
