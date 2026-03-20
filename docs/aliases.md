# Useful Shell Aliases

Aliases let you create shorthand commands. Add them to your `~/.bashrc` or `~/.zshrc` and then run `source ~/.bashrc` (or `~/.zshrc`) to apply.

```bash
# File & directory utilities
alias fcnt='ls -l | wc -l'   # count files in current directory
```

---

## Applying Changes

After editing your shell config, reload it:

```bash
source ~/.bashrc   # if using bash
source ~/.zshrc    # if using zsh
```
