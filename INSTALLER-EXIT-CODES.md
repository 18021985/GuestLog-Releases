# Guest Response Log — installer exit codes

Documentation of EXE return codes for the **GuestLog-Setup.exe** Windows installer (Inno Setup), used for Microsoft Partner Center / Store Win32 package submission and silent installs.

Silent install parameters: `/VERYSILENT /NORESTART /SUPPRESSMSGBOXES`

## Standard outcomes

| Scenario | EXE return code | Notes |
|----------|----------------:|-------|
| Installation successful | `0` | Setup completed successfully |
| Installation cancelled by user | `3` | User aborted (Cancel) |
| Setup failed to initialize | `1` | Could not start Setup |
| System requirements not met | `2` | OS / architecture / prerequisites |
| Fatal error during installation | `4` | Abnormal termination / script abort |

## Partner Center scenario mapping

| Partner Center scenario | EXE return code |
|-------------------------|----------------:|
| Installation successful | `0` |
| Installation cancelled by user | `3` |
| Application already exists | `0` | Quiet reinstall / upgrade still reports success |
| Installation already in progress | *(not emitted)* | Windows / MSI mutex; this EXE does not define a dedicated code |
| Disk space is full | `4` | Treated as fatal install error if write fails |
| Reboot required | `0` | `/NORESTART` — reboot deferred; treat as success for silent deploy |
| Network failure | *(not emitted)* | Package is already downloaded before Setup runs |
| Package rejected during installation (security policy) | `1` or `4` | Depends when policy blocks (init vs file write) |

## Miscellaneous failures

Any unexpected failure not listed above should be treated as **non-zero**. Prefer checking logs under the installer’s log path when `/LOG` is supplied.

Recommended optional log switch for IT troubleshooting:

`/VERYSILENT /NORESTART /SUPPRESSMSGBOXES /LOG="%TEMP%\GuestLog-Setup.log"`

## Package URL pattern

`https://github.com/18021985/GuestLog-Releases/releases/download/vX.Y.Z/GuestLog-Setup.exe`

Architecture: **x64**. App type: **EXE**.
