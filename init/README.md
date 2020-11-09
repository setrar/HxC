# Cross Compiling 

## Creating a sandbox:

## :one: GHC

Using [`gchcup`](https://www.haskell.org/ghcup/)

```
% ghcup --version
The GHCup Haskell installer, version v0.1.9
```

- [ ] Changing version

use:

```
% ghcup tui
```

## :two: [xcode-select](https://stackoverflow.com/questions/9600615/xcode-stops-working-after-set-xcode-select-switch) switch

```
% xcode-select --print-path
/Applications/Xcode.app/Contents/Developer
```

Switch to another version

```
% sudo xcode-select --switch /Applications/Xcode.app/Contents/Developer
```
