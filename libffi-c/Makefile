TOOLPATH = ${LVM_HOME}/bin
LIBFFI_HOME = ../libffi
ARCH = x86_64
ARCH_FLAGS = -arch ${ARCH} -sdk_version 8
TARGET = ${ARCH}-apple-ios


CFLAGS=-I ${LLVM_HOME}/include -I ${LIBFFI_HOME}/${TARGET}/include
LFLAGS=-L ${LLVM_HOME}/lib -L ${LIBFFI_HOME}/${TARGET}/lib

ffi_closure_alloc_test: ffi_closure_alloc_test.o
	$(TOOLPATH)/ld64.lld -o ffi_closure_alloc_test ${ARCH_FLAGS} ${LFLAGS} ffi_closure_alloc_test.o

ffi_closure_alloc_test.o: ffi_closure_alloc_test.c
	$(TOOLPATH)/clang -o ffi_closure_alloc_test.o ${CFLAGS} ffi_closure_alloc_test.c
