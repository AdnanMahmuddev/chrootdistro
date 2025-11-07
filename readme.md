<div align="center">

# Chroot Distro

#### Install Linux distributions on Android devices using chroot

</div>

---

> [!WARNING]
>
> - Root access is required
> - Back up important files before use

---

## Requirements

- Rooted Android Device
- Install the [latest BusyBox for Android NDK by osm0sis](https://github.com/osm0sis/android-busybox-ndk) as a [Magisk module](https://github.com/Magisk-Modules-Repo/busybox-ndk) (**Recommended:** v1.36.1)

> [!TIP]
> If you use KernelSU then there's no need to flash the busybox-ndk module, it already has builtin busybox support

---

## Supported Distributions

- Debian
- Ubuntu
- Fedora
- Arch Linux
- Kali Linux

---

## Quick Start

```bash

# List available distributions
chroot-distro list

# Install a distribution
chroot-distro install debian

# Login to the distribution
chroot-distro login debian
```

---

## Command Reference

| Command       | Aliases                     | Description                  |
| ------------- | --------------------------- | ---------------------------- |
| `help`        | `--help`, `-h`, `he`, `hel` | Display help information     |
| `version`     | `--version`, `-v`           | Show version information     |
| `list`        | `li`, `ls`                  | List available distributions |
| `install`     | `i`, `in`, `ins`, `add`     | Install a distribution       |
| `login`       | `sh`                        | Enter distribution shell     |
| `remove`      | `rm`                        | Remove a distribution        |
| `unmount`     | `umount`, `um`              | Unmount distribution         |
| `clear-cache` | `clear`, `cl`               | Clear downloaded files       |

---

## Commands

### `help`

Display general help or command-specific help information:

```bash
chroot-distro help
chroot-distro <command> --help
```

### `list`

List all available distributions with their aliases, installation status, and additional information:

```bash
chroot-distro list
```

### `install <distro>`

Install a supported distribution:

```bash
chroot-distro install debian
```

### `login <distro>`

Enter a shell session inside the installed distribution:

```bash
chroot-distro login debian
```

#### Available Options

- `--user <username>` – Login as a specified user (user must exist in chroot environment)
- `--termux-home` – Mount Termux home directory inside chroot
- `--bind <host_path>:<chroot_path>` – Bind mount a path from host to chroot
- `--work-dir <path>` – Set custom working directory (default: user's home directory)

#### Execute Commands

Run commands directly inside the chroot environment:

```bash
chroot-distro login debian -- /bin/sh -c 'apt update'
```

Use `--` to separate chroot-distro options from the target command.

### `unmount <distro>`

Unmount all mount points associated with a distribution:

```bash
chroot-distro unmount debian
```

#### Options

- `--help` – Display help for this command

#### Examples

```bash
chroot-distro unmount debian
```

### `remove <distro>`

Permanently remove an installed distribution.

> [!WARNING]
> This operation is irreversible and does not prompt for confirmation.

```bash
chroot-distro remove fedora
```

### `clear-cache`

Remove all downloaded rootfs archives to free up storage space:

```bash
chroot-distro clear-cache
```

---

## Termux Integration

To simplify usage from Termux, create a wrapper script:

1. Open Termux and run:

```bash
nano $PREFIX/bin/chroot-distro
```

2. Paste the following content:

```bash
#!/data/data/com.termux/files/usr/bin/bash

args=""
for arg in "$@"; do
    escaped_arg=$(printf '%s' "$arg" | sed "s/'/'\\\\''/g")
    args="$args '$escaped_arg'"
done

su -c "/system/bin/chroot-distro $args"
```

3. Make the script executable:

```bash
chmod +x $PREFIX/bin/chroot-distro
```

- You can now use chroot-distro directly from Termux without switching to root user manually.

---



## License

This project is licensed under the [GNU General Public License v3.0](https://choosealicense.com/licenses/gpl-3.0/).

## Acknowledgments

This project builds upon the work of:

- [Adnan](https://github.com/adnanmahmuddev)

---


</div>
