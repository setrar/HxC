# HxC
Haskell Cross Compiler

This is an attempt to understand the Haskell Cross Compiler blog written by [zw3rk](https://github.com/zw3rk)

https://medium.com/@zw3rk/a-haskell-cross-compiler-for-ios-7cc009abe208

Also see the toolchain wrapper

https://github.com/zw3rk/toolchain-wrapper

```
$ git clone --recurse-submodules https://gitlab.haskell.org/ghc/ghc.git
```

## Cross Compiling Euterpea Links


https://gitlab.haskell.org/ghc/ghc/-/wikis/building/cross-compiling

http://donyaquick.com/running-haskell-on-linux-on-android/

https://gitlab.haskell.org/ghc/ghc/-/wikis/building/cross-compiling/iOS

https://medium.com/@zw3rk/a-haskell-cross-compiler-for-ios-7cc009abe208

https://github.com/setrar/toolchain-wrapper


## Games on iPhone

https://github.com/ivanperez-keera/haskanoid

```
$ cabal install --flags="-kinect -wiimote"
```

```
$ brew install sdl sdl_image sdl_mixer sdl_ttf
```

```
cabal install \
       --extra-include-dirs=/usr/local/Cellar/sdl/1.2.15_2/include \
       --extra-include-dirs=/usr/local/Cellar/sdl_image/1.2.12_7/include/SDL \
       --extra-include-dirs=/usr/local/Cellar/sdl_mixer/1.2.12_4/include/SDL \
       --extra-include-dirs=/usr/local/Cellar/sdl_ttf/2.0.11_1/include \
       --extra-lib-dirs=/usr/local/Cellar/sdl_image/1.2.12_7/lib/ \
       --ghc-options=-optP-D_SDL_main_h SDL-image-0.6.1.2
```

