load(
    "@com_github_mvukov_rules_ros//ros:interfaces.bzl",
    "cc_ros_interface_library",
    "ros_interface_library",
)

ros_interface_library(
    name = "bond_interface",
    srcs = glob([
        "bond/msg/*",
    ]),
    deps = [
        "@ros_common_msgs//:geometry_msgs",
        "@ros_std_msgs//:std_msgs",
    ],
    # strip the "_msgs" from final search path. 
    # Use this for backwards compatability to avoid changing imports for msgs.
    strip_end = True, 
)

# Defines a C++ library made of auto-generated code from the given messages.
cc_ros_interface_library(
    name = "cc_bond_interface",
    deps = [":bond_interface"],
    strip_end = True,
)

cc_library(
    name = "scmlib",
    hdrs = [
        "smclib/include/smclib/statemap.h"
    ],
    includes = [
        "smclib/include"
    ],
)

cc_library(
    name = "bondcpp",
    srcs = [ 
        "bondcpp/src/bond.cpp",
        "bondcpp/src/BondSM_sm.cpp",
        "bondcpp/src/timeout.cpp",
    ],
    hdrs = [
        "bondcpp/include/bondcpp/bond.h",
        "bondcpp/include/bondcpp/BondSM_sm.h",
        "bondcpp/include/bondcpp/timeout.h"
    ],
    includes = [
        "bondcpp/include"
    ],
    linkopts = [
        "-luuid"
    ],
    deps = [
        "@ros_comm//:roscpp_lib",
        ":cc_bond_interface",
        ":scmlib",
    ],
    visibility = [
        "//visibility:public"
    ]
)