# Fix: Slow Training Loops (DataLoader CPU Affinity)

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
