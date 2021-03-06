PLATFORM_DEFINES = select({
    "//:linux": [
        "OS_LINUX",
        "ROCKSDB_PLATFORM_POSIX",
        "HAVE_SSE42",
        "ROCKSDB_LIB_IO_POSIX",
        "ROCKSDB_SUPPORT_THREAD_LOCAL",
        "ROCKSDB_FALLOCATE_PRESENT",
        "ROCKSDB_MALLOC_USABLE_SIZE",
        "ROCKSDB_PTHREAD_ADAPTIVE_MUTEX",
        "ROCKSDB_RANGESYNC_PRESENT",
        "ROCKSDB_SCHED_GETCPU_PRESENT",
        "rocksdb_shared_EXPORTS",
        "NPERF_CONTEXT",
        "ROCKSDB_OPENSSL_AES_CTR",
    ],
    "//:osx": [
        "OS_MACOSX",
        "ROCKSDB_PLATFORM_POSIX",
        "HAVE_SSE42",
        "ROCKSDB_LIB_IO_POSIX",
        "rocksdb_shared_EXPORTS",
        "NPERF_CONTEXT",
        "ROCKSDB_OPENSSL_AES_CTR",
    ],
    "//:windows": [
        "OS_WIN",
        "NPERF_CONTEXT",
        "_WIN32_WINNT=_WIN32_WINNT_VISTA",
    ],
    "//conditions:default": [],
})

FEATURE_DEFINES = [
    "LZ4",
    "SNAPPY",
]

DEFAULT_DEFINES = PLATFORM_DEFINES + FEATURE_DEFINES

COMMON_HDRS = [
    "dirent.h",
    "likely.h",
    "port.h",
    "jemalloc_helper.h",
    "stack_trace.h",
    "sys_time.h",
    "util_logger.h",
]

PLATFORM_HDRS = select({
    "//:linux" : [
        "port_posix.h",
    ],
    "//:osx" : [
        "port_posix.h",
    ],
    "//:windows" : glob(["win/*.h"]) + ["xpress.h"],
})

COMMON_SRCS = [
    "stack_trace.cc",
]

PLATFORM_SRCS = select({
    "//:linux" : [
        "port_posix.cc",
    ],
    "//:osx" : [
        "port_posix.cc",
    ],
    "//:windows" : glob(["win/*.cc"], exclude = ["win/win_jemalloc.cc"]),
})

cc_library(
    name = "port",
    srcs = COMMON_SRCS + PLATFORM_SRCS,
    deps = [
        ":headers",
        "//util:headers",
        "//monitoring:headers",
        "//include:include",
    ],
    visibility = ["//visibility:public"],
    defines = DEFAULT_DEFINES,
)

cc_library(
    name = "headers",
    hdrs = COMMON_HDRS + PLATFORM_HDRS,
    deps = [
        "//env:headers",
    ],
    visibility = ["//visibility:public"],
    defines = DEFAULT_DEFINES,
)
