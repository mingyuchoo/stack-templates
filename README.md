# stack-templates

Templates for Stack

- `nix-template`: for NixOS
- `new-template`: for others

## Prerequsites

**As of March 2024, there is no lts-22.11 in the NixOS channel.
so an error occurs when running `stack`.

```bash
...
     error: attribute 'ghc964' missing
     at <<string>>:1:43:
...
   Did you mean one of ghc924, ghc94, ghc944, ghc96 or ghc962?
```

To resolve this, change the resolver version
in the `$HOME/.stack/global-project/stack.yaml` file
to the version that exists in the NixOS channel.
For example, it could be `lts-22.6`.**


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

# Latest version support by NixOS below
resolver: lts-22.6

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

## Basic Stack Commands

```bash
$ stack new <project-name>
# or
$ stack new <project-name> quanterall/basic

$ stack build --test --file-watch --watch-all
# or
# build more faster
$ stack build --fast --file-watch --ghc-options "-j4 +RTS -A128m -n2m -RTS"

$ stack test --file-watch --watch-all
# or
# test automatically
$ ghcid --command "stack ghci test/Spec.hs"

# https://docs.haskellstack.org/en/stable/build_command/
$ stack test --coverage --fast --file-watch --watch-all --haddock

$ stack run
```

## Reformat using Stylish-haskell

```bash
$ stylish-haskell -ri **/*.hs
```

## Tips and Tech

### `haskell-language-server` doesn't run in Emacs

When developing Haskell code using Emacs, an error may occur in haskell-language-server.
In that case, the error will be resolved by installing haskell-language-server,
which is the same as the GHC version, in the lsp-haskell settings in `.emacs` and setting the path correctly.
