# This for Proton Clang

#### For example, i will compile kernel for ```tissot```
### First

Export your device arch

#### For ```arm64``` device
    export ARCH=arm64 && export SUBARCH=arm64
#### For ```arm32``` device
    export ARCH=arm32 && export SUBARCH=arm32
#### Export your ```clang```
    export PATH="/home/kakashi/proton-clang/bin:$PATH"
#### Export the ```strip``` 
    export STRIP="/home/kakashi/proton-clang/aarch64-linux-gnu/bin/strip"
    
### If you never ccompile kernel before (it's first time), skip this step, go to defconfig

    make O=out clean && make O=out mrpoper
    
###  Make your ```device_defconfigs```

    make tissot_defconfig O=out

### Let compile the kernel

    make -j$(nproc --all) O=out \
    ARCH=arm64 \
    AR=llvm-ar \
    NM=llvm-nm \
    OBJCOPY=llvm-objcopy \
    OBJDUMP=llvm-objdump \
    STRIP=llvm-strip \
    CC=clang \
    CROSS_COMPILE=aarch64-linux-gnu- \
    CROSS_COMPILE_ARM32=arm-linux-gnueabi-
