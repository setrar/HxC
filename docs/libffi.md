


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
$ LIBFFI_SRC=/User/valiha/Developer/HxC/libffi
```

```
$ ./configure \
     --prefix=$LIBFFI_SRC/aarch64-apple-ios \
     --host=aarch64-apple-ios \
     --enable-static=yes --enable-shared=yes
```

  CC="aarch64-apple-ios-clang" \
  CXX="aarch64-apple-ios-clang" \

```
$ make && make install
```


```
$ git clean -f -x -d
```

```
$ ./autogen.sh
```

  CC="x86_64-apple-ios-clang" \
  CXX="x86_64-apple-ios-clang" \

```
$ ./configure \
     --prefix=$LIBFFI_SRC/x86_64-apple-ios \
     --host=x86_64-apple-ios \
     --enable-static=yes --enable-shared=yes
```

```
$ make && make install
```

