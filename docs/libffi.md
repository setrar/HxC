


```
$ cd ~/Developer
```


```
$ git clone https://github.com/libffi/libffi.git && cd libffi
```

```
$ ./autogen.sh
```

```
$ LIBFFI_HOME=${HOME}/Developer/HxC/libffi
```

- [x] Working

```
$ SDK="iphoneos" \
  CHOST="arm-apple-darwin" \
  CC=$(xcrun --find --sdk "${SDK}" gcc) CXX=$(xcrun --find --sdk "${SDK}" g++) \
  ./configure \
     --prefix=$LIBFFI_HOME/${CHOST} \
     --host=${CHOST} \
     --enable-static=yes --enable-shared=yes
```


- [ ] Working

```
$  CC="aarch64-apple-ios-clang" CXX="aarch64-apple-ios-clang" \
   ./configure \
     --prefix=$LIBFFI_HOME/aarch64-apple-ios \
     --host=aarch64-apple-ios \
     --enable-static=yes --enable-shared=yes
```

```
$ make -j && make install
```

```
$ git clean -f -x -d
```

```
$ ./autogen.sh
```

  CC="x86_64-apple-ios-clang" CXX="x86_64-apple-ios-clang" \

```
$ ./configure \
     --prefix=$LIBFFI_HOME/x86_64-apple-ios \
     --host=x86_64-apple-ios \
     --enable-static=yes --enable-shared=yes
```

```
$ make -j && make install
```

# References

https://stackoverflow.com/questions/26812060/cross-compile-to-static-lib-libgcrypt-for-use-on-ios/26812514#26812514
