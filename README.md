# About this repo
This repo is forked from https://github.com/UtsavBalar1231/kernel_xiaomi_sm8250. Thanks to [@UtsavBalar1231](https://github.com/UtsavBalar1231/)!

The main purpose is fix [this battery stuck at 1% problem](https://github.com/liyafe1997/Xiaomi-fix-battery-one-percent), and some small changes and optimizations of defconfig. Also provide KernelSU integrated pre-built image(flashable anykernel3 zip), and a more intuitive and easy-to-use build script and build guide that allow you to try to build by yourself. 

该repo fork自https://github.com/UtsavBalar1231/kernel_xiaomi_sm8250，感谢[@UtsavBalar1231](https://github.com/UtsavBalar1231/)！

主要目的是想修复[电量卡在1%的问题](https://github.com/liyafe1997/Xiaomi-fix-battery-one-percent)，以及defconfig有一些小的改动和优化，以及提供带KernelSU的预编译好的内核（原作的没提供有KernelSU，而且原作release里的lmi内核在我的K30Pro上无法启动，所以就想着自己编译了）。以及再提供一个更直观和易用的编译脚本和README，方便大家自己折腾和修改，编译自己的内核。

# How to build
1. Prepair basic build environment. 
    You have to have the basic common toolchains, like `git`, `make`, `curl`, etc. 
    In Debian/Ubuntu, you can just `sudo apt install build-essential`, In RHEL/RPM based OS, you can `sudo yum groupinstall 'Development Tools'`.

2. Download compiler from Google
    You have to have `aarch64-linux-android`, `arm-linux-androideabi`, `clang`. They are avaliable in these repository:
    https://android.googlesource.com/platform/prebuilts/gcc/linux-x86/aarch64/aarch64-linux-android-4.9
    https://android.googlesource.com/platform/prebuilts/gcc/linux-x86/arm/arm-linux-androideabi-4.9
    https://android.googlesource.com/platform/prebuilts/clang/host/linux-x86

    The branch `android12-gsi` is recommanded. But it just a compiler, it doesn't really tied to any specific Android/Kernel version, so use similar versions should be OK. I don't know the real meaning of "android12-gsi" branch in these compiler's repo is, I guess Google uses that or recommand that for compiling the Android 12 GSI's kernel :) So we can just use that, and I tested that it has no problem. 

    It is recommand to direcly download the tar ball instead of `git clone` these repository, because it is super large and takes a long time. So you can just follow these commands to get the compilers binary.

    ```
    mkdir aarch64-linux-android-4.9
    cd aarch64-linux-android-4.9
    wget https://android.googlesource.com/platform/prebuilts/gcc/linux-x86/aarch64/aarch64-linux-android-4.9/+archive/refs/heads/android12-gsi.tar.gz
    tar xvf android12-gsi.tar.gz
    cd ..

    mkdir arm-linux-androideabi-4.9
    cd arm-linux-androideabi-4.9
    wget https://android.googlesource.com/platform/prebuilts/gcc/linux-x86/arm/arm-linux-androideabi-4.9/+archive/refs/heads/android12-gsi.tar.gz
    tar xvf android12-gsi.tar.gz
    cd ..

    mkdir clang-android
    cd clang-androids
    wget https://android.googlesource.com/platform/prebuilts/clang/host/linux-x86/+archive/refs/heads/android12-gsi.tar.gz
    tar xvf android12-gsi.tar.gz
    cd ..
    ```

3. Set the environment.
    If you followed the above command and downloaded to your home directory, you can directly use this command to put them to the `PATH`, otherwise change to the correct location.
    ```
    export PATH="$HOME/arm-linux-androideabi-4.9/bin:$HOME/aarch64-linux-android-4.9/bin:$HOME/clang-android/clang-r416183b1/bin:$PATH"
    ```

4. Build

    Build without KernelSU: 
    ```
    bash build.sh TARGET_DEVICE
    ```
    
    Build with KernelSU:
    ```
    bash build.sh TARGET_DEVICE ksu
    ```

    For example, build for lmi (Redmi K30 Pro/POCO F2 Pro) without KernelSU:
    ```
    bash build.sh lmi
    ````

    For example, build for umi (Mi 10) with KernelSU:
    ```
    bash build.sh umi ksu
    ```



