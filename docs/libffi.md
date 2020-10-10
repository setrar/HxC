


```
$ cd ~/Developer
```

Set destination folder upfront

```
$ LIBFFI_HOME=${HOME}/Developer/HxC/libffi
```


```
$ git clone https://github.com/libffi/libffi.git && cd libffi
```

```
$ ./autogen.sh
```



- [x] Working

```
$ CC=$(xcrun --find --sdk "iphoneos" gcc) CXX=$(xcrun --find --sdk "iphoneos" g++) \
  ./configure \
     --prefix=${LIBFFI_HOME}/aarch64-apple-ios \
     --host=aarch64-apple-ios \
     --enable-static=yes --enable-shared=yes
```


- [ ] Working

```
$  CHOST="aarch64-apple-ios" \
   CC="aarch64-apple-ios-clang" CXX="aarch64-apple-ios-clang" \
   ./configure \
     --prefix=$LIBFFI_HOME/${CHOST} \
     --host=${CHOST} \
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

- [x] Working

```
$ CC=$(xcrun --find --sdk "iphonesimulator" g++) CXX=$(xcrun --find --sdk "iphonesimulator" g++) \
  ./configure \
     --prefix=${LIBFFI_HOME}/x86_64-apple-ios \
     --host=x86_64-apple-ios \
     --enable-static=yes --enable-shared=yes
```

- [x] Working  

```
$ CC="x86_64-apple-ios-clang" CXX="x86_64-apple-ios-clang" \
  ./configure \
     --prefix=$LIBFFI_HOME/x86_64-apple-ios \
     --host=x86_64-apple-ios \
     --enable-static=yes --enable-shared=yes
```

```
$ make -j && make install
```

# References

https://stackoverflow.com/questions/26812060/cross-compile-to-static-lib-libgcrypt-for-use-on-ios/26812514#26812514
