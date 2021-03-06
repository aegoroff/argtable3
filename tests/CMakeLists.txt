cmake_minimum_required(VERSION 3.2)
project(tests)

include_directories("..")

if("${CMAKE_CXX_COMPILER_ID}" STREQUAL "MSVC")
    set(CMAKE_CXX_FLAGS_RELEASE  "/MP /Zc:wchar_t /Zc:inline /MT /Ox /Ob2 /Oy /Oi /Ot /GL /D NDEBUG")
    set(CMAKE_C_FLAGS_RELEASE  "/MP /Zc:wchar_t /Zc:inline /MT /Ox /Ob2 /Oy /Oi /Ot /GL /D NDEBUG")
    set(CMAKE_CXX_FLAGS_DEBUG  "/MP /Zc:wchar_t /Zc:inline /MTd /Od")
    set(CMAKE_C_FLAGS_DEBUG  "/MP /Zc:wchar_t /Zc:inline /MTd /Od")
    if(CMAKE_BUILD_TYPE STREQUAL "Debug")
    else()
        set(CMAKE_EXE_LINKER_FLAGS "${CMAKE_EXE_LINKER_FLAGS} /LTCG")
        set(CMAKE_STATIC_LINKER_FLAGS "${CMAKE_STATIC_LINKER_FLAGS} /LTCG")
    endif()
else()
    set(CMAKE_CXX_FLAGS_RELEASE  "-Wall -Ofast -mfpmath=both")
    set(CMAKE_CXX_FLAGS_DEBUG  "-Wall -mfpmath=both")
endif()

file(GLOB TEST_SOURCE_FILES "*.c")
file(GLOB LIB_SOURCE_FILES "../*.c")

add_executable(tests ${TEST_SOURCE_FILES} ${LIB_SOURCE_FILES})
