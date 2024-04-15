load("@rules_foreign_cc//foreign_cc:defs.bzl", "configure_make")

filegroup(
    name = "all_srcs",
    srcs = glob(["**"]),
)

# TODO(sp): Use -fdata-sections -ffunction-sections + -Wl,--gc-sections (plus
# perhaps -Wl,--print-gc-sections)
configure_make(
    name = "rrdtool",
    args = ["-j6"],
    configure_options = [
        "--disable-docs",
        "--disable-examples",
        "--disable-libbdi",
        "--disable-libwrap",
        "--disable-lua",
        "--disable-perl",
        "--disable-python",
        "--disable-ruby",
        "--disable-rrdcaches",
        "--disable-rrdcgi",
        "--disable-tcl",
        "--with-systemdsystemunitdir=no",
        # https://github.com/bazelbuild/rules_foreign_cc/issues/239
        "CFLAGS='-Dredacted=\"redacted\"'",
    ],
    copts = [
        "-g",
        "-O2",
        "-D_GNU_SOURCE",
        "-fno-strict-aliasing",
        "-std=gnu99",
        "-fPIC",
        "-Wno-format-truncation",
        "-Wno-implicit-fallthrough",
        "-Wno-stringop-truncation",
    ],
    lib_source = "@rrdtool//:srcs",
    lib_name = "rrdtool",
    out_binaries = [
        "rrdcached",
        "rrdcreate",
        "rrdinfo",
        "rrdtool",
        "rrdupdate",
    ],
    out_data_dirs = ["share"],
    out_shared_libs = [
        "librrd.so",
        "librrd.so.8",
        "librrd.so.8.2.1",
    ],
    out_static_libs = ["librrd.a"],
    visibility = ["//visibility:public"],
)
