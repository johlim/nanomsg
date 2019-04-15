cmake example for embed

# prepare crosscompile setting

cat arm-cortex_a9-linux-gnueabi.cmake

#CROSS COMPILE EXAMPLE
set(CMAKE_CXX_COMPILER  /opt/crosstools/arm-cortex_a9-eabi-4.7-eglibc-2.18/bin/arm-cortex_a9-linux-gnueabi-g++)
set(CMAKE_C_COMPILER  /opt/crosstools/arm-cortex_a9-eabi-4.7-eglibc-2.18/bin/arm-cortex_a9-linux-gnueabi-gcc)
set(CMAKE_FIND_ROOT_PATH  /opt/crosstools/arm-cortex_a9-eabi-4.7-eglibc-2.18/arm-cortex_a9-linux-gnueabi/sysroot/ )
# search for programs in the build host directories
SET(CMAKE_FIND_ROOT_PATH_MODE_PROGRAM NEVER)
# for libraries and headers in the target directories
SET(CMAKE_FIND_ROOT_PATH_MODE_LIBRARY ONLY)
SET(CMAKE_FIND_ROOT_PATH_MODE_INCLUDE ONLY)


cd nanomsg/demo
mkdir build
cd build
cmake -DCMAKE_INSTALL_PREFIX=/opt/crosstools/arm-cortex_a9-eabi-4.7-eglibc-2.18/arm-cortex_a9-linux-gnueabi/sysroot/usr/ -DLIBINSTALL_DIR=/opt/crosstools/arm-cortex_a9-eabi-4.7-eglibc-2.18/arm-cortex_a9-linux-gnueabi/sysroot/usr/lib -DCMAKE_TOOLCHAIN_FILE=~/CROSSCOMPILETIP/arm-cortex_a9-linux-gnueabi.cmake .. 
cmake --build .


ls  *_demo
async_demo  device_demo  pthread_demo  pubsub_demo  rpc_demo

cp libnanomsg.so libnanomsg.so.5 libnanomsg.so.5.1.0 to embed machine
cp async_demo  device_demo  pthread_demo  pubsub_demo  rpc_demo to embed machine

and  run like this
0. connect embed machine and setup runtime env 
   ( export LD_LIBRARY_PATH=/mnt/nand1/lib:/mnt/nand1/usr/lib://mnt/nfs/nand1/usr/lib )
1. pthread_demo  ipc:///tmp/survey.ipc -s
2. pthread_demo  ipc:///tmp/survey.ipc client
