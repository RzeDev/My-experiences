# 1- RPM-Based Distributions:

### 001- Package Verification (`rpm`)

```bash
rpm -V sudo
```

### Verification Output Codes

| Code | Meaning |
|:----:|----------|
| `?` | Unable to perform verification tests |
| `5` | Digest number has changed |
| `c` | File is a configuration file |
| `D` | Device number (major or minor) has changed |
| `G` | Group ownership has changed |
| `L` | Symbolic link path has changed |
| `missing` | File is missing |
| `M` | File mode (permissions or type) has changed |
| `P` | File capabilities have changed |
| `S` | File size has changed |
| `T` | Modification timestamp has changed |
| `U` | User ownership has changed |

> NOTE:
> If the command produces **no output**, the package has passed all verification checks and no problems were detected.

---

## 002- YUM Commands:

| Command | Description |
|----------|-------------|
| `check-update` | Checks repositories for package updates |
| `clean` | Removes cached files downloaded during installations |
| `deplist` | Displays package dependencies |
| `groupinstall` | Installs a package group |
| `info` | Displays package information |
| `install` | Installs a package |
| `list` | Lists installed or available packages |
| `localinstall` | Installs a local RPM package |
| `localupdate` | Updates packages from local RPM files |
| `provides` | Finds which package owns a file |
| `reinstall` | Reinstalls a package |
| `remove` | Removes a package |
| `resolvedep` | Resolves dependencies |
| `search` | Searches package names and descriptions |
| `shell` | Starts interactive YUM shell |
| `update` | Updates package(s) |
| `upgrade` | Updates packages and removes obsolete ones |

---
