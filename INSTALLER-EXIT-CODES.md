| Network failure | *(not emitted)* | Package is already downloaded before Setup runs |
| Package rejected during installation (security policy) | `1` or `4` | Depends when policy blocks (init vs file write) |

## Miscellaneous failures

Any unexpected failure not listed above should be treated as **non-zero**. Prefer checking logs under the installer’s log path when `/LOG` is supplied.

Recommended optional log switch for IT troubleshooting:

`/VERYSILENT /NORESTART /SUPPRESSMSGBOXES /LOG="%TEMP%\GuestLog-Setup.log"`

## Package URL pattern

`https://github.com/18021985/GuestLog-Releases/releases/download/vX.Y.Z/GuestLog-Setup.exe`

Architecture: **x64**. App type: **EXE**.
