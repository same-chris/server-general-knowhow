# Monitoring Server Usage

---

## CPU & Memory — `htop`

`htop` is an interactive process viewer for monitoring CPU and memory usage across all cores.

```bash
htop
```

- Use arrow keys to navigate, `F6` to sort, `q` to quit.

---

## GPU — `nvidia-smi`

`nvidia-smi` shows a snapshot of current GPU usage, memory, and running processes.

```bash
nvidia-smi
```

To watch it update in real time (every 0.5 seconds):

```bash
watch -n 0.5 nvidia-smi
```

- `-n 0.5` sets the refresh interval in seconds. Adjust as needed.
- Press `Ctrl+C` to exit.
