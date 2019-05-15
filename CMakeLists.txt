cmake_minimum_required(VERSION 3.10)

PROJECT(uWebsockets)

INCLUDE_DIRECTORIES(src)

SET(CMAKE_CXX_FLAGS "-std=c++17 -DLIBUS_NO_SSL -DLIBUS_USE_LIBUV -DUWS_NO_ZLIB")
SET(CMAKE_C_FLAGS  "-std=c11 -DLIBUS_NO_SSL -DLIBUS_USE_LIBUV -DUWS_NO_ZLIB")

ADD_EXECUTABLE(echo_server examples/EchoServer.cpp)

ADD_EXECUTABLE(load_test benchmarks/load_test.c)

TARGET_LINK_LIBRARIES(echo_server usockets)

TARGET_LINK_LIBRARIES(load_test usockets ssl crypto)
