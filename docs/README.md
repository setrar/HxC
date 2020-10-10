# Update 

I mostly followed the [medium blog](https://medium.com/@zw3rk/a-haskell-cross-compiler-for-ios-7cc009abe208) more recent [Mobile-Haskell blog](https://codetalk.io/posts/2018-02-07-Mobile-Haskell.html)

I place most of my code in the `~/Developer` folder

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


## :b: Prerequisites

- [x] Check if `llvm` is installed

```
% brew list --versions llvm
llvm 10.0.0_3
```

- [ ] otherwise install the latest version

```
$ brew install llvm
```

- [x] Check LLVM

```
% clang --version
Apple clang version 11.0.3 (clang-1103.0.32.62)
Target: x86_64-apple-darwin19.6.0
Thread model: posix
InstalledDir: /Applications/Xcode.app/Contents/Developer/Toolchains/XcodeDefault.xctoolchain/usr/bin
```

```
$ brew info llvm
```

will give the LLVM's location which is generally

```
$ export LLVM_HOME=/usr/local/opt/llvm
```

```
% $LLVM_HOME/bin/clang --version       
clang version 10.0.0 
Target: x86_64-apple-darwin19.6.0
Thread model: posix
InstalledDir: /usr/local/opt/llvm/bin
```

- [ ] Check if `libffi` is installed

`libffi` is usually installed since it is used by cairo, csound, faust, ffmpeg and more

:warning: This version is generally deployed for `X86_64` Architecture

```
% brew list --versions libffi
libffi 3.3
```

- [ ] Capture `ghc` version

```
$ GHC_VERSION=`ghc --version | awk '{print $8}'`
```

```
$  cat $HOME/.ghcup/ghc/${GHC_VERSION}/lib/ghc-${GHC_VERSION}/settings
```

```
$ cabal install happy alex
```

- [ ] Set your PREFIX

```
$ cd ~/Developer/HxC 
```

- [ ] [Getting the sources](https://gitlab.haskell.org/ghc/ghc/-/wikis/building/getting-the-sources)

```
$ git clone --recurse-submodules https://gitlab.haskell.org/ghc/ghc.git && cd ghc
$ git checkout ghc-8.6.5-release
$ git submodule update --init --recursive
```

```
# set paths
export PREFIX=${HOME}/Developer/HxC/build
export PATH=~/Developer/toolchain-wrapper:$PATH
```


- [ ] Clean up the build tree
 
``` 
$ git clean -x -f -d
```

- [ ] Reboot all ??

```
$ ./boot
```



https://github.com/zw3rk/ghc-build-scripts

              
- [ ] use [GNU Autoconf](https://www.gnu.org/software/autoconf/) to generate `make scripts`

To check all optional FEATURES, PACKAGES, TUNING and SYSTEM TYPES (build, host, target), type:

```
% ./configure --help
```

    --build=x86_64-apple-ios \
    --host=x86_64-apple-ios \ 
    --target=aarch64-apple-ios

:x: The GNU Autoconf is critical and generally fails when given wrong information

```
$ export TARGET=aarch64-apple-ios
```

- [ ] Add [LVM](http://llvm.org/docs/GettingStarted.html#id34)  and [LIBFFI](https://sourceware.org/libffi/)to your path and reopen a terminal

```
### LLVM binaries and libraries along with LIBFFI###
export LLVM_HOME="/usr/local/opt/llvm"
export PATH=${LLVM_HOME}/bin:$PATH:

export LBFFI_HOME=/Users/valiha/Developer/HxC/libffi
export LDFLAGS="-L${LLVM_HOME}/lib -L${LIBFFI_HOME}/${TARGET}/lib"
export CPPFLAGS="-I${LLVM_HOME}/include -I${LIBFFI_HOME}/${TARGET}/include"
```


```
%   ./configure \
    --prefix=$PREFIX \
    --with-system-libffi --with-ffi-includes=$LIBFFI_HOME/${TARGET}/include --with-ffi-libraries=$LIBFFI_HOME/${TARGET}/lib \
    --disable-large-address-space \
    --target=${TARGET}
```

  --  Create a mk/build.mk and set the BuildFlavour to quick-cross
```
$  sed -E "s/^#(BuildFlavour[ ]+= quick-cross)$/\1/" mk/build.mk.sample > mk/build.mk
```

```
$ make -j16 && make install
```



https://gitlab.haskell.org/ghc/ghc/-/issues/17174

"Not in scope: type variable `a'" while cross-compiling GHC 8.6.5 for armhf on amd64


[How to catch up my git fork to master](https://garygregory.wordpress.com/2016/11/10/how-to-catch-up-my-git-fork-to-master/)
