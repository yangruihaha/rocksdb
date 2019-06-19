config_setting(
    name = "tests_enabled_debug_mode",
    values = {
        "compilation_mode": "dbg",
        "define": "enable_tests=1",
    },
    visibility = ["//visibility:public"],
)

config_setting(
    name = "tests_enabled_fastbuild_mode",
    values = {
        "compilation_mode": "fastbuild",
        "define": "enable_tests=1",
    },
    visibility = ["//visibility:public"],
)

cc_library(
    name = "rocksdb",
    deps = [
        "//cache",
        "//db",
        "//env",
        "//include",
        "//memtable",
        "//monitoring",
        "//options",
        "//port",
        "//table",
        "//third_party/gtest",
        "//third_party/lz4",
        "//third_party/snappy",
        "//util",
        "//utilities",
        "//utilities/backupable",
        "//utilities/checkpoint",
        "//utilities/leveldb_options",
        "//utilities/merge_operators",
        "//utilities/merge_operators/string_append",
        "//utilities/options",
        "//utilities/table_properties_collectors",
        "//utilities/transactions",
        "//utilities/ttl",
        "//utilities/write_batch_with_index",
    ],
    visibility = ["//visibility:public"],
)

cc_library(
    name = "empty_main",
    srcs = ["empty_main.cc"],
    visibility = ["//visibility:public"],
)

SHARED_LIBRARY_LINKOPTS = select({
    "@toolchain//:is_target_linux": [
        "-static-libgcc",
        "-static-libstdc++",
    ],
    "@toolchain//:is_target_osx": [
        "-static-libstdc++",
    ],
    "@toolchain//:is_target_windows": [],
})

filegroup(
    name = "librocksdb",
    srcs = select({
        "@toolchain//:is_target_linux": [":librocksdb.so"],
        "@toolchain//:is_target_osx": [":librocksdb.dylib"],
        "@toolchain//:is_target_windows": [":librocksdb.dll"],
    }),
)

cc_binary(
    name = "librocksdb.so",
    deps = [
        ":rocksdb",
    ],
    linkshared = True,
    linkopts = SHARED_LIBRARY_LINKOPTS,
)

cc_binary(
    name = "librocksdb.dylib",
    deps = [
        ":rocksdb",
    ],
    linkshared = True,
    linkopts = SHARED_LIBRARY_LINKOPTS,
)

cc_binary(
    name = "librocksdb.dll",
    deps = [
        ":rocksdb",
    ],
    linkshared = True,
    linkopts = SHARED_LIBRARY_LINKOPTS,
)
