# Data Transfer Guide

This guide covers how to transfer files between your local computer and a remote server.

---

## Copying Files from Local to Server

Run this in your **local computer's terminal**:

```bash
scp -r <local_filepath> <server_name>:<server_filepath>
```

**Example:**

```bash
scp -r ~/my-project/ my_server:/home/user/my-project/
```

---

## Copying Files from Server to Local

### Using `scp`

Run this in your **local computer's terminal**:

```bash
scp -r <server_name>:<server_filepath> <local_filepath>
```

**Example:**

```bash
scp -r my_server:/home/user/results/ ~/results/
```

### Using `rsync` (recommended for large transfers)

`rsync` is preferred for large or incremental transfers — it resumes interrupted transfers and only copies changed files.

```bash
rsync -avP <server_name>:<server_filepath> <local_filepath>
```

**Example:**

```bash
rsync -avP my_server:/home/user/results/ ~/results/
```

#### `rsync` flag breakdown

| Flag | Description |
|------|-------------|
| `-a` | Archive mode — preserves permissions, timestamps, symlinks, etc. |
| `-v` | Verbose — shows files being transferred |
| `-P` | Shows progress and keeps partial files (allows resuming) |

---

## Notes

- Replace `<server_name>` with your actual server hostname or SSH alias (e.g. as configured in `~/.ssh/config`).
- Replace `<local_filepath>` and `<server_filepath>` with the actual paths on your machine and the server respectively.
- The `-r` flag in `scp` copies directories recursively.
