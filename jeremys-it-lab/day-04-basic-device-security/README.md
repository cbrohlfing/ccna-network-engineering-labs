# Day 04 — Basic Device Security

**Course:** Jeremy's IT Lab — CCNA  
**Topic:** Cisco IOS CLI, Device Configuration, and Basic Security  
**Lab Type:** Guided Packet Tracer Exercise  
**Status:** Completed — Configuration Verified  
**Platform:** Cisco Packet Tracer

---

## 1. Lab Overview

This lab introduces basic Cisco IOS command-line configuration and device security using a Cisco router and switch.

The exercise focuses on navigating IOS command modes, configuring device hostnames, securing privileged EXEC access, enabling password encryption, and saving configurations.

Both devices were configured during the guided exercise. Their running and startup configurations were subsequently inspected to verify that the expected settings were present.

## 2. Learning Objectives

- Navigate user EXEC, privileged EXEC, and global configuration modes.
- Configure router and switch hostnames.
- Configure and test an `enable password`.
- Enable password encryption using `service password-encryption`.
- Configure an `enable secret` for privileged EXEC access.
- Understand the security differences between Type 7 encryption and Type 5 password hashing.
- Save configuration changes to NVRAM.
- Verify running and startup configurations.

## 3. Network Topology

The exercise used two Cisco network devices:

| Device | Hostname | Role |
|---|---|---|
| Cisco Router | R1 | Router configuration and security |
| Cisco Switch | SW1 | Switch configuration and security |

This lab focused on local IOS administration rather than IP addressing, routing, or end-to-end connectivity.

**Supporting topology:** A separate topology screenshot is optional because the exercise focuses on device configuration rather than network connectivity.

## 4. Addressing and Design

No IP addressing plan was required for the documented security tasks.

The primary design objective was to apply consistent basic administrative security settings to both devices.

| Configuration | R1 | SW1 |
|---|---|---|
| Hostname | R1 | SW1 |
| Enable password | Configured | Configured |
| Enable secret | Configured | Configured |
| Password encryption | Enabled | Enabled |
| Startup configuration | Verified | Verified |

The exercise intentionally included both `enable password` and `enable secret` to demonstrate their behavior and security differences.

## 5. Implementation

### Accessing Configuration Mode

Cisco IOS uses a hierarchy of command modes:

```text
Router> enable
Router# configure terminal
Router(config)#
```

The `>` prompt indicates user EXEC mode, `#` indicates privileged EXEC mode, and `(config)#` indicates global configuration mode.

### Configuring Device Hostnames

The devices were assigned the following hostnames:

```text
Router(config)# hostname R1
Switch(config)# hostname SW1
```

### Configuring Basic Device Security

The exercise covered the following commands:

```text
enable password <lab-password>
service password-encryption
enable secret <lab-secret>
```

The password values are intentionally omitted from this report.

`service password-encryption` obscures applicable plaintext passwords using reversible Type 7 encryption. This offers limited protection against casual observation.

`enable secret` stores a hashed password and takes precedence over `enable password` when both are configured.

### Saving Configuration Changes

The active configuration is saved using:

```text
copy running-config startup-config
```

This copies the running configuration from RAM into the startup configuration stored in NVRAM.

## 6. Verification and Testing

After completing the guided exercise, the running and startup configurations of both devices were inspected.

### Router R1

Commands used:

```text
show running-config
show startup-config
```

Verified settings:

```text
service password-encryption
hostname R1
enable secret 5 <redacted-hash>
enable password 7 <redacted-value>
```

The expected settings were present in both configurations.

### Switch SW1

Commands used:

```text
show running-config
show startup-config
```

Verified settings:

```text
service password-encryption
hostname SW1
enable secret 5 <redacted-hash>
enable password 7 <redacted-value>
```

The expected settings were present in both configurations.

### Verification Summary

| Verification | R1 | SW1 |
|---|---|---|
| Hostname configured | PASS | PASS |
| Password encryption enabled | PASS | PASS |
| Enable password present | PASS | PASS |
| Enable secret present | PASS | PASS |
| Running configuration inspected | PASS | PASS |
| Startup configuration inspected | PASS | PASS |

**Result:** Both devices contained the expected security settings in their active and saved configurations.

A separate reboot persistence test was not performed during the documented verification.

## 7. Troubleshooting

No unresolved configuration problems were identified during final verification.

The lab reinforced several useful IOS troubleshooting techniques:

- Use `?` to display context-sensitive command help.
- Use `show running-config` to inspect active settings.
- Use `show startup-config` to inspect saved settings.
- Use `do` to execute supported EXEC commands from configuration mode.
- Use `no` before a configuration command to remove or reset the corresponding setting.
- Recognize that `--More--` indicates paginated CLI output.

The exercise also demonstrated why verifying both configuration files matters: a device may be configured correctly in RAM without those changes being saved for the next startup.

## 8. Key Concepts and Lessons Learned

### IOS Command Modes

Cisco IOS separates monitoring and configuration commands into different privilege levels and modes.

Understanding the CLI prompt helps identify which commands are available.

### Configuration Persistence

The running configuration is active in RAM, while the startup configuration is saved in NVRAM.

The command direction is important:

```text
copy running-config startup-config
```

**Source → Destination**

### Password Security

Type 7 password encryption is reversible and should not be considered strong security.

The observed Type 5 `enable secret` uses an MD5-based hash, which is also outdated for modern production security.

The lab demonstrates foundational Cisco IOS behavior rather than a complete production device-hardening procedure.

### Verification as an Engineering Practice

Configuration commands alone do not prove that a task was completed successfully.

Inspecting device state using `show` commands provides evidence that expected settings are present.

## 9. Lab Outcome

**Status: Successfully completed.**

The guided Packet Tracer exercise provided practical experience with Cisco IOS administration and basic device security.

Both R1 and SW1 were verified to contain the expected hostname, password encryption, enable password, and enable secret settings in their running and startup configurations.

This exercise strengthened familiarity with IOS command modes, configuration persistence, and fundamental password security.

## 10. Supporting Files and References

### Lab Files

| File | Description |
|---|---|
| `README.md` | Lab documentation and verification report |
| `day-04-basic-device-security.pkt` | Completed Cisco Packet Tracer project — to be uploaded |

### References

- Jeremy McDowell, *Acing the CCNA Exam, Volume 1: Fundamentals and Protocols*, Chapter 5.
- Jeremy's IT Lab — CCNA Day 04, Basic Device Security Packet Tracer exercise.
- Cisco IOS command-line documentation.

---

**Portfolio:** [CCNA Network Engineering Labs](https://github.com/cbrohlfing/ccna-network-engineering-labs)

**Lab Track:** Jeremy's IT Lab

**Documentation Standard:** Network Engineering Lab Report Standard v1.0
