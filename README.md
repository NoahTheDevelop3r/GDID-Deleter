![CleanGDID banner](https://i.ibb.co/SDkC3DPq/cleangdid.jpg)

# CleanGDID

**A simple Windows 10 & 11 privacy cleanup utility focused on GDID artifacts and supported Windows privacy settings.**

CleanGDID is designed to make Windows privacy cleanup straightforward.

Press **Win + R**, launch CleanGDID, and let it:

1. Check your Windows version and configuration.
2. Create a backup of settings it may change.
3. Apply the selected Windows privacy settings.
4. Search for known local GDID-related artifacts.
5. Clean those local artifacts when found.
6. Verify the result.
7. Show you exactly what changed.

The goal is simple:

> **Clean the local data that can be cleaned, keep normal Windows functionality intact, and clearly show you the result.**

---

## Why CleanGDID?

Windows contains several privacy-related settings, diagnostic features, connected experiences, and device-identity components.

CleanGDID brings the relevant cleanup steps into one small utility instead of requiring users to manually search through Windows Settings, Registry locations, and administrative tools.

The project takes inspiration from research projects such as **deGDID**, while keeping its own workflow focused on an approachable Windows privacy cleanup experience.

CleanGDID does not describe ordinary Windows components as malware. Instead, it separates:

* Windows privacy settings;
* optional diagnostic features;
* local device-identity artifacts;
* and unrelated Windows system components.

This makes the cleanup easier to understand and reduces the chance of changing something unrelated to the user's privacy goal.

---

# How it works

CleanGDID follows a simple five-stage process.

```text
             ┌──────────────────┐
             │  Start CleanGDID │
             └────────┬─────────┘
                      ↓
             ┌──────────────────┐
             │ Inspect Windows  │
             │ & privacy state  │
             └────────┬─────────┘
                      ↓
             ┌──────────────────┐
             │ Create a backup  │
             └────────┬─────────┘
                      ↓
             ┌──────────────────┐
             │ Apply privacy    │
             │ configuration    │
             └────────┬─────────┘
                      ↓
             ┌──────────────────┐
             │ Clean local GDID │
             │ artifacts        │
             └────────┬─────────┘
                      ↓
             ┌──────────────────┐
             │ Verify & report  │
             └──────────────────┘
```

### 1. Inspect

CleanGDID first identifies:

* Windows edition;
* Windows build;
* current user context;
* available privacy controls;
* relevant local GDID-related locations;
* whether previous CleanGDID backups exist.

Nothing is changed during this stage.

### 2. Back up

Before making changes, CleanGDID saves the settings it is going to modify.

This gives the user a straightforward way to restore the previous configuration.

### 3. Apply

CleanGDID applies the selected privacy profile.

Depending on Windows version and configuration, this can include settings related to:

* optional diagnostic data;
* Tailored experiences;
* Advertising ID;
* Activity History;
* diagnostic-data controls.

Unsupported settings are simply reported rather than replaced with guesses.

### 4. Clean local GDID artifacts

CleanGDID checks known local locations associated with GDID research.

If a matching local artifact exists, the tool:

```text
Detect
   ↓
Back up
   ↓
Remove
   ↓
Verify
```

Only known, explicitly targeted locations are handled.

### 5. Verify

After cleanup, CleanGDID checks the relevant locations again.

The final report can look like:

```text
CleanGDID
────────────────────────────────

Windows:
  Windows 11 Pro
  Build 26H1

Privacy settings:
  Optional diagnostics       CLEANED
  Tailored experiences       OFF
  Advertising ID             OFF
  Activity History            OFF

GDID:
  Local artifact detected    YES
  Local artifact removed     YES
  Verification                PASS

Backup:
  Created                     YES

System:
  Windows Update              UNCHANGED
  Microsoft Defender          UNCHANGED
  Firewall                    UNCHANGED
  UAC                         UNCHANGED

Result:
  CLEANUP COMPLETE
```

---

# Quick start

CleanGDID is designed around a simple **Win + R** workflow.

Press:

```text
Win + R
```

Then launch the installed utility.

For example:

```text
powershell.exe -NoProfile -Command "Start-Process powershell.exe -Verb RunAs -ArgumentList '-NoProfile -File ""C:\Program Files\CleanGDID\CleanGDID.ps1"" -Apply'"
```

Windows will request administrator approval when required.

After approval, CleanGDID handles the cleanup automatically.

---

# Preview first

If you want to see what CleanGDID would change without applying anything:

```text
Win + R
```

then:

```text
powershell.exe -NoProfile -Command "Start-Process powershell.exe -Verb RunAs -ArgumentList '-NoProfile -File ""C:\Program Files\CleanGDID\CleanGDID.ps1"" -Audit'"
```

This produces a report without modifying the system.

---

# Restore

CleanGDID keeps a backup of the configuration it changes.

To restore the previous state:

```text
Win + R
```

then:

```text
powershell.exe -NoProfile -Command "Start-Process powershell.exe -Verb RunAs -ArgumentList '-NoProfile -File ""C:\Program Files\CleanGDID\CleanGDID.ps1"" -Restore'"
```

CleanGDID restores the saved values instead of trying to guess what Windows' original configuration was.

---

# What gets cleaned?

CleanGDID has two main jobs.

## Windows privacy settings

The default profile can configure supported Windows privacy controls such as:

| Setting                  | CleanGDID action                |
| ------------------------ | ------------------------------- |
| Optional diagnostic data | Reduce where supported          |
| Tailored experiences     | Disable                         |
| Advertising ID           | Disable where supported         |
| Activity History         | Disable where supported         |
| Diagnostic-data cleanup  | Use supported Windows mechanism |

## Local GDID artifacts

CleanGDID also checks known local locations identified through GDID research.

For example, research has identified local identity information associated with:

```text
HKCU\SOFTWARE\Microsoft\IdentityCRL\ExtendedProperties
```

CleanGDID does not assume that this location contains GDID data on every computer.

Instead:

```text
Check → identify → back up → clean → verify
```

That distinction is important because Windows configurations differ between versions and users.

---

# What CleanGDID does not do

CleanGDID does not attempt to remove normal Windows components simply because they are associated with diagnostics or connected experiences.

It leaves core functionality such as:

* Microsoft Defender;
* Windows Firewall;
* Windows Update;
* UAC;
* BitLocker;
* Windows Recovery;
* normal Windows networking

alone.

This makes CleanGDID a **privacy cleanup utility**, rather than a tool that aggressively modifies the operating system.

---

# Does removing a local GDID remove Microsoft's copy?

Not necessarily.

CleanGDID can inspect and remove **local** GDID-related artifacts.

It cannot inspect Microsoft's internal databases or guarantee that a server-side identifier or historical record has been deleted.

Therefore CleanGDID reports:

```text
Local GDID artifact removed
```

rather than making a broader claim such as:

```text
Microsoft no longer has this identifier
```

This makes the result measurable and honest.

---

# Compatibility

CleanGDID targets:

* Windows 10;
* Windows 11;
* 64-bit Windows PowerShell;
* personal or otherwise authorized Windows installations.

The exact privacy controls available can vary between Windows releases and editions.

CleanGDID detects the operating-system version before applying version-dependent settings.

---

# CleanGDID profiles

## PrivacyCleanup

The default profile.

Designed for users who want a straightforward privacy cleanup while keeping normal Windows functionality.

```powershell
.\CleanGDID.ps1 -Profile PrivacyCleanup -Apply
```

## MinimalChanges

Applies only the most direct privacy settings and performs the local GDID cleanup.

```powershell
.\CleanGDID.ps1 -Profile MinimalChanges -Apply
```

## Audit

Read-only inspection.

```powershell
.\CleanGDID.ps1 -Audit
```

## Verify

Checks the current state.

```powershell
.\CleanGDID.ps1 -Verify
```

## Restore

Restores the previous configuration from the CleanGDID backup.

```powershell
.\CleanGDID.ps1 -Restore
```

---

# Project structure

```text
CleanGDID/
├── README.md
├── LICENSE
├── SECURITY.md
├── CHANGELOG.md
│
├── CleanGDID.ps1
│
├── config/
│   └── profiles.json
│
├── docs/
│   ├── WINDOWS-10.md
│   ├── WINDOWS-11.md
│   └── GDID.md
│
└── tests/
    └── CleanGDID.Tests.ps1
```

---

# Logging

CleanGDID stores its local reports under:

```text
%ProgramData%\CleanGDID\
```

For example:

```text
%ProgramData%\CleanGDID\
├── Backups\
├── Logs\
└── Reports\
```

A report records:

```text
Windows version
CleanGDID version
Selected profile
Settings changed
GDID artifacts found
GDID artifacts removed
Verification results
Timestamp
```

Sensitive identifiers should be redacted when reports are shared publicly.

---

# A typical CleanGDID session

For a normal user, the entire process can be as simple as:

```text
Win + R
   ↓
Launch CleanGDID
   ↓
Approve UAC
   ↓
"Checking your system..."
   ↓
"Creating backup..."
   ↓
"Updating privacy settings..."
   ↓
"Checking local GDID data..."
   ↓
"Cleaning local artifacts..."
   ↓
"Verifying..."
   ↓
"CleanGDID completed successfully."
```

There is no need to manually hunt through Registry Editor or disable Windows services one by one.

---

# Why the Win + R launcher?

The Win + R workflow keeps CleanGDID easy to start without requiring a dedicated graphical installer.

It also makes the project convenient for:

* personal PCs;
* troubleshooting;
* privacy maintenance;
* testing;
* virtual machines;
* repeat cleanup after major Windows updates.

The Win + R command is simply a launcher. The actual cleanup logic lives in the open-source PowerShell script.

Users can inspect the script before running it.

---

# Inspired by GDID research

CleanGDID takes inspiration from community research into Windows GDID behavior, particularly projects such as **deGDID**.

That research has helped document:

* local GDID-related identity stores;
* device-identity lifecycle behavior;
* rehydration scenarios;
* the relationship between local state and network activity;
* methods for testing whether local identity state returns.

CleanGDID turns the useful parts of that research into a simpler user-facing workflow:

```text
Research
   ↓
Detect known local state
   ↓
Back up
   ↓
Clean
   ↓
Verify
```

The project does not treat third-party research as official Microsoft documentation. Windows builds can change, so CleanGDID records what it actually observes on the machine.

---

# Verification

A successful cleanup should end with a clear status.

Example:

```text
CLEAN GDID
──────────

Privacy configuration:     PASS
Local GDID cleanup:        PASS
Backup:                    READY
System integrity:          PASS

CleanGDID has finished.
```

If something cannot be changed:

```text
CLEAN GDID

Privacy configuration:     PASS
Local GDID cleanup:        PARTIAL
Backup:                    READY

1 item could not be changed.
See the report for details.
```

This is preferable to reporting success when the tool could not verify the requested operation.

---

# Restore anytime

CleanGDID is designed around reversible changes.

The basic workflow is:

```text
Clean
  ↓
Use Windows normally
  ↓
Restore if desired
```

Restoring returns the settings that CleanGDID changed to the values captured in the backup.

---

# Privacy-focused by design

CleanGDID intentionally avoids making broad claims such as:

* “Windows is completely private now.”
* “All Microsoft tracking has been removed.”
* “Every telemetry component has been deleted.”
* “Microsoft has deleted every record of this device.”

Instead, it reports specific things that can actually be tested on the computer.

For example:

```text
Advertising ID: disabled
Activity History: disabled
Tailored experiences: disabled
Local GDID artifact: removed
Verification: passed
```

That makes the tool useful without promising something a local Windows application cannot prove.

---

# Responsible use

CleanGDID is intended for privacy maintenance on systems you own or are authorized to administer.

It is not intended to interfere with another person's computer or bypass organizational administration.

On a managed work or school computer, CleanGDID should report centrally managed settings rather than attempting to override them.

---

# License

MIT License

Copyright (c) 2026

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, subject to the conditions of the MIT License.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND.
