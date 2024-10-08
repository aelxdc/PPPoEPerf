# CMake version
cmake_minimum_required(VERSION 3.5)

project(pppoe_perf C CXX)

enable_testing()

if(NOT CMAKE_BUILD_TYPE)
  set(CMAKE_BUILD_TYPE "Debug")
endif()

set(CMAKE_CXX_FLAGS "-Wall -Wno-unused-local-typedefs -DBOOST_LOG_DYN_LINK -D_GNU_SOURCE -DSESS_BSIZ -std=c++0x -O2")
set(CMAKE_CXX_COMPILER "g++")

set(EXECUTABLE_OUTPUT_PATH ${PROJECT_BINARY_DIR}/bin)
#set(OPENSSL_USE_STATIC_LIBS on)
#set(OPENSSL_ROOT_DIR "/usr")
#set(OPENSSL_LIBRARIES "/usr/include/openssl/")

set(OPENSSL_ROOT_DIR "/usr")
set(OPENSSL_INCLUDE_DIR "/usr/include/openssl")
set(OPENSSL_CRYPTO_LIBRARY "/usr/lib/x86_64-linux-gnu/libcrypto.so")
set(OPENSSL_SSL_LIBRARY "/usr/lib/x86_64-linux-gnu/libssl.so")




find_package (Threads REQUIRED)
find_package (Boost REQUIRED COMPONENTS program_options regex system log_setup log random thread)
find_package (OpenSSL REQUIRED)

include_directories(/usr/include)
include_directories(${Boost_INCLUDE_DIRS})

if((Boost_FOUND) AND (OPENSSL_FOUND))
  add_subdirectory(PPPoEPerf)
endif()
