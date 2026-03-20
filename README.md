# Server Data Transfer Guide

This guide covers how to transfer files between your local computer and a remote server.

---

## Copying Files from Local to Server

Run this in your **local computer's terminal**:

```bash
scp -r <local_filepath> <server_name>:<server_filepath>
```

**Example:**

```bash
scp -r ~/my-project/ <server_name>:/home/user/my-project/
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
scp -r <server_name>:/home/user/results/ ~/results/
```

### Using `rsync` (recommended for large transfers)

`rsync` is preferred for large or incremental transfers — it resumes interrupted transfers and only copies changed files.

```bash
rsync -avP <server_name>:<server_filepath> <local_filepath>
```

**Example:**

```bash
rsync -avP <server_name>:/home/user/results/ ~/results/
```

#### `rsync` flag breakdown

| Flag | Description |
|------|-------------|
| `-a` | Archive mode — preserves permissions, timestamps, symlinks, etc. |
| `-v` | Verbose — shows files being transferred |
| `-P` | Shows progress and keeps partial files (allows resuming) |

---

## Fix: Slow Training Loops (DataLoader CPU Affinity)

If you're experiencing slow training loops when using multiple DataLoader workers, the issue may be that all workers get pinned to a single CPU core instead of being distributed across cores.

To fix this, add the following worker init function and pass it to your `DataLoader`:

```python
import os

def _reset_worker_affinity(_worker_id: int):
    try:
        os.sched_setaffinity(0, set(range(os.cpu_count() or 1)))
    except Exception:
        pass
```

Then pass it to your `DataLoader`:

```python
DataLoader(..., num_workers=..., worker_init_fn=_reset_worker_affinity)
```

This resets each worker's CPU affinity to allow it to run on any available core.

---

## Notes

- Replace `<server_name>` with your actual server hostname or SSH alias (e.g. as configured in `~/.ssh/config`).
- Replace `<local_filepath>` and `<server_filepath>` with the actual paths on your machine and the server respectively.
- The `-r` flag in `scp` copies directories recursively.
