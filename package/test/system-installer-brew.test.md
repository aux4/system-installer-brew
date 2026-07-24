# system-installer-brew

These tests verify that the `brew` and `cask` system-package managers route to the
correct `brew` invocation. A fake `brew` executable is placed on `PATH`; it records
the arguments it receives to `$BREW_LOG` so each test can assert the exact command
line — no real Homebrew calls are made. Each test truncates the log first so it sees
only its own invocation.

```file:brew
#!/bin/sh
echo "$@" >> "$BREW_LOG"
```

## brew formula manager

### should run 'brew install <package>' for a formula

```execute
chmod +x brew
export PATH="$PWD:$PATH"
export BREW_LOG="$PWD/brew.log"
rm -f "$BREW_LOG"
aux4 aux4 pkger system brew install wget
cat brew.log
```

```expect
install wget
```

### should run 'brew uninstall <package>' for a formula

```execute
chmod +x brew
export PATH="$PWD:$PATH"
export BREW_LOG="$PWD/brew.log"
rm -f "$BREW_LOG"
aux4 aux4 pkger system brew uninstall wget
cat brew.log
```

```expect
uninstall wget
```

## cask manager

### should run 'brew install --cask <name>' for a cask

```execute
chmod +x brew
export PATH="$PWD:$PATH"
export BREW_LOG="$PWD/brew.log"
rm -f "$BREW_LOG"
aux4 aux4 pkger system cask install chromium
cat brew.log
```

```expect
install --cask chromium
```

### should run 'brew uninstall --cask <name>' for a cask

```execute
chmod +x brew
export PATH="$PWD:$PATH"
export BREW_LOG="$PWD/brew.log"
rm -f "$BREW_LOG"
aux4 aux4 pkger system cask uninstall chromium
cat brew.log
```

```expect
uninstall --cask chromium
```
