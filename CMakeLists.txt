#
# Copyright (C) 2017 yumo
#


# Define project
# project(folly)

set(VERSION_MAJOR 57)
set(VERSION_MINOR 0)
set(VERSION_MICRO 0)
set(VERSION_PATCH 0)

cmake_minimum_required(VERSION 2.8.12)

set(CMAKE_MODULE_PATH "${CMAKE_CURRENT_SOURCE_DIR}/cmake-scripts")

# Required packages
set(CMAKE_THREAD_PREFER_PTHREAD TRUE)
find_package(Threads REQUIRED)

set(Boost_USE_STATIC_LIBS ON)
set(Boost_USE_MULTITHREADED ON)

find_package(Boost 1.60.0 COMPONENTS context filesystem program_options regex system thread REQUIRED)

set(FOLLY_HAVE_BOOST True)
set(FOLLY_HAVE_BOOST_CONTEXT True)
set(FOLLY_HAVE_BOOST_FILESYSTEM True)
set(FOLLY_HAVE_BOOST_PROGRAM_OPTIONS True)
set(FOLLY_HAVE_BOOST_REGEX True)
set(FOLLY_HAVE_BOOST_SYSTEM True)
set(FOLLY_HAVE_BOOST_THREAD True)

set(FOLLY_HAVE_LIBDOUBLE_CONVERSION True)

set(FOLLY_HAVE_LIBGFLAGS True)

set(FOLLY_HAVE_LIBGLOG True)

set(FOLLY_HAVE_VLA True)

set(FOLLY_HAVE_LIBEVENT True)

set(FOLLY_HAVE_LIBSSL True)


# Options
include(CMakeOptions.cmake)

# Setup environment
set(CMAKE_BUILD_TYPE Release)
set(CMAKE_VERBOSE_MAKEFILE OFF)

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++14 -fPIC")

# Link libraries
link_libraries(
    ${AIO_LIBRARIES}
    ${OPENSSL_LIBRARIES}
    dl
)



# Check and setup configurations
include(CheckCXXSourceCompiles REQUIRED)
include(CheckFunctionExists REQUIRED)
include(CheckIncludeFileCXX REQUIRED)
include(CheckLibraryExists REQUIRED)
include(CheckTypeSize REQUIRED)

check_include_file_cxx(byteswap.h FOLLY_HAVE_BYTESWAP_H)
check_include_file_cxx(dlfcn.h FOLLY_HAVE_DLFCN_H)
check_include_file_cxx(emmintrin.h FOLLY_HAVE_EMMINTRIN_H)
check_include_file_cxx(fcntl.h FOLLY_HAVE_FCNTL_H)
check_include_file_cxx(features.h FOLLY_HAVE_FEATURES_H)
check_include_file_cxx(inttypes.h FOLLY_HAVE_INTTYPES_H)
check_include_file_cxx(limits.h FOLLY_HAVE_LIMITS_H)
check_include_file_cxx(malloc.h FOLLY_HAVE_MALLOC_H)
check_include_file_cxx(memory.h FOLLY_HAVE_MEMORY_H)
check_include_file_cxx(mutex.h FOLLY_HAVE_MUTEX_H)
check_include_file_cxx(stdbool.h FOLLY_HAVE_STDBOOL_H)
check_include_file_cxx(stdint.h FOLLY_HAVE_STDINT_H)
check_include_file_cxx(stdlib.h FOLLY_HAVE_STDLIB_H)
check_include_file_cxx(string.h FOLLY_HAVE_STRING_H)
check_include_file_cxx(strings.h FOLLY_HAVE_STRINGS_H)
check_include_file_cxx(unistd.h FOLLY_HAVE_UNISTD_H)
check_include_file_cxx(bits/c++config.h FOLLY_HAVE_BITS_C__CONFIG_H)
check_include_file_cxx(bits/functexcept.h FOLLY_HAVE_BITS_FUNCTEXCEPT_H)
check_include_file_cxx(sys/stat.h FOLLY_HAVE_SYS_STAT_H)
check_include_file_cxx(sys/time.h FOLLY_HAVE_SYS_TIME_H)
check_include_file_cxx(sys/types.h FOLLY_HAVE_SYS_TYPES_H)

check_type_size(__int128 INT128_T)
set(FOLLY_HAVE_INT128_T ${HAVE_INT128_T})
check_type_size(pthread_spinlock_t PTHREAD_SPINLOCK_T)
set(FOLLY_HAVE_PTHREAD_SPINLOCK_T ${HAVE_PTHREAD_SPINLOCK_T})
check_type_size(ptrdiff_t PTRDIFF_T)
set(FOLLY_HAVE_PTRDIFF_T ${HAVE_PTRDIFF_T})

check_function_exists(getdelim FOLLY_HAVE_GETDELIM)
check_function_exists(gettimeofday FOLLY_HAVE_GETTIMEOFDAY)
check_function_exists(malloc_size FOLLY_HAVE_MALLOC_SIZE)
check_function_exists(malloc_usable_size FOLLY_HAVE_MALLOC_USABLE_SIZE)
check_function_exists(memmove FOLLY_HAVE_MEMMOVE)
check_function_exists(memrchr FOLLY_HAVE_MEMRCHR)
check_function_exists(memset FOLLY_HAVE_MEMSET)
check_function_exists(pipe2 FOLLY_HAVE_PIPE2)
check_function_exists(strerror FOLLY_HAVE_STRERROR)

check_library_exists(iberty
    cplus_demangle_v3_callback /usr/lib FOLLY_HAVE_CPLUS_DEMANGLE_V3_CALLBACK)
check_library_exists(m
    pow /usr/lib FOLLY_HAVE_POW)
check_library_exists(pthread
    pthread_atfork /usr/lib FOLLY_HAVE_PTHREAD_ATFORK)
check_library_exists(pthread
    pthread_yield /usr/lib FOLLY_HAVE_PTHREAD_YIELD)
check_library_exists(rt
    clock_gettime /usr/lib FOLLY_HAVE_CLOCK_GETTIME)

if(FOLLY_HAVE_CPLUS_DEMANGLE_V3_CALLBACK)
    link_libraries(iberty)
endif()


if(NOT FOLLY_HAVE_PTHREAD_YIELD)
    check_include_file_cxx(sched.h FOLLY_HAVE_SCHED_H)
    check_function_exists(sched_yield FOLLY_HAVE_SCHED_YIELD)
endif()

set(CMAKE_REQUIRED_FLAGS "-std=c++14")

check_cxx_source_compiles("
    class C {
        virtual void f() final {}
        virtual void g() {}
    };
    class D : public C {
        virtual void g() override {}
    };
    int main() { return 0; }"
    FOLLY_FINAL)
set(FOLLY_OVERRIDE ${FOLLY_FINAL})

check_cxx_source_compiles("
    #include <type_traits>
    #if !_LIBCPP_VERSION
    #error No libc++
    #endif
    int main() { return 0; }"
    FOLLY_USE_LIBCPP)
    
if ( CMAKE_SYSTEM_NAME MATCHES "Linux" )
    unset(FOLLY_USE_LIBCPP)
endif()

check_cxx_source_compiles("
    #include <cstring>
    static constexpr int val = strlen(\"foo\");
    int main() { return 0; }"
    FOLLY_HAVE_CONSTEXPR_STRLEN)

check_cxx_source_compiles("
    #pragma GCC diagnostic error \"-Wattributes\"
    extern \"C\" void (*test_ifunc(void))() { return 0; }
    void func() __attribute__((ifunc(\"test_ifunc\")));
    int main() { return 0; }"
    FOLLY_HAVE_IFUNC)

check_cxx_source_compiles("
    #include <type_traits>
    const bool val = std::is_trivially_copyable<bool>::value;
    int main() { return 0; }"
    FOLLY_HAVE_STD__IS_TRIVIALLY_COPYABLE)

check_cxx_source_compiles("
    #include <thread>
    #include <chrono>
    void func() { std::this_thread::sleep_for(std::chrono::seconds(1)); }
    int main() { return 0; }"
    FOLLY_HAVE_STD__THIS_THREAD__SLEEP_FOR)

check_cxx_source_compiles("
    #include <stdio.h>
    int main() {
        char buf[256];
        return vsnprintf(buf, sizeof(buf), \"%\", 1) < 0 ? 0 : 1;
    }"
    FOLLY_HAVE_VSNPRINTF_ERRORS)

check_cxx_source_compiles("
    extern \"C\" void configure_link_extern_weak_test() __attribute__((weak));
    int main() {
        return configure_link_extern_weak_test == nullptr;
    }"
    FOLLY_HAVE_WEAK_SYMBOLS)

check_cxx_source_compiles("
    #include <string.h>
    #include <errno.h>
    int main() {
        char buf[1024];
        buf[0] = 0;
        int ret = strerror_r(ENOMEM, buf, sizeof(buf));
        return ret;
    }"
    FOLLY_HAVE_XSI_STRERROR_R)

if(GFLAGS_FOUND)
    set(CMAKE_REQUIRED_LIBRARIES "gflags")

    check_cxx_source_compiles("
        #include <gflags/gflags.h>
        void foo() { google::GetArgv(); }
        int main() { return 0; }"
        FOLLY_UNUSUAL_GFLAGS_NAMESPACE)

    if(FOLLY_UNUSUAL_GFLAGS_NAMESPACE)
        set(FOLLY_GFLAGS_NAMESPACE "google")
    else()
        set(FOLLY_GFLAGS_NAMESPACE "gflags")
    endif()
endif()

configure_file(
    "${CMAKE_CURRENT_SOURCE_DIR}/folly/folly-config.h.in"
    "${CMAKE_CURRENT_BINARY_DIR}/folly/folly-config.h"
)


include_directories(${CMAKE_CURRENT_SOURCE_DIR})
include_directories(${CMAKE_CURRENT_BINARY_DIR})

# Work on all sub directories
add_subdirectory(folly)
add_subdirectory(folly/experimental)
add_subdirectory(folly/experimental/io)

add_subdirectory(folly/futures)
add_subdirectory(folly/io)
add_subdirectory(folly/io/async)
add_subdirectory(folly/stats)
add_subdirectory(folly/fibers)
add_subdirectory(folly/detail)
add_subdirectory(folly/build)
add_subdirectory(folly/portability)

FILE(GLOB_RECURSE FOLLY_INCLUDES_EXPORT folly/*.h)
FILE(GLOB_RECURSE FOLLY_EXCLUDED_EXPORT folly/SingletonStackTrace.h
										folly/experimental/RCUUtils.h
										folly/experimental/io/AsyncIO.h
										folly/experimental/symbolizer/*.h
										folly/experimental/exception_tracer/*.h)

LIST(REMOVE_ITEM FOLLY_INCLUDES_EXPORT ${FOLLY_EXCLUDED_EXPORT})

# Link libraries
add_library(folly STATIC
    $<TARGET_OBJECTS:folly_base>
    $<TARGET_OBJECTS:folly_experimental>
    $<TARGET_OBJECTS:folly_experimental_io>
    $<TARGET_OBJECTS:folly_fibers>
    $<TARGET_OBJECTS:folly_futures>
    $<TARGET_OBJECTS:folly_io>
    $<TARGET_OBJECTS:folly_io_async>
    $<TARGET_OBJECTS:folly_stats>
	$<TARGET_OBJECTS:folly_portability>
	$<TARGET_OBJECTS:folly_detail>
	$<TARGET_OBJECTS:folly_build>
)
install(FILES ${FOLLY_INCLUDES_EXPORT} DESTINATION include)
