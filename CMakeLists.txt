CMAKE_MINIMUM_REQUIRED(VERSION 3.0 FATAL_ERROR)
PROJECT("CppConcurrencyInAction")

ADD_COMPILE_OPTIONS(-std=c++11 -pthread)
SET(CMAKE_EXPORT_COMPILE_COMMANDS 1)
MESSAGE("${CMAKE_CXX_COMPILER_ID}")

IF("${CMAKE_CXX_COMPILER_ID}" STREQUAL "GNU")
    SET(WARNINGS "-Wall -Wextra")
ELSEIF("${CMAKE_CXX_COMPILER_ID}" MATCHES "Clang")
    SET(WARNINGS "-Weverything -Wall -Wextra -Wno-c++98-compat \
            -Wno-c++98-compat-pedantic -Wno-padded -Wno-global-constructors \
            -Wno-exit-time-destructors -Wno-newline-eof -Werror")
ENDIF()
IF(NOT CONFIGURED_ONCE)
    SET(CMAKE_CXX_FLAGS "${WARNINGS}"
        CACHE STRING "Flags used by the compiler during all build types."
        FORCE)
ENDIF(NOT CONFIGURED_ONCE)

ADD_EXECUTABLE(HelloConcurrentWorld
    chapter_01_hello_world_of_concurrency_in_cpp/HelloConcurrentWorld.cpp)

SET(CONFIGURED_ONCE TRUE CACHE INTERNAL
        "A flag showing that CMake has configured at least once.")
