export ARCH=arm64 && export SUBARCH=arm64
export PATH="/home/anothermi/proton-clang/bin:$PATH"
export STRIP="/home/anothermi/proton-clang/aarch64-linux-gnu/bin/strip"
make O=out clean && make O=out mrpoper
make tissot_defconfig
make -j$(nproc --all) O=out \
ARCH=arm64 \
AR=llvm-ar \
NM=llvm-nm \
OBJCOPY=llvm-objcopy \
OBJDUMP=llvm-objdump \
STRIP=llvm-strip \
CC=clang \
CROSS_COMPILE=aarch64-linux-gnu- \
CROSS_COMPILE_ARM32=arm-linux-gnueabi- 2>&1
