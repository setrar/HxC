# Tooling 

I mostly followed the [medium blog](https://medium.com/@zw3rk/a-haskell-cross-compiler-for-ios-7cc009abe208) more recent [Mobile-Haskell blog](https://codetalk.io/posts/2018-02-07-Mobile-Haskell.html)

I place most of my code in the `~/Developer` folder


:o: Set `path` to use the tool chain wrapper

```
# set paths
export PATH=~/Developer/toolchain-wrapper:$PATH
```


## :a: Toolchain Wrapping 

- [ ] clone `toolchain-wrapper` repository and the run the `bootstrap` script to create the `wrapper` links


```
$ git clone https://github.com/zw3rk/toolchain-wrapper && cd toolchain-wrapper
```

Before generating the wrapper links

```
$ ls -l 
-rw-r--r--  1 valiha  staff   533 Oct  7 22:13 README.md
-rw-r--r--  1 valiha  staff  2466 Oct  7 22:13 android-toolchain.config
-rwxr-xr-x  1 valiha  staff   529 Oct  7 22:13 bootstrap
-rwxr-xr-x  1 valiha  staff  1532 Oct  7 22:13 libtool-lite
-rw-r--r--  1 valiha  staff   121 Oct  7 22:13 linux-android-toolchain.config
-rw-r--r--  1 valiha  staff   289 Oct  7 22:13 raspberrypi-toolchain.config
-rw-r--r--  1 valiha  staff   113 Oct  7 22:13 wasm-toolchain.config
-rwxr-xr-x  1 valiha  staff  4471 Oct  7 22:13 wrapper
```

- [ ] run the `bootsrap` script that will generate wrappers 

```
$ ./bootstrap
```

After generating the wrapper links

```
$ ls -l 
total 72
-rw-r--r--  1 valiha  staff   533 Oct  7 22:13 README.md
lrwxr-xr-x  1 valiha  staff     7 Oct  7 22:14 aarch64-apple-darwin-ar -> wrapper
lrwxr-xr-x  1 valiha  staff     7 Oct  7 22:14 aarch64-apple-darwin-cabal -> wrapper
....
lrwxr-xr-x  1 valiha  staff     7 Oct  7 22:14 x86_64-linux-android-nm -> wrapper
lrwxr-xr-x  1 valiha  staff     7 Oct  7 22:14 x86_64-linux-android-ranlib -> wrapper
```

