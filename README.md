# stack-templates

Templates for Stack

- `nix-template`: for NixOS
- `new-template`: for others

## How to use stack templates

### NixOS

```bash
stack new <project-name> mingyuchoo/nix-template
```

### Others

```bash
stack new <project-name> mingyuchoo/new-template
```

## How to upgrade versions of GHC and `base` package

### How to upgra GHC

Check the current ghc version

```bash
ghc-pkg --version
```

Update `resolver` in `stack.yaml` file

```yaml
...
resolver: lts-22.11
...
```

### How to upgrade `base` package

Check the current `base` package version

```bash
ghc-pkg list base
```

Update `base` version in `dependencies` in `package.yaml` file

```yaml
...
dependencies:
- base >= 4.18 && < 5
...
```
